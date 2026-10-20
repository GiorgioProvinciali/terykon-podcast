# Terykon podcast

The episodes of the Terykon podcast: every article of [terykon.com](https://terykon.com), read by an AI-generated voice
(Kokoro-82M, voice af_heart), with the Terykon sting. Feed: <https://podcast.terykon.com/feed.xml>.

- The MP3s are the assets of the releases `episodes-<year>-0` and `episodes-<year>-1` (the article id's parity).
  They are served as `https://audio.terykon.com/<year>/terykon-<id>.mp3`, a Cloudflare Worker that redirects here.
- The branch `catalog` holds `manifest.jsonl`, one line per episode (id, file, seconds, bytes, title, authors, date, loudness,
  true peak, text_sha256, release).
- `.github/workflows/podcast.yml` makes them: `plan` (the slices), `make` (up to 20 jobs, 4 cores each), `feed`
  (the catalogue and the RSS feed, deployed to Cloudflare Pages, with `listen-index.json`: the episodes terykon.com's
  Listen button plays, read by the site's server once an hour). The tools live in the private repository terykon-engine
  (`cartographic/tools/podcast_*.py`, `tts_texts.mjs`, `podcast_feed.mjs`); this repository holds only the workflow,
  the pinned Python requirements and the outputs.

Run: Actions → podcast → Run workflow (`full` the first time, then `incremental` runs every night by itself).

Text © Terykon (Giorgio Provinciali, Alla Perdei). All rights reserved; the audio is a reading of the published articles.
