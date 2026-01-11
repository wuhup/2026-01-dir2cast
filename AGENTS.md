# Repository Guidelines

## Project Structure & Module Organization
- `dir2cast.php` is the primary PHP script that generates the podcast feed.
- `dir2cast.ini` contains runtime configuration (feed metadata, paths, cache settings).
- `getID3/` is the bundled media tag parser used by the main script.
- `test/` holds PHPUnit tests, a `bootstrap.php`, and fixture data in `test/fixtures/`.
- `docker-compose.yml` and `docker-compose/nginx/default.conf` provide a local Nginx + PHP-FPM setup.

## Build, Test, and Development Commands
- `php ./dir2cast.php <media_dir>` runs the script from the CLI (useful for quick validation).
- `docker-compose up` starts a local stack; visit `http://localhost:8080/` (see comments in `docker-compose.yml`).
- `cd test && composer install` installs test dependencies (PHPUnit, Symfony filesystem).
- `./test/run.sh` runs the full test suite; `./test/run.sh SomeTest.php` runs a single test.
- `PATH_COVERAGE=yes ./test/run.sh` enables slower path coverage (requires Xdebug).

## Coding Style & Naming Conventions
- Target PHP 5.4 compatibility; avoid newer syntax and features.
- Follow existing 4-space indentation and file layout in `dir2cast.php`.
- Tests live in `test/` and use the `*Test.php` naming convention.
- Config keys in `dir2cast.ini` are uppercase with underscores (e.g., `FORCE_PASSWORD`).

## Testing Guidelines
- PHPUnit is configured via `test/bootstrap.php` and executed through `test/run.sh`.
- Add or update fixtures in `test/fixtures/` when altering media tag parsing or feed output.
- Coverage files are written to `/tmp` during runs and cleaned up by the script.

## Commit & Pull Request Guidelines
- History shows a mix of short imperative messages and occasional `feat:` prefixes; keep subjects concise and descriptive.
- PRs should explain user-visible behavior changes, include reproduction steps or sample feed output, and link related issues when applicable.
- Update documentation (`README.md`) or `CHANGELOG.txt` when behavior or requirements change.

## Configuration & Runtime Notes
- The cache directory (typically `temp/`) must be writable by the PHP process.
- `dir2cast.ini` can be overridden per media directory by placing another `dir2cast.ini` alongside the media files.
