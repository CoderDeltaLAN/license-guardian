# license-guardian

CLI to enforce **SPDX headers** in source files and ensure a **LICENSE** file exists.
Designed for an **Always Green** workflow and clean OSS repos.

![CI](https://img.shields.io/github/actions/workflow/status/CoderDeltaLAN/license-guardian/ci.yml?label=CI)
![CodeQL](https://img.shields.io/github/actions/workflow/status/CoderDeltaLAN/license-guardian/codeql.yml?label=CodeQL)

---

## Why

Projects break compliance and traceability when files lack an SPDX header or when the repository misses the LICENSE file.  
`license-guardian` keeps both in check from day one, locally and in CI.

## Features

- Validates and inserts `SPDX-License-Identifier: <ID>` at the top of source files.
- Ensures a **LICENSE** file exists (**MIT** template included).
- Idempotent fixes. Running twice does not duplicate headers.
- Clear exit codes for CI gating.
- Fast, zero-config defaults with sensible ignores.
- Current focus: Python files (`.py`). Roadmap may expand to more languages via comment-style detection.

## Installation

### From PyPI (when published)

```bash
pip install license-guardian
```

### From source (local checkout)

```bash
# inside the project root
pip install .
# or using Poetry build artifact
poetry build && pip install dist/*.whl
```

## Quick Start

```bash
# Show help
license-guardian --help

# Check that all .py files under the current repo have an SPDX header
license-guardian --path . --ext .py --mode check

# Insert headers where missing and create LICENSE if absent
license-guardian --path . --ext .py --mode fix
```

Typical directories are ignored automatically: `.git`, `.venv`, `venv`, `env`, `dist`, `build`, `__pycache__`, `.mypy_cache`, `.pytest_cache`.

## CLI Reference

```
license-guardian
  --path PATH              Root directory to scan. Default: "."
  --ext EXT                File extension to validate. Repeat for multiple. Default: ".py"
  --mode {check|fix}       "check" only validates; "fix" inserts headers and may create LICENSE.
  --license-id TEXT        SPDX License Identifier to enforce. Default: "MIT"
  --require-license-file   When true and --mode=check, fail if LICENSE is missing.
  --author TEXT            Author to render in LICENSE when creating it in --mode=fix.
```

**Exit codes**

- `0`: All good.
- `1`: Missing headers and/or required LICENSE not satisfied.

## Examples

**Check only**

```bash
license-guardian --path . --ext .py --mode check
```

**Fix headers and ensure LICENSE**

```bash
license-guardian --path . --ext .py --mode fix --license-id MIT --author "CoderDeltaLAN"
```

**Require LICENSE even in check mode**

```bash
license-guardian --path . --ext .py --mode check --require-license-file
```

**Scan a specific subtree**

```bash
license-guardian --path ./src --ext .py --mode check
```

## CI Usage (GitHub Actions snippet)

```yaml
- run: poetry run license-guardian --path . --ext .py --mode check
```

Combine with required status checks to keep `main` always green.

## Contributing

- Use **Poetry** for local setup.
- Run local gate before any push:

```bash
poetry run ruff check . --fix
poetry run ruff format .
poetry run black .
PYTHONPATH=src poetry run pytest -q
poetry run mypy .
```

- Conventional Commits recommended. Small, atomic PRs. CI must be green.

See `SECURITY.md` for vulnerability reporting.

---

## 🔍 SEO Keywords

AI code analyzer, Python linter, bug detection CLI, refactor AI code, Python static analysis, clean code automation, catch bugs early, developer productivity tools, SPDX headers, license compliance, open source tooling, CI gating.

---

## 💖 Donations & Sponsorship

Support open‑source: your donations keep projects clean, secure, and continuously evolving for the global community.

[![Donate](https://img.shields.io/badge/Donate-PayPal-0070ba.svg?logo=paypal&logoColor=white)](https://www.paypal.com/donate/?hosted_button_id=YVENCBNCZWVPW)

---

## 👤 Author

**CoderDeltaLAN (Yosvel)**  
📧 `coderdeltalan.cargo784@8alias.com`  
🐙 https://github.com/CoderDeltaLAN

---

## 📄 License

Licensed under the **MIT License**. See [LICENSE](./LICENSE) for details.
