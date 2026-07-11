# streamwatch-iptv

A/B fork of [streamwatch](https://github.com/Pablomx2/streamwatch), swapping its match-based streamed.pk/embed.st backend for [iptv-org/api](https://github.com/iptv-org/api)'s live sports TV channels.

**Live at:** https://pablomx2.github.io/streamwatch-iptv/ (once GitHub Pages is enabled on this repo and this PR is merged)

## What it is

A single static `index.html` — same dark UI, category tabs, search, and player modal as the main streamwatch app, but:

- **Data:** fetches `channels.json` / `streams.json` / `blocklist.json` / `logos.json` directly from `iptv-org.github.io/api` (CORS-open, no backend needed).
- **Content:** 24/7 linear sports channels (ESPN, beIN Sports, regional networks, etc.), not scheduled matches — everything is always shown as live.
- **Categories:** iptv-org has one flat `sports` category; `classify()` re-buckets each channel by name/network keywords into the same category set the main app uses (basketball, football, american-football, hockey, baseball, motor-sports, fight, tennis, rugby, golf, cricket, billiards, afl, darts, other).
- **Playback:** raw `.m3u8` HLS URLs played via a `<video>` element — native HLS on Safari, [hls.js](https://github.com/video-dev/hls.js) (CDN) elsewhere.

## Deploy

GitHub Pages, source = `main` branch, root. No build step, no functions, no `package.json`.

## Known limitation

Some public IPTV streams require a spoofed `Referer`/`User-Agent` to play, which a static frontend can't set — those show an in-player error rather than failing silently.
