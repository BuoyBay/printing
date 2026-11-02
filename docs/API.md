# Printing and PDF export · 0.1.0

`Import printing`. The package contains its own Linux CUPS/Pango/Cairo and Windows GDI/WinSpool implementations. macOS native control printing and page setup require the main thread. `PrintingSupported()` retains its original native-control meaning (macOS only); use `PrintingCapabilities()` for individual buffered-job features.

`New PrintSettingsSnapshot()` reads `PaperName` and native `Orientation` without changing shared print settings. `ExportControlPDF(control)` returns in-memory PDF bytes for a native view; it writes no file and submits no print job. `PrintControl(control, showPrintPanel = True)` runs an `NSPrintOperation` and returns its outcome. The print panel is shown by default; passing `False` permits direct submission. Window arguments use their content view.

## PrinterSetup

`New PrinterSetup()` owns a private copy of `NSPrintInfo`. Changing it never changes the application's shared settings.

| Member | Behavior |
| --- | --- |
| `Landscape` | Read/write orientation; changes native paper orientation. |
| `PageWidth`, `PageHeight` | Read-only paper dimensions, rounded to integer points. |
| `Width`, `Height` | Read-only dimensions after subtracting native page margins. |
| `Left`, `Top` | Printable coordinate origin, both zero, following Xojo. |
| `PageLeft`, `PageTop` | Negative offsets from printable origin to the paper edge. |
| `HorizontalResolution`, `VerticalResolution` | Both 72: macOS virtual drawing points per inch, not printer hardware DPI. |
| `Settings` | Read/write versioned Buoy JSON containing size, orientation, four margins, and scaling. |
| `ShowPageSetupDialog()` | Modal native page setup; returns `False` on cancel, with settings unchanged. |
| `PageSetupDialog()` | Legacy Realbasic/Xojo alias for `ShowPageSetupDialog()`. |
| `PrintControl(control, showPrintPanel = True)` | Print a native control using a private copy of this setup. |

`Settings` is a Buoy format, not a Xojo settings string. It preserves page geometry and scale to three decimal places; it does not serialize printer selection, paper names, copies, page ranges, device-specific options, or complete driver state. Incoming numeric values are rounded to that precision before validation and native application, so a positive area or scale that would round to zero is rejected. Invalid values are rejected before changing the instance. Geometry is reported in unscaled native points; print operations apply the saved scaling factor. Page setup methods accept `Optional Of Window = None`; supplying a parent currently raises `UnsupportedOperationException` because attached sheets require an asynchronous lifecycle.

## Compatibility limits

