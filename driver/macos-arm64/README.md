# ProGlove driver — macos-arm64

Version 0.4.14.0

`proglove-headless-ipc-host` owns the glove's USB link, filters the tactile
stream and publishes it over ZeroMQ for the SDK:

```
./proglove-headless-ipc-host --hand left|right [--serial PRO-G…]
```

Status: `ipc:///tmp/proglove-<side>-status.ipc`, commands
`ipc:///tmp/proglove-<side>-commands.ipc`. `--help` lists every option.
