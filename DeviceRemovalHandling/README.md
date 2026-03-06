# DeviceRemovalHandling

## 📋 Purpose
Demonstrates how to **detect camera disconnection** and **reconnect** to the same device after it has been physically removed and re-attached.

## 🔑 Key Concepts
- **Device removal detection** — The camera's `IsCameraDeviceRemoved()` method is used to check if a physical disconnection occurred.
- **Configuration event handler** — A custom `CSampleConfigurationEventHandler` is registered to receive `OnCameraDeviceRemoved` callbacks from a separate thread.
- **Heartbeat timeout** — For GigE cameras in debug mode, the heartbeat timeout is reduced to **1000 ms** (from the 5-minute debug default) so that disconnection is detected quickly.
- **Device reconnection** — After removal, the camera's serial number and device class are remembered. The application then polls `EnumerateDevices()` with a filter to detect when the same camera reappears, and re-attaches it.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `CConfigurationEventHandler` | Base class for handling camera lifecycle events |
| `OnCameraDeviceRemoved()` | Callback fired when physical removal is detected |
| `camera.IsCameraDeviceRemoved()` | Checks if the camera has been physically removed |
| `camera.DestroyDevice()` | Releases the internal pylon device after removal |
| `tlFactory.EnumerateDevices()` | Scans for available cameras matching a filter |
| `camera.Attach()` | Re-attaches a newly found pylon device |
| `CIntegerParameter("HeartbeatTimeout")` | Configures the GigE heartbeat timeout |

## 📌 When to Use
- Applications that must handle **hot-plug / hot-unplug** scenarios gracefully.
- Systems requiring **automatic reconnection** after a cable disconnect or power cycle.
- GigE camera setups where the default 5-minute debug heartbeat is too slow for disconnect detection.
