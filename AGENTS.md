# Sleuth Mode project instructions

Read `docs/PROJECT_BRIEF.md`, `docs/OWNERSHIP.md`, `docs/DEV_SETUP.md` and your assigned lane before editing. Inspect existing files. Do not invent a repository structure when the real one differs.

## Working rules

- Work on exactly one assigned task and feature branch. State the lane ID (S0–S3) and intended files before editing.
- Stay within your lane's paths in `docs/OWNERSHIP.md`. A dependency outside them is a blocker to report to the lead, not permission to change it.
- Only the lead (Deston) changes shared types and context (`sleuth/core/**`), the orchestrator, dependencies (`pyproject.toml`), CI and repository settings, unless explicitly delegated.
- Do not add packages without the lead's approval.
- Do not read secret files, print environment values, or place API keys in code, logs, reports, screenshots or prompts. Never commit `.env`.
- Every finding an agent reports must cite evidence IDs that exist in the loaded case. Never invent transactions, documents, people, amounts or dates. "Insufficient evidence" is a valid answer.
- Never hardcode the answer to a case. Conclusions must come from the agents reading the case files.
- Fictional practice data lives only in `cases/sample/` and is labelled fictional. Never silently fall back to it when the real case fails to load.
- Tests run offline with the sample case and a fake Claude client. No test may call the real API.
- Run the checks in `docs/DEV_SETUP.md` before opening a PR. Never remove tests or disable lint to manufacture a pass.
- Report exact commands and actual results. An unrun check is "NOT RUN", not "passed".
- After two unsuccessful attempts at the same fix, report a minimal reproduction to the lead and continue other work in your lane.
- **Deston (@Chi944) reviews and merges every PR into `main`.** Teammates and their AI agents may commit and push their own branches and open PRs. They may not merge, push to `main`, force-push or change repository settings.

## Handoff

Return the lane ID, changed files, behavior delivered, actual checks, how to run or view it, known limitations, and any integration needed from the lead. Explain the change in plain language.

## Code review rules

Flag out-of-scope edits, secret exposure, new dependencies, findings without evidence, hardcoded case answers, tests that hit the real API, unhandled API errors and missing empty/error states. These instructions guide behavior; they do not replace access controls or human review.
