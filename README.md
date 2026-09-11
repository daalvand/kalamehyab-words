# kalamehyab-words

Public dictionary source for the [کلمه‌یاب](https://github.com/daalvand/kalamehyab) app,
served for free via [jsDelivr](https://www.jsdelivr.com/) CDN (no server needed).

The app checks `meta.json` at most once every 24 hours and downloads a fresh
`words.json` only when the version changes. If the app is offline or this repo
is unreachable, it silently keeps using the last cached copy.

## How to publish a dictionary update

1. Edit `words.json` in this repo (same format as the app's `web/words.json`:
   `{ "normalizedKey": "originalWord" }`).
2. Commit and push to `main`.
3. Copy the new commit's SHA.
4. Update `meta.json` with that SHA:
   ```json
   {
     "version": "<new-commit-sha>",
     "updatedAt": "<ISO timestamp>",
     "url": "https://cdn.jsdelivr.net/gh/daalvand/kalamehyab-words@<new-commit-sha>/words.json"
   }
   ```
5. Commit and push `meta.json`. Apps will pick it up within 24 hours automatically.

Using the commit SHA (not `@main`/`@latest`) in the jsDelivr URL keeps each
version's URL immutable, so the CDN never serves stale content for it.
