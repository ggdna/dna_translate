# dna_translate

English | [Deutsch](README.de.md)

Gives a repo the rules and a skill to keep its English and German
documentation and README in sync.

## Motivation

A repo that documents in English and in German needs both versions to say the
same. Without a rule they drift apart: a change lands in one language only, a
file has no counterpart, a translation follows the words instead of the
meaning. This layer says where each language lives, when and how to
translate, and gives a skill that finds the files that are missing or out of
date.

## Usage

Declare it as a dev-dependency and initialize once:

```bash
pnpm add -D @ggdna/dna-translate   # TypeScript projects
dart pub add dev:dna_translate     # Dart projects
helix init
```

`helix init` places a test that instantiates and verifies the DNA on every
test run. It copies the guide to `doc/guides/`, the template to
`doc/templates/` and the skill to `.claude/skills/translate/`.

Type `/translate` in Claude Code before publishing. The skill lists English
files without a German counterpart, German files without an English one and
pairs whose newer side changed after the older one, and stops there when
everything is current. Otherwise it translates what is missing and lists the
files it wrote for review.

## Guides

- `dna/doc/guides/translate-guide.md` — English documentation in `doc`,
  German in `doc/de`, `README.md` next to `README.de.md`; start in the
  language of the prompt, translate shortly before publishing, content- and
  structure-equal but not literally, and where blog posts of each language go

## Templates

- `dna/doc/templates/blog-template-de.md` — the structure of a German blog
  post; the English one comes from
  [dna_blog](https://github.com/ggdna/dna_blog)

## Skills

- `/translate` — reports missing counterparts and pairs that drifted apart in
  `doc`, `doc/de`, the READMEs and the blog, then translates what is missing;
  follows the translate guide

## Scope

The layer only keeps the two languages in sync; it supports English and
German, no other language. It leaves commands, code, paths and API names
untranslated, and leaves the blog guide and the English blog template to
dna_blog — the translate guide links `blog-guide.md`, which only that layer
places.

## Layers

The layer is orthogonal: `dna/_dna.json` lists no parent layers. It carries
only its own topic and is combined with other layers by the consuming repo.

## Variables

- `dnaCopyrightHolder` — the holder named in the copyright header of every
  placed file. `mustOverride` in `dna/_dna.json` forces every repo or layer
  that lists this layer to set it in its own `dna/_vars.json`; an umbrella
  such as dna_ggdna sets it once for its organization

## Development

The `dna/` folder is hand-authored source and is never generated. The repo
instantiates its own DNA — run `dart test` after changes; commit first, a file
the DNA would overwrite must not carry uncommitted work.

Edit the files below `dna/`, never their copies in `doc/` and `.claude/`: the
test overwrites them.

## License

MIT — see [LICENSE](LICENSE).
