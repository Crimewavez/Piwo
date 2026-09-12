# 🍺 PIWO

**MOHAA server and mod setup without the usual mess.**

PIWO is a server management tool for Medal of Honor: Allied Assault and OpenMoHAA.

It provides a ready-made structure for running a dedicated server, installing supported mods, managing their configuration, and keeping the whole setup in one place.

PIWO does not replace OpenMoHAA's mod or scripting systems. It manages the mess and configuration around them.

## What is PIWO?

Running a modded MOHAA server usually means manually dealing with:

* PK3 files
* server CFGs
* mod-specific CFGs
* scripts
* launch arguments
* file ordering
* Linux permissions
* startup scripts
* systemd services
* logs

PIWO handles the repetitive server-administration side of that.

Supported mods come with a PIWO integration describing which of their existing settings PIWO can configure. You configure the server through PIWO, and PIWO handles the rest.

## Example

Instead of manually maintaining several files you can keep the supported configuration together:

```yaml
mods:
  freezetag:
    enabled: true

  weapon_manager:
    enabled: true
```

Exactly which settings are available depends on the mod being managed. PIWO does not add configuration options that the underlying mod or OpenMoHAA does not support.

## Features

* Central PIWO configuration
* Installation of supported mods
* Enable/disable supported mod packages
* Generation of server and mod CFG files
* Sensible default configurations
* OpenMoHAA dedicated-server setup
* Linux service setup using systemd
* Server start, stop and restart
* Log access
* Configuration validation
* Installation and server health checks
* Simple structure for adding support for additional mods

## Supported Mods

PIWO ships with integrations for commonly used MOHAA mods.

For example:

* FreezeTag
* BaseBuilder
* Weapon Manager
* Realism configurations
* more over time

A PIWO integration contains the files, defaults and configuration information required to install and configure that particular mod.

## Adding Mods

Additional configuration can be exposed when the underlying mod provides settings that PIWO can safely manage. Adding support for a new mod therefore mostly means teaching PIWO how that particular mod is installed and configured. It does not modify the mod itself.

## Server Setup

PIWO can prepare a Linux machine for hosting OpenMoHAA.

The setup process can handle:

* server directories
* dedicated Linux user
* permissions
* OpenMoHAA server binaries
* PIWO files
* systemd service
* server configuration
* installed PIWO mod packages

You still need to provide the required original Medal of Honor: Allied Assault game files. PIWO does not distribute proprietary MOHAA assets.

## Server Management

Typical commands may look like:

```bash
placeholder
```

Configuration management:

```bash
placeholder
```

Mod management:

```bash
placeholder
```

## Diagnostics

```bash
piwo doctor
```

PIWO can check things such as:

```text
[OK] OpenMoHAA server binary found
[OK] MOHAA game files found
[OK] PIWO configuration valid
[OK] server.cfg generated
[OK] FreezeTag files installed
[OK] server user has correct permissions
[OK] UDP port 12203 available
```

This checks the server environment and PIWO-managed files. It is not a replacement for debugging bugs inside individual MOHAA mods.

## Philosophy

PIWO does not try to create a new modding system for MOHAA, it takes the modding system that already exists and makes the administrative side less painful.

```text
             PIWO
               |
     files / cfg / startup
               |
               v
          OpenMoHAA
               |
        MOHAA scripts/mods
```

OpenMoHAA and individual mods remain responsible for gameplay, PIWO is responsible for putting the server together.

## Why PIWO?

Because installing five mods should not mean manually reconstructing somebody's server setup from fifteen-year-old forum posts and twelve different CFG files.

Configure it. Start it. Grab a beer.
