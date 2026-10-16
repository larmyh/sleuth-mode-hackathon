# File ownership and integration contract

**Deston (@Chi944) is the lead.** Deston builds the shared core, reviews every PR
and is the only person who merges into `main`. Everyone else works on their own
branch and opens a PR. Ownership is a coordination agreement so four people can
build at once without merge conflicts — everyone reviews their own diff, and the
lead reviews every merge.

## Lanes

| Lane | Owner | Delivers | Editable paths |
|---|---|---|---|
| **S0** Lead / integration | Deston (@Chi944) | Package skeleton, shared types, Claude client + agent base, case context, Lead Detective orchestrator, CLI, CI, dependencies; reviews and merges | `sleuth/core/**`, `sleuth/agents/lead_detective.py`, `sleuth/__main__.py`, `pyproject.toml`, `.github/**`, `AGENTS.md`, `CLAUDE.md`, `docs/PROJECT_BRIEF.md`, `docs/OWNERSHIP.md` |
| **S1** Transaction Analyst | Kym (@kloo007) | Agent that finds suspicious money movement: anomalies (round amounts, just-under-threshold, odd hours, duplicates, velocity), money-flow tracing, circular transfers, shell accounts | `sleuth/agents/transactions.py`, `sleuth/tools/transactions.py`, `tests/test_transactions*.py` |
| **S2** Document Investigator | YeeWei (@yeeweiii) | Agent that reads emails, chats, memos and invoices: keyword/semantic search, timeline builder, people/company extraction, contradictions between what people said and what the money did | `sleuth/agents/documents.py`, `sleuth/tools/documents.py`, `tests/test_documents*.py` |
| **S3** Case data, report and QA | Larm (@larmyh) | Loaders for whatever format the real case uses, the fictional sample case, the Markdown case report, QA checklist runs, demo script and submission | `sleuth/data/**`, `sleuth/report.py`, `cases/**`, `tests/test_data*.py`, `tests/test_report*.py`, `docs/QA_CHECKLIST.md`, `docs/SUBMISSION.md`, `docs/qa/**` |

Shared by everyone (small, append-only edits; mention them in your PR):
`README.md`, `docs/STATUS.md`, `docs/DEV_SETUP.md`, `.env.example`.

Anything not listed belongs to the lead. A change you need outside your lane is a
blocker to raise with Deston, not permission to edit it.

## Shared interfaces

The lead lands these as stubs in S0 so the other lanes can build against them
straight away. Lanes must not change their shape without the lead.

```python
# sleuth/core/types.py  (S0, lead-owned)
@dataclass
class Document:
    id: str                 # evidence ID, e.g. "DOC-007"
    kind: str               # "email" | "chat" | "memo" | "invoice" | "statement" | ...
    title: str
    date: datetime | None
    author: str | None
    text: str

@dataclass
class Case:
    case_id: str
    title: str
    briefing: str           # the challenge prompt / case description
    transactions: pd.DataFrame   # one row per transaction; column "id" = evidence ID, e.g. "TX-0042"
    documents: list[Document]
    extras: dict[str, Any]  # anything else the real case ships with

@dataclass
class Finding:
    agent: str              # "transactions" | "documents" | "lead"
    claim: str              # one plain-language sentence
    evidence_ids: list[str] # must exist in the Case
    confidence: Literal["low", "medium", "high"]
```

| Contract | Owner | Signature |
|---|---|---|
| Load a case | S3 | `sleuth.data.load_case(path: Path) -> Case` |
| Current case for tools | S0 | `sleuth.core.context.current_case() -> Case` |
| Specialist agent | S1, S2 | `investigate(case: Case, brief: str) -> list[Finding]` in `sleuth/agents/<name>.py` |
| Tools | S1, S2 | Plain functions in `sleuth/tools/<lane>.py`, registered with the SDK tool runner (`@beta_tool`), simple JSON-able args, return a JSON string, read data via `current_case()` |
| Orchestrator | S0 | `sleuth.agents.lead_detective.solve(case: Case) -> CaseReport` |
| Report | S3 | `sleuth.report.render(report: CaseReport) -> str` (Markdown) |

Evidence IDs come from the case files when they have them; otherwise the S3
loader assigns stable ones (`TX-0001`, `DOC-001`, …). Tests use the fictional
sample case and a fake Claude client — no test may call the real API.

## Branches and pull requests

- Branch from current `main`: `feat/<lane>-<thing>`, `fix/…`, `test/…`, `docs/…`
  (e.g. `feat/s1-anomaly-tools`).
- PR title starts with the lane ID: `S1: Add just-under-threshold anomaly tool`.
- Fill in the PR template. Keep PRs small — several small PRs merge faster than
  one big one.
- Deston reviews and merges. GitHub does not let anyone approve their own PR, so
  **Larm approves Deston's own PRs**; Deston still merges them.
- Branches are deleted after merge. Run `git pull origin main` before starting
  each new branch.
