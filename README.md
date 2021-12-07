# github-actions

A collection of my own GitHub actions

[![pre-commit.ci status](https://results.pre-commit.ci/badge/github/browniebroke/github-actions/main.svg)](https://results.pre-commit.ci/latest/github/browniebroke/github-actions/main)

## List of actions

### Lint for a Typescript project

Run a set of linting tools (eslint, prettier & tsc) for a typical Typescript project:

```yaml
name: CI

on:
  pull_request:

jobs:
  lint:
    uses: browniebroke/github-actions/.github/workflows/ts-lint.yml@v1
```

### Bundlewatch

Runs [bundlewatch](https://bundlewatch.io):

```yaml
name: CI

on:
  pull_request:

jobs:
  bundlewatch:
    uses: browniebroke/github-actions/.github/workflows/bundlewatch.yml@v1
    secrets:
      bundlewatch_token: ${{ secrets.BUNDLEWATCH_GITHUB_TOKEN }}
```

### Dependencies upgrader

Run npm upgrade and creates a pull request:

```yaml
name: Upgrader

on:
  workflow_dispatch:

jobs:
  upgrade:
    uses: browniebroke/github-actions/.github/workflows/npm-upgrade.yml@v1
    secrets:
      github_token: ${{ secrets.GITHUB_TOKEN }}
```
