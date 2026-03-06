# 📷 Basler pylon 6.2.0 — C++ Sample Code

Complete collection of **Basler pylon SDK 6.2.0** C++ sample programs with detailed explanations. These samples demonstrate how to use the pylon C++ API for industrial camera applications — from basic image grabbing to advanced camera parameterization and utilities.

> **SDK:** pylon 6.2.0 · **Language:** C++ · **Standard:** GenICam / SFNC  
> **Camera Support:** GigE Vision, USB3 Vision, CoaXPress-12 (CXP-12), IEEE 1394

---

## 📁 Repository Structure

```
├── DeviceRemovalHandling/          # Camera hot-plug & reconnection
├── Grab/                           # Basic image grabbing
├── Grab_CameraEvents/              # Camera event handling
├── Grab_ChunkImage/                # Per-frame metadata (chunk data)
├── Grab_MultiCast/                 # GigE multicast streaming
├── Grab_MultipleCameras/           # Multi-camera acquisition
├── Grab_Strategies/                # Grab queue strategies
├── Grab_UsingActionCommand/        # GigE synchronized triggering
├── Grab_UsingBufferFactory/        # Custom buffer allocation
├── Grab_UsingExposureEndEvent/     # Low-latency exposure events
├── Grab_UsingGrabLoopThread/       # Background grab thread
├── Grab_UsingSequencer/            # Auto-cycling parameters
├── ParametrizeCamera_AutoFunctions/        # Auto Gain/Exposure/WB
├── ParametrizeCamera_Configurations/       # Configuration event handlers
├── ParametrizeCamera_GenericParameterAccess/  # Generic (string-based) access
├── ParametrizeCamera_LoadAndSave/          # Save/load .pfs files
├── ParametrizeCamera_LookupTable/          # Luminance LUT
├── ParametrizeCamera_NativeParameterAccess/   # Native (typed) access
├── ParametrizeCamera_SerialCommunication/  # Built-in UART
├── ParametrizeCamera_Shading/              # Gain shading correction
├── ParametrizeCamera_UserSets/             # User set presets
├── Utility_GrabVideo/              # Record to MP4
├── Utility_Image/                  # CPylonImage class usage
├── Utility_ImageDecompressor/      # Compression Beyond
├── Utility_ImageFormatConverter/   # Pixel format conversion
├── Utility_ImageLoadAndSave/       # Save/load TIFF, PNG, BMP
├── Utility_InstantInterface/       # CXP-12 interface control
├── Utility_IpConfig/               # GigE IP configuration
├── include/                        # Shared headers
└── Makefile                        # Top-level build file
```

Each folder contains:
- **`.cpp`** — The sample source code
- **`Makefile`** — Build rules (requires pylon 6.2.0 SDK installed)
- **`README.md`** — Detailed explanation of that sample

---

## 🔌 Device Management

### DeviceRemovalHandling
Demonstrates how to **detect camera disconnection** and **automatically reconnect** after a physical removal. Uses `CConfigurationEventHandler` to receive `OnCameraDeviceRemoved` callbacks. For GigE cameras, reduces the heartbeat timeout to **1000 ms** for fast detection. After removal, polls `EnumerateDevices()` with a serial-number filter to detect when the same camera reappears.

**Key API:** `CConfigurationEventHandler`, `OnCameraDeviceRemoved()`, `camera.IsCameraDeviceRemoved()`, `camera.DestroyDevice()`, `camera.Attach()`

---

## 📷 Image Grabbing

### Grab
The **simplest grabbing sample** — the starting point for any pylon application. Shows the basic workflow: create a `CInstantCamera`, start grabbing, retrieve `CGrabResultPtr` results in a loop, access pixel data and dimensions.

**Key API:** `CInstantCamera`, `StartGrabbing()`, `RetrieveResult()`, `CGrabResultPtr`

---

### Grab_CameraEvents
Demonstrates receiving **asynchronous camera event messages** such as **Exposure End** and **Event Overrun**. Multiple `CBaslerUniversalCameraEventHandler` instances are registered for different event types. The sample uses software triggering to control exactly when images are captured.

**Key API:** `CBaslerUniversalCameraEventHandler`, `RegisterCameraEventHandler()`, `camera.GrabCameraEvents`, `EventSelector`, `EventNotification`

