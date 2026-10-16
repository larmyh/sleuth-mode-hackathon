# Current delivery status

Updated 16 October 2026 (Singapore). Team: Deston, Kym, Larm and YeeWei.
Hackathon day: **17 October 2026**.

## Lanes

| Lane | Owner | Status | Latest PR |
|---|---|---|---|
| S0 Lead / integration | Deston | Not started | — |
| S1 Transaction Analyst | Kym | Not started | — |
| S2 Document Investigator | YeeWei | Not started | — |
| S3 Case data, report and QA | Larm | Not started | — |

## Day plan

| When | Everyone | Deston (S0) | Kym (S1) | YeeWei (S2) | Larm (S3) |
|---|---|---|---|---|---|
| **Tonight (16 Oct)** | Accept invite, clone, finish [DEV_SETUP](DEV_SETUP.md), read the brief and your lane | Merge the setup PR; land the S0 skeleton with type stubs, fake client and CI (`checks.yml` is in the setup PR description) | Sketch the anomaly checks you'll build | Sketch the search and timeline tools | Write the fictional sample case (`cases/sample/`) and a first `load_case` |
| **Kickoff (first hour)** | Read the real case together; agree what "cracked" means | Turn the briefing into the Lead Detective's goal | Look at the transaction data shape | Look at the document types | Adapt `load_case` to the real files; get them into `cases/<real>/` |
| **Build** | Small PRs, pull `main` often | Orchestrator loop; review and merge PRs quickly | Transaction tools + agent | Document tools + agent | Report renderer; QA on each merged PR |
| **Integrate** | Freeze new features | End-to-end run on the real case | Fix what the run exposes | Fix what the run exposes | Run QA_CHECKLIST; record evidence |
| **Polish and demo** | Rehearse | Prompt and effort tuning | Best finding for the demo | Timeline for the demo | Demo script, submission, verify links |

## Progress log

Add one line per merged PR: date/time, PR, lane, what changed.

- _Nothing merged yet._
