# copier-python-uv

A minimal Copier template for bootstrapping Python projects managed with `uv`.

This template intentionally does **not** enforce a Python package structure. The generated project
starts from a single entry file: `src/main.py`, which is suitable for scripts, batch jobs, small
tools, and prototypes. You can refactor into a package structure later if or when the project grows.

## Features

- Python project scaffold using `uv` (`pyproject.toml`)
- Minimal, non-package-oriented project layout
- Optional `tests/` directory (controlled via Copier prompts)
- Ruff configuration for formatting and linting
- Static type checking via `ty`
- Task runner configuration using `taskipy`
- Docker support:
  - `Dockerfile` for runtime usage
  - `Dockerfile_dev` for development usage
- Makefile helpers for common Docker workflows

## Requirements

- Copier >= 9.0.0
- `uv` (recommended; required to use the generated project as intended)
- Docker (optional; only required if you use Docker-related features)

## Usage

Generate a new project using Copier:

```bash
copier copy <PATH_OR_GIT_URL_TO_THIS_TEMPLATE> <DESTINATION_DIRECTORY>
```

Example:

```bash
copier copy . ../my-project
```

During generation, you will be prompted for values such as:

- `project_name` (kebab-case, e.g. `my-tool`)
- `python_version` (e.g. `3.13`)
- Whether to include a `tests/` directory

## Post-generation behavior

After project generation, Copier may perform lightweight setup tasks:

- If `uv` is available and `.venv` does not exist:
  - Attempt to create a virtual environment using the selected Python version
  - Run `uv lock`

If `uv` is not available or the requested Python version cannot be resolved, these steps are skipped
without failing generation.

## Generated project structure

A typical generated project looks like this:

```text
<project>/
  pyproject.toml
  README.md
  src/
    main.py
  tests/              # optional
  Dockerfile
  Dockerfile_dev
  Makefile
  .gitignore
```

The default entry point is:

```bash
python src/main.py
```

## Common commands (generated project)

Synchronize the environment:

```bash
uv sync
```

Run formatting and linting tasks:

```bash
uv run task fmt
uv run task lint
```

Run tests (when enabled):

```bash
uv run task test
```

## Docker and Makefile

The generated Makefile provides simple targets such as:

- `make build` — build the runtime Docker image
- `make build_dev` — build the development Docker image
- `make bash` — open a shell inside the development container
- `make jupyter` — start Jupyter Lab in the development container

You can override variables when invoking Make targets, for example:

```bash
make build DOCKER_PLATFORM=linux/amd64
```
