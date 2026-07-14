# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/),
and this project adheres to [Semantic Versioning](https://semver.org/).

## [1.0.0] - 2026-07-13

### Added

- CI test suite under `tests/` (`./tests/run.sh`) and GitHub Actions workflow (`.github/workflows/ci.yml`): CLI surface, companion digest, isolated install lifecycle against a local HTTP channel, uninstall fail-closed, optional `CHECKSUM` pin match/mismatch.
- Initial public baseline of the `selfmanaged` POSIX `/bin/sh` CLI (Type 0 self-management surface).
- Commands: install, version-check, self-update, self-uninstall, about, help, version.
- Centralized `out_*` output SSOT with quiet / JSON / debug modes.
- Online install integrity via **automatic** companion `selfmanaged.sha256` (primary) and optional secondary `CHECKSUM` pin.
- Project requirements under `docs/requirements/` for automatic-checksum (transparent link/value/result), CLI, output, self-management, modular design, idempotency, and interactive vs non-interactive behavior.
- Portable template `template-automatic-checksum.md` for automatic companion-digest + transparency pattern.
- Root `.gitignore` (docs requirements tracked; agent harness docs and build/temp artifacts ignored).
- Product root [`LICENSE.md`](./LICENSE.md) (MIT) with author-email SSOT on the Copyright line.
- Product root [`SECURITY.md`](./SECURITY.md): vulnerability reporting contact (from LICENSE), supported versions, and Security Design Principles (CIAO).

### Changed

- Product version SSOT set to `1.0.0` for first-commit baseline (`VERSION="1.0.0"`).
- Product [`README.md`](./README.md) rewritten to the product header kit and mandatory section order (Features → Quick Installation → Usage → Examples → Platform Compatibility → Related Projects → Contributing → License → Last Update).
- README identity triad: **selfmanaged** / Shell script bootstrap for self Installation & Maintenance / **1.0.0**; Stars banner for `cloudgen/selfmanaged`.

### Fixed

- Requirements Implementation Notes aligned to product **VERSION `1.0.0`** (removed stale `1.0.0-dev` SSOT text in CLI interface + self-management REQs).
- `version` command routes through `app_version` (single path; JSON `app` + `version` fields preserved).
- `path_add_*` / uninstall PATH cleanup use **`USER_BIN`** (not hardcoded `~/.local/bin` only).
- `version-check` / `self-update` remote fetch via `util_fetch_remote_version` (**curl or wget**).
- SHA-256 via `util_sha256_file` (**sha256sum → shasum → openssl**) for install integrity on Linux/macOS toolchains.
- `out_json` / `out_json_error` escape all string fields (type, message, keys, values, codes).
- `help` Environment lists **`REPO_USER` / `REPO_NAME` / `SCRIPT_URL`** (still omits `CHECKSUM`).
- `util_resolve_storage` third fallback is set -u safe (XDG cache / per-user isolation); `util_get_install_bin_path` wired into uninstall path selection; stale “git-sync” / “RuoYi” comments cleaned.
- `version-check --json` now emits proper key/value fields (`local_version`, `remote_version`, `is_latest`) instead of mis-ordering `out_json` arguments so keys landed in `message`.
- Under `set -u`, resolve/default `HOME` before `USER_BIN` so `env -u HOME` no longer aborts every command (INC-20260713-001 P0).
- Zero-arg auto-install (`curl | sh` / not-installed empty argv) propagates install failure exit status instead of always `exit 0`.
- Automatic companion checksum path sets verified success (`INST_AUTO_CHECKSUM_OK` → `downloaded_checksum_ok`) and prints companion link, expected/actual SHA-256, and PASS/FAIL result in human mode (requirement-shell-automatic-checksum transparency).
- CI suite expanded: strict `ver_check` JSON keys, `env -u HOME`, zero-arg non-zero exit, self-update already-latest, human integrity transparency, downgrade refuse/`--force`.
- `self-uninstall --json` (and quiet/non-TTY without `--force`) no longer emits fake success JSON `"Uninstall cancelled by user."`; it fail-closes with `out_json_error` / `code=confirm_required` and a clear `--force` requirement (binary left in place). Interactive TTY cancel still says cancelled by user.
- Product `README.md` install docs aligned with Config channel SSOT: simple literal online one-liners (`curl -fsSL https://raw.githubusercontent.com/cloudgen/selfmanaged/main/selfmanaged | sh` and elevated shape); **automatic SHA-256** sidecar verification documented from install code (match/mismatch/missing outcomes); no toy hosts; hollow license stub removed.
- Progressive disclosure for newcomers: primary one-liners first; integrity table visible; optional pin and digest regeneration under Examples (INC-20260712-004 class).
- Integrity docs (README + write-readme skill) lead with automatic companion fetch; ban same-origin `CHECKSUM=$(curl …sha256)` as “highest assurance” (INC-20260713-003 partial remediation).
- `CHECKSUM` treated as install-path runtime pin only: removed from `help` Environment; requirements/templates forbid listing it in `help`/`about`.
- Install channel Config: `REPO_USER` / `REPO_NAME` compose default `SCRIPT_URL` as raw GitHub content URL (`https://raw.githubusercontent.com/${REPO_USER}/${REPO_NAME}/main/${APP_NAME}`); header comment and product docs aligned.
- Agent process docs (`skill-write-readme`, `skill-commit-check`, online-install template/term/checklist, no-hardcode policy) require Config-channel → simple README one-liner and forbid 404 veto on pre-publish projects.
