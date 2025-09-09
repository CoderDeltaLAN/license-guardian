## Summary

## How to test
- Run `poetry install`
- `poetry run ruff check . && poetry run black --check . && PYTHONPATH=src poetry run pytest -q && poetry run mypy .`

## Checklist
- [ ] Tests pass
- [ ] Lint passes (ruff/black/mypy)
- [ ] Ready label added; not a draft
- [ ] No unrelated changes
