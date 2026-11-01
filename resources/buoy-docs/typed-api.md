---
title: "printing typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["BuoyPrintDocument", "BuoyPrintPage", "BuoyPrintText", "LinuxPrinterInfo", "LinuxPrintingDestination", "PrintCapabilities", "PrintJobSetup", "PrintRectangle", "PrintSettingsSnapshot", "PrintSize", "PrinterGraphics", "PrinterInfo", "PrinterSetup", "WinPrintingDocument", "WinPrintingPrinter4", "WinPrintingSize", "WindowsPrinterInfo"]
dependencies: []
symbols: ["BuoyPrintDocument", "BuoyPrintPage", "BuoyPrintText", "LinuxPrinterInfo", "LinuxPrintingDestination", "PrintCapabilities", "PrintJobSetup", "PrintRectangle", "PrintSettingsSnapshot", "PrintSize", "PrinterGraphics", "PrinterInfo", "PrinterSetup", "WinPrintingDocument", "WinPrintingPrinter4", "WinPrintingSize", "WindowsPrinterInfo"]
related: ["api.md", "getting-started.md", "index.md"]
---

# printing typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## Printing functions

### PrintingSupported

`Public Function PrintingSupported() As Boolean`

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### ExportControlPDF

`Public Function ExportControlPDF(control As UIControl) As Bytes`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `control` | `UIControl` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Bytes` |

### PrintControl

`Public Function PrintControl(control As UIControl, showPrintPanel As Boolean = True) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `control` | `UIControl` | `ByVal` | Required |
| `showPrintPanel` | `Boolean` | `ByVal` | `True` |

#### Returns

| Type |
| --- |
| `Boolean` |

### BufferedPrintingSupported

`Public Function BufferedPrintingSupported() As Boolean`

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### OpenPrinter

`Public Function OpenPrinter(setup As PrintJobSetup) As PrinterGraphics`

Legacy REALbasic-style global spelling, alongside PrintJobSetup.OpenPrinter.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `setup` | `PrintJobSetup` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `PrinterGraphics` |

### OpenPrinter (overload 2)

`Public Function OpenPrinter() As PrinterGraphics`

No parameters.

#### Returns

| Type |
| --- |
| `PrinterGraphics` |

### PrintingAvailable

`Public Function PrintingAvailable() As Boolean`

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### Printers

`Public Function Printers() As Array Of PrinterInfo`

No parameters.

#### Returns

| Type |
| --- |
| `Array Of PrinterInfo` |

### DefaultPrinter

`Public Function DefaultPrinter() As Optional Of String`

No parameters.

#### Returns

| Type |
| --- |
| `Optional Of String` |

### PrintText

`Public Function PrintText(printerName As String, title As String, text As String) As Integer`

Submit UTF-8 text to an explicitly selected printer; returns the spool job ID.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `printerName` | `String` | `ByVal` | Required |
| `title` | `String` | `ByVal` | Required |
| `text` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Integer` |

### OpenPrinter (overload 3)

`Public Function OpenPrinter(setup As PrinterSetup) As PrinterGraphics`

Explicit adapter: copies paper geometry/orientation, not native driver settings.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `setup` | `PrinterSetup` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `PrinterGraphics` |

### PrintingCapabilities

`Public Function PrintingCapabilities() As PrintCapabilities`

Implementation capabilities and library-only availability; never contacts a spooler.

No parameters.

#### Returns

| Type |
| --- |
| `PrintCapabilities` |

## PrintRectangle

`Sequential Structure PrintRectangle`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `X` | `Double` | — | — |
| `Y` | `Double` | — | — |
| `Width` | `Double` | — | — |
| `Height` | `Double` | — | — |

## PrintSettingsSnapshot

`Public Class PrintSettingsSnapshot`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `PaperName` | `String` | Yes | No | — | — |
| `Orientation` | `Integer` | Yes | No | — | — |

### Constructor

`Public Sub Constructor()`

No parameters.

Returns: no value.

## PrintSize

`Sequential Structure PrintSize`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `Width` | `Double` | — | — |
| `Height` | `Double` | — | — |

## PrinterSetup

`Public Class PrinterSetup`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Landscape` | `Boolean` | No | No | — | — |
| `PageWidth` | `Integer` | Yes | No | — | — |
| `PageHeight` | `Integer` | Yes | No | — | — |
| `Width` | `Integer` | Yes | No | — | — |
| `Height` | `Integer` | Yes | No | — | — |
| `Left` | `Integer` | Yes | No | — | — |
| `Top` | `Integer` | Yes | No | — | — |
| `PageLeft` | `Integer` | Yes | No | — | — |
| `PageTop` | `Integer` | Yes | No | — | — |
| `HorizontalResolution` | `Integer` | Yes | No | — | — |
| `VerticalResolution` | `Integer` | Yes | No | — | — |
| `Settings` | `String` | No | No | — | — |

