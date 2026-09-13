# PIWO YAML subset

`piwo/core/yaml.scr` parses PIWO configuration inside OpenMoHAA. It is **not**
a general YAML 1.2 parser. Unsupported syntax is an error, so a setting is not
silently interpreted differently from the administrator's intent.

Supported syntax:

- LF or CRLF line endings, at most 32,768 bytes. UTF-8 values are expected;
  the parser does not validate their encoding.
- Nested mappings, using exactly two spaces per level (maximum eight levels).
- Keys made of ASCII letters, digits, `_`, and `-`.
- Scalar lists (`- item`), replacing the entire inherited list on override.
- Strings (plain, single quoted, or double quoted), decimal integers and
  floats, `true`, `false`, `null`, and `~`.
- Blank lines and `#` comments. A `#` inside quotes or inside a plain word
  remains part of the value.

A mapping colon must be followed by a space or the end of the line. Quote a
plain string containing colon-space. Double-quoted strings recognize `\\`,
`\"`, `\n`, and `\t`; single-quoted strings double an apostrophe (`''`).

Quote values such as times, IP addresses, and strings starting with a digit.
Flow collections (`[a, b]`, `{a: b}`), anchors, tags, multiline scalars,
mapping entries inside lists, and tabs are not supported.

The public script labels are `parse_file`, `parse_text`, and `merge`. Labels
beginning with `_` are internal helpers. The parser returns a document with
`ok`, `error`, `line`, `paths`, `types`, and `values`. Paths are flattened:
`mods.freezetag.freeze_time` names the setting
from the README example. `parse_file` reads through OpenMoHAA's virtual
filesystem. `merge global per_map` applies the per-map document over the
global one, recursively for mappings and atomically for lists. A missing key
inherits its global value; explicit `null` replaces a scalar value. Changing
a mapping or list into another type is an error. The caller must check `ok`
before using the document. Mod-specific type/range validation is a separate
layer; the test module checks its own settings.

## Runtime loading

`global/DMprecache.scr` executes `piwo/main.scr` during map startup. The entry
point reads the required `piwo/config/global.yaml`, then looks for an optional
map override at `piwo/config/maps/<mapname>.yaml`. OpenMoHAA's `mapname` can
include a directory: `dm/mohdm1` uses
`piwo/config/maps/dm/mohdm1.yaml`. Missing map files are ignored; malformed
files stop mod startup and print an error to the server console. Settings are
read again on the next map load.

The first registered module is `piwo/mods/test_mod.scr`. Its configuration is:

```yaml
mods:
  test_mod:
    enabled: true
    message: "Hello from PIWO"
```

When enabled, it prints `message` to the server console and sets the
`piwo_test_mod_message` cvar to the same value. The cvar is cleared on each
map load before applying the new configuration, including when the module is
disabled. `main.scr` dispatches this module explicitly; it does not discover
or load arbitrary mods from the directory.
