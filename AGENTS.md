# AGENTS.md

Article store. No build, no site, no dependencies. Don't add tooling, front matter, or config.


## Layout

- `posts/` — one article per file.
- `README.md` — no copyright claimed, contact address. Leave it alone.

## Article format

- Filename: lowercase-hyphenated slug of the title, `.md`. No date prefix.
- 
- Line 1 is `# Title`.
  line 2 : `(N words)` , last edited: yyyy.mm.dd morning, afternoon, or evening
- Line 3 is blank. Nothing above the H1.
-  no metadata block.
- LF endings, trailing newline. Body Markdown is untouched — hard-wrap breaks,
  escaped headings, and tables stay as they came.
Heading depth below the H1 varies by article. Don't normalize it.

## Commits

Commit message is the commit's date, `YYYY-MM-DD`, published date, source, the last line is 'tags: .." and includes things like subject, the model that generated it, publisher, original format etc . One article per
commit.

There is usually no local checkout. Commit through the API:

```sh
gh api --method PUT repos/05802/_assets/contents/posts/<slug>.md \
  -f message='<YYYY-MM-DD>' \
  -f content="$(base64 -w0 <file>)"
```

