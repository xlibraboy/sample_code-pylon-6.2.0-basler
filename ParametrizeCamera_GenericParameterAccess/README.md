# ParametrizeCamera_GenericParameterAccess

## 📋 Purpose
Demonstrates the **"generic" approach** for reading and writing camera parameters using the `GenApi::INodeMap` interface with string-based parameter names.

## 🔑 Key Concepts
- **GenICam node map** — Camera parameters are represented as nodes in a node map, accessible by their name strings (e.g., `"Width"`, `"Gain"`, `"PixelFormat"`).
- **Parameter types** — `CIntegerParameter`, `CFloatParameter`, `CEnumParameter`, `CStringParameter` are used to wrap node map entries.
- **Value correction** — `IntegerValueCorrection_Nearest` automatically rounds values to the nearest valid increment.
- **SFNC versioning** — SFNC 2.0+ cameras use `"Gain"` (float); older cameras use `"GainRaw"` (integer).
- **"Try" functions** — `TrySetToMinimum()`, `TrySetValue()` only execute if the parameter is writable, avoiding exceptions.

## ⚙️ Key pylon API Used
| API | Description |
|---|---|
| `CIntegerParameter(nodemap, "Width")` | Wraps an integer node by name |
| `CFloatParameter(nodemap, "Gain")` | Wraps a float node by name |
| `CEnumParameter(nodemap, "PixelFormat")` | Wraps an enum node by name |
| `CStringParameter(nodemap, "DeviceVendorName")` | Wraps a string node by name |
| `SetValuePercentOfRange(50.0)` | Sets value to 50% of [Min, Max] range |

## 📌 When to Use
- When parameter names are **dynamic** (read from a config file, user input, etc.).
- **Transport-layer-agnostic** code that works across GigE, USB, CXP cameras.
- See also: `ParametrizeCamera_NativeParameterAccess` for the type-safe alternative.
