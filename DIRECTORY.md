```
piwo/
├── cfg/        ordinary MOHAA/OpenMoHAA CFG files used by PIWO
├── config/     YAML configuration, including global and per-map config
├── core/       shared PIWO framework scripts
├── docs/       PIWO technical/mod documentation
├── mods/       PIWO-native and PIWO-ported mods
├── scripts/    install/VPS/update/maintenance shell scripts
└── tests/      tests and test fixtures
```

runtime relationship:

```
global/DMprecache.scr //executes our main file by exec
        to
piwo/...
```