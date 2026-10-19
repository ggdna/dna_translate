# dna_translate

[English](README.md) | Deutsch

Gibt einem Repo die Regeln und einen Skill, um seine englische und deutsche
Dokumentation und README synchron zu halten.

## Motivation

Ein Repo, das auf Englisch und auf Deutsch dokumentiert, braucht zwei
Fassungen, die dasselbe sagen. Ohne Regel laufen sie auseinander: Eine
Änderung landet nur in einer Sprache, einer Datei fehlt das Gegenstück, eine
Übersetzung folgt den Wörtern statt dem Sinn. Diese Schicht legt fest, wo
welche Sprache liegt, wann und wie übersetzt wird, und liefert einen Skill, der
die fehlenden oder veralteten Dateien findet.

## Verwendung

Als Dev-Dependency eintragen und einmal initialisieren:

```bash
pnpm add -D @ggdna/dna-translate   # TypeScript projects
dart pub add dev:dna_translate     # Dart projects
helix init
```

`helix init` legt einen Test ab, der die DNA bei jedem Testlauf instanziiert
und prüft. Er kopiert den Guide nach `doc/guides/`, das Template nach
`doc/templates/` und den Skill nach `.claude/skills/translate/`.

Tippe vor dem Publish `/translate` in Claude Code. Der Skill listet englische
Dateien ohne deutsches Gegenstück, deutsche ohne englisches und Paare, deren
neuere Seite sich nach der älteren geändert hat, und hört dort auf, wenn alles
aktuell ist. Sonst übersetzt er, was fehlt, und listet die geschriebenen
Dateien zur Durchsicht.

## Guides

- `dna/doc/guides/translate-guide.md` — englische Dokumentation in `doc`,
  deutsche in `doc/de`, `README.md` neben `README.de.md`; in der Sprache des
  Prompts beginnen, kurz vor dem Publish übersetzen, inhalts- und
  strukturgleich, aber nicht wörtlich, und wohin die Blogposts jeder Sprache
  gehören

## Templates

- `dna/doc/templates/blog-template-de.md` — der Aufbau eines deutschen
  Blogposts; der englische kommt aus
  [dna_blog](https://github.com/ggdna/dna_blog)

## Skills

- `/translate` — meldet fehlende Gegenstücke und auseinandergelaufene Paare in
  `doc`, `doc/de`, den READMEs und im Blog und übersetzt dann, was fehlt; folgt
  dem Übersetzungs-Guide

## Umfang

Die Schicht hält nur die beiden Sprachen synchron; sie unterstützt Englisch und
Deutsch, keine weitere Sprache. Befehle, Code, Pfade und API-Namen bleiben
unübersetzt, und den Blog-Guide und das englische Blog-Template überlässt sie
dna_blog — der Übersetzungs-Guide verlinkt `blog-guide.md`, das nur diese
Schicht ablegt.

## Schichten

Die Schicht ist orthogonal: `dna/_dna.json` nennt keine Eltern-Schichten. Sie
trägt nur ihr eigenes Thema und wird vom nutzenden Repo mit anderen Schichten
kombiniert.

## Variablen

- `dnaCopyrightHolder` — der Rechteinhaber im Copyright-Kopf jeder abgelegten
  Datei. `mustOverride` in `dna/_dna.json` zwingt jedes Repo und jede Schicht,
  die diese Schicht einbindet, ihn in der eigenen `dna/_vars.json` zu setzen;
  ein Umbrella wie dna_ggdna setzt ihn einmal für seine Organisation

## Entwicklung

Der Ordner `dna/` ist handgeschriebene Quelle und wird nie generiert. Das Repo
instanziiert seine eigene DNA — nach Änderungen `dart test` laufen lassen;
vorher committen, denn eine Datei, die die DNA überschreiben würde, darf keine
uncommittete Arbeit enthalten.

Bearbeite die Dateien unter `dna/`, nie ihre Kopien in `doc/` und `.claude/`:
Der Test überschreibt sie.

## Lizenz

MIT — siehe [LICENSE](LICENSE).
