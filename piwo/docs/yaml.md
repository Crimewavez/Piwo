# PIWO YAML configuration

Edit `piwo/config/global.yaml` for settings used on every map. To change settings for one map, create `piwo/config/maps/<mapname>.yaml` (for example, `piwo/config/maps/dm/mohdm1.yaml`). Include only the settings you want to override. Settings in a map file replace the whole global list.

```yaml
mods:
  test_mod:
    enabled: true
    message: "Hello from PIWO"

configs:
  weekend:
    days:
      - saturday
      - sunday
```

Use **two spaces** per indentation level, never tabs. Keys can contain letters, numbers, `_`, and `-`. Values can be text, numbers, `true`, `false`, or `null`. Quote text containing `: ` or text that looks like a number. Comments start with `#` at the beginning of a line or after whitespace.

PIWO supports only this simple YAML format: nested keys and lists of single values. Inline lists (`[a, b]`), inline maps, and multiline values are not supported. If a file has an error, PIWO prints its path, line number, and the problem in the server console.
