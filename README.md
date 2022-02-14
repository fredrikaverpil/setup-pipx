# pipx-action

[Pipx](https://github.com/pypa/pipx) setup for GitHub Actions.

## Quickstart example

This example pipx-installs [`creosote`](https://github.com/fredrikaverpil/creosote) and
then executes it, using Python 3.10.

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
      - uses: fredrikaverpil/pipx-action@v1.1
      - run: pipx install creosote
      - run: creosote
```

## Why?

Pipx is installed by default in the GitHub Action runners. However, you can't control
which Python version will be used by pipx.

This GitHub Action aims to solve this problem, by utilizing
[`actions/setup-python`](https://github.com/actions/setup-python) to pick the desired
Python version.
