# ParametrizeCamera_LoadAndSave

## 📋 Purpose
Demonstrates how to **save** all camera settings to a `.pfs` file and **load** them back, enabling persistent configuration across sessions.

## 🔑 Key Concepts
- **pylon Feature Stream (.pfs)** — A text-based file format that stores all writable camera parameters and their values.
- **`CFeaturePersistence::Save()`** — Writes the complete node map state to a `.pfs` file.
- **`CFeaturePersistence::Load()`** — Reads a `.pfs` file and applies the saved values to the camera, with optional validation.
- **Validation** — When the third parameter is `true`, pylon validates that the loaded parameter values are compatible with the current camera model.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `CFeaturePersistence::Save()` | Saves camera parameters to a `.pfs` file |
| `CFeaturePersistence::Load()` | Loads parameters from a `.pfs` file back to the camera |
| `camera.GetNodeMap()` | Provides the node map for persistence operations |

## 📌 When to Use
- **Storing camera recipes** for different products or inspection jobs.
- **Backing up** camera configuration before firmware updates.
- **Deploying identical settings** to multiple cameras of the same model.
