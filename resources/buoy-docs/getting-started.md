---
title: "Printing and page setup getting started"
summary: "Install and use printing with an availability check and a complete example."
category: "Guides"
order: 10
keywords: ["printing", "install", "example"]
related: ["index.md", "api.md", "typed-api.md"]
---

# Getting started

## Install and import

Copy the sealed `printing-0.1.0.buipkg` archive into your application's `packages/` folder. Build the package using the native package builder described in
[CONTRIBUTING](https://github.com/BuoyBay/printing/blob/main/CONTRIBUTING.md).

## First use

Use `PrintSettingsSnapshot` for read-only inspection. Create `PrinterSetup` to change orientation or persist the package's versioned `Settings` string. Export a native UIControl with `ExportControlPDF` when in-memory PDF bytes are enough. Start a print operation only after a user action; the print panel is shown by default.

```buoy
Import printing

Sub Main()
    If Not PrintingSupported() Then
        Print "Native page setup requires macOS."
        Return
    End If
    Dim setup As New PrinterSetup()
    setup.Landscape = True
    Dim saved As String = setup.Settings
    Print setup.Width
    Print setup.Height
    setup.Settings = saved
End Sub
```

The example checks backend availability before invoking macOS-only operations. It does not catch input or access failures; catch exceptions at your application boundary and present a useful message to the user.

## Platform and error handling

`PrintingSupported()` covers macOS native control printing and page setup, which require the main thread. `BufferedPrintingSupported()` and `PrintingCapabilities()` describe Linux/Windows buffered printing, including discovery, `PrintText`, and `OpenPrinter`. This is a useful printing subset, not a complete Xojo printing framework. `OpenPrinter` returns buffered `PrinterGraphics`, with `NextPage` pagination and `Close` submission. ExportControlPDF writes no file and submits no job. Passing false for showPrintPanel permits direct job submission. Window controls use their content view. Page setup dialogs are modal; supplying a parentWindow currently throws because asynchronous attached sheets are not implemented.
## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
