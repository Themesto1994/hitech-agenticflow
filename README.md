# Agentic Test Pipeline — Hi Tech

> One loop, from requirement to proof — powered by TestMu AI kane-cli Assurance.

## The 6-Phase Loop

```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│   Phase 1 ─ CONTEXT    Ingest the PRD                  │
│      │                                                  │
│      ▼                                                  │
│   Phase 2 ─ DESIGN     ACs to tests                    │
│      │                                                  │
│      ▼                                                  │
│   Phase 3 ─ RUN        Author, replay on LambdaTest    │
│      │                                                  │
│      ▼                                                  │
│   Phase 4 ─ COVER      Prove and gate                  │
│      │                                                  │
│      ▼                                                  │
│   Phase 5 ─ EVIDENCE   The proof                       │
│      │                                                  │
│      ▼                                                  │
│   Phase 6 ─ MAINTAIN   Reconcile change ───────────────┘
│
```

| Phase | kane-cli command(s) | What it does |
|---|---|---|
| 1 — Context | `context ingest` → `context extract` → `context review` | Snapshot PRD, extract use-cases, promote to trusted |
| 2 — Design | `design tests` → `context review` | Generate ACs, scenarios, `*_test.md` files |
| 3 — Run | `testmd run` → `testrun run` | Author + replay each test; seal evidence packs |
| 4 — Cover | `cover` | Measure proved vs still-owed requirements |
| 5 — Evidence | `evidence validate` → `evidence merge` | Verify pack integrity, merge into one archive |
| 6 — Maintain | `maintain` | Reconcile suite when requirements change |

---

## Setup

### 1. Add your requirements document

Place your PRD in the repo root:
```
my-requirements.pdf
```
The pipeline auto-detects the first `.pdf` or `.docx` in the repo root. Or pass it explicitly when triggering.

### 2. Add secrets

Go to **Settings → Secrets and variables → Actions** and add:

| Secret | What it is |
|---|---|
| `KANE_USERNAME` | Your kane-cli / TestMu username |
| `KANE_ACCESS_KEY` | Your kane-cli / TestMu access key |
| `LT_USERNAME` | Your LambdaTest username |
| `LT_ACCESS_KEY` | Your LambdaTest access key |

### 3. Run the pipeline

**Actions tab → Agentic Test Pipeline → Run workflow**

Available inputs:

| Input | Description | Default |
|---|---|---|
| `requirements_doc` | Path to PRD (blank = auto-detect) | _(auto)_ |
| `test_language` | `javascript` or `python` | `javascript` |
| `max_tests_to_run` | Cap on tests authored (0 = all) | `0` |
| `start_url` | Default browser start URL | _(blank)_ |
| `kane_project_id` | LambdaTest project ID | _(account default)_ |
| `kane_folder_id` | LambdaTest folder ID | _(account default)_ |

---

## Artifacts produced each run

| Artifact | Contents | Kept |
|---|---|---|
| `context-store` | `.context/` — ingested PRD snapshot | 14 days |
| `designed-tests` | `*_test.md` files with AC traceability | 14 days |
| `run-outputs` | Evidence packs + testrun NDJSON + Playwright code | 14 days |
| `coverage-report` | `kane-cli cover` output | 14 days |
| `evidence-merged` | Single consolidated `.evidence` archive | **30 days** |

### Viewing the evidence pack locally
```bash
npm install -g @testmuai/kane-cli@latest
kane-cli evidence serve <downloaded>.evidence
```

---

## Required secrets
```
KANE_USERNAME
KANE_ACCESS_KEY
LT_USERNAME
LT_ACCESS_KEY
```