### ToPrintJobSetup

`Public Function ToPrintJobSetup(printerName As String = "", jobName As String = "Buoy document") As PrintJobSetup`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `printerName` | `String` | `ByVal` | `""` |
| `jobName` | `String` | `ByVal` | `"Buoy document"` |

#### Returns

| Type |
| --- |
| `PrintJobSetup` |

### Constructor

`Public Sub Constructor()`

No parameters.

Returns: no value.

### Destructor

`Public Sub Destructor()`

No parameters.

Returns: no value.

### PrintControl

`Public Function PrintControl(control As UIControl, showPrintPanel As Boolean = True) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `control` | `UIControl` | `ByVal` | Required |
| `showPrintPanel` | `Boolean` | `ByVal` | `True` |

#### Returns

| Type |
| --- |
| `Boolean` |

### ShowPageSetupDialog

`Public Function ShowPageSetupDialog(parentWindow As Optional Of Window = None) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `parentWindow` | `Optional Of Window` | `ByVal` | `None` |

#### Returns

| Type |
| --- |
| `Boolean` |

### PageSetupDialog

`Public Function PageSetupDialog(parentWindow As Optional Of Window = None) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `parentWindow` | `Optional Of Window` | `ByVal` | `None` |

#### Returns

| Type |
| --- |
| `Boolean` |

## PrinterInfo

`Public Class PrinterInfo`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Name` | `String` | No | No | — | — |
| `IsDefault` | `Boolean` | No | No | — | — |

## PrintJobSetup

`Public Class PrintJobSetup`

Xojo-inspired setup. Page dimensions are a logical canvas in 72-point inches.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Copies` | `Integer` | No | No | `1` | Collated copies; inclusive one-based range. LastPage = 0 means through the end. |
| `FirstPage` | `Integer` | No | No | `1` | — |
| `LastPage` | `Integer` | No | No | `0` | — |
| `PrinterName` | `String` | No | No | `""` | — |
| `JobName` | `String` | No | No | `"Buoy document"` | — |
| `Landscape` | `Boolean` | No | No | `False` | — |
| `PageWidth` | `Double` | No | No | `595.275590551` | — |
| `PageHeight` | `Double` | No | No | `841.88976378` | — |
| `HorizontalResolution` | `Integer` | Yes | No | — | — |
| `VerticalResolution` | `Integer` | Yes | No | — | — |

### OpenPrinter

`Public Shared Function OpenPrinter() As PrinterGraphics`

No parameters.

#### Returns

| Type |
| --- |
| `PrinterGraphics` |

### OpenPrinter (overload 2)

`Public Shared Function OpenPrinter(setup As PrintJobSetup) As PrinterGraphics`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `setup` | `PrintJobSetup` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `PrinterGraphics` |

## PrinterGraphics

`Public Class PrinterGraphics`

Buffered text drawing. Explicit Close submits; Cancel/destruction never submits.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `FontName` | `String` | No | No | `"System"` | — |
| `FontSize` | `Double` | No | No | `12.0` | — |
| `Copies` | `Integer` | Yes | No | — | — |
| `FirstPage` | `Integer` | Yes | No | — | — |
| `LastPage` | `Integer` | Yes | No | — | — |
| `SubmissionState` | `String` | Yes | No | — | — |
| `SubmissionFailure` | `Exception` | Yes | No | — | — |
| `Width` | `Double` | Yes | No | — | — |
| `Height` | `Double` | Yes | No | — | — |
| `PageCount` | `Integer` | Yes | No | — | — |
| `IsClosed` | `Boolean` | Yes | No | — | — |
| `PrintingCancelled` | `Boolean` | Yes | No | — | — |
| `JobId` | `Integer` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(setup As PrintJobSetup)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `setup` | `PrintJobSetup` | `ByVal` | Required |

Returns: no value.

### DrawText

`Public Sub DrawText(str As String, x As Double, y As Double)`

Single-line text at x and baseline y, in points; no automatic wrapping.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `str` | `String` | `ByVal` | Required |
| `x` | `Double` | `ByVal` | Required |
| `y` | `Double` | `ByVal` | Required |

Returns: no value.

### ExportPDF

`Public Sub ExportPDF(fileName As String)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `fileName` | `String` | `ByVal` | Required |

