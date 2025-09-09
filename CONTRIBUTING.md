# Contributing

Use Poetry locally. Before any push:

```bash
poetry run ruff check . --fix
poetry run ruff format .
poetry run black .
PYTHONPATH=src poetry run pytest -q
poetry run mypy .
```

Small, atomic PRs. Follow Conventional Commits. CI must be green.
