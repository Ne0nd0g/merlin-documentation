[![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Release](https://img.shields.io/github/release/Ne0nd0g/merlin-documentation.svg)](https://github.com/Ne0nd0g/merlin/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/Ne0nd0g/merlin-documentation/total.svg)](https://github.com/Ne0nd0g/merlin/releases)
[![Twitter Follow](https://img.shields.io/twitter/follow/merlin_c2.svg?style=social&label=Follow)](https://twitter.com/merlin_c2)

# Merlin Documentation

Documentation source code repository for Merlin C2 at https://merlin-c2.readthedocs.io

## Supported Versions

This repository contains documentation for the following Merlin components and their individual version numbers:

- [Merlin Server v1.5.1](https://github.com/Ne0nd0g/merlin/releases/tag/v1.5.1)
- [Merlin Agent v1.6.3](https://github.com/Ne0nd0g/merlin-agent/releases/tag/v1.6.3)
- [Merlin Agent DLL v1.6.0](https://github.com/Ne0nd0g/merlin-agent-dll)

## Build & View

Use the following steps to build and view the documentation locally:

1. **OPTIONAL** - Create a Python virtual environment: `python -m venv .venv`
2. **OPTIONAL** - Activate the Python virtual environment: `source .venv/bin/activate`
3. Ensure the Python `sphinx` & required packages are installed with: `python -m pip install sphinx sphinx_rtd_theme recommonmark`
4. Build the documentation with: `sphinx-build -b html docs/source/ docs/build/html`
5. Open [docs/build/html/index.html](docs/build/html/index.html)

## Layout

The project's directory layout is:

- [docs/CHANGELOG.MD](docs/CHANGELOG.MD) - This project's changelog
- [docs/build](docs/build) - Rendered documentation ready to be viewed in a browser
- [docs/source](docs/source) - Source reStructuredText documentation files
