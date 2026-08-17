# Contributing

Thanks for considering a contribution to a Yii.Rocks package! This guide walks you through the process.

## Getting started

1. Fork the repository and create a branch off the default branch.
2. Install dependencies with Composer: `composer update`.
3. Make your change, adding or updating tests as needed.

## Before opening a pull request

Packages run the same checks locally and in CI. Run these before opening a PR:

### Unit testing

The package is tested with [PHPUnit](https://phpunit.de/). To run the full suite:

```bash
composer phpunit
```

To run a single test or filter:

```bash
vendor/bin/phpunit --filter testMethodName
vendor/bin/phpunit tests/Service/User/RegisterServiceTest.php
```

### Coverage

Coverage is measured separately from the mutation score. `composer infection` doesn't produce a coverage report, so
check it explicitly:

```bash
vendor/bin/phpunit --coverage-text --colors=never --coverage-filter=src
```

Confirm the `Summary` block shows `Methods: 100.00%` and `Lines: 100.00%`. Infection only generates mutants for lines
PHPUnit actually executes during its coverage run. A method with zero coverage produces zero mutants, so it passes
mutation testing silently — making full coverage a hard prerequisite.

### Mutation testing

The package is checked with the [Infection](https://infection.github.io/) mutation testing framework, enforcing
`min-msi=100` and `min-covered-msi=100`:

```bash
composer infection
```

A full run mutates all of `src` and runs the entire PHPUnit suite as its coverage-collection pass, so it can take
minutes even on a fast machine. For quick local feedback while iterating, scope it to the diff instead:

```bash
vendor/bin/infection --git-diff-lines --git-diff-base=main --map-source-class-to-test --threads=max
```

This narrows both the mutated lines and the coverage pass to what actually changed. A single-line change runs in
seconds instead of a minute-plus. Use it as an intermediate check only — it isn't a substitute for the full
`composer infection` run before committing. It can't catch mutants outside the diff, and unlike the full run, it
isn't enforced by any script or CI gate.

### Static analysis

The code is statically analyzed with [Psalm](https://psalm.dev/) at `errorLevel 1`, the strictest setting:

```bash
composer psalm
```

### Code style

[PHP CS Fixer](https://cs.symfony.com/) enforces `@PER-CS3.0` plus alphabetically ordered class elements and
imports:

```bash
composer php-cs-fixer
```

Run whichever of these checks apply to the package before pushing. Make sure the full matrix (all supported PHP
versions, Linux and Windows where applicable) still passes in CI.

## Pull requests

- Keep changes focused — one concern per PR.
- Describe *why* the change is needed, not just what it does.
- Note any breaking changes explicitly.

## Reporting bugs or suggesting features

Please use the existing issue templates when reporting bugs or requesting features.
