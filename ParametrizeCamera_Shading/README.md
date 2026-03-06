# ParametrizeCamera_Shading

## 📋 Purpose
Demonstrates how to **calculate, upload, and apply gain shading correction** to compensate for non-uniform illumination across the sensor — **specific to Basler runner line scan cameras**.

## 🔑 Key Concepts
- **Gain shading** — Per-pixel gain multipliers that compensate for brightness variations across the sensor width (caused by uneven lighting or optical vignetting).
- **Calibration workflow:**
  1. **Acquire** a flat-field image (uniform illumination) with shading disabled.
  2. **Average** pixel intensities for each column (and color channel for RGB).
  3. **Calculate multipliers** so that `multiplier × intensity = max_intensity` for every pixel column.
  4. **Upload** the computed shading data to the camera's internal memory.
  5. **Verify** by grabbing a new image with shading enabled and checking uniformity.
- **Two shading sets** — The camera stores two user shading sets (`UserShadingSet1`, `UserShadingSet2`).
- **Fixed-point format** — Multipliers are stored as 32-bit fixed-point numbers (16.16 format), clamped to max 3.99998.
- **RGB support** — Handles both Mono8 and RGB8Packed pixel formats.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `camera.ShadingSelector` | Selects Gain or Offset shading |
| `camera.ShadingEnable` | Enables/disables shading correction |
| `camera.ShadingSetSelector` | Selects the target shading set |
| `camera.ShadingSetActivate.Execute()` | Activates the selected shading set |
| `GenApi::ODevFileStream` | Uploads data to the camera's internal file system |

## 📌 When to Use
- **Line scan applications** with non-uniform lighting across the web/field.
- **Paper, textile, or film inspection** using Basler runner cameras.
- Calibrating the camera to produce **uniform intensity output** under given lighting conditions.