Names and coordinate origins follow the official [Xojo PrinterSetup reference](https://docs.xojo.com/api/printing/printersetup.html), including the legacy page setup alias. This is a useful subset, not a drop-in implementation of the entire Xojo printing framework.

`OpenPrinter()` and `OpenPrinter(PrintJobSetup)` return a buffered `PrinterGraphics` on Linux/Windows. This is a separate text drawing object, not Buoy `Graphics`. Set an explicit `PrintJobSetup.PrinterName` to avoid default-printer lookup. `PageWidth`/`PageHeight` are writable Double logical canvas dimensions in points (A4 by default); they do not negotiate driver media. Landscape swaps portrait dimensions. Font sizes and DrawText baseline coordinates use points.

`DrawText` and `NextPage` buffer only. `Close()` attempts submission once; its positive job ID means spool acceptance, not physical output. Failure is terminal and rethrows the original exception, available as `SubmissionFailure` (including its native code where supplied by the backend). `SubmissionState` is `open`, `accepted`, `failed`, or `cancelled`. Repeated `Close()` returns the prior accepted ID, or zero after failure/cancellation. `Cancel()` and destruction never submit. There is no automatic retry or destructor printing.

`PrintJobSetup.OpenPrinter` also provides the no-argument and setup overloads. `PrinterSetup.ToPrintJobSetup(printerName, jobName)` explicitly copies precise native paper dimensions and orientation without mutating native settings; it does not copy margins/scaling as drawing transforms or driver state. `OpenPrinter(PrinterSetup)` uses that adapter, but buffered rendering is currently unavailable on macOS. The original `PrinterSetup` remains macOS-only with unchanged read-only Integer geometry and Settings semantics.

`Printers()` returns owned name/default records; `DefaultPrinter()` returns an optional name. `PrintText(printerName, title, text)` submits immediately. `PrintingAvailable()` probes backend libraries, not spooler reachability or printer existence. Discovery errors remain exceptions; an empty successful list means no queues. Linux `PrinterGraphics.ExportPDF(path)` renders without submitting or closing the job. Windows Print-to-PDF is a virtual printer, not this PDF export API.

Capabilities distinguish discovery, text submission, buffered pages, buffered PDF export, native-control PDF export/printing and page setup. `*Supported` means implemented; `*Available` probes required libraries only. Linux/Windows support discovery/text/buffered jobs, Linux supports buffered PDF export, and macOS supports the original control APIs/page setup. Buffered printer dialogs and paper selection are not exposed by this API. Copies and page ranges are available as described below. Richer dialogs/options, macOS buffered rendering, shapes/images and printer-backed Buoy Graphics remain future work. Native macOS control print panels retain their existing behavior.

Buffered jobs retain limits of 1000 pages, 100000 text runs, 16 MiB UTF-8, dimensions 1..14400 points, font sizes 1..1000 points and font names of at most 31 UTF-16 code units. DrawText accepts single lines without tabs, CR or LF. Setup is snapshotted when opened; drawing is for one owner thread. Linux uses Pango shaping; Windows uses GDI, so identical text layout is not guaranteed.

The legacy source facade in `containers/integrations/printing` remains usable independently, including writable Double `PrinterSetup.PageWidth/PageHeight`. Do not mix it with the canonical package in one application: aliased imports still produce duplicate classes. No safe mixed-import adapter is claimed and no read-only geometry substitution has been made. Migrate the whole consumer to `PrintJobSetup` and the package together.

Implemented against [Apple NSPrintInfo](https://developer.apple.com/documentation/appkit/nsprintinfo), [NSPageLayout](https://developer.apple.com/documentation/appkit/nspagelayout), and [NSPrintOperation](https://developer.apple.com/documentation/appkit/nsprintoperation).

Linux-host macOS cross-link validation may be blocked by toolchain Security/libc++ stubs, CoreFoundation framework layout/search paths, and missing CFData symbols. Semantic checks alone do not establish native linking or execution. The runner retains link failures and returns nonzero for an incomplete matrix. macOS native compatibility, ARM64 execution, visual inspection and physical output require separate validation.

## Buffered copies and page ranges

`PrintJobSetup.Copies` (default 1, allowed 1..1000), `FirstPage` (default 1), and `LastPage` (default 0, meaning through the final buffered page) are writable job options. Page numbers are one-based and inclusive, bounded by 1000. Nonzero `LastPage` must be at least `FirstPage`. `OpenPrinter` validates and snapshots these options before any default-printer lookup; `PrinterGraphics.Copies`, `FirstPage`, and `LastPage` expose the read-only snapshot. Names follow [Xojo Graphics](https://docs.xojo.com/api/graphics/graphics.html); these options are supplied programmatically, without a dialog.

Draw every source page normally. `Close` selects the requested range and emits collated copies (for example, range 2..3 with two copies produces 2,3,2,3). Linux PDF export applies the same selection without submitting or closing. `PageCount` remains the buffered source count. A range extending past the actual document throws rather than silently truncating. Such bounds are checked at export/close, when the final page count is known. A failed export leaves the buffer open; a failed close is terminal with the original exception recorded. Output is bounded to 1000 pages and the existing backend limits of 100000 text runs / 16 MiB of UTF-8, including repetitions. Copies are rendered into one native job, not requested as driver-side copies; spooler acceptance still does not guarantee physical completion.

`CopiesSupported` and `PageRangesSupported` are true on Linux/Windows and false on macOS, matching the implemented buffered API. The shared selection stage feeds the existing CUPS/Pango and GDI renderers, without editing either backend copy or concurrent text-shaping work. The legacy container facade does not gain these setup options.

Paper selection remains unexposed: the Linux backend sends PDF page dimensions but no `media` option, and Windows `CreateDCW` receives no DEVMODE (dimensions only control logical clipping). Neither establishes that a queue supports a requested paper size, tray, or form. `PageWidth`/`PageHeight` remain logical canvas dimensions, not a media-selection promise. There is no placeholder paper capability.

When another agent is updating backend copies concurrently, `--record-backend-drift` allows the package runner to finish its compiler/runtime checks while recording mismatched source hashes and returning an incomplete result. The default remains strict. Receipts identify the exact source snapshot tested; reconcile container/package differences before declaring integration complete.

The dialog/paper placeholder properties are absent, while implemented copies/ranges remain. Failed Close explicitly clears buffered pages before rethrowing, avoiding the BUI-015 skipped-Finally behavior; PageCount is zero afterwards.
