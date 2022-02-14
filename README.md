# pipx-action

Pipx setup for GitHub Actions.

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

[Pipx](https://github.com/pypa/pipx) is installed by default in `/usr/local/pipx`
(using Python 3.8) when using GitHub Actions and `ubuntu-latest`.

This GitHub Action adds the ability to use another Python version for pipx.
