# Grab

## 📋 Purpose
The **simplest image grabbing sample** — demonstrates the basic workflow of grabbing and processing images asynchronously using `CInstantCamera`.

## 🔑 Key Concepts
- **Asynchronous grabbing** — While the application processes one buffer, the next image is being acquired in parallel.
- **Buffer pool** — `CInstantCamera` uses an internal pool of buffers (`MaxNumBuffer = 5`) to retrieve image data from the camera.
- **Grab result smart pointer** — `CGrabResultPtr` holds the image data and metadata; the buffer is automatically reused when the smart pointer is released.
- **Free-running continuous acquisition** — The default configuration sets up the camera for continuous image capture without external triggers.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `CInstantCamera` | High-level camera class for easy image acquisition |
| `camera.StartGrabbing(count)` | Starts grabbing a specified number of images |
| `camera.RetrieveResult()` | Waits for and retrieves the next grab result |
| `CGrabResultPtr` | Smart pointer holding image data, dimensions, and error info |
| `ptrGrabResult->GetWidth()` | Returns the width of the grabbed image |
| `ptrGrabResult->GetBuffer()` | Returns a pointer to the raw pixel data |

## 📌 When to Use
- **Starting point** for any pylon-based application.
- Quick prototyping of image acquisition pipelines.
- Learning the fundamental pylon grab workflow before adding complexity.
