# dna_translate

The DNA layer that keeps documentation in sync across languages.

## Guides

- `dna/doc/guides/translate-guide.md` — when and how to translate `doc`,
  `doc/de`, `README.md` and `README.de.md`, and where blog posts of each
  language belong

## Templates

- `dna/doc/templates/blog-template-de.md` — the structure of a german
  blog post; the english one comes from
  [dna_blog](https://github.com/ggdna/dna_blog)

## Skills

- `/translate` — reports missing counterparts and pairs that drifted
  apart, then translates what is missing

## Layers

Orthogonal: this layer carries only its own topic and is combined with
other layers by the consuming repo.

## Variables

- `dnaCopyrightHolder` — the name in the license header of every file
- `dnaYear` — the year folder blog posts are filed under

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
