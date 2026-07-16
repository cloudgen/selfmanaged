# Reviews index — selfmanaged

**Registry** of review plan artifacts and run reports. Keep rows in sync with disk.  
**Updated:** 2026-07-16 (plan + product re-check)

## Plan artifacts

| Artifact | Path | Role |
|----------|------|------|
| What to review | `what-to-review.md` | Living checklist |
| Test plan | `test-plan.md` | TP-* lock-in |
| Lessons | `lessons.md` | L-* re-check |
| README | `README.md` | Surface rules |

## Reports

| Date | File | Scope | Baseline | Verdict |
|------|------|-------|----------|---------|
| 2026-07-15 | `reports/2026-07-15-selfmanaged-product-review.md` | Full Type 0 + storage emphasis | PASS=93 FAIL=0 | Open findings (storage debt) |
| 2026-07-16 | `reports/2026-07-16-selfmanaged-product-review.md` | Full re-check + plan bootstrap | PASS=93 FAIL=0 | **Revise** — prior opens confirmed |
| 2026-07-16 | `reports/2026-07-16-bootstrap-origin-from-timer.md` | Origin A from timer B report | A prior PASS=93 | **Block** — then fixed same day |
| 2026-07-16 | `reports/2026-07-16-selfmanaged-origin-a-fix.md` | Close all origin-A findings | PASS=102 FAIL=0 | **Pass** |
| 2026-07-16 | `reports/2026-07-16-plan-and-product-review.md` | Plan review + full Type 0 re-check | PASS=102 FAIL=0 | **Pass with nits** |

## Open items summary

| ID | Severity | Status | One-line |
|----|----------|--------|----------|
| SM-PLAN-01 | P3 | open | TP-JSON-RAW-01 suite lock-in still **TODO** |
| SM-DOC-01 | P3 | **closed** (2026-07-16) | AGENTS.md + docs maps list nine REQs incl. storage |
| L-CSUM-01 | partial | vigilance | Suite OK; SECURITY trust wording refreshed with 1.2.0 |

## Notes

- Product class: **bootstrap project** (no domain SSOT).  
- Storage is wired Type 0 scratch isolation — not domain product ops.  
