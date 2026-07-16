# Test plan — selfmanaged

Maps **baseline coverage** and **finding lock-in (TP-*)** to `tests/`.  
**Suite entry:** `./tests/run.sh`  
**Last update:** 2026-07-16 (plan + product re-check)

Status: **have** = automated today · **TODO** = needed · **n/a** = not applicable / product choice

---

## Baseline coverage (Type 0)

| Area | Coverage | Evidence |
|------|----------|----------|
| Syntax | have | `sh -n selfmanaged` |
| Companion digest matches ship unit | have | `selfmanaged.sha256` check in suite |
| version / help / about human + JSON | have | `tests/test_cli.sh` |
| help must not list CHECKSUM | have | test_cli |
| about must not include CHECKSUM | have | test_cli |
| about storage fields | **have** | effective_storage / storage_dir |
| Storage isolation / dir exists | **have** | test_cli after SM-STOR wire |
| Unknown command fail-closed | have | test_cli |
| quiet / env -u HOME | have | test_cli |
| Zero-arg Type O paths | have | test_cli + lifecycle |
| self-uninstall --json without --force | have | confirm_required |
| Install / re-install idempotent | have | test_install_lifecycle |
| version-check / self-update / checksum / downgrade | have | lifecycle |

**Baseline result (2026-07-16 origin fix):** PASS=102 FAIL=0 SKIP=0

---

## Finding-linked TP rows

| TP-ID | Related finding / lesson | Intent | Status | Target / notes |
|-------|--------------------------|--------|--------|----------------|
| TP-STOR-01 | SM-STOR-01, L-STOR-01 | Storage resolver invoked; root exists | **have** | test_cli about + dir exists |
| TP-STOR-02 | SM-STOR-02 | Product law documents storage | **have** | requirement-shell-cli-storage.md |
| TP-STOR-03 | SM-TEST-01 | Isolation: path under APP_NAME + user | **have** | test_cli isolation |
| TP-HYG-01 | SM-HYG-01 | Companion `*.tmp` not present | **have** | removed; gitignore `*.tmp` |
| TP-ID-01 | SM-ID-01 | `APP_NAME="…"` hard-assign | **have** | static + extractors |
| TP-OUT-01 | SM-OUT-01 | about JSON storage fields | **have** | test_cli |
| TP-CSUM-01 | SM-SEC-01, L-CSUM-01 | help/about never advertise CHECKSUM | **have** | test_cli |
| TP-BOOT-01 | L-BOOT-01 | Always reach app_main under pipe | **have** | Indirect via zero-arg |
| TP-UNIN-01 | L-UNIN-01 | self-uninstall --json no force → confirm_required | **have** | test_cli + lifecycle |
| TP-SETU-01 | L-SETU-01 | env -u HOME still works | **have** | test_cli |
| TP-CITE-TERM-01 | L-CITE-TERM-01 | Bootstrap footer cites requirements | **have** | static fix |
| TP-JSON-RAW-01 | L-JSON-RAW-01, SM-PLAN-01 | `out_json` `@key` raw nested | **TODO** (impl present) | Code has `@*` branch; no suite assertion yet — mark **have** only after test or reclassify n/a |

---

## Rules

1. Closing a **bug** finding updates the matching TP to **have**.  
2. Do not mark TP **have** without a suite assertion (or documented static fix for cite/ID).  
3. Bootstrap project: no domain TP suite required.  