Returns: no value.

### NextPage

`Public Sub NextPage()`

No parameters.

Returns: no value.

### Cancel

`Public Sub Cancel()`

No parameters.

Returns: no value.

### Close

`Public Function Close() As Integer`

Submit once. A failed submission is terminal to prevent accidental retries.

No parameters.

#### Returns

| Type |
| --- |
| `Integer` |

## PrintCapabilities

`Public Class PrintCapabilities`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `CopiesSupported` | `Boolean` | Yes | No | — | — |
| `PageRangesSupported` | `Boolean` | Yes | No | — | — |
| `DiscoverySupported` | `Boolean` | Yes | No | — | — |
| `TextSubmissionSupported` | `Boolean` | Yes | No | — | — |
| `BufferedPagesSupported` | `Boolean` | Yes | No | — | — |
| `ControlPDFExportSupported` | `Boolean` | Yes | No | — | — |
| `NativeControlPrintSupported` | `Boolean` | Yes | No | — | — |
| `PageSetupDialogSupported` | `Boolean` | Yes | No | — | — |
| `DiscoveryAvailable` | `Boolean` | Yes | No | — | — |
| `TextSubmissionAvailable` | `Boolean` | Yes | No | — | — |
| `PDFExportSupported` | `Boolean` | Yes | No | — | — |
| `PDFExportAvailable` | `Boolean` | Yes | No | — | — |
| `BufferedPagesAvailable` | `Boolean` | Yes | No | — | — |

## BuoyPrintText

`Public Class BuoyPrintText`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Content` | `String` | No | No | — | — |
| `X` | `Double` | No | No | — | — |
| `Y` | `Double` | No | No | — | — |
| `FontName` | `String` | No | No | `"sans-serif"` | — |
| `FontSize` | `Double` | No | No | `12.0` | — |

## BuoyPrintPage

`Public Class BuoyPrintPage`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Items` | `Array Of BuoyPrintText` | No | No | `[]` | — |

## BuoyPrintDocument

`Public Class BuoyPrintDocument`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `PageWidth` | `Double` | No | No | `595.275590551` | — |
| `PageHeight` | `Double` | No | No | `841.88976378` | — |
| `Pages` | `Array Of BuoyPrintPage` | No | No | `[]` | — |

## LinuxPrinterInfo

