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
| CLI surface | `test_cli.sh` | `sh -n`, companion digest (bare hex), `version` / `help` / `about` (human + JSON; version via live `PRODUCT_VERSION`; about `effective_storage` / `storage_dir` + isolation), unknown command, quiet, `CHECKSUM` not on help/about, `env -u HOME`, zero-arg install failure exit, uninstall fail-closed JSON |
| Install lifecycle | `test_install_lifecycle.sh` | Isolated `HOME` / `USER_BIN` / **`GLOBAL_BIN`**, **TP-LC-10** `inst_maybe_install` under JSON/QUIET (place or fail closed), local channel install, idempotent re-install, **Type O** zero-arg already-installed (local Case B + global Case C, not help), strict `version-check` JSON keys, self-update already-latest, human integrity transparency, uninstall refuse / `--force`, `CHECKSUM` pin match/mismatch, downgrade refuse / `--force` (older channel derived from live `PRODUCT_VERSION`) |

**Version note:** suites source `PRODUCT_VERSION` from `grep '^VERSION="' ./selfmanaged` (via `helpers.sh`). After a product version bump, regenerate `selfmanaged.sha256` and re-run `./tests/run.sh` — do not hardcode the semver in new tests.

**Isolation note (1.2.2+):** `ci_isolated_env` always creates a private `GLOBAL_BIN` under the temp home. Without that, a real host install at `/usr/local/bin/${APP_NAME}` makes `inst_is_installed` true and lifecycle tests false-pass. Specializee suites **must** keep this pattern.

## Specializee porting checklist (A → B)

When specializing a product from this bootstrap, port tests as follows:

1. Copy `tests/` and retarget `SCRIPT` / `APP_NAME` / channel basenames only (not CIAO org URLs in requirements).  
2. Keep **`GLOBAL_BIN=${CI_GLOBAL_BIN}`** on every isolated install/update/uninstall env block.  
3. Keep Type 0 suites; add a domain suite for B’s verbs (help rows, empty argv ≠ domain, root fail-closed for host ops).  
4. Map domain TP rows in B’s `reviews/test-plan.md`.  
5. Re-baseline PASS count after green run.

Product law: `requirement-shell-cli-zero-arguments` §2.2.1 · `requirement-shell-cli-interface` §2.5.1 · `reviews/revision-plan.md`.

## CI

GitHub Actions: [`.github/workflows/ci.yml`](../.github/workflows/ci.yml) runs `./tests/run.sh` on push/PR to `main`/`master`.

No secrets and no root. Install tests serve the checkout over `127.0.0.1` so they do not depend on the public raw GitHub channel being published.
