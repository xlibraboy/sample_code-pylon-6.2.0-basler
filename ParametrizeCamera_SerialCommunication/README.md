# ParametrizeCamera_SerialCommunication

## 📋 Purpose
Demonstrates how to use the camera's built-in **UART (asynchronous serial communication)** module to transmit and receive data via digital I/O lines.

## 🔑 Key Concepts
- **UART capability** — Available on select camera models (e.g., **ace 2 Pro**), enabling serial communication with external devices (sensors, PLCs, etc.) directly through the camera.
- **Loopback mode** — For testing, the TX output is routed directly to the RX input without external hardware.
- **GPIO mode** — In production, Lines 2 and 3 can be used as TX (output) and RX (input) respectively.
- **Transfer buffer** — Data is written/read through `BslSerialTransferBuffer` in chunks; GigE cameras require multiples of 4 bytes (with padding).
- **Error detection** — Overflow, parity, and stop bit error flags are checked after each receive operation.
- **Break condition** — Can be sent/detected to signal special events on the serial line.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `camera.BslSerialBaudRate` | Sets the serial baud rate (e.g., 115200) |
| `camera.BslSerialTransferBuffer` | Read/write transfer buffer |
| `camera.BslSerialTransmit.Execute()` | Starts data transmission |
| `camera.BslSerialReceive.Execute()` | Receives data from the FIFO |
| `camera.BslSerialRxSource` | Configures the RX input source |
| `camera.BslSerialTxFifoEmpty` | Checks if the TX FIFO is empty |

## 📌 When to Use
- **Communicating with external devices** (barcode readers, encoders, actuators) without additional serial adapters.
- **Tight integration** of serial I/O with camera acquisition timing.
- **ace 2 Pro cameras** and similar models with built-in UART support.
