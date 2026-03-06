# Utility_InstantInterface

## 📋 Purpose
Demonstrates how to use **`CUniversalInstantInterface`** to access and control parameters of a **Basler CXP-12 interface card**, such as **Power-over-CoaXPress (PoCXP)** settings.

## 🔑 Key Concepts
- **Interface-level access** — Unlike camera-level access, this sample targets the **frame grabber / interface card** itself.
- **CXP-12** — CoaXPress-12 is a high-speed camera interface standard; the CXP interface card provides power and data connectivity.
- **PoCXP control** — The sample demonstrates switching power **off** and **on** (Auto mode), then waiting for the camera to start up.
- **Power monitoring** — Real-time readings of current (mA), voltage (V), and power (W) on Port 0 of the interface card.
- **`PylonAutoInitTerm`** — An RAII wrapper that automatically initializes and terminates the pylon runtime.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `CUniversalInstantInterface` | High-level interface card access class |
| `CInterfaceInfo` | Filters for specific interface card types |
| `instantInterface.CxpPoCxpStatus` | Controls PoCXP power state |
| `instantInterface.CxpPort0Current()` | Reads current draw on port 0 |
| `instantInterface.CxpPort0Voltage()` | Reads voltage on port 0 |
| `instantInterface.DeviceUpdateList.Execute()` | Refreshes the device list |

## 📌 When to Use
- **CXP-12 frame grabber management** — power cycling, diagnostics.
- Monitoring **power consumption** of connected CXP cameras.
- Automated **power-on/off sequences** in production systems.
