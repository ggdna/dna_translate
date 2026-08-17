# dna_translate

The DNA layer that keeps German and English documentation in sync.

## Content

- `dna/doc/en/guides/multi-language-guide.md` — when and how to translate
  `doc/de`, `doc/en`, `README.md` and `README.de.md`

## Usage

Declare it as a dev-dependency and initialize once:

```bash
pnpm add -D @ggdna/dna-translate   # TypeScript projects
dart pub add dev:dna_translate    # Dart projects
helix init
```

The placed test instantiates and verifies the DNA on every test run. This
layer sits on top of
[dna_base](https://github.com/ggsuite/dna_base) — everything generic comes
from there, this repo only adds its own topic.

## Development

This repo has `role: "dna"` in `dna/_dna.json`: the `dna/` folder is
authored by hand, never generated. The repo instantiates its own DNA — run
`dart test` after changes; commit first (a file the DNA would overwrite
must not carry uncommitted work).
