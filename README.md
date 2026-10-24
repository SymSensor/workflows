# SymSensor workflows

Shared reusable GitHub Actions workflows for the SymSensor bundles.

## `symfony-bundle.yaml`

Runs PHPUnit against every maintained Symfony version listed in
<https://symfony.com/releases.json>. Each version is tested on every non-EOL PHP version it supports (PHP versions from <https://endoflife.date/php>).

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

## `php-cs-fixer.yaml` and `phpstan.yaml`

Run `php-cs-fixer fix --dry-run` and `phpstan analyse` of the calling repository.

```yaml
name: phpstan

on:
    push:
    pull_request:

jobs:
    phpstan:
        uses: SymSensor/workflows/.github/workflows/phpstan.yaml@v1
```

### PHP version of these tools

Both workflows install PHP through `shivammathur/setup-php`, which reads the `.php-version` file of the calling
repository. Commit a `.php-version` with the lowest supported PHP version of the bundle, so that the result of
php-cs-fixer and phpstan does not depend on whatever PHP version is the newest. Without that file the newest
stable PHP is used.
