# Using LLMs Effectively

A slide deck on how to get good results from large language models — prompting
fundamentals, working style, failure modes, and verification. Built with
[Slidev](https://sli.dev), so the slides are plain markdown (`slides.md`).

**▶ View the slides:** <https://harrisonschwarzer.github.io/using-llms-effectively/>

## Run locally

```bash
npm install
npm run dev      # opens the slideshow at http://localhost:3030
```

Handy keys while presenting: `space`/arrows to navigate, `o` for slide
overview, `f` for fullscreen. Presenter view (with notes and a timer) lives at
`http://localhost:3030/presenter`.

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

## License

Copyright © 2026 Harrison Schwarzer.

- **Slide content** (`slides.md`, slide assets):
  [CC BY 4.0](LICENSE-CONTENT.md) — share and adapt with attribution.
- **Code and configuration** (build setup, workflow, snippets):
  [MIT](LICENSE).
