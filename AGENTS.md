# AGENTS.md

Article store. No build, no dependencies. Don't add tooling, front matter, or config.

## Layout

- `posts/` — one article per file.
- `README.md` — leave it alone.

## Article format

```
# Electronics through copper
(1783 words), last edited: 2026.08.08 evening

Body starts here.
```

H1, metadata, blank line, body. LF endings, trailing newline. The body is verbatim —
hard-wrap breaks, escaped headings, tables, and whatever heading depth it came with.

The five articles from 2026-08-08 predate line 2; add it when you next touch one.

## Naming

Lowercase-hyphenated slug of the title, no date prefix:

`# Change and Adaptation in Complex Systems` → `posts/change-and-adaptation-in-complex-systems.md`

`electrons-through-copper.md` doesn't match its H1. Leave it — renaming breaks links.

## Commits

One article per commit. Line 1 is the commit's date; `tags:` comes last — subject,
model, publisher, original format.

```
2026-08-08
published: 2025-11-15
source: https://www.ft.com/content/1f3e5472
tags: electronics, claude-opus-5, ft, google-docs
```

## Publishing

No local checkout. Add `-f sha="$(gh api repos/05802/_assets/contents/posts/<slug>.md --jq .sha)"`
when updating an existing article.

```sh
gh api --method PUT repos/05802/_assets/contents/posts/<slug>.md \
  -f message="$(cat msg.txt)" \
  -f content="$(base64 -w0 <file>)"
```
