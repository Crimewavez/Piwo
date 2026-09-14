# 🍺 PIWO

**A mod framework and server toolkit for Medal of Honor: Allied Assault and OpenMoHAA.**

PIWO provides a common structure and configuration system for MOHAA server mods, together with tools for quickly deploying and managing an OpenMoHAA server on Linux.

See the [YAML configuration guide](piwo/docs/yaml.md) for the supported config format.

Existing mods are adapted or rewritten for PIWO so they follow the same configuration conventions and are designed to work together instead of behaving as unrelated script packages.

**AI-driven contributions are accepted, but only if it's visible that you have read the output and gave solution a thought**

## What does PIWO provide?

PIWO consists of two main parts:

### Mod framework

Supported mods are maintained as PIWO-compatible versions and configured through one central YAML configuration.

```yaml
mods:
  freezetag:
    enabled: true
    freeze_time: 5

  weapon_manager:
    enabled: true
    sniper: true
    rocket: false
```


### Server toolkit

PIWO also provides scripts for preparing and installing a server on a fresh Linux VPS.

The tooling can handle things such as:

* OpenMoHAA installation
* server directories
* Linux users and permissions
* required dependencies
* systemd service setup
* firewall configuration
* PIWO installation
* bundled PIWO mods
* basic server configuration
* updates and health checks

The goal is to make a fresh VPS usable as a MOHAA server with as little manual Linux configuration as possible.

## Per-map configuration

Every map can have its own YAML file which overrides the global PIWO configuration.

Global configuration:

```yaml
mods:
  freezetag:
    freeze_time: 5

  weapon_manager:
    sniper: true
```

`maps/mp_foy.yaml`:

```yaml
mods:
  weapon_manager:
    sniper: false
```

Only settings that differ from the global configuration need to be specified.

## Conditional CFGs

PIWO can also apply ordinary MOHAA CFG files based on server conditions.

```yaml
configs:
  low_pop:
    file: lowpop.cfg
    players:
      max: 6

  night:
    file: night.cfg
    time:
      from: "22:00"
      to: "06:00"

  weekend:
    file: weekend.cfg
    days:
      - saturday
      - sunday
```

The CFG files can be named however you want. This can be used to change server behaviour based on:

* player count
* time of day
* day of week
* other supported server conditions

## PIWO mods

PIWO ships with maintained versions of commonly used MOHAA mods. Planned examples include:

* FreezeTag
* BaseBuilder
* Weapon Manager
* realism-related modules
* more over time

A PIWO port may modify or restructure the original mod to use PIWO's configuration and integration conventions. Not every internal value becomes configurable. PIWO exposes settings that are useful to server administrators.

## Quick installation

A fresh VPS should require little more than running the PIWO setup script and answering a few questions.

```bash
./install.sh
```

The installer prepares the system, installs PIWO and OpenMoHAA components, configures the service, and creates the initial server setup.

Original Medal of Honor: Allied Assault game files are not distributed by PIWO and must be provided separately.

## Goals

PIWO aims to provide:

* one predictable configuration system for supported mods
* global settings with per-map overrides
* mods designed to work together
* conditional server configurations
* fast deployment on a fresh Linux VPS
* simple server maintenance
* a clear structure for adding new PIWO mods

## Why PIWO?

Because running a modded MOHAA server should not require manually stitching old mods together, and spending an evening configuring a VPS.

Configure it. Run it. Grab a beer. 🍺
