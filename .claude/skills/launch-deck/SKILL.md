---
name: launch-deck
description: Launch the Slidev dev server and open the slides in the browser. Use when asked to run, launch, start, preview, or open the deck locally.
---

Launch the deck from the repo root as follows:

1. **Check Slidev is installed:** `ls node_modules/.bin/slidev`. If missing,
   run `npm install` first (one-time, downloads Slidev).

2. **Start the dev server in the background:**

   ```bash
   npm run dev -- --open false
   ```

   Run this with `run_in_background: true`. The `--open false` matters: the
   `dev` script is `slidev slides.md --open`, and without the override the
   background process tries to auto-launch a browser itself — pass it so you
   control when the browser opens.

3. **Wait until it responds** (usually ~1s):

   ```bash
   for i in $(seq 1 30); do
     curl -sf -o /dev/null http://localhost:3030 && { echo up; break; }
     sleep 1
   done
   ```

   Verify it's really the deck: `curl -s http://localhost:3030 | head -c 500`
   should contain the title `Using LLMs Effectively - Slidev`.

   If 3030 never responds, the port was taken and Slidev picked the next one
   (3031, 3032, …) — Read the background task's output file for the actual URL.

4. **Open it for the user:** `open http://localhost:3030` (macOS).

Useful URLs once running: `/presenter` for presenter view (notes + timer),
`/print` for the print layout. To stop the server, stop the background task.
