# uv Virtual Environment Setup

This project ships with a `pyproject.toml`, so you can let the [`uv`](https://github.com/astral-sh/uv) package manager create and maintain a virtual environment for you. The commands below default to creating `.venv/` in the repository root. We target Python 3.10 here (the project supports any Python ≥3.10).

## 1. Install `uv`

`uv` is distributed as a single binary (no Python required). Install it once and keep it on your `PATH`.

- Linux / macOS  
  ```bash
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```
- Windows (PowerShell)  
  ```powershell
  powershell -ExecutionPolicy Bypass -NoProfile -Command "iwr https://astral.sh/uv/install.ps1 -UseBasicParsing | iex"
  ```

After installation, restart your shell or run the snippet that the installer prints so that `uv` is available immediately.

## 2. Sync dependencies into a virtualenv

```bash
uv python install 3.10          # optional; ensures Python 3.10 is available
uv sync                         # creates .venv/ and installs project dependencies
```

`uv sync` reads `pyproject.toml` and installs the main dependencies. Use extras if you need the development toolchain:

```bash
uv sync --extra dev             # include black, pytest, etc.
```

## 3. Activate the environment

- Linux / macOS  
  ```bash
  source .venv/bin/activate
  ```
- Windows (PowerShell)  
  ```powershell
  .\.venv\Scripts\Activate.ps1
  ```

Activation is optional; you can also prefix commands with `uv run`, for example:

```bash
uv run python examples/demo.py
```

## 4. Managing dependencies

- Add a package to the project: `uv add PACKAGE_NAME`
- Upgrade to the latest compatible versions: `uv lock --upgrade && uv sync`
- Remove a package: `uv remove PACKAGE_NAME`

All of these commands update the lockfile (`uv.lock`) so that the environment stays reproducible for the team.

## 5. Deactivating or recreating the environment

- Leave the shell session: `deactivate`
- Start clean: delete `.venv/` (or run `uv clean`) and then rerun `uv sync`.

That’s it—`uv` keeps the virtual environment aligned with the configuration in `pyproject.toml`.
