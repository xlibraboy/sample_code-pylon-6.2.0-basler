# ParametrizeCamera_UserSets

## 📋 Purpose
Demonstrates how to use **user configuration sets (user sets)** to save and load camera parameter presets, and how to set a user set as the **default power-up configuration**.

## 🔑 Key Concepts
- **User sets** — The camera can store multiple parameter presets (Default, UserSet1, UserSet2, UserSet3) in non-volatile memory.
- **Save/Load workflow:**
  1. Load defaults, modify gain and exposure, save to UserSet1.
  2. Switch between Default and UserSet1 to compare settings.
  3. Set UserSet1 as the **startup default** so the camera uses these settings on power-up.
- **SFNC versioning** — USB cameras use `UserSetDefault`, older GigE cameras use `UserSetDefaultSelector`.
- **Auto function interaction** — Auto Gain and Auto Exposure must be disabled before manually setting gain/exposure values.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `camera.UserSetSelector` | Selects which user set to work with |
| `camera.UserSetSave.Execute()` | Saves current settings to the selected user set |
| `camera.UserSetLoad.Execute()` | Loads the selected user set into the camera |
| `camera.UserSetDefault` | Sets which user set to load on power-up (SFNC 2.0+) |

## ⚠️ Warning
> Executing this sample will **overwrite all current settings** in UserSet1.

## 📌 When to Use
- **Storing product-specific recipes** in the camera itself (no external config files needed).
- Configuring the camera's **power-up defaults** for standalone or embedded deployments.
- Quick switching between different inspection configurations.
