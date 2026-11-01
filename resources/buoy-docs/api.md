---
title: "Printing and page setup API"
summary: "Public printing types and operations with behavior and lifetime notes."
category: "Reference"
order: 20
keywords: ["printing", "API", "reference"]
symbols: ["PrintingSupported", "PrintSettingsSnapshot", "PrintSettingsSnapshot.PaperName", "PrintSettingsSnapshot.Orientation", "ExportControlPDF", "PrintControl", "PrinterSetup", "PrinterSetup.Landscape", "PrinterSetup.Settings", "PrinterSetup.ShowPageSetupDialog", "PrinterSetup.PageSetupDialog", "PrinterSetup.PrintControl", "PrinterSetup.PageWidth", "PrinterSetup.PageHeight", "PrinterSetup.Width", "PrinterSetup.Height", "PrinterSetup.Left", "PrinterSetup.Top", "PrinterSetup.PageLeft", "PrinterSetup.PageTop", "PrinterSetup.HorizontalResolution", "PrinterSetup.VerticalResolution"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# API reference

`Import printing` exposes the following public API. Properties described as read-only have no public setter.

| Symbol | Behavior |
| --- | --- |
| `PrintingSupported() As Boolean` | Reports native printing availability. |
| `PrintSettingsSnapshot()` | Capture shared native PaperName As String and Orientation As Integer without changing them. |
| `ExportControlPDF(control As UIControl) As Bytes` | Export a native control in memory; no file is written and no print job is submitted. |
| `PrintControl(control As UIControl, showPrintPanel As Boolean = True) As Boolean` | Run an explicit native print operation with shared settings; false panel argument permits direct submission. |
| `PrinterSetup()` | Own a private settings copy; automatically releases it on destruction. |
| `PrinterSetup.Landscape As Boolean` | Read/write orientation. |
| `PrinterSetup.PageWidth / PageHeight As Integer` | Read-only paper dimensions rounded to native points. |
| `PrinterSetup.Width / Height As Integer` | Read-only dimensions after native page margins. |
| `PrinterSetup.Left / Top As Integer` | Read-only printable coordinate origin; both are zero. |
| `PrinterSetup.PageLeft / PageTop As Integer` | Read-only negative offsets from printable origin to paper edges. |
| `PrinterSetup.HorizontalResolution / VerticalResolution As Integer` | Read-only virtual drawing resolution; both 72 points per inch, not hardware DPI. |
| `PrinterSetup.Settings As String` | Read/write versioned Buoy JSON containing geometry, orientation, four margins, and scaling. |
| `PrinterSetup.ShowPageSetupDialog(parentWindow As Optional Of Window = None) As Boolean` | Show modal page setup; cancel leaves settings unchanged. Omit the unsupported attached-sheet parent. |
| `PrinterSetup.PageSetupDialog(parentWindow As Optional Of Window = None) As Boolean` | Legacy alias for ShowPageSetupDialog. |
| `PrinterSetup.PrintControl(control As UIControl, showPrintPanel As Boolean = True) As Boolean` | Run a print operation with a private copy of this setup. |

## Errors and availability

`PrintingSupported()` covers macOS native control printing and page setup, which require the main thread. `BufferedPrintingSupported()` and `PrintingCapabilities()` describe Linux/Windows buffered printing, including discovery, `PrintText`, and `OpenPrinter`. This is a useful printing subset, not a complete Xojo printing framework. `OpenPrinter` returns buffered `PrinterGraphics`, with `NextPage` pagination and `Close` submission. ExportControlPDF writes no file and submits no job. Passing false for showPrintPanel permits direct job submission. Window controls use their content view. Page setup dialogs are modal; supplying a parentWindow currently throws because asynchronous attached sheets are not implemented.

## Settings compatibility

`Settings` is Buoy JSON with format `buoy.printing.page-setup.v1`, not a Xojo settings string or a complete driver-state archive. It preserves orientation, paper dimensions, four margins, and scaling to three decimal places. It omits printer selection, paper names, copies, page ranges, and device-specific options. Invalid rounded geometry or nonpositive scale is rejected before changing the instance. Reported geometry is unscaled native points; printing applies the saved scaling.

## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)


[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
