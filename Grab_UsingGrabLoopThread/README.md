# Grab_UsingGrabLoopThread

## 📋 Purpose
Demonstrates how to use the **internal grab loop thread** provided by `CInstantCamera` to decouple image acquisition from the main application thread.

## 🔑 Key Concepts
- **`GrabLoop_ProvidedByInstantCamera`** — pylon runs the grab loop in a background thread, automatically calling registered image event handlers when images arrive.
- **Image event handlers** — `CImageEventHandler` subclasses process images in the grab loop thread (e.g., display, save, process).
- **Software triggering** — The main thread sends software triggers on user input, while the grab loop thread handles the results asynchronously.
- **Interactive control** — The user can press `t` to trigger the camera or `e` to exit.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `GrabLoop_ProvidedByInstantCamera` | Enables pylon's internal grab loop thread |
| `CImageEventHandler` | Base class for processing grabbed images |
| `camera.RegisterImageEventHandler()` | Registers one or more image handlers |
| `camera.WaitForFrameTriggerReady()` | Waits for the camera to accept the next trigger |
| `camera.ExecuteSoftwareTrigger()` | Sends a software trigger command |

## 📌 When to Use
- When the **main thread** should remain responsive (e.g., handling UI, user input).
- Event-driven architectures where image processing is done in callbacks.
- Decoupling acquisition from processing for better throughput.
