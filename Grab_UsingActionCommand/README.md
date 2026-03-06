# Grab_UsingActionCommand

## 📋 Purpose
Demonstrates how to use **GigE Vision Action Commands** to trigger **multiple cameras simultaneously** over the network.

## 🔑 Key Concepts
- **Action Commands** — A network broadcast that triggers all GigE cameras with matching `DeviceKey`, `GroupKey`, and `GroupMask` to grab an image at the same time.
- **Synchronized triggering** — Unlike software triggers (which are sent individually), action commands reach all cameras on the subnet simultaneously.
- **`CActionTriggerConfiguration`** — A provided configuration class that sets up `DeviceKey`, `GroupKey`, `GroupMask`, and configures `FrameTrigger` to listen for action commands.
- **Same-subnet filtering** — Cameras on different subnets are excluded since action commands are broadcast-based.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `IGigETransportLayer` | Interface to the GigE transport layer |
| `pTL->IssueActionCommand()` | Broadcasts the action command to all cameras |
| `CActionTriggerConfiguration` | Pre-built configuration for action command triggering |
| `CBaslerUniversalInstantCameraArray` | Array of device-specific instant cameras |

## 📌 When to Use
- **Synchronized multi-camera capture** in GigE setups.
- When software triggering latency is unacceptable and hardware trigger wiring is impractical.
- **GigE Vision only**.
