# pipx-action

[Pipx](https://github.com/pypa/pipx) setup for GitHub Actions.

## Quickstart example

```yaml
on: [push]

jobs:
  example:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
        with:
          python-version: "3.10"
      - uses: fredrikaverpil/pipx-action@v1.3
        with:
          pipx-version: "1.0"
      - run: pipx install <package>
```

## Features

- Pipx will be installed in an isolated virtual environment (not in the system install of Python)
- Control the Python interpreter version with [`actions/setup-python`](https://github.com/actions/setup-python)
- Control the pipx version using the optional `with: pipx-version` statement
