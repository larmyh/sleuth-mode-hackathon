# Sleuth Mode product scope

**Hackathon:** Sleuth Mode — crack a fraud case by building your own AI agents.
**Date:** 17 October 2026. **Team:** Deston, Kym, Larm and YeeWei.

## Product

A Python command-line investigator. One command loads the case files, a
**Lead Detective** agent hands work to specialist agents, and the run writes a
case report that answers:

1. **Who** committed the fraud (and who helped or knew)?
2. **How** was it done?
3. **How much** money moved, and where did it go?
4. **When** did it happen (timeline)?
5. **What evidence** proves each of the above?

```bash
python -m sleuth investigate cases/<case-name>
# -> reports/<case-name>.md
```

## Rules

- **Evidence first.** Every claim in the report cites evidence IDs that exist in
  the loaded case. "Insufficient evidence" is a valid answer; a guess is not.
- **The real case format is unknown until kickoff.** The data layer must adapt
  quickly; everything else works against the shared `Case` type, not raw files.
- **Claude API** through the official `anthropic` Python SDK. Default model
  `claude-opus-5-5`. The lead owns model and effort settings.
- **No hardcoded answers.** Agents must reach conclusions from the case files.
- **No web UI** unless the core flow is finished (see stretch scope).

## Architecture

```
cases/<case>/ ──load_case()──► Case ──► Lead Detective (orchestrator, S0)
                                          ├─► Transaction Analyst   (S1)
                                          │     tools: query, anomalies, money flow
                                          ├─► Document Investigator (S2)
                                          │     tools: search, timeline, entities
                                          ▼
                                    list[Finding] ──► report.py (S3) ──► reports/<case>.md
```

| Path | Purpose |
|---|---|
| `sleuth/core/` | Shared types, Claude client, agent base, case context (lead) |
| `sleuth/agents/` | One file per agent |
| `sleuth/tools/` | Tool functions the agents call, one file per lane |
| `sleuth/data/` | Case loaders (CSV, JSON, text, email, PDF) |
| `sleuth/report.py` | Findings → Markdown case report |
| `cases/sample/` | **Fictional** practice case for building and tests |
| `cases/<real>/` | The real case, added at kickoff |
| `tests/` | Offline tests — never call the real API |

## Stretch scope

Only after the completion criteria below pass:

- **Devil's Advocate agent** that challenges each finding before the report.
- **Money-flow graph** image in the report.
- **Small web UI** (e.g. Streamlit) to show the case and the evidence trail live.

## Completion

- Runs end-to-end on the real case from a clean clone with one command.
- Report answers who / how / how much / when.
- Every claim cites real evidence IDs (QA_CHECKLIST A1).
- Demo rehearsed; [SUBMISSION](SUBMISSION.md) links verified.
