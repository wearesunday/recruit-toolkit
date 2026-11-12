# Job Upload Toolkit

A single-file browser tool that speeds up uploading job adverts to a job board.

- **Job copy:** drop a .docx, .pdf or .txt file, or paste text, and get clean HTML (bold, italic, underline, bullets, links and paragraph spacing kept; styles, tables and images removed), a 150 character search result summary, suggested keywords and suggested tags.
- **Logo 360×180:** fits a logo into a 360×180 PNG with a 5px margin, trimming white or transparent space and flattening transparency to white.

Everything runs in the browser. The PDF reader, Word reader and fonts are built into the file, so it works offline and nothing is sent anywhere. Both pages are marked `noindex` so search engines don't list them.

## Live URLs

| Version | URL |
|---|---|
| Production | https://wearesunday.github.io/recruit-toolkit/recruit-toolkit.html |
| Dev | https://wearesunday.github.io/recruit-toolkit/recruit-toolkit-dev.html |

GitHub Pages serves the root of `main`. Changes can take a few minutes to go live.

## Files

| File | Purpose |
|---|---|
| `recruit-toolkit.html` | Production. Only changed by a promote or a rollback. |
| `recruit-toolkit-dev.html` | Dev. All edits happen here. |

## Workflow

### Update (dev only)

1. Edit `recruit-toolkit-dev.html`. Never edit `recruit-toolkit.html` directly.
2. Run the privacy check (below).
3. Commit with a short description of the change and push to `main`.
4. Check the Pages build shows `built` for the new commit and that the raw file matches the local copy, then test the dev URL.

### Promote dev to production

Only when the change has been tested and approved:

```bash
cp recruit-toolkit-dev.html recruit-toolkit.html
git add recruit-toolkit.html
git commit -m "Promote dev to production"
git push
```

Then verify the build and test the production URL.

### Roll back production

```bash
git log --oneline -- recruit-toolkit.html   # find the last good commit
git checkout <commit> -- recruit-toolkit.html
git commit -m "Roll back production to <commit>"
git push
```

The dev file isn't touched, so the faulty change can be fixed there and promoted again.

## Privacy check before every push

This repo is public and the pages can be opened by anyone with the link. Before each push, check the file contains no client names or branding, people's names, email addresses or phone numbers, credentials or tokens, internal or admin URLs, sample job adverts or logos, and no network calls (no fetch, XHR, external scripts, fonts or images).
