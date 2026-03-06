# ParametrizeCamera_NativeParameterAccess

## 📋 Purpose
Demonstrates the **"native" approach** for reading and writing camera parameters using **device-specific instant camera classes** with **typed member variables**.

## 🔑 Key Concepts
- **`CBaslerUniversalInstantCamera`** — A device-specific class that exposes all GenICam parameters as **strongly-typed class members** (e.g., `camera.Width`, `camera.Gain`, `camera.PixelFormat`).
- **Type safety** — Native access uses enum constants (e.g., `PixelFormat_Mono8`) and typed members, catching errors at compile time instead of runtime.
- **Same operations, different syntax** — Achieves the same results as `ParametrizeCamera_GenericParameterAccess`, but with cleaner, more readable code.
- **Auto-complete support** — IDEs can provide auto-completion for all available camera parameters.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `camera.Width.SetValue(202, ...)` | Directly sets the Width parameter |
| `camera.Gain.SetValuePercentOfRange(50.0)` | Sets Gain to 50% of its range |
| `camera.PixelFormat.SetValue(PixelFormat_Mono8)` | Sets pixel format using an enum |
| `camera.GainAuto.TrySetValue(GainAuto_Off)` | Safely disables auto gain |
| `camera.GetSfncVersion()` | Checks the camera's SFNC version |

## 📌 When to Use
- **Preferred approach** for applications targeting a known set of camera models.
- When **compile-time type checking** and **IDE auto-completion** are desired.
- See also: `ParametrizeCamera_GenericParameterAccess` for the string-based alternative.
