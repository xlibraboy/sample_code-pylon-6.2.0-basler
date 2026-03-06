# Utility_ImageDecompressor

## 📋 Purpose
Demonstrates how to enable the **Compression Beyond** feature on supported cameras and how to **decompress** the resulting images using `CImageDecompressor`.

## 🔑 Key Concepts
- **Compression Beyond** — A Basler feature that compresses images inside the camera before transfer, reducing bandwidth usage.
- **Lossless vs. Fix Ratio** — Two compression modes:
  - **Lossless** — No quality loss, variable compression ratio.
  - **Fix Ratio** — Guaranteed compression ratio, potentially lossy.
- **`CImageDecompressor`** — Initialized with the camera's node map; must be re-initialized via `SetCompressionDescriptor()` if compression parameters change.
- **`CompressionInfo_t`** — Contains metadata about the compressed image (status, dimensions, pixel type, decompressed size).
- **Transparent decompression** — Some transport layers may automatically decompress images, in which case the decompressor step can be skipped.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `camera.ImageCompressionMode` | Sets the compression mode (Off / BaslerCompressionBeyond) |
| `camera.ImageCompressionRateOption` | Selects Lossless or FixRatio compression |
| `CImageDecompressor(nodemap)` | Creates a decompressor initialized from camera settings |
| `decompressor.GetCompressionInfo()` | Retrieves compression metadata from a grab result |
| `decompressor.DecompressImage()` | Decompresses a compressed grab result into a target image |

## 📌 When to Use
- **Bandwidth-constrained** systems where the camera's output exceeds network capacity.
- GigE or USB setups where **reducing data transfer** is critical for high frame rates.
- Applications requiring minimal CPU overhead for decompression.
