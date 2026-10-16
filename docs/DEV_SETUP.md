# Sleuth Mode development setup

## Requirements

- Python **3.11+**
- Git, and access to this repository (accept the invite first)
- An Anthropic API key (or the hackathon's provided key) — keep it in `.env` only

## Install and run

```bash
git clone https://github.com/larmyh/sleuth-mode-hackathon.git
cd sleuth-mode-hackathon
python -m venv .venv
```

Activate the virtual environment:

- Windows (PowerShell): `.venv\Scripts\Activate.ps1`
- macOS / Linux: `source .venv/bin/activate`

```bash
pip install -e ".[dev]"
cp .env.example .env        # Windows: copy .env.example .env
# then put your key in .env
python -m sleuth investigate cases/sample
```

`pyproject.toml` and the `sleuth` package arrive with Deston's S0 skeleton PR.
Until it merges, only the docs exist.

## Checks

The same commands run in CI (`.github/workflows/checks.yml`, added by Deston in
S0). If CI and this file disagree, this file is wrong — fix it rather than
weakening CI.

```bash
ruff check .
pytest -q
```

- Tests run **offline**: use the fictional sample case and a fake Claude client.
  CI has no API key, so a test that calls the real API will fail there.
- Real end-to-end runs (`python -m sleuth investigate …`) cost API credits. Record
  them in your PR under "Checks actually run", with the case name and outcome.

## Troubleshooting

- `ModuleNotFoundError: sleuth` → the venv isn't active, or you skipped
  `pip install -e ".[dev]"`.
- `AuthenticationError` → `.env` is missing or the key is wrong. Never paste the key
  into chat, issues or PRs.
