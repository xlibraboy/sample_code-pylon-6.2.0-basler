# Utility_Image

## 📋 Purpose
Comprehensive demonstration of the **`CPylonImage`** and **`CPylonBitmapImage`** classes for creating, copying, manipulating, and displaying images.

## 🔑 Key Concepts
- **`CPylonImage`** — A reference-counted image container supporting various pixel types. Assigning or copying creates shared references (no data copy); use `CopyImage()` for a full copy.
- **User buffers** — `AttachUserBuffer()` allows wrapping externally owned memory as a pylon image for interop with third-party libraries.
- **Grab result attachment** — `AttachGrabResultBuffer()` wraps a grab result buffer, preventing its reuse until released.
- **AOI (Area of Interest)** — `GetAoi()` creates a sub-image view without copying data (uses padding to skip pixels outside the ROI).
- **Plane access** — `GetPlane()` extracts individual color planes from planar images (e.g., RGB8planar → separate R/G/B mono images).
- **`CPylonBitmapImage`** — Windows-specific class that auto-converts images to Windows bitmap format for display.
- **Sample images** — Uses `SampleImageCreator` to generate Julia and Mandelbrot fractals for demonstration.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `CPylonImage::Create()` | Creates an image with specified properties |
| `CopyImage()` | Creates a deep copy of the image |
| `AttachUserBuffer()` | Wraps external memory as a pylon image |
| `AttachGrabResultBuffer()` | Wraps a grab result buffer |
| `GetAoi()` | Creates a sub-image view (zero-copy) |
| `GetPlane()` | Extracts a single color plane |
| `Reset()` | Reuses or reallocates the buffer with new properties |

## 📌 When to Use
- Understanding pylon's image memory management model.
- **Zero-copy integration** with third-party image libraries.
- Extracting **regions of interest** or **color planes** efficiently.
