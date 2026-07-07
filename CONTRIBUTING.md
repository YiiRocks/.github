# Contributing

Thanks for considering a contribution to a Yii.Rocks package!

This file is a default for repositories under the [YiiRocks](https://github.com/YiiRocks) organization that don't provide their own `CONTRIBUTING.md`.

## Getting started

1. Fork the repository and create a branch off the default branch.
2. Install dependencies with Composer: `composer update`.
3. Make your change, adding or updating tests as needed.

## Before opening a pull request

Most packages run the same checks in CI:

- **Tests** — `vendor/bin/phpunit`
- **Static analysis** — [Psalm](https://psalm.dev/)
- **Coding standard** — [PHP-CS-Fixer](https://cs.symfony.com/), configured in `.php-cs-fixer.php`

Run whichever of these apply to the package before pushing, and make sure the full matrix (current supported PHP versions, Linux and Windows where applicable) still passes.

## Pull requests

- Keep changes focused — one concern per PR.
- Describe *why* the change is needed, not just what it does.
- Note any breaking changes explicitly.

## Reporting bugs or suggesting features

Please use the issue templates on the relevant repository.
