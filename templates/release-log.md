# Release log template

Keep one table per app, in that app's repo. Add a row for **every upload**, so the next release knows what to compare against, especially CloudKit schema changes.

| Build | Date | Commit | Schema deployed | Notes |
| --- | --- | --- | --- | --- |
| `1.0.0 (1)` | YYYY-MM-DD | `abc1234` | None / list of new models and fields | TestFlight only / App Store submission / released |

Check what changed in the models since the last shipped build:

```bash
git diff <last-shipped-commit> HEAD -- path/to/Models.swift
```
