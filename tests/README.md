# Tests (selfmanaged)

POSIX `/bin/sh` CI suite for the Type 0 ship unit `./selfmanaged`.

## Run locally

```sh
./tests/run.sh
```

Requires: `sh`, `curl`, `python3` (local HTTP channel), `sha256sum`, `grep`.

## What is covered

| Suite | File | Focus |
|-------|------|--------|
| CLI surface | `test_cli.sh` | `sh -n`, companion digest, `version` / `help` / `about` (human + JSON), unknown command, quiet, `CHECKSUM` not on help/about, `env -u HOME`, zero-arg install failure exit, uninstall fail-closed JSON |
| Install lifecycle | `test_install_lifecycle.sh` | Isolated `HOME`/`USER_BIN`, local channel install, idempotent re-install, **Type O** zero-arg already-installed (local Case B + global Case C, not help), strict `version-check` JSON keys, self-update already-latest, human integrity transparency, uninstall refuse / `--force`, `CHECKSUM` pin match/mismatch, downgrade refuse / `--force` |

## CI

GitHub Actions: [`.github/workflows/ci.yml`](../.github/workflows/ci.yml) runs `./tests/run.sh` on push/PR to `main`/`master`.

No secrets and no root. Install tests serve the checkout over `127.0.0.1` so they do not depend on the public raw GitHub channel being published.
