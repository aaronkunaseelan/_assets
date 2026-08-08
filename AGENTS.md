# AGENTS.md

Article store. No build, no site, no dependencies. Don't add tooling, front matter, or
config.

## Layout

- `posts/` — one article per file.
- `README.md` — leave it alone.

## Article format

```
# Electronics through copper
(1783 words), last edited: 2026.08.08 evening

Short version:
Body starts here.
```

- Line 1: `# Title`. Nothing above it.
- Line 2: word count, then last edited as `yyyy.mm.dd` plus `morning`, `afternoon`, or
  `evening`.
- Line 3: blank.
- No YAML front matter, no metadata block. Everything else lives in the commit message.
- LF endings, trailing newline.
- Body Markdown is copied verbatim — hard-wrap breaks, escaped headings
  (`## **1\. …**`), and tables stay as they came. Heading depth below the H1 varies by
  article; don't normalize it.

The five articles committed on 2026-08-08 predate line 2. Add it when you next touch
one; don't sweep them all in one commit.

## Naming

Lowercase-hyphenated slug of the title, `.md`. No date prefix.

`# Change and Adaptation in Complex Systems` → `posts/change-and-adaptation-in-complex-systems.md`

`posts/electrons-through-copper.md` predates this and doesn't match its H1
("Electronics through copper"). Leave it — renaming breaks links.

## Commits

One article per commit. The message carries the metadata:

```
2026-08-08
published: 2025-11-15
source: https://www.ft.com/content/1f3e5472
tags: electronics, claude-opus-5, ft, google-docs
```

- Line 1: the commit's own date, `YYYY-MM-DD`.
- `published:` the article's original date.
- `source:` where it came from.
- Last line, `tags:` — subject, the model that generated it, publisher, original format.
  Omit what doesn't apply; keep the order.

## Publishing

There is usually no local checkout. Commit through the API:

```sh
gh api --method PUT repos/05802/_assets/contents/posts/<slug>.md \
  -f message="$(cat msg.txt)" \
  -f content="$(base64 -w0 <file>)"
```

Updating an existing article needs its blob sha as well:

```sh
  -f sha="$(gh api repos/05802/_assets/contents/posts/<slug>.md --jq .sha)"
```
