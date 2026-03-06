# Utility_IpConfig

## 📋 Purpose
A **command-line utility** for configuring the **IP address** of GigE Vision cameras, supporting static IP, DHCP, and Auto-IP (LLA) modes.

## 🔑 Key Concepts
- **IP configuration modes:**
  - **Static (Persistent IP)** — Sets a specific IP address, subnet mask, and gateway.
  - **DHCP** — Camera obtains its IP from a DHCP server.
  - **AUTO (LLA)** — Camera self-assigns a link-local address (169.254.x.x).
- **Broadcast IP configuration** — Uses `BroadcastIpConfiguration()` to configure cameras that may not yet have a valid IP on the current subnet.
- **Device enumeration** — Lists all GigE cameras with their MAC, IP, subnet mask, gateway, current mode, and supported capabilities.
- **MAC address identification** — The target camera is identified by its MAC address (no separators, e.g., `0030531596CF`).

## 💻 Usage
```bash
Utility_IpConfig <MAC> <IP> [MASK] [GATEWAY]

# Examples:
Utility_IpConfig 0030531596CF 192.168.1.100              # Static IP
Utility_IpConfig 0030531596CF 192.168.1.100 255.255.255.0 192.168.1.1
Utility_IpConfig 0030531596CF DHCP                        # DHCP mode
Utility_IpConfig 0030531596CF AUTO                        # Auto-IP (LLA)
```

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `IGigETransportLayer` | GigE-specific transport layer interface |
| `pTl->EnumerateAllDevices()` | Discovers all GigE cameras on the network |
| `pTl->BroadcastIpConfiguration()` | Broadcasts IP config to a camera by MAC |
| `pTl->RestartIpConfiguration()` | Restarts the camera's network stack |
| `CDeviceInfo` | Provides MAC, IP, subnet, gateway, and mode info |

## 📌 When to Use
- **Initial camera network setup** — assigning IP addresses to new cameras.
- **Switching between DHCP and static** configurations.
- Automating camera network configuration in **deployment scripts**.
- **GigE Vision only**.
