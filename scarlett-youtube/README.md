# scarlett-youtube

YouTube research dump for the Scarlett site audit. Generated 2026-04-26 via the Aqua `youtube-processor` skill (transcript + frame sampling + tesseract OCR).

## Contents

### `garrys-list-audit/` — primary reference
- **Source:** [ThePrimeagenHighlights — *Garry's List Audited*](https://www.youtube.com/watch?v=mJ2GZRV63TE)
- **Mode:** technical (transcript + 260 sampled frames @ 2 fps + OCR)
- **Why it's here:** real-world audit of a vibecoded Rails site. Concrete anti-patterns to check for on Scarlett.

Findings touched on in the video (use as a checklist):
- 6.42 MB / 169 requests for a homepage load
- Test files (`*.test` controllers) shipped to clients, returning HTTP 200 unminified
- 78 Stimulus controllers loaded per page (most unused on the homepage)
- Same image asset duplicated across 8 files (3 PNG, 2 WebP, 2 AVIF, 1 favicon) — one AVIF was 0 bytes
- Article images served as raw uncompressed PNG despite `Accept: image/avif, image/webp`
- 520 KB Trix rich-text editor leaking from admin into public bundle
- 47 `<img>` with empty `alt` on a 501(c)(4) civic-engagement site
- Two `<title>` tags
- SDK loaded via same-origin proxy to bypass user ad blockers
- ~73% of bandwidth is waste once you discount images

### `postgres-stack/` — secondary
- **Source:** [The Coding Gopher — *I replaced my entire stack with Postgres...*](https://youtu.be/TdondBmyNXc)
- **Mode:** podcast (transcript only)
- **Why it's here:** stack-collapse reference (JSONB, `SKIP LOCKED`, tsvector, pgvector, partitioning, materialized views, PostgREST). Tangentially relevant if Scarlett's backend is overprovisioned.

## File layout

```
scarlett-youtube/
├── README.md
├── garrys-list-audit/
│   ├── context.md      # token-conscious markdown summary + OCR snippets
│   ├── result.json     # full structured output (segments, frames, OCR per frame)
│   └── frames/         # 260 sampled frames @ 2 fps
└── postgres-stack/
    ├── context.md
    └── result.json
```

`context.md` is the right thing to read first. `result.json` has per-segment timestamps and per-frame OCR text if you want to pin specific findings to specific moments in the video.
