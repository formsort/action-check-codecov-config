# action-check-codecov-config

A GitHub Action to ensure the validity of your codecov.yaml file

## How

Just add a new workflow to your project with contents adapted from:

```yaml
name: "Check Codecov Config"
on:
  push:
    branches:
      - master
      - gh-readonly-queue/master/**
  pull_request:
    branches: [master]

jobs:
  validate_config:
    name: Valid codecov.yml
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          # This is to avoid errors when using with merge-queues
          fetch-depth: 100
      - name: Validate codecov.yml
        uses: formsort/action-check-codecov-config@v1
```

## Why

[Codecov](https://about.codecov.io/) is great but their docs on `codecov.yml` file is not
the easiest to navigate, especially for larger projects. Even worse, they don't even tell
you when your config is broken. You _may_ notice a discrepancy with the "active" yaml config
and the one in your repo if you ever go to your project settings and check the `Yaml` section
there.

Well, we got burnt by this and realized Codecov actually provides a validation service, just not
in a very visible or easy-to use way. We fixed it for ourselves and wanted to share the solution
to avoid further pain.
