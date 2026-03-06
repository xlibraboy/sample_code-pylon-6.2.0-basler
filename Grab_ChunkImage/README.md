# Grab_ChunkImage

## 📋 Purpose
Demonstrates how to use **chunk features** to retrieve metadata (timestamps, frame counters, CRC checksums) that is **appended to each image** by the camera.

## 🔑 Key Concepts
- **Chunk mode** — When enabled, the camera transfers data blocks partitioned into chunks: the first chunk is always image data, followed by metadata chunks.
- **Chunk types** — This sample enables **Timestamp**, **Framecounter** (if available), and **PayloadCRC16** chunks.
- **CRC integrity check** — After grabbing, the CRC checksum can validate that the image data was not corrupted during transfer.
- **Accessing chunk data** — Chunk values can be read via the grab result's chunk data node map (generic) or via device-specific grab result members (native).

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `camera.ChunkModeActive` | Enables/disables chunk mode on the camera |
| `camera.ChunkSelector` | Selects which chunk feature to configure |
| `camera.ChunkEnable` | Enables the selected chunk feature |
| `ptrGrabResult->GetChunkDataNodeMap()` | Access chunk data via generic node map |
| `ptrGrabResult->ChunkTimestamp` | Direct access to timestamp chunk (native) |
| `ptrGrabResult->HasCRC() / CheckCRC()` | Validates image data integrity |

## 📌 When to Use
- When you need **per-frame metadata** (precise timestamps, frame IDs) embedded with the image.
- For **data integrity verification** using CRC checksums.
- Synchronizing images from multiple cameras using hardware timestamps.
