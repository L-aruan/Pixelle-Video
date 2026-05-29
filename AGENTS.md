# Repository Guidelines

## Project Structure & Module Organization

Pixelle-Video is a Python 3.11 project for AI-assisted short-video generation. Core application code lives in `pixelle_video/`, with services, pipelines, prompts, models, config loading, and utilities split by responsibility. FastAPI routes, schemas, and task management live in `api/`. The Streamlit UI is in `web/`, including pages, components, state, i18n, and UI pipelines. Workflow presets are JSON files under `workflows/`, HTML rendering templates are under `templates/`, static project assets are in `resources/`, and documentation is in `docs/`. Packaging helpers live in `packaging/`.

## Build, Test, and Development Commands

Use `uv` for dependency management:

```bash
uv sync
uv run streamlit run web/app.py
uv run uvicorn api.app:app --host 0.0.0.0 --port 8000
uv run pytest
uv run ruff check .
```

`uv sync` installs runtime and development dependencies from `pyproject.toml` and `uv.lock`. The Streamlit command starts the web UI. The Uvicorn command starts the API server. Run pytest and Ruff before submitting changes.

## Coding Style & Naming Conventions

Follow PEP 8 with Ruff enforcement. The configured line length is 100 characters, target Python version is 3.11, and Ruff checks `E`, `F`, and import sorting (`I`) while ignoring `E501`. Use four-space indentation, `snake_case` for functions/modules, `PascalCase` for classes and Pydantic models, and descriptive service names such as `tts_service.py` or `frame_processor.py`. Keep code and comments in English.

## Testing Guidelines

Pytest is configured with `asyncio_mode = "auto"` and `testpaths = ["tests"]`. Add tests under `tests/` when changing services, API routes, config behavior, or pipelines. Prefer filenames like `test_video_service.py` and test functions like `test_generates_frame_plan()`. Include async tests for async route/service behavior and use small fixtures instead of real external AI calls.

## Commit & Pull Request Guidelines

Recent history uses concise subjects, including plain descriptions and occasional Conventional Commit prefixes such as `fix:`. Keep commit subjects short and imperative, for example `fix: handle missing workflow output` or `Add template preview docs`. Pull requests should describe the change, list verification steps, link related issues, and include screenshots or sample outputs for UI, template, or generated-media changes.

## Security & Configuration Tips

Do not commit secrets, API keys, generated media, or local runtime output. Start from `config.example.yaml` for configuration changes, and document new settings in `docs/en/reference/config-schema.md` and `docs/zh/reference/config-schema.md` when applicable.
