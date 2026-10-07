<div align="center">

# 🎶 Wavecord

**A Discord music bot for playing your favorite music from YouTube.**

[![Version](https://img.shields.io/badge/version-0.1.0--dev-0A7BBC)](#project-status)
[![Python](https://img.shields.io/badge/Python-3.11%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Discord](https://img.shields.io/badge/Discord-music_bot-5865F2?logo=discord&logoColor=white)](https://discord.com/)
[![CI/CD checks](https://github.com/shliakhovai/wavecord/actions/workflows/quality.yml/badge.svg?branch=master&event=push)](https://github.com/shliakhovai/wavecord/actions/workflows/quality.yml)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-FAB040?logo=pre-commit&logoColor=white)](https://pre-commit.com/)
[![code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

</div>

## About

Wavecord is a Python-powered Discord music bot designed to make listening to YouTube music with friends simple.
The project is currently in its initial development stage, with automated code-quality checks already in place.

## Project status

| Item | Value |
| --- | --- |
| Version | `0.1.0-dev` |
| Python | `3.11+` |
| Status | Active development |
| Default branch | `master` |

## Code quality

Every contribution is checked with the same tools locally and in GitHub Actions:

- **Black** formats Python code with a 120-character line length.
- **isort** sorts and groups imports using the Black-compatible profile.
- **Flake8** catches style errors, common bugs, and overly complex code.
- **flake8-docstrings** requires NumPy-style docstrings for public functions and methods.
- **pre-commit-hooks** validates YAML, TOML, JSON, Python syntax, line endings, merge markers, and large files.

Module-level docstrings and docstrings for `__init__.py` files are not required.

## Development setup

Clone the repository and enter the project directory:

```bash
git clone git@github.com:shliakhovai/wavecord.git
cd wavecord
```

Create and activate a virtual environment:

```bash
python3.11 -m venv .venv
source .venv/bin/activate
```

Install and enable pre-commit:

```bash
python -m pip install pre-commit==4.5.1
pre-commit install
```

Run all checks manually:

```bash
pre-commit run --all-files
```

## CI/CD

The [Python quality workflow](https://github.com/shliakhovai/wavecord/actions/workflows/quality.yml) runs automatically:

- for every push;
- for every pull request;
- after a pull request is merged into `master`;
- on demand through the GitHub Actions interface.

The workflow runs the complete pre-commit suite against the repository. A deployment stage will be added when the
bot's runtime environment is selected.

## Contributing

1. Create a branch for your change.
2. Make the change and add or update tests when applicable.
3. Run `pre-commit run --all-files`.
4. Open a pull request and wait for the **CI/CD checks** workflow to pass.
