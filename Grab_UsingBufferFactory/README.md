# Grab_UsingBufferFactory

## 📋 Purpose
Demonstrates how to provide a **custom buffer factory** for grabbing images into **user-supplied memory buffers** instead of pylon-allocated buffers.

## 🔑 Key Concepts
- **`IBufferFactory` interface** — Implement `AllocateBuffer()`, `FreeBuffer()`, and `DestroyBufferFactory()` to supply your own memory management.
- **Buffer context** — Each allocated buffer can carry a user-defined context value (retrieved via `ptrGrabResult->GetBufferContext()`), useful for tracking buffers.
- **Zero-copy integration** — Allows grabbing directly into buffers owned by your image processing library, avoiding unnecessary memory copies.
- **Thread safety** — `AllocateBuffer()` and `FreeBuffer()` can be called from different threads.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `IBufferFactory` | Interface for custom buffer allocation |
| `camera.SetBufferFactory()` | Registers the custom buffer factory |
| `AllocateBuffer()` | Called by pylon when a new buffer is needed |
| `FreeBuffer()` | Called by pylon when a buffer is released |
| `GetBufferContext()` | Retrieves the user context from a grab result |

## 📌 When to Use
- **Advanced use cases** requiring control over buffer memory (e.g., GPU-pinned memory, shared-memory IPC).
- Integration with third-party libraries that require specific buffer alignment or allocation strategies.
