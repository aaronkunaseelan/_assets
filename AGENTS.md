# AGENTS.md

Plain-Markdown article store. No build, no site, no dependencies — the files are the
product. Keep it that way: don't add tooling, front matter, or config.

## Layout

- `posts/` — one article per file.
- `README.md` — no copyright claimed, contact address. Leave it alone.

## Article format

- Filename: lowercase-hyphenated slug of the title, `.md`. No date prefix.
- Line 1 is `# Title`. Line 2 is blank. Nothing above the H1.
- No date line, no `(N words)` line, no metadata block.
- LF endings, trailing newline. Body Markdown is untouched — hard-wrap breaks,
  escaped headings, and tables stay as they came.

Heading depth below the H1 varies by article. Don't normalize it.

## Commits

Commit message is the article's date, `YYYY-MM-DD` — not a summary. One article per
commit.

## Publishing

There is usually no local checkout. Commit through the API:

```sh
gh api --method PUT repos/05802/_assets/contents/posts/<slug>.md \
  -f message='<YYYY-MM-DD>' \
  -f content="$(base64 -w0 <file>)"
```

Read the last few commits first — they are the reference for the conventions above.
