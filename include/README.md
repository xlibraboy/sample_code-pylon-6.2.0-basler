# include (Shared Headers)

## 📋 Purpose
Contains **shared header files** used by multiple C++ sample applications. These are helper utilities — not standalone samples.

## 📁 Files

| Header | Description |
|---|---|
| `CameraEventPrinter.h` | Prints camera events (e.g., Exposure End, Event Overrun) to the console. Used by event-handling samples. |
| `ConfigurationEventPrinter.h` | Prints configuration lifecycle events (`OnAttach`, `OnOpen`, `OnGrabStart`, etc.) for debugging camera state transitions. |
| `ImageEventPrinter.h` | Prints image event callbacks (`OnImageGrabbed`, `OnImagesSkipped`) to the console. |
| `PixelFormatAndAoiConfiguration.h` | A reusable configuration handler that sets the pixel format to Mono8 and adjusts the AOI (Area of Interest) for maximum frame rate. |
| `SampleImageCreator.h` | Generates **Julia fractal** and **Mandelbrot fractal** test images in various pixel formats — used by Utility_Image, Utility_ImageFormatConverter, and Utility_ImageLoadAndSave samples. |

## 📌 When to Use
These headers are included by the sample `.cpp` files as needed. They are useful as **reference implementations** for custom event printers, configuration handlers, and test image generators.
