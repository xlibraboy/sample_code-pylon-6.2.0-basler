# Grab_Strategies

## 📋 Purpose
Demonstrates the different **grab strategies** available in `CInstantCamera` that control how images are queued and retrieved.

## 🔑 Key Concepts

### Strategies Demonstrated
| Strategy | Behavior |
|---|---|
| `GrabStrategy_OneByOne` | Images are processed in arrival order. All acquired images are queued. |
| `GrabStrategy_LatestImageOnly` | Only the **most recent** image is kept in the output queue; older images are discarded. |
| `GrabStrategy_LatestImages` | The N most recently received images are kept (controlled by `OutputQueueSize`). |
| `GrabStrategy_UpcomingImage` | A buffer is queued only when `RetrieveResult()` is called, ensuring the returned image is the **next** one captured. (Not available for USB cameras.) |

- **Software triggering** is used to control exactly when images are captured.
- `GetNumberOfSkippedImages()` reports how many images were discarded by the strategy.
- Setting `OutputQueueSize = 1` makes `LatestImages` equivalent to `LatestImageOnly`.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `camera.StartGrabbing(strategy)` | Starts grabbing with the specified strategy |
| `camera.OutputQueueSize` | Controls the output queue size for `LatestImages` |
| `GetNumberOfSkippedImages()` | Reports images discarded by the strategy |
| `GetGrabResultWaitObject()` | Checks if results are waiting in the output queue |

## 📌 When to Use
- **`OneByOne`** — When every image must be processed (inspection, recording).
- **`LatestImageOnly`** — When only the newest frame matters (live display).
- **`LatestImages`** — When a short history of recent frames is needed.
- **`UpcomingImage`** — When you need the very next frame after a processing step (GigE only).
