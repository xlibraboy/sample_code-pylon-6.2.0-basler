# Utility_GrabVideo

## 📋 Purpose
Demonstrates how to **grab images from a camera and save them as an MP4 video file** using the `CVideoWriter` class.

## 🔑 Key Concepts
- **`CVideoWriter`** — pylon's built-in class for creating MPEG-4 video files from grabbed images.
- **Dependency** — Requires the **pylon Supplementary Package for MPEG-4** (checked at runtime via `CVideoWriter::IsSupported()`).
- **Configuration** — Frame rate (playback), quality (1–100), resolution, and pixel type must be set before opening the writer.
- **Auto-conversion** — If the grabbed image format doesn't match the video format, the writer automatically converts it (including flipping to `ImageOrientation_TopDown`).
- **Size limit** — The sample stops writing when a byte threshold (`c_maxImageDataBytesThreshold = 50 MB`) is exceeded.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `CVideoWriter` | Creates and writes MP4 video files |
| `CVideoWriter::IsSupported()` | Checks if the MPEG-4 package is installed |
| `videoWriter.SetParameter()` | Configures width, height, pixel type, FPS, quality |
| `videoWriter.Open("file.mp4")` | Opens the video file for writing |
| `videoWriter.Add(ptrGrabResult)` | Adds a grabbed frame to the video |
| `videoWriter.BytesWritten` | Reports the total bytes written so far |

## 📌 When to Use
- **Recording camera footage** for later review or analysis.
- Creating **video logs** of production line inspections.
- Quick prototyping of video capture applications.
