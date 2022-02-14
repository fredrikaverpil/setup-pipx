# pipx-action

Pipx setup for GitHub Actions.

## Quickstart example

```yaml
on: [push]

jobs:
  unused-deps:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
      - uses: fredrikaverpil/pipx-action@v1
      - run: |
          pipx install <package>
          pipx list
```
