# Follow-up tasks

Left out of scope when the URL fetcher was added (`fetchPage` / `askFetch` in `index.html`).

## 1. Handle fetched pages that overflow the model context

A long page is pasted in full and sent to the model as one request per level, so it can exceed the model's context window or get its JSON output cut off ("Could not parse the model output").

- Decide the behaviour: warn and truncate, or split into chunks and compress each one.
- Show the size of the fetched text before compressing, so the limit is not a surprise.

## 2. Handle pages with no main text

When a page has no article body (navigation only, login wall, JS-only app shell), the reader returns empty or junk content and it is pasted as is. An empty result currently just leaves the editor empty with no explanation.

- Detect empty or near-empty results and say so in the fetch dialog instead of pasting.
- Consider a heuristic for "navigation only" output (mostly links, almost no prose).

## 3. Convert pictures

Images are currently dropped at fetch time (`X-Retain-Images: none`), so figures, charts and their captions are lost.

- Decide what a picture becomes in the original text: alt text, a caption, or a generated description.
- Keep the result as its own paragraph so it maps to compressed blocks like any other text.
