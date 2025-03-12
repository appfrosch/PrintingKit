# Getting Started

This article explains how to get started with PrintingKit.

@Metadata {

    @PageImage(
        purpose: card,
        source: "Page",
        alt: "Page icon"
    )

    @PageColor(blue)
}


## Overview

PrintingKit currently supports the following ``PrintItem`` types:

* ``PrintItem/attributedString(_:configuration:)`` - an attributed string.
* ``PrintItem/imageData(_:)`` - JPG or PNG data (iOS only).
* ``PrintItem/imageFile(at:)`` - a JPG or PNG file at a certain URL.
* ``PrintItem/pdfData(_:)`` - PDF document data.
* ``PrintItem/pdfFile(at:)`` - a PDF document file at a certain URL.
* ``PrintItem/string(_:configuration:)`` - a plain string.
* ``PrintItem/view(_:withScale:)`` - any SwiftUI view.

More types can be added in the future. Feel free to contribute if you have a new type that you'd like to support.


## How to print a print item

To print any of the supported ``PrintItem``s, just create a ``Printer`` instance, or use ``Printer/shared``:

```swift
struct MyView: View {

    let printer = Printer.shared

    var body: some View {
        VStack {
            Button("Print PDF") {
                try? printer.print(.pdf(at: anyUrl))
            }
            Button("Print view") {
                try? printer.print(image)
            }
            Button("Print view without try") {
                printer.printInTask(image)
            }
        }
    }
}
```

This will show a print dialog that you can use to perform the print operation, or export to PDF.


## PDF support

PrintingKit also has ``Pdf`` utilities, that can be used to configure a PDF documentations, page margins, etc. They're used by the SDK when printing ``PrintItem/pdfData(_:)`` and ``PrintItem/pdfFile(at:)``, but you can use then as standalone utilities as well.


## Configuring your project for macOS

There are two settings that are manadatory for a sandboxed application on macOS (which is default). In the target's "Signing & Capabilities" > "App Sandbox" section 
1. check the "Printer" checkbox or you'll be met with the error "This application does not support printing." (required for printing itself) and
2. set the "User Selected File" type under "File Access" to "Read/Write", or the error "Unable to display save panel …" will show up (required if you want to save the to a PDF file)