---

### Grab_ChunkImage
Shows how to enable **chunk features** to retrieve per-frame metadata (**timestamps**, **frame counters**, **CRC checksums**) that is appended to each image by the camera. Demonstrates accessing chunk data via the grab result's node map (generic approach) and via device-specific members (native approach).

**Key API:** `ChunkModeActive`, `ChunkSelector`, `ChunkEnable`, `GetChunkDataNodeMap()`, `HasCRC()`, `CheckCRC()`

---

### Grab_MultiCast
Demonstrates **GigE multicast streaming** so multiple computers can receive the same camera stream simultaneously. One application opens the camera with full control and starts multicast streaming; a second application opens in **monitor mode** to receive the multicast stream without camera control.

**Key API:** `MonitorModeActive`, `TransmissionType_Multicast`, `DestinationAddr`, `DestinationPort` *(GigE only)*

---

### Grab_MultipleCameras
Shows how to grab images from **multiple cameras simultaneously** using `CInstantCameraArray`. Each camera is assigned a context value (its array index) which is attached to every grab result for identification. Important considerations: GigE bandwidth sharing via `GevSCPD` and `GevSCFTD` parameters.

**Key API:** `CInstantCameraArray`, `GetCameraContext()`, `EnumerateDevices()`

---

### Grab_Strategies
Explores the different **grab strategies** that control how images are queued and retrieved:

| Strategy | Behavior |
|---|---|
| `OneByOne` | All images queued in arrival order — process every frame |
| `LatestImageOnly` | Only the newest frame is kept — for live display |
| `LatestImages` | The N most recent frames are kept (configurable `OutputQueueSize`) |
| `UpcomingImage` | Returns the very next captured frame (GigE only) |

**Key API:** `StartGrabbing(strategy)`, `OutputQueueSize`, `GetNumberOfSkippedImages()`

---

### Grab_UsingActionCommand
Demonstrates using **GigE Vision Action Commands** to trigger multiple cameras simultaneously over the network. Unlike software triggers (sent individually), action commands are broadcast and reach all cameras with matching `DeviceKey`, `GroupKey`, and `GroupMask` at the same time.

**Key API:** `IGigETransportLayer`, `IssueActionCommand()`, `CActionTriggerConfiguration` *(GigE only)*

---

### Grab_UsingBufferFactory
Shows how to provide a **custom buffer factory** (`IBufferFactory`) for grabbing images into user-supplied memory buffers. Useful for zero-copy integration with third-party image processing libraries, GPU-pinned memory, or shared-memory IPC.

**Key API:** `IBufferFactory`, `SetBufferFactory()`, `AllocateBuffer()`, `FreeBuffer()`, `GetBufferContext()`

---

### Grab_UsingExposureEndEvent
Demonstrates using the **Exposure End event** to react before the image data transfer is complete — allowing earlier movement of objects or sensor heads. Events and images are correlated by frame number for matching.

**Key API:** `CBaslerUniversalCameraEventHandler`, `CBaslerUniversalImageEventHandler`, `EventExposureEndFrameID`, `GetBlockID()`

---

### Grab_UsingGrabLoopThread
Shows how to use the **internal grab loop thread** provided by `CInstantCamera`. The grab loop runs in a background thread, calling registered `CImageEventHandler` instances when images arrive. The main thread remains free for UI or other tasks.

**Key API:** `GrabLoop_ProvidedByInstantCamera`, `CImageEventHandler`, `RegisterImageEventHandler()`

---

### Grab_UsingSequencer
Demonstrates the camera's **sequencer feature** to automatically cycle through different acquisition settings (e.g., different image heights) on successive frames — useful for multi-exposure inspection or HDR-like acquisition.

**Key API:** `SequencerMode`, `SequencerConfigurationMode`, `SequencerSetSelector`, `SequencerSetSave`, `SequencerTriggerSource`

---

## ⚙️ Camera Parameterization

### ParametrizeCamera_AutoFunctions
Comprehensive demonstration of **Auto Gain** (once/continuous), **Auto Exposure** (once/continuous), and **Auto White Balance**. Shows how to set target brightness, limits, and regions of interest for the auto functions.

**Key API:** `GainAuto`, `ExposureAuto`, `BalanceWhiteAuto`, `AutoTargetBrightness`, `AutoFunctionROISelector`

