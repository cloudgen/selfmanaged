# Lessons — selfmanaged

**Prior-report failure modes** to re-check on every product review.  
**Mandatory load** before findings.  
**Last update:** 2026-07-16 (plan + product re-check)

| L-ID | Failure mode | Re-check | Source | Open? |
|------|--------------|----------|--------|-------|
| L-STOR-01 | Storage resolver dead code; tiers 1–2 no mkdir; not called from main/about | Call sites of `util_resolve_storage`; mkdir all tiers; about JSON storage fields | SM-STOR-01 | **Closed** (2026-07-16 wire) |
| L-STOR-02 | No storage product law | `requirement-shell-cli-storage.md` + index row | SM-STOR-02 | **Closed** (2026-07-16) |
| L-BOOT-01 | Basename / `$0` APP_NAME gate blocks `curl\|sh` | End of ship unit always `app_main "$@"` | INC-20260712-001 | **Closed** (re-check still) |
| L-TYPEO-01 | Empty argv dumps help instead of install-ensure | Zero-arg tests | requirement-shell-cli-zero-arguments | **Closed** (suite) |
| L-UNIN-01 | self-uninstall --json without --force fakes success cancel | confirm_required | INC-20260713-002 | **Closed** (suite) |
| L-SETU-01 | `set -u` with bare HOME / privilege defaults | env -u HOME | INC-20260713-001 | **Closed** (suite) |
| L-CSUM-01 | CHECKSUM trust UX / overclaim authenticity | Companion primary; CHECKSUM not in help/about; SECURITY bounds | INC-20260713-003 | **Partial** — suite OK; wording vigilance |
| L-CITE-01 | Product source cites templates/skills as law | ALIGNMENT cites live `requirement-shell-*` only | INC-20260712-002 | **Closed** (process) |
| L-HYG-01 | Companion `*.tmp` left at repo root | No `selfmanaged.sha256.tmp` | SM-HYG-01 | **Closed** (2026-07-16) |
| L-ID-01 | APP_NAME only `:=` without hard-assign | `APP_NAME="selfmanaged"` present | SM-ID-01 | **Closed** (2026-07-16) |
| L-CITE-TERM-01 | Bootstrap footer cites terminologies | Footer cites requirement-shell-cli-* | origin 2026-07-16 | **Closed** (2026-07-16) |
| L-JSON-RAW-01 | `out_json` lacks `@key` raw nested path | `@key` supported in out_json | timer origin map | **Closed** (impl 2026-07-16); TP-JSON-RAW-01 still **TODO** suite lock-in (SM-PLAN-01) |

## How to use

1. For each open L-*, re-verify with evidence in the new report.  
2. When fixed, set Open? to **Closed** and point to TP / commit / date.  
3. Promote new modes from reports into this table (do not rely on chat memory).  
