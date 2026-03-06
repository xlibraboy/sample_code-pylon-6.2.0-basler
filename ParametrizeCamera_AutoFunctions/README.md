# ParametrizeCamera_AutoFunctions

## 📋 Purpose
Comprehensive demonstration of the camera's **auto functions**: **Auto Gain** (once/continuous), **Auto Exposure** (once/continuous), and **Auto White Balance**.

## 🔑 Key Concepts
- **"Once" mode** — The camera automatically adjusts the parameter until a target brightness is reached, then switches to "Off".
- **"Continuous" mode** — The camera continuously adjusts the parameter on every frame to maintain the target brightness.
- **Auto Function ROI/AOI** — Defines the region of the sensor used for gathering luminance/white balance statistics.
- **Target brightness** — `AutoTargetBrightness` (SFNC 2.0+, 0.0–1.0) or `AutoTargetValue` (0–255) sets the desired brightness.
- **Color cameras** — `BalanceWhiteAuto` adjusts R/G/B balance ratios for color cameras.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `camera.GainAuto` | Controls Auto Gain mode (Once/Continuous/Off) |
| `camera.ExposureAuto` | Controls Auto Exposure mode |
| `camera.BalanceWhiteAuto` | Controls Auto White Balance mode |
| `camera.AutoTargetBrightness` | Target brightness for luminance control |
| `camera.AutoFunctionROISelector` | Selects the ROI for auto function statistics |

## 📌 When to Use
- Initial camera setup to determine appropriate gain/exposure values.
- Applications with **varying lighting conditions** that need continuous adjustment.
- Color calibration using auto white balance.
