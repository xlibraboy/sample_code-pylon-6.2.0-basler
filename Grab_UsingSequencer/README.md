# Grab_UsingSequencer

## 📋 Purpose
Demonstrates how to use the camera's **sequencer feature** to automatically cycle through different acquisition settings (e.g., different image heights) on successive frames.

## 🔑 Key Concepts
- **Sequencer / Sequence sets** — Pre-defined parameter sets that the camera cycles through automatically during acquisition.
- **Three sequence steps** — The sample configures: quarter-height → half-height → full-height images, repeating cyclically.
- **SFNC 2.0+ vs legacy** — USB cameras use `SequencerMode` / `SequencerConfigurationMode`; older GigE cameras use `SequenceEnable` / `SequenceAdvanceMode`.
- **Auto advance** — The camera automatically advances to the next set on each frame trigger.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `camera.SequencerMode` | Enables/disables the sequencer (SFNC 2.0+) |
| `camera.SequencerConfigurationMode` | Enters/exits sequence configuration mode |
| `camera.SequencerSetSelector` | Selects the set to configure |
| `camera.SequencerSetSave.Execute()` | Saves the current parameters to the selected set |
| `camera.SequencerTriggerSource` | Defines what advances to the next set |

## 📌 When to Use
- **Multi-exposure inspection** — Cycling through different exposure times or image sizes per frame.
- **HDR-like acquisition** — Alternating between bright and dark exposures.
- Reducing host-side parameter changes by letting the camera auto-cycle.