---

### ParametrizeCamera_Configurations
Demonstrates using **configuration event handlers** to modularly set up camera acquisition modes. Pylon provides standard handlers: `CAcquireContinuousConfiguration`, `CSoftwareTriggerConfiguration`, `CAcquireSingleFrameConfiguration`. Shows registration modes (`ReplaceAll` vs `Append`) and handler stacking.

**Key API:** `CConfigurationEventHandler`, `RegisterConfiguration()`, `DeregisterConfiguration()`

---

### ParametrizeCamera_GenericParameterAccess
The **"generic" approach** for reading/writing camera parameters using string-based names via `GenApi::INodeMap`. Uses `CIntegerParameter`, `CFloatParameter`, `CEnumParameter`, `CStringParameter` wrappers. Transport-layer-agnostic — works across GigE, USB, and CXP cameras.

**Key API:** `CIntegerParameter(nodemap, "Width")`, `CFloatParameter(nodemap, "Gain")`, `CEnumParameter(nodemap, "PixelFormat")`, `SetValuePercentOfRange()`

---

### ParametrizeCamera_NativeParameterAccess
The **"native" approach** using `CBaslerUniversalInstantCamera` which exposes all GenICam parameters as **strongly-typed class members** (e.g., `camera.Width`, `camera.Gain`, `camera.PixelFormat`). Provides compile-time type checking and IDE auto-completion.

**Key API:** `CBaslerUniversalInstantCamera`, `camera.Width.SetValue()`, `camera.Gain.SetValuePercentOfRange()`, `camera.PixelFormat.SetValue(PixelFormat_Mono8)`

---

### ParametrizeCamera_LoadAndSave
Demonstrates how to **save** all camera settings to a `.pfs` (pylon Feature Stream) file and **load** them back. Useful for storing camera recipes, backing up configurations, and deploying identical settings to multiple cameras.

**Key API:** `CFeaturePersistence::Save()`, `CFeaturePersistence::Load()`

---

### ParametrizeCamera_LookupTable
Shows how to use the **Luminance Lookup Table (LUT)** to transform sensor pixel values before output. The sample creates an LUT that inverts sensor values. Supports both 10-bit (1024 entries) and 12-bit (4096 entries) lookup tables.

**Key API:** `LUTSelector`, `LUTIndex`, `LUTValue`, `LUTEnable`

---

### ParametrizeCamera_SerialCommunication
Demonstrates the camera's built-in **UART (serial communication)** module available on select models (e.g., ace 2 Pro). Shows transmitting and receiving data via GPIO lines in loopback and external modes. Configures baud rate, data bits, parity, and stop bits. Includes error detection for overflow, parity, and stop-bit errors.

**Key API:** `BslSerialBaudRate`, `BslSerialTransferBuffer`, `BslSerialTransmit`, `BslSerialReceive`, `BslSerialRxSource`

---

### ParametrizeCamera_Shading
Demonstrates how to **calculate, upload, and apply gain shading correction** for Basler runner **line scan cameras**. Compensates for non-uniform illumination by computing per-pixel gain multipliers from a flat-field calibration image.

**Key API:** `ShadingSelector`, `ShadingEnable`, `ShadingSetSelector`, `ShadingSetActivate`, `GenApi::ODevFileStream` *(Line scan cameras only)*

---

### ParametrizeCamera_UserSets
Shows how to use **user configuration sets (user sets)** to save/load camera parameter presets in non-volatile memory, and how to set a user set as the **default power-up configuration**.

> ⚠️ Executing this sample will overwrite settings in UserSet1.

**Key API:** `UserSetSelector`, `UserSetSave`, `UserSetLoad`, `UserSetDefault`

---

## 🔧 Utilities

### Utility_GrabVideo
Creates an **MP4 video file** from grabbed camera images using `CVideoWriter`. Requires the pylon Supplementary Package for MPEG-4. Configures frame rate, quality, resolution, and handles automatic format conversion.

**Key API:** `CVideoWriter`, `IsSupported()`, `SetParameter()`, `Add()`, `BytesWritten`

---

