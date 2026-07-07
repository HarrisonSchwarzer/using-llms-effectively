---
name: launch-deck
description: Launch the Slidev dev server and open the slides in the browser, killing any stale instance first. Use when asked to run, launch, start, preview, relaunch, or open the deck locally.
---

Launch the deck from the repo root as follows:

1. **Kill any stale instance from this repo.** Sessions often end without
   stopping the dev server, leaving an old process squatting on port 3030 and
   serving outdated slides — a fresh launch then silently lands on 3031+.
   Always clear ours out first:

   ```bash
   pkill -f "$PWD/node_modules/.bin/slidev" && sleep 1 || true
   lsof -nP -iTCP:3030 -sTCP:LISTEN || echo "port 3030 free"
   ```

   The `$PWD` anchor matches only Slidev processes launched from this repo, so
   other projects' dev servers are untouched. `pkill` exits non-zero when
   nothing matched — that's fine, hence `|| true`. If this session already has
   a Slidev background task running, the pkill terminates it too (its task
   will report completion; that's expected).

   If `lsof` still shows a listener on 3030, it's some other program — leave
   it alone, launch anyway, and expect Slidev on the next port (see step 3).

2. **Check Slidev is installed:** `ls node_modules/.bin/slidev`. If missing,
   run `npm install` first (one-time, downloads Slidev).

3. **Start the dev server in the background:**

   ```bash
   npm run dev -- --open false
   ```

   Run this with `run_in_background: true`. The `--open false` matters: the
   `dev` script is `slidev slides.md --open`, and without the override the
   background process tries to auto-launch a browser itself — pass it so you
   control when the browser opens.

4. **Confirm the port, then wait until it responds.** Read the background
   task's output file — it prints the actual URL (`public slide show >
   http://localhost:XXXX/`). Use the Read tool, not `grep 'localhost:[0-9]*'`:
   Slidev wraps the port in ANSI escape codes, which silently breaks the
   pattern. After step 1 this is normally 3030, but never assume: a probe
   against the wrong port can hit an unrelated server.

   ```bash
   for i in $(seq 1 30); do
     curl -sf -o /dev/null http://localhost:3030 && { echo up; break; }
     sleep 1
   done
   ```

   Verify it's really the deck: `curl -s http://localhost:3030 | head -c 500`
   should contain the title `Using LLMs Effectively - Slidev`.

5. **Open it for the user:** `open http://localhost:3030` (macOS), using the
   port from step 4.

Useful URLs once running: `/presenter` for presenter view (notes + timer),
`/print` for the print layout. To stop the server, stop the background task.
