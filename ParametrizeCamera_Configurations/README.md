# ParametrizeCamera_Configurations

## 📋 Purpose
Demonstrates how to use **configuration event handlers** to modularly set up camera acquisition modes (continuous, software trigger, single frame).

## 🔑 Key Concepts
- **Configuration event handlers** — Classes derived from `CConfigurationEventHandler` that override `OnOpened()` to apply camera parameters when the camera is opened.
- **Standard configurations** — pylon provides `CAcquireContinuousConfiguration`, `CSoftwareTriggerConfiguration`, and `CAcquireSingleFrameConfiguration`.
- **Registration modes** — `RegistrationMode_ReplaceAll` replaces all existing handlers; `RegistrationMode_Append` adds a new one alongside existing ones.
- **Stacking configurations** — Multiple configuration handlers can be registered (appended) for layered parameterization.
- **Cleanup options** — `Cleanup_Delete` lets pylon manage handler lifetime; `Cleanup_None` requires manual deletion.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `CAcquireContinuousConfiguration` | Configures free-running continuous acquisition |
| `CSoftwareTriggerConfiguration` | Configures software-triggered acquisition |
| `CAcquireSingleFrameConfiguration` | Configures single-frame acquisition |
| `camera.RegisterConfiguration()` | Registers a configuration event handler |
| `camera.DeregisterConfiguration()` | Removes a registered handler |

## 📌 When to Use
- Implementing **reusable camera setup modules** for different acquisition scenarios.
- Quickly switching between acquisition modes in the same application.
- Creating custom configuration handlers for application-specific setups.