`Public Class LinuxPrinterInfo`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Name` | `String` | No | No | — | — |
| `IsDefault` | `Boolean` | No | No | — | — |

## LinuxPrintingDestination

`Sequential Structure LinuxPrintingDestination`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `QueueName` | `Ptr` | — | — |
| `InstanceName` | `Ptr` | — | — |
| `DefaultFlag` | `Int32` | — | — |
| `OptionCount` | `Int32` | — | — |
| `Options` | `Ptr` | — | — |

## PrintingLinuxBackend functions

### ExportPDF

`Public Sub ExportPDF(fileName As String, document As BuoyPrintDocument)`

Export the same shaped PDF used by PrintPages without contacting CUPS. The explicit destination is overwritten; invalid documents are rejected first.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `fileName` | `String` | `ByVal` | Required |
| `document` | `BuoyPrintDocument` | `ByVal` | Required |

Returns: no value.

### PrintPages

`Public Function PrintPages(printerName As String, title As String, document As BuoyPrintDocument) As Integer`

Render explicit point-coordinate text pages to PDF and submit the accepted job.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `printerName` | `String` | `ByVal` | Required |
| `title` | `String` | `ByVal` | Required |
| `document` | `BuoyPrintDocument` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Integer` |

### IsSupported

`Public Function IsSupported() As Boolean`

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### IsAvailable

`Public Function IsAvailable() As Boolean`

Library capability only: does not contact the server or promise a printer exists.

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### Printers

`Public Function Printers() As Array Of LinuxPrinterInfo`

Owned base queue names. Named option instances collapse into the same queue.

No parameters.

#### Returns

| Type |
| --- |
| `Array Of LinuxPrinterInfo` |

### DefaultPrinter

`Public Function DefaultPrinter() As Optional Of String`

No parameters.

#### Returns

| Type |
| --- |
| `Optional Of String` |

### PrintText

`Public Function PrintText(printerName As String, title As String, text As String) As Integer`

Submit UTF-8 text/plain to an explicit CUPS queue; returns its accepted job ID.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `printerName` | `String` | `ByVal` | Required |
| `title` | `String` | `ByVal` | Required |
| `text` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Integer` |

## WindowsPrinterInfo

`Public Class WindowsPrinterInfo`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Name` | `String` | No | No | — | — |
| `IsDefault` | `Boolean` | No | No | — | — |

## WinPrintingPrinter4

`Sequential Structure WinPrintingPrinter4`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `PrinterName` | `Ptr` | — | — |
| `ServerName` | `Ptr` | — | — |
| `Attributes` | `UInt32` | — | — |

## WinPrintingDocument

`Sequential Structure WinPrintingDocument`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `Size` | `Int32` | — | — |
| `DocumentName` | `Ptr` | — | — |
| `OutputName` | `Ptr` | — | — |
| `DataType` | `Ptr` | — | — |
| `Options` | `UInt32` | — | — |

## WinPrintingSize

`Sequential Structure WinPrintingSize`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `Width` | `Int32` | — | — |
| `Height` | `Int32` | — | — |

## PrintingWindowsBackend functions

### PrintPages

`Public Function PrintPages(printerName As String, title As String, document As BuoyPrintDocument) As Integer`

Explicit pages of baseline-positioned text; requested page sizes are logical clipping only.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `printerName` | `String` | `ByVal` | Required |
| `title` | `String` | `ByVal` | Required |
| `document` | `BuoyPrintDocument` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Integer` |

### IsSupported

`Public Function IsSupported() As Boolean`

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### IsAvailable

`Public Function IsAvailable() As Boolean`

Tests system library loading, not spooler service health or printer presence.

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### DefaultPrinter

`Public Function DefaultPrinter() As Optional Of String`

No parameters.

#### Returns

| Type |
| --- |
| `Optional Of String` |

### Printers

`Public Function Printers() As Array Of WindowsPrinterInfo`

Current user's local printers and established remote connections, level 4.

No parameters.

#### Returns

| Type |
| --- |
| `Array Of WindowsPrinterInfo` |

### PrintText

`Public Function PrintText(printerName As String, title As String, text As String) As Integer`

Explicit GDI text job, 12-point Segoe UI, half-inch printable-area margins.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `printerName` | `String` | `ByVal` | Required |
| `title` | `String` | `ByVal` | Required |
| `text` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Integer` |
