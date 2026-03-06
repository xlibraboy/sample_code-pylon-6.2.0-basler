# Utility_ImageFormatConverter

## 📋 Purpose
Demonstrates how to use the **`CImageFormatConverter`** class to convert images between different pixel formats (e.g., RGB8 → Mono16).

## 🔑 Key Concepts
- **Pixel format conversion** — Converts between any pylon-supported pixel formats (color ↔ mono, 8-bit ↔ 16-bit, Bayer ↔ RGB, etc.).
- **Bit alignment** — `OutputBitAlignment` controls whether higher bit-depth outputs are MSB or LSB aligned.
- **Skip optimization** — `ImageHasDestinationFormat()` checks if the source image already matches the target format, allowing you to skip unnecessary conversions.
- **Multiple overloads** — `Convert()` can output to `CPylonImage`, `CPylonBitmapImage`, or user buffers.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `CImageFormatConverter` | Main converter class |
| `converter.OutputPixelFormat` | Sets the target pixel format |
| `converter.OutputBitAlignment` | Controls MSB/LSB alignment for higher bit-depths |
| `converter.Convert(target, source)` | Performs the conversion |
| `converter.ImageHasDestinationFormat()` | Checks if conversion is needed |

## 📌 When to Use
- Converting Bayer-pattern images to RGB for display or processing.
- Standardizing images to a consistent pixel format for downstream algorithms.
- Preparing images for file formats that require specific pixel formats.
