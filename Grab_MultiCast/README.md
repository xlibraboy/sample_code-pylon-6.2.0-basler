# Grab_MultiCast

## 📋 Purpose
Demonstrates how to use **GigE multicast streaming** so that multiple computers can receive the same camera stream simultaneously.

## 🔑 Key Concepts
- **Control mode** — One application (Computer A) opens the GigE camera with full control, configures it for multicast streaming, and starts acquisition.
- **Monitor mode** — A second application (Computer B) opens the camera in **monitor mode** (`MonitorModeActive = true`) and receives the multicast stream without being able to change camera parameters.
- **Multicast transmission** — The stream is sent to a multicast IP address (default `239.0.0.1:49152`), allowing any device on the network to subscribe.
- **`TransmissionType_UseCameraConfig`** — The monitor application can automatically pick up the multicast configuration from the controlling application.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `camera.MonitorModeActive` | Enables monitor (read-only) mode |
| `GetStreamGrabberParams().TransmissionType` | Configures multicast or unicast streaming |
| `TransmissionType_Multicast` | Sets the stream to multicast mode |
| `TransmissionType_UseCameraConfig` | Uses the active camera's multicast configuration |
| `DestinationAddr / DestinationPort` | Multicast IP address and port settings |

## 📌 When to Use
- **Multi-viewer setups** where multiple PCs need to see the same camera feed.
- **Distributed inspection systems** with separate processing nodes.
- **GigE Vision only** — this feature is specific to GigE cameras.