### Utility_Image
Comprehensive demonstration of the **`CPylonImage`** class: creating images, reference counting, full copies, attaching user buffers, attaching grab result buffers, extracting **AOIs** (zero-copy), extracting **color planes**, and the Windows-specific `CPylonBitmapImage` class.

**Key API:** `CPylonImage::Create()`, `CopyImage()`, `AttachUserBuffer()`, `GetAoi()`, `GetPlane()`, `Reset()`

---

### Utility_ImageDecompressor
Demonstrates enabling the **Compression Beyond** feature and decompressing images using `CImageDecompressor`. Supports both **lossless** and **fix ratio** (lossy) compression modes. Shows compression ratio calculation and metadata extraction.

**Key API:** `ImageCompressionMode`, `ImageCompressionRateOption`, `CImageDecompressor`, `GetCompressionInfo()`, `DecompressImage()`

---

### Utility_ImageFormatConverter
Shows how to use **`CImageFormatConverter`** to convert between pixel formats (e.g., RGB8 → Mono16). Includes output bit alignment control and a check to skip conversion when the image already matches the target format.

**Key API:** `CImageFormatConverter`, `OutputPixelFormat`, `OutputBitAlignment`, `Convert()`, `ImageHasDestinationFormat()`

---

### Utility_ImageLoadAndSave
Demonstrates **saving images** to TIFF, PNG, BMP (Windows), and JPEG (Windows) formats, and **loading** them back. Shows JPEG quality control, auto-conversion for incompatible pixel formats, and direct save from grab results.

**Key API:** `CImagePersistence::Save()`, `CImagePersistence::Load()`, `CanSaveWithoutConversion()`, `CImagePersistenceOptions::SetQuality()`

---

### Utility_InstantInterface
Shows how to use **`CUniversalInstantInterface`** to access **CXP-12 interface card** parameters, specifically **Power-over-CoaXPress (PoCXP)** control. Demonstrates power cycling and real-time monitoring of current, voltage, and power on port 0.

**Key API:** `CUniversalInstantInterface`, `CxpPoCxpStatus`, `CxpPort0Current()`, `CxpPort0Voltage()`, `CxpPort0Power()` *(CXP-12 only)*

---

### Utility_IpConfig
A **command-line utility** for configuring GigE camera IP addresses. Supports **static IP**, **DHCP**, and **Auto-IP (LLA)** modes. Enumerates all GigE devices and displays their network configuration. Uses broadcast-based IP configuration for cameras not yet reachable on the current subnet.

```bash
# Usage:
Utility_IpConfig <MAC> <IP> [MASK] [GATEWAY]
Utility_IpConfig 0030531596CF 192.168.1.100            # Static IP
Utility_IpConfig 0030531596CF DHCP                      # DHCP mode
Utility_IpConfig 0030531596CF AUTO                      # Auto-IP
```

**Key API:** `IGigETransportLayer`, `EnumerateAllDevices()`, `BroadcastIpConfiguration()`, `RestartIpConfiguration()` *(GigE only)*

---

## 📁 Shared Headers (`include/`)

| Header | Description |
|---|---|
| `CameraEventPrinter.h` | Prints camera events to the console |
| `ConfigurationEventPrinter.h` | Prints configuration lifecycle events for debugging |
| `ImageEventPrinter.h` | Prints image event callbacks |
| `PixelFormatAndAoiConfiguration.h` | Sets Mono8 pixel format and max frame rate AOI |
| `SampleImageCreator.h` | Generates Julia/Mandelbrot fractal test images |

---

## 🛠️ Building

### Prerequisites
- **Basler pylon SDK 6.2.0** installed (default: `/opt/pylon`)
- **Linux** with GCC / G++ compiler
- **Make** build tool

### Build All Samples
```bash
make -j$(nproc)
```

### Build a Single Sample
```bash
cd Grab
make
```

### Run a Sample
```bash
cd Grab
./Grab
```

---

## 📚 Reference

- [Basler pylon SDK Documentation](https://docs.baslerweb.com/)
- [pylon C++ API Reference](https://docs.baslerweb.com/pylon-api)
- [GenICam Standard (EMVA)](http://www.genicam.org/)
- [Basler Product Documentation](https://docs.baslerweb.com/)

---

## 📄 License

These samples are provided by Basler AG as part of the pylon SDK 6.2.0. Refer to the Basler pylon license agreement for usage terms.
