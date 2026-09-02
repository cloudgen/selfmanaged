# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/),
and this project adheres to [Semantic Versioning](https://semver.org/).

## [1.2.3] - 2026-09-02

### Fixed

- **SM-BUG-01:** `inst_maybe_install` under quiet/JSON now calls `inst_perform_install` and returns its status (no fake success skip). Prompt helpers consume process `TTY`.

### Changed

- Product version SSOT bumped to **`1.2.3`** (ship unit, README badge, SECURITY, companion digest).
- Every registered requirement now has a **§1.1 Human-facing** block (who / what happens / what you type).
- First-install helper law: under quiet/JSON, `inst_maybe_install` **must place** the program (same as empty-argv Case A).

### Added

- Review report `reviews/reports/2026-09-02-bug-inst-maybe-install-quiet-json-skip.md`; lesson `L-INST-MAYBE-01`; test-plan row `TP-INST-MAYBE-01` / **TP-LC-10**.
- `.gitignore` entries for harness transfer safety backups (`.h1-backup-*` / `.h2-backup-*` / `.harness-*-bak-*`).

## [1.2.2] - 2026-08-11

### Added

- **Specializee contract** (bootstrap A → specialized B) in product law:
  - Empty argv stays Type O install-ensure; domain setup uses explicit verbs (`requirement-shell-cli-zero-arguments` v1.2.0).
  - Channel / identity / `out_*` / root host-mutation / help order / REQ retarget hygiene (`requirement-shell-cli-interface` v1.1.0).
  - Domain prefix + temporary output-shim note (`requirement-shell-modular-function-design`); `@key` nested JSON specializee note (`requirement-shell-output-requirements`).
- **Ship-unit injection anchors** in `./selfmanaged`: `DOMAIN_HELP_ROWS`, `DOMAIN_ABOUT_FIELDS`, `DOMAIN_DISPATCH_FLAGS`, `DOMAIN_DISPATCH_COMMANDS`, `DOMAIN_DISPATCH_ROUTES`.
- **CI test isolation:** `ci_isolated_env` exports isolated `GLOBAL_BIN` so host `/usr/local/bin/selfmanaged` cannot shadow install lifecycle tests (port from gitlab-nginx specialize lesson).
- Living **revision plan:** `reviews/revision-plan.md` (items 1–3 closed in 1.2.2; residual backlog).

### Changed

- Product version SSOT bumped to **`1.2.2`** (ship unit, README badge, SECURITY, companion digest).
- Requirements Implementation Notes Version SSOT aligned to **1.2.2** (`requirement-class-software-dev`, `requirement-shell-self-management`); registry header date refreshed.
- Reviews residual: report baseline `PASS=102`; `L-REQ-CIAO-URL-01` / SM-REV-05 lesson recorded.

## [1.2.1] - 2026-07-19

### Changed

- Product version SSOT bumped to **`1.2.1`**:
  - Runtime: `VERSION="1.2.1"` in `./selfmanaged`.
  - Docs: README Version badge + runtime SSOT prose + Last Update; [`SECURITY.md`](./SECURITY.md) supported versions (`1.2.1` current).
  - Requirements: class law `requirement-class-software-dev.md` registered; shell REQs CIAO v2.10.2 principle renumber; DoD on storage + automatic-checksum; registry inventory **1 class + 9 shell**.
- Companion digest **`selfmanaged.sha256`** regenerated (bare 64-char hex of `./selfmanaged`).

### Added

- Software-development **class requirement** (`requirement-class-software-dev.md`) + registry Area `class`.
- Product review report `reviews/reports/2026-07-19-selfmanaged-product-review.md` (baseline PASS=102).

### Fixed

- Requirements hygiene from review: class gate, CIAO principle numbering, definition-of-done gaps, git-identity / SSH profile pre-git reporting (harness).

## [1.2.0] - 2026-07-16

### Changed

- Product version SSOT bumped to **`1.2.0`**:
  - Runtime: `VERSION="1.2.0"` in `./selfmanaged` (and matching defaults in `app_about` / `app_version`).
  - Docs: README Version badge + runtime SSOT prose + Features / Environment / Examples for storage + Last Update; [`SECURITY.md`](./SECURITY.md) supported versions (`1.2.0` current) and isolation/trust notes; [`AGENTS.md`](./AGENTS.md) + `docs/README.md` nine-REQ inventory; [`tests/README.md`](./tests/README.md) about storage coverage.
  - Requirements Implementation Notes: CLI interface + self-management document live product version `1.2.0`.
- Companion digest **`selfmanaged.sha256`** regenerated (bare 64-char hex of `./selfmanaged`).

### Added

- **CLI storage resolve** as product law and ship-unit wire:
  - `requirement-shell-cli-storage.md` (Active) + registry row (nine shell REQs total).
  - `util_resolve_storage` creates chosen tier root fail-closed; `app_main` exports `EFFECTIVE_STORAGE_DIR` + `TMPDIR`; `about` human/JSON expose `effective_storage` / `storage_dir`.
  - Tests: about storage fields, isolation under app name + user, directory exists after resolve.
- Origin-A lock-in from reviews (APP_NAME hard-assign, footer cites live REQs only, `out_json` `@key` raw nested support).

### Fixed

- Storage resolver previously dead / unused from main (SM-STOR-01 class) — wired and covered by suite.

## [1.1.0] - 2026-07-14

### Changed

- Product version SSOT bumped to **`1.1.0`**:
  - Runtime: `VERSION="1.1.0"` in `./selfmanaged` (and matching defaults in `app_about` / `app_version`).
  - Docs: README Version badge + runtime SSOT prose + Last Update; [`SECURITY.md`](./SECURITY.md) supported versions (`1.1.0` current).
  - Requirements Implementation Notes: CLI interface + self-management document live product version `1.1.0`.
- Philosophy alignment upgraded to **[CIAO](https://github.com/cloudgen/ciao) v2.10.*** (aligned on **v2.10.2**; previously documented on the 2.9.x line) — README badge, Related Projects, and Contributing call out the 2.10.* target with CIAO-Lite.
- CI tests read product version from the ship unit (`PRODUCT_VERSION` in `tests/helpers.sh`) instead of hardcoding `1.0.0`, so version bumps no longer break CLI / lifecycle assertions or the downgrade-sed path.
- Companion digest **`selfmanaged.sha256`** kept as **bare 64-char hex** of `./selfmanaged` (publisher format; install still first-field-parses `hash  file` lines if present).
- Product ship-unit header/footer: Type 0 bootstrap wording only (foreign product / reverse-lineage claims removed).

### Fixed

- Incomplete version-identity package after the 1.1.0 runtime bump (docs, SECURITY, REQ notes, and tests aligned together).
- Downgrade lifecycle tests failed when `VERSION` was no longer `1.0.0` because channel aging used a frozen sed pattern; tests now rewrite the live `PRODUCT_VERSION`.

## [1.0.0] - 2026-07-13

### Added

- CI test suite under `tests/` (`./tests/run.sh`) and GitHub Actions workflow (`.github/workflows/ci.yml`): CLI surface, companion digest, isolated install lifecycle against a local HTTP channel, uninstall fail-closed, optional `CHECKSUM` pin match/mismatch.
- Initial public baseline of the `selfmanaged` POSIX `/bin/sh` CLI (Type 0 self-management surface).
- Commands: install, version-check, self-update, self-uninstall, about, help, version.
- Centralized `out_*` output SSOT with quiet / JSON / debug modes.
- Online install integrity via **automatic** companion `selfmanaged.sha256` (primary) and optional secondary `CHECKSUM` pin.
- Project requirements under `docs/requirements/` for automatic-checksum (transparent link/value/result), CLI interface, **CLI zero-arguments (Type O)**, output, self-management, modular design, idempotency, and interactive vs non-interactive behavior.
- Portable template `template-automatic-checksum.md` for automatic companion-digest + transparency pattern.
- Root `.gitignore` (docs requirements tracked; agent harness docs and build/temp artifacts ignored).
- Product root [`LICENSE.md`](./LICENSE.md) (MIT) with author-email SSOT on the Copyright line.
- Product root [`SECURITY.md`](./SECURITY.md): vulnerability reporting contact (from LICENSE), supported versions, and Security Design Principles (CIAO).

### Changed

- Product version SSOT set to `1.0.0` for first-commit baseline (`VERSION="1.0.0"`).
- Product [`README.md`](./README.md) rewritten to the product header kit and mandatory section order (Features → Quick Installation → Usage → Examples → Platform Compatibility → Related Projects → Contributing → License → Last Update).
- README identity triad: **selfmanaged** / Shell script bootstrap for self Installation & Maintenance / **1.0.0**; Stars banner for `cloudgen/selfmanaged`.

### Fixed

- Empty argv (**Type O** install-ensure): when already installed (local or global), one-liner / zero-arg reports **already installed** success instead of dumping **help**; `--force` only for deliberate reinstall. Product law: `requirement-shell-cli-zero-arguments`. Tests cover Case A failure, Case B local, and Case C global empty-argv paths.
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
