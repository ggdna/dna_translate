# dna_translate

The DNA layer that keeps documentation in sync across languages.

## Guides

- `dna/doc/en/guides/translate-guide.md` — which languages the repo keeps,
  how `doc/<lang>`, `pm/<lang>` and `README.<lang>.md` stay in sync, and
  where blog posts of each language belong

Every file of `dna/doc/en/` also ships in German and Farsi, with the
same name:

- `dna/doc/de/guides/`
- `dna/doc/fa/guides/`

## Skills

- `/translate` — reports missing counterparts and pairs that drifted
  apart, then translates what is missing

## Publishing

`dna/dot-pubignore` keeps `/doc/*/guides/` out of the
package `dart pub publish` uploads. helix joins it with the ignore files of the
other layers into the project's `.pubignore`.

## Layers

Orthogonal: this layer carries only its own topic and is combined with
other layers by the consuming repo.

## Variables

- `dnaCopyrightHolder` — the name in the license header of every file
- `dnaLanguages` — the languages of the repo as two-letter codes, the
  leading one first, separated by commas; default `en`, e.g. `en,de,fa`

## Usage

Declare it as a dev-dependency and initialize once:

```bash
pnpm add -D @ggdna/dna-translate   # TypeScript projects
dart pub add dev:dna_translate         # Dart projects
helix init
```

The placed test instantiates and verifies the DNA on every test run.

## Development

The `dna/` folder is hand-authored source and is never generated. The repo
instantiates its own DNA — run `dart test` after changes; commit first, a
file the DNA would overwrite must not carry uncommitted work.
