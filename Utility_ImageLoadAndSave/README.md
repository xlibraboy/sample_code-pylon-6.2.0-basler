# Utility_ImageLoadAndSave

## 📋 Purpose
Demonstrates how to **save images to disk** and **load images from disk** in various file formats using the `CImagePersistence` class.

## 🔑 Key Concepts
- **Supported formats** — TIFF, PNG, BMP (Windows), JPEG (Windows).
- **Auto-conversion** — If the image pixel format is not directly supported by the file format, pylon automatically converts it (e.g., RGB16 → BGR8 for BMP).
- **16-bit support** — TIFF and PNG support 16-bit pixel data; the output is MSB-aligned.
- **`CanSaveWithoutConversion()`** — Checks whether format conversion will be needed for the given combination of image and file format.
- **JPEG quality** — Adjustable via `CImagePersistenceOptions::SetQuality()` (0–100).
- **Save from grab result** — `CGrabResultPtr` provides an `IImage` cast operator, allowing direct save without intermediate copies.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `CImagePersistence::Save()` | Saves an image or raw buffer to a file |
| `CImagePersistence::Load()` | Loads an image from a file into a `CPylonImage` |
| `CImagePersistence::CanSaveWithoutConversion()` | Checks if format conversion is needed |
| `CImagePersistenceOptions::SetQuality()` | Sets JPEG compression quality |

## 📌 When to Use
- **Saving defect images** for later review or reporting.
- **Loading reference images** for comparison-based inspection.
- **Archiving** grabbed images in standard file formats.
