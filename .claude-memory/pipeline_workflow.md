# Pipeline Workflow

## 6-Phase Loop (TestMu AI Assurance)

| Phase | Job name in GH Actions | Commands |
|---|---|---|
| 1 — Context | `Phase 1 — Context: Ingest the PRD` | `context ingest` → `context extract` → `context review` |
| 2 — Design | `Phase 2 — Design: ACs to Tests` | `design tests` → `context review` |
| 3 — Run | `Phase 3 — Run: Author, Replay` | `testmd run` → `testrun run` |
| 4 — Cover | `Phase 4 — Cover: Prove and Gate` | `cover` |
| 5 — Evidence | `Phase 5 — Evidence: The Proof` | `evidence validate` → `evidence merge` |
| 6 — Maintain | `Phase 6 — Maintain: Reconcile Change` | `maintain` |

## Key inputs
- `requirements_doc` — path to PRD (auto-detected if blank)
- `start_url` — browser start URL passed to `kane-cli config set-url`
- `test_language` — javascript (default) or python
- `max_tests_to_run` — cap on tests (0 = all)

## Artifacts
- `context-store` — .context/ directory (Phase 1 output)
- `designed-tests` — *_test.md files (Phase 2 output)
- `run-outputs` — evidence packs + testrun NDJSON (Phase 3 output)
- `coverage-report` — cover output text (Phase 4 output)
- `evidence-merged` — single .evidence archive, 30-day retention (Phase 5 output)
