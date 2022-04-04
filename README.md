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

### NPM Dependencies upgrader

Run npm upgrade and creates a pull request:

```yaml
name: Upgrader

on:
  workflow_dispatch:

jobs:
  upgrade:
    uses: browniebroke/github-actions/.github/workflows/npm-upgrade.yml@v1
    secrets:
      gh_pat: ${{ secrets.GH_PERSONAL_ACCESS_TOKEN }}
```

### Poetry Dependencies upgrader

Clear the Poetry lock file and regenerate it:

```yaml
name: Upgrader

on:
  workflow_dispatch:

jobs:
  upgrade:
    uses: browniebroke/github-actions/.github/workflows/poetry-upgrade.yml@v1
    secrets:
      gh_pat: ${{ secrets.GH_PERSONAL_ACCESS_TOKEN }}
```

### Cookie taster

To help run some end-to-end tests for a cookiecutter project. The action assumes that bot the template and generated projects are using Poetry to manage their dependencies.

```yaml
name: CI

on:
  pull_request:

jobs:
  cookie:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: "3.9"
      - uses: browniebroke/github-actions/cookie-taster@v1
        with:
          # Inputs listed with their default (all optional)
          os: "ubuntu-latest"
          python-version: "3.9"
          tasting-dir: ".tasting"
          cc-options: ""
          pkg-dir: "my-package"
          command-dir: ""
          command: "pytest"
```

### Netlify deploy

Deploy site to Netlify.

```yaml
name: CI

on:
  pull_request:

jobs:
  deploy:
    uses: browniebroke/github-actions/.github/workflows/netlify-deploy.yml@v1
    with:
      publish_dir: "public"
      netlify_site_id: "229636ec-152c-4cef-b9fe-481f3ca066ab"
    secrets:
      netlify_auth_token: ${{ secrets.NETLIFY_AUTH_TOKEN }}
```
