# setup-pipx

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
      - uses: fredrikaverpil/setup-pipx@v1.5
        with:
          pipx-version: "1.0"
      - run: pipx install <package>
```

## Features

- You decide the Python and pipx versions used.
- Pipx will be installed in an isolated virtual environment, in `.venv_pipx`. You may want to add this to your `.gitignore` so to avoid a dirty git branch during CI execution.
- Can be used in conjunction with [`actions/cache`](https://github.com/actions/cache)
- Support for linux, macOS and windows runners

## Inputs

| Inputs       | Description                      | Required | Default      |
| ------------ | -------------------------------- | -------- | ------------ |
| pipx-version | Pipx Version                     | false    | `N/A`        |
| venv-name    | Name of pipx virtual environment | false    | `.venv_pipx` |

## Advanced usage

### Matrix with caching and poetry

```yaml
on: [push]

jobs:
  example:
    strategy:
      fail-fast: false
      matrix:
        python-version: ["3.7", "3.8", "3.9", "3.10"]
        pipx-version: ["1.0.0"]
        poetry-version: ["1.1.13"]
        os: [ubuntu-latest, windows-latest, macos-latest]
    runs-on: ${{ matrix.os }}
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
        with:
          python-version: ${{ matrix.python-version }}
      - uses: fredrikaverpil/setup-pipx@v1.5
        with:
          pipx-version: ${{ matrix.pipx-version }}
      - uses: actions/cache@v2
        id: cache
        with:
          path: |
            ~/.cache/pip
            ~/.cache/pypoetry/virtualenvs
            .venv_pipx
          key: ${{ runner.os }}-${{ runner.arch }}-py-${{ matrix.python-version }}-pipx-${{ matrix.pipx-version }}-poetry-${{ matrix.poetry-version }}-${{ hashFiles('poetry.lock') }}

      - run: pipx install poetry==${{ matrix.poetry-version }}
      - run: poetry install
      - run: poetry show --outdated
```
