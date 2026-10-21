# ProGlove SDK

Client SDK and host driver for the ProGlove tactile glove (`PRO-G01` / `PRO-G02`).

Version 0.4.14.0

## Layout

```
sdk/proglove_sdk/
├── cpp/       C header, C++ RAII wrapper, CMake package
├── python/    ctypes bindings (pip install -e sdk/proglove_sdk/python)
├── android/   AAR, JNI library and header for USB OTG
└── lib/       libproglove_client_sdk: .dylib (macOS arm64), .so (Linux x86_64),
               _aarch64.so (Linux arm64)
driver/
├── <platform>/proglove-headless-ipc-host   the host that owns the glove's USB link
└── udev/      Linux rules and installer for non-root USB access
```

Platforms: macos-arm64 linux-arm64 linux-x64

## Quick start

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

## License

The SDK libraries and drivers are proprietary (`LICENSE`). Use requires
Proception hardware.
