# Grab_UsingExposureEndEvent

## 📋 Purpose
Shows how to use the **Exposure End event** to speed up image acquisition by reacting **before the image data transfer is complete** — enabling earlier movement of objects or sensor heads.

## 🔑 Key Concepts
- **Early action** — The Exposure End event arrives before the corresponding image, allowing the application to move the imaged item or sensor head while the data is still being transferred.
- **Event & image matching** — Events and images are correlated by frame number (`EventExposureEndFrameID` ↔ `ptrGrabResult->GetBlockID()`).
- **Event logging** — High-precision timestamps are recorded for each event/image/move action to measure timing.
- **Lost event detection** — The handler checks for unexpected frame numbers to detect lost events (especially relevant for GigE where network packets can be dropped).

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `CBaslerUniversalCameraEventHandler` | Base class for Exposure End event callbacks |
| `CBaslerUniversalImageEventHandler` | Base class for image arrival callbacks |
| `camera.GrabCameraEvents = true` | Enables camera event processing |
| `camera.EventExposureEndFrameID` | Frame ID from the event |
| `ptrGrabResult->GetBlockID()` | Frame ID from the grabbed image |

## 📌 When to Use
- **High-throughput inspection** where minimizing idle time between exposures is critical.
- Systems with **mechanical motion** that must begin moving immediately after exposure.
- **Note:** For ace 2 cameras, use chunk FrameID instead of `GetBlockID()` for matching.
