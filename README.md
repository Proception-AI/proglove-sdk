# ProGlove SDK

Client SDKs and host drivers for the ProGlove tactile glove (`PRO-G01` /
`PRO-G02`) and the ProWristCam wrist camera.

Product line `gen2` (branch `release/gen2`) · ProGlove SDK
0.4.14.1 · ProWristCam SDK 0.4.4.0

Releases of this line are tags named `gen2/<version>`.

## Layout

```
sdk/proglove_sdk/
├── cpp/       C header, C++ RAII wrapper, CMake package
├── python/    ctypes bindings (pip install -e sdk/proglove_sdk/python)
├── android/   AAR, JNI library and header for USB OTG
└── lib/       libproglove_client_sdk: .dylib (macOS arm64), .so (Linux x86_64),
               _aarch64.so (Linux arm64)
sdk/prowrist_sdk/
├── cpp/       C header, C++ wrapper, CMake package
├── python/    ctypes bindings (pip install -e sdk/prowrist_sdk/python)
└── lib/       libprowristcam_client_sdk, same platforms as above
driver/
├── <platform>/proglove-headless-ipc-host      the host that owns the glove's USB link
├── <platform>/prowristcam-headless-ipc-host   the host that owns the wrist camera
└── udev/      Linux rules and installer for non-root USB access to the glove
```

Platforms: macos-arm64 linux-arm64 linux-x64

## Quick start: glove

1. Plug the glove in and start the host for its side:

   ```bash
   ./driver/macos-arm64/proglove-headless-ipc-host --hand left
   ```

   It publishes the glove's status on `ipc:///tmp/proglove-left-status.ipc`.

1. Read it from Python:

   ```python
   import sys; sys.path.insert(0, "sdk/proglove_sdk/python")
   import proglove_sdk

   with proglove_sdk.ProGloveClient("ipc:///tmp/proglove-left-status.ipc") as client:
       client.send_ping()
       status = client.try_recv_status()
       if status and status.is_valid:
           print(status.t_dip)
   ```

   C and C++: `sdk/proglove_sdk/cpp/include/proglove_sdk/`. Android: `sdk/proglove_sdk/android/`.

On Linux, run `driver/udev/install-udev-rules.sh` once for non-root USB access.

## Quick start: wrist camera

1. Plug the camera in and start the host for its side:

   ```bash
   ./driver/macos-arm64/prowristcam-headless-ipc-host --side left
   ```

   It publishes JPEG frames on `ipc:///tmp/prowristcam-left-stream.ipc`.
   `--list-cameras` lists the cameras it sees; `--camera-id` picks one by
   serial or name.

1. Read frames from Python:

   ```python
   import sys; sys.path.insert(0, "sdk/prowrist_sdk/python")
   import prowrist_sdk

   with prowrist_sdk.WristCamClient("ipc:///tmp/prowristcam-left-stream.ipc") as client:
       frame = client.try_recv_frame()
       if frame:
           print(frame.width, frame.height, len(frame.jpeg))
   ```

   C and C++: `sdk/prowrist_sdk/cpp/include/prowrist_sdk/`.

On Linux, the camera is a standard UVC device: the user needs access to
`/dev/video*` (the `video` group).

## License

The SDK libraries and drivers are proprietary (`LICENSE`). Use requires
Proception hardware.
