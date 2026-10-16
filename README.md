# Sleuth Mode Hackathon 🕵️

**Crack a fraud case by building your own AI agents.**

A Lead Detective agent hands a fraud case to specialist agents — a Transaction
Analyst and a Document Investigator — and writes a case report that says who did
it, how, how much, and when, citing the evidence for every claim.

## Start here

| Doc | What it's for |
|---|---|
| [Project brief](docs/PROJECT_BRIEF.md) | What we're building, rules, architecture |
| [Ownership](docs/OWNERSHIP.md) | Who owns which files, shared interfaces, PR rules |
| [Dev setup](docs/DEV_SETUP.md) | Install, run, checks |
| [Status](docs/STATUS.md) | Day plan and progress |
| [QA checklist](docs/QA_CHECKLIST.md) | How we know it works |
| [Submission](docs/SUBMISSION.md) | Final links and checklist |
| [AGENTS.md](AGENTS.md) | Rules for AI coding assistants working in this repo |

## Team

| Lane | Name | GitHub | Working on |
|---|---|---|---|
| S0 | Deston (lead) | [@Chi944](https://github.com/Chi944) | Core, Lead Detective, integration; reviews and merges all PRs |
| S1 | Kym | [@kloo007](https://github.com/kloo007) | Transaction Analyst agent |
| S2 | YeeWei | [@yeeweiii](https://github.com/yeeweiii) | Document Investigator agent |
| S3 | Larm | [@larmyh](https://github.com/larmyh) | Case data, report, QA, submission |

## Quick start

```bash
git clone https://github.com/larmyh/sleuth-mode-hackathon.git
cd sleuth-mode-hackathon
```

Then follow [DEV_SETUP](docs/DEV_SETUP.md).

**API keys:** copy `.env.example` to `.env` and add your own key. Never commit
`.env` — this repo is public.

## How we work

1. Pull `main`, then branch: `feat/s1-anomaly-tools`, `fix/…`, `test/…`, `docs/…`
2. Stay inside your lane's files ([Ownership](docs/OWNERSHIP.md)).
3. Open a PR titled with your lane (`S1: …`) and fill in the template.
4. **Deston reviews and merges.** Nobody pushes directly to `main`.
