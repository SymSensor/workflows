# SymSensor workflows

Shared reusable GitHub Actions workflows for the SymSensor bundles.

## `symfony-bundle.yaml`

Runs PHPUnit against every maintained Symfony version listed in
<https://symfony.com/releases.json>. Each version is tested on its minimum PHP version and on PHP 8.4.

Usage in a bundle (`.github/workflows/build.yaml`):

```yaml
name: Build

on:
    push:
    pull_request:

jobs:
    test:
        uses: SymSensor/workflows/.github/workflows/symfony-bundle.yaml@v1
```

`@v1` is a moving tag; pin a commit SHA if you need reproducibility.
