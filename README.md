# Using LLMs Effectively

A slide deck on how to get good results from large language models — prompting
fundamentals, working style, failure modes, and verification. Built with
[Slidev](https://sli.dev), so the slides are plain markdown (`slides.md`).

**▶ View the slides:** <https://harrisonschwarzer.github.io/using-llms-effectively/>

## How the pieces fit together

- **`slides.md`** is the presentation. It's plain markdown — this is the only
  file you normally edit.
- **Slidev** is the open-source tool that turns that markdown into a browser
  slideshow. It's installed via npm into `node_modules/` (local only, not
  committed to the repo).
- **GitHub Actions** rebuilds the slideshow on GitHub's servers every time you
  push to `main`, and publishes the result to the live URL above. You never
  build or upload anything manually.
- Nothing here is published *to* npm — `package.json` is marked private; npm
  is only used to download Slidev.

## Day-to-day workflow

```bash
# 1. Edit slides.md in any editor, then preview live:
npm run dev

# 2. Happy with it? Publish:
git add slides.md
git commit -m "Update slides"
git push
```

About a minute after the push, the live URL reflects your changes (watch
progress under the repo's **Actions** tab).

Handy keys while presenting: `space`/arrows to navigate, `o` for slide
overview, `f` for fullscreen. Presenter view (with notes and a timer) lives at
`http://localhost:3030/presenter`.

## Setting up on a new machine

```bash
git clone https://github.com/HarrisonSchwarzer/using-llms-effectively.git
cd using-llms-effectively
npm install      # one-time: downloads Slidev
npm run dev      # opens the slideshow at http://localhost:3030
```

## Edit

Everything is in [`slides.md`](slides.md) — one slide per `---` separator.
Presenter notes go in HTML comments at the end of a slide. See the
[Slidev docs](https://sli.dev/guide/syntax) for layouts, themes, and animations.

## Export to PDF

```bash
npm install -D playwright-chromium   # one-time, needed by the exporter
npm run export                       # produces slides-export.pdf
```

## Deploy

Pushing to `main` triggers a GitHub Actions workflow
([`.github/workflows/deploy.yml`](.github/workflows/deploy.yml)) that builds
the deck and publishes it to GitHub Pages.

## References

Source material the deck draws on:

- **"Full Walkthrough: Workflow for AI Coding"** — Matt Pocock, AI Engineer
  conference (Europe), April 24, 2026. A ~96-minute workshop; no published
  slide deck exists, so the video is the canonical source.
  - [Talk video](https://www.youtube.com/watch?v=-QFHIoCo-Ko)
  - [Announcement post](https://x.com/mattpocockuk/status/2053583757743911232)
  - [dictionary-of-ai-coding](https://github.com/mattpocock/dictionary-of-ai-coding)
    — his written definitions of the talk's terms, e.g.
    [Smart zone](https://github.com/mattpocock/dictionary-of-ai-coding/blob/main/dictionary/Smart%20zone.md)
  - [AI Engineer Workshop 2026](https://www.aihero.dev/ai-engineer-workshop-2026~dwnll)
    — companion course on aihero.dev covering the same material

## License

Copyright © 2026 Harrison Schwarzer.

- **Slide content** (`slides.md`, slide assets):
  [CC BY 4.0](LICENSE-CONTENT.md) — share and adapt with attribution.
- **Code and configuration** (build setup, workflow, snippets):
  [MIT](LICENSE).
