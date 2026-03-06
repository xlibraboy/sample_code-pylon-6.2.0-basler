# ParametrizeCamera_LookupTable

## 📋 Purpose
Demonstrates how to use the **Luminance Lookup Table (LUT)** to transform sensor pixel values before they are output as image data.

## 🔑 Key Concepts
- **LUT (Lookup Table)** — Maps every possible input pixel value to a custom output value, allowing arbitrary intensity transformations.
- **LUT types** — Cameras may have **10-bit** (1024 entries) or **12-bit** (4096 entries) lookup tables.
- **Intensity inversion** — The sample creates an LUT that inverts sensor values (e.g., bright pixels become dark and vice versa).
- **Enable/Disable** — The LUT can be toggled on/off at runtime via `LUTEnable`.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `camera.LUTSelector` | Selects which LUT to configure (e.g., Luminance) |
| `camera.LUTIndex` | Sets the input index for the current LUT entry |
| `camera.LUTValue` | Sets the output value for the current LUT entry |
| `camera.LUTEnable` | Enables/disables the selected LUT |

## 📌 When to Use
- **Gamma correction** or custom tone-curve mapping in-camera.
- **Threshold-based filtering** (e.g., mapping all values below a threshold to 0).
- Performing **intensity transformations** without host CPU overhead.
