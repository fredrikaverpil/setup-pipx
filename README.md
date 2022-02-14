# pipx-action

[Pipx](https://github.com/pypa/pipx) setup for GitHub Actions.

## Quickstart example

```yaml
on: [push]

jobs:
  creosote:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
        with:
          python-version: "3.10"
      - uses: fredrikaverpil/pipx-action@v1.2
      - run: pipx install <package>
```

## Why?

Pipx is installed by default in the GitHub Action runners. However, you can't control
which the versions used for pipx and the Python interpreter itself.

This GitHub Action aims to solve this problem, by utilizing
[`actions/setup-python`](https://github.com/actions/setup-python) to pick the desired
Python version.

As a bonus, this action installs pipx into an isolated virtual environment, avoiding
installing it in the system installation of Python.
