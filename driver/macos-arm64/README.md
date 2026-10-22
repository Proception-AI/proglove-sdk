# ProGlove drivers — macos-arm64

ProGlove SDK 0.4.14.1 · ProWristCam SDK 0.4.4.0

`proglove-headless-ipc-host` owns the glove's USB link, filters the tactile
stream and publishes it over ZeroMQ for the SDK:

```
./proglove-headless-ipc-host --hand left|right [--serial PRO-G…]
```

Status: `ipc:///tmp/proglove-<side>-status.ipc`, commands
`ipc:///tmp/proglove-<side>-commands.ipc`.

`prowristcam-headless-ipc-host` captures the wrist camera and publishes JPEG
frames for the SDK:

```
./prowristcam-headless-ipc-host --side left|right [--camera-id <serial or name>]
```

Frames: `ipc:///tmp/prowristcam-<side>-stream.ipc`, control
`ipc:///tmp/prowristcam-<side>-control.ipc`. `--help` lists every option of
either host.
