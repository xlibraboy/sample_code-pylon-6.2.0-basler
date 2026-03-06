# Grab_CameraEvents

## 📋 Purpose
Demonstrates how to **receive and process camera event messages** such as **Exposure End** and **Event Overrun**, which are sent asynchronously by the camera.

## 🔑 Key Concepts
- **Camera events** — USB3, GigE, and IEEE 1394 cameras can send event messages (e.g., "exposure finished") before the image data transfer is complete.
- **Event handlers** — Multiple `CBaslerUniversalCameraEventHandler` instances can be registered for different event types (Exposure End, Event Overrun).
- **Event nodes** — Event data is exposed as parameter nodes in the camera node map (e.g., `EventExposureEndFrameID`, `EventExposureEndTimestamp`).
- **Software triggering** — The sample uses `CSoftwareTriggerConfiguration` to control exactly when images are captured.
- **SFNC versioning** — Handles both SFNC 2.0+ (USB cameras) and older naming conventions (GigE cameras).

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `CBaslerUniversalCameraEventHandler` | Base class for camera event callbacks |
| `camera.RegisterCameraEventHandler()` | Registers a handler for a specific event node |
| `camera.GrabCameraEvents = true` | Enables camera event processing |
| `camera.EventSelector` | Selects which event type to configure |
| `camera.EventNotification` | Enables/disables notification for the selected event |
| `CSoftwareTriggerConfiguration` | Configures the camera for software-triggered acquisition |

## 📌 When to Use
- When you need to **react immediately** after a sensor exposure finishes (before the image arrives).
- Implementing **low-latency triggering** of downstream hardware (e.g., moving a conveyor belt).
- Monitoring for **event overruns** that indicate dropped events due to bandwidth constraints.
