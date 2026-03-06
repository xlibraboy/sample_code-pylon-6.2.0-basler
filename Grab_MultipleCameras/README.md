# Grab_MultipleCameras

## 📋 Purpose
Demonstrates how to **grab images from multiple cameras** simultaneously using `CInstantCameraArray`.

## 🔑 Key Concepts
- **`CInstantCameraArray`** — A convenience class that manages an array of `CInstantCamera` objects, providing a single `RetrieveResult()` method for all cameras.
- **Camera context** — Each camera in the array is assigned a context value (its array index), which is attached to every grab result to identify the source camera.
- **Bandwidth management** — When multiple GigE cameras share a network adapter, the `GevSCPD` (interpacket delay) and `GevSCFTD` (frame transmission delay) parameters should be configured to avoid bandwidth conflicts.
- **Sequential start** — Grabbing starts one camera at a time; for truly simultaneous capture, a hardware trigger setup is needed.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `CInstantCameraArray` | Array wrapper for multiple instant cameras |
| `cameras.StartGrabbing()` | Starts grabbing on all cameras in the array |
| `cameras.RetrieveResult()` | Retrieves the next result from any camera |
| `ptrGrabResult->GetCameraContext()` | Identifies which camera produced the result |
| `tlFactory.EnumerateDevices()` | Discovers all connected camera devices |

## 📌 When to Use
- **Multi-camera inspection** setups (e.g., top/bottom/side views).
- Acquiring images from up to `c_maxCamerasToUse` cameras in a single application.
- Any scenario requiring **centralized multi-camera management**.
