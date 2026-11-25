# Example

`dna_translate` is a DNA layer: it ships the translation rules, the German
blog template and the `/translate` skill, no library code. Declare it as a
dev dependency and instantiate it once:

```bash
dart pub add dev:dna_translate    # Dart projects
pnpm add -D @ggdna/dna-translate  # TypeScript projects
gg dna init
gg dna build
```

Then type `/translate` in Claude Code to create or update the translated
READMEs, docs and blog posts.
