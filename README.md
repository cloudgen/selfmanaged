# selfmanaged - Shell script bootstrap for self Installation & Maintenance

![Version](https://img.shields.io/badge/Version-1.0.0-blue?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)
[![CIAO](https://img.shields.io/badge/Philosophy-CIAO%20(Caution%20%E2%80%A2%20Intentional%20%E2%80%A2%20Anti--fragile%20%E2%80%A2%20Over--engineered)-purple.svg)](https://github.com/cloudgen/ciao)
[![Stars](https://img.shields.io/github/stars/cloudgen/selfmanaged?style=flat-square)](https://github.com/cloudgen/selfmanaged)

POSIX `/bin/sh` **Type 0** CLI for **self-installation and self-maintenance**: install, version-check, self-update, self-uninstall, and about/diagnostics. Ship unit is the single-file script `./selfmanaged` (CIAO / CIAO-Lite defensive design).

Runtime version SSOT: `VERSION="1.0.0"` in `./selfmanaged`. Install channel SSOT: `SCRIPT_URL` composed from `REPO_USER` / `REPO_NAME` / `APP_NAME` (default `https://raw.githubusercontent.com/cloudgen/selfmanaged/main/selfmanaged`).

## Features

- Single-file script for direct execution and online install (`curl | sh` / `wget`)
- User vs global install paths (`~/.local/bin` / `/usr/local/bin`)
- **Type O empty argv = install-ensure** (not help): not installed → install (TTY confirm when interactive; automatic under pipe / quiet / json); already installed (local or global) → success no-op without `--force`
- Centralized output (`out_*`) with `--quiet`, `--json`, `--debug`
- Self-update / version-check against `SCRIPT_URL`
- **Automatic checksum (SHA-256):** default install/self-update fetches `${SCRIPT_URL}.sha256` itself (no env pin); human mode is designed to show companion **link**, expected **value**, and **result**; mismatch aborts; missing sidecar warns and continues
- **Optional strict pin:** `CHECKSUM` env for out-of-band / CI freeze only (secondary—not required for normal install)

## Quick Installation

### Online (recommended)

Copy-paste (channel URL is Config default in `./selfmanaged`):

**Per-user (non-root):**

```sh
curl -fsSL https://raw.githubusercontent.com/cloudgen/selfmanaged/main/selfmanaged | sh
```

**System-wide (root / elevated):**

```sh
sudo curl -fsSL https://raw.githubusercontent.com/cloudgen/selfmanaged/main/selfmanaged | sudo sh
```

Then verify:

```sh
selfmanaged about
```

### Integrity (automatic checksum)

**Primary path:** the program downloads the companion digest **itself**. You do **not** set `CHECKSUM` for normal online install or self-update. Product law: live requirement `requirement-shell-automatic-checksum` (transparency: companion **link**, expected **value**, verification **result**).

Online install / self-update does **not** only trust the download blindly. Behavior is implemented in `./selfmanaged`:

| Mode | When | Algorithm | What happens |
|------|------|-----------|--------------|
| **Automatic (default)** | `CHECKSUM` **unset** (default one-liner) | **SHA-256** via `sha256sum` | After download, fetch companion **`${SCRIPT_URL}.sha256`**. Human mode shows the companion **link**, expected **value**, and **result** (design intent; see requirement). **Match** → install continues. **Mismatch** → install **aborts**. **Sidecar missing** → **warning**, install continues (best-effort). |
| **Strict pin (optional)** | `CHECKSUM` set to an out-of-band hex digest | **SHA-256** | Download must match the pin exactly; **mismatch aborts**. Secondary—CI / freeze installs only. |

Default channel companion path (`${SCRIPT_URL}.sha256`)—fetched automatically:

```text
https://raw.githubusercontent.com/cloudgen/selfmanaged/main/selfmanaged.sha256
```

In this repository the companion file is **`selfmanaged.sha256`** (bare 64-char hex of `./selfmanaged`). Publishers should ship it next to the install script (same directory on the raw channel) so the automatic path can succeed. Same-channel SHA-256 proves **consistency** of the two files on that channel; it is not a substitute for signed releases.

### From a local checkout

```sh
chmod +x ./selfmanaged
./selfmanaged install
selfmanaged about
```

- Non-root install → typically `~/.local/bin/selfmanaged`
- Root install → typically `/usr/local/bin/selfmanaged`
- Already installed (empty argv or `install`) → success / no-op unless `--force` (reinstall is deliberate; not required for a second one-liner)

### Prerequisites

- POSIX-compatible `sh`, standard core utilities
- `curl` or `wget` for network install/update
- `sha256sum` for integrity checks (required when digests are verified)

## Usage

```sh
selfmanaged                # empty argv: Type O install-ensure (install or already-installed)
selfmanaged help
selfmanaged about
selfmanaged version
selfmanaged install        # same ensure semantics as empty argv
selfmanaged version-check
selfmanaged self-update
selfmanaged self-uninstall
```

### Global options

| Flag | Meaning |
|------|---------|
| `--quiet` / `-q` | Suppress non-error human chatter (errors and warnings still shown) |
| `--json` | Machine-readable JSON (forces quiet human output) |
| `--debug` | Extra diagnostics on stderr when supported |
| `--force` | Force reinstall / skip uninstall confirm / allow downgrade where implemented |

### Environment

| Variable | Purpose |
|----------|---------|
| `REPO_USER` | GitHub owner (default `cloudgen`); used to compose default `SCRIPT_URL` |
| `REPO_NAME` | GitHub repo name (default `selfmanaged`); used to compose default `SCRIPT_URL` |
| `SCRIPT_URL` | Install-script URL (default `https://raw.githubusercontent.com/${REPO_USER}/${REPO_NAME}/main/${APP_NAME}`; override for a full custom channel) |
| `APP_NAME` | Override app name (default `selfmanaged`; also the raw path segment in the default channel URL) |

`CHECKSUM` is an optional **install-path runtime** pin for CI/freeze (not shown in `help` / `about`). Empty default uses automatic `${SCRIPT_URL}.sha256`. See Advanced example below if you need an out-of-band pin.

## Examples

Show diagnostics (works before or after install):

```sh
./selfmanaged about
```

Quiet install from a local checkout:

```sh
./selfmanaged install --quiet
```

JSON version for automation:

```sh
selfmanaged version --json
```

JSON / non-interactive uninstall (must pass `--force`; confirm is never auto-yes):

```sh
selfmanaged self-uninstall --json --force
```

Optional **out-of-band** strict pin (Advanced / CI freeze). Use a digest you already trust from release notes or a locked CI file—not “curl the same origin right now” (that is no stronger than automatic mode):

```sh
# Replace with a pinned hex from your trusted source (not live same-origin fetch as "higher security")
export CHECKSUM='replace-with-known-good-sha256-hex'
curl -fsSL https://raw.githubusercontent.com/cloudgen/selfmanaged/main/selfmanaged | sh
```

Regenerate the companion digest after every script change (publisher hygiene for automatic mode):

```sh
sha256sum ./selfmanaged | cut -d' ' -f1 > selfmanaged.sha256
```

Release trees should include:

```text
selfmanaged           # installable script
selfmanaged.sha256    # bare SHA-256 hex of that file (companion digest)
```

## Platform Compatibility

| Platform | Status |
|----------|--------|
| Linux (POSIX `/bin/sh`) | Supported primary target |
| macOS (POSIX `sh`, Homebrew-friendly paths) | Best-effort; standard user/global bin paths |
| Alpine / minimal containers | Designed for limited toolsets (`curl`/`wget`, `sha256sum`) |
| Windows (native) | Not targeted; use WSL or a POSIX environment |

## Related Projects

| Project | Relationship |
|---------|----------------|
| [cloudgen/ciao](https://github.com/cloudgen/ciao) | CIAO defensive programming principles |
| [cloudgen/ciao-lite](https://github.com/cloudgen/ciao-lite) | Agent-facing CIAO-Lite contract |

## Contributing

- Keep changes **surgical**; do not rewrite the whole script for small fixes.
- Respect **CIAO Protection Zones** and intentional defensive checks — do not “simplify” them away.
- After editing `./selfmanaged`, regenerate `selfmanaged.sha256` (see Examples).
- Align user-facing docs with Config SSOTs (`VERSION`, `SCRIPT_URL`, checksum behavior).
- Product rules live under `docs/requirements/` when present; do not invent requirement paths.
- Run the CI suite before opening a PR: `./tests/run.sh` (details in [`tests/README.md`](./tests/README.md)). GitHub Actions runs the same entrypoint on push/PR.

## License

MIT License — see [`LICENSE.md`](./LICENSE.md).

Security reporting: see [`SECURITY.md`](./SECURITY.md). Maintainer contact email is the **author-email** on the Copyright line in `LICENSE.md` (not a second SSOT).

## Last Update

2026-07-14 — Product **1.0.0** SSOT aligned; Type O empty argv = install-ensure (not help when already installed); integrity docs lead with automatic `${SCRIPT_URL}.sha256`; M1+ quality fixes (`app_version`, `USER_BIN` PATH, curl|wget version fetch, portable SHA-256, JSON escape, help `REPO_*`).
