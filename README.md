# Native control printing and in-memory PDFs

`Import printing`. The package contains its own Linux CUPS/Pango/Cairo and Windows GDI/WinSpool implementations. macOS native control printing and page setup require the main thread. `PrintingSupported()` retains its original native-control meaning (macOS only); use `PrintingCapabilities()` for individual buffered-job features.

`New PrintSettingsSnapshot()` reads `PaperName` and native `Orientation` without changing shared print settings. `ExportControlPDF(control)` returns in-memory PDF bytes for a native view; it writes no file and submits no print job. `PrintControl(control, showPrintPanel = True)` runs an `NSPrintOperation` and returns its outcome. The print panel is shown by default; passing `False` permits direct submission. Window arguments use their content view.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add printing --git https://github.com/BuoyBay/printing.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

```basic
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

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer printing
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
