# Sleuth Mode acceptance checklist

Record each run as PASS, FAIL or NOT RUN, with the commit, the case and the
command used. An unrun check is NOT RUN, never PASS.

## Agent and report checks

| ID | Check | Expected |
|---|---|---|
| A1 | Evidence citations | Every claim in the report cites evidence IDs, and every ID exists in the loaded case |
| A2 | No fabrication | Names, amounts and dates in the report match the source files exactly |
| A3 | Insufficient evidence | When the data can't support a claim, the report says so instead of guessing |
| A4 | The five questions | Report answers who, how, how much, when, and lists the evidence |
| A5 | Empty / missing data | A case with no documents (or no transactions) still runs and says what is missing |
| A6 | API failure | A failed or refused API call shows a clear error; no partial report presented as complete |
| A7 | Secrets | No API key in code, logs, reports, screenshots or commits |

## Integrated checks

| ID | Check | Expected |
|---|---|---|
| I1 | Clean clone | DEV_SETUP steps work on a fresh clone |
| I2 | Sample case | `python -m sleuth investigate cases/sample` finds the planted fraud |
| I3 | Real case | End-to-end run on the real case finishes and writes `reports/<case>.md` |
| I4 | Repeat run | A second run reaches the same core conclusion |
| I5 | Offline tests | `ruff check .` and `pytest -q` pass with no API key set |
| I6 | Demo | The demo runs (or a recording plays) start to finish within the time limit |
