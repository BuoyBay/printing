---
title: "Printing and page setup"
summary: "Export native controls to PDF and manage isolated macOS print settings."
category: "Overview"
order: 0
keywords: ["printing", "macOS", "native"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# Printing and page setup

Use `printing` for native control PDF export, explicit print operations, and page setup. `PrinterSetup` owns a private copy of native settings, so changing an instance does not change application-wide shared print settings.

## Platform availability

`PrintingSupported()` covers macOS native control printing and page setup, which require the main thread. `BufferedPrintingSupported()` and `PrintingCapabilities()` describe Linux/Windows buffered printing, including discovery, `PrintText`, and `OpenPrinter`.

## Package use

Install `printing-0.1.0.buipkg` in the consumer project's `packages/` directory, then use `Import printing`. This package is independently sealed; it does not require importing the other desktop integration packages.

## Behavior and lifetime

This is a useful printing subset, not a complete Xojo printing framework. `OpenPrinter` returns buffered `PrinterGraphics`, with `NextPage` pagination and `Close` submission. ExportControlPDF writes no file and submits no job. Passing false for showPrintPanel permits direct job submission. Window controls use their content view. Page setup dialogs are modal; supplying a parentWindow currently throws because asynchronous attached sheets are not implemented.
## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
