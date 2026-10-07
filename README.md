# EliseAI Leasing Deck

A single-file HTML deck, served by nginx in Docker. This is the build behind the public Railway link.

- `index.html` is the full deck (29 slides), with Fee Transparency and Team Optimization broken out: https://leasing-leave-behind-production.up.railway.app
- `presenting/` is the shorter presenting cut. Fee Transparency and Team Optimization are combined on one slide, with a "go deeper" link to each: https://leasing-deck-production.up.railway.app

## Open it locally

Open `index.html` in a browser. It needs no build step.

Controls:
- ← / → / space move between slides.
- F goes fullscreen.
- O shows the overview.
- Move the mouse to the top of the page to see the section navigator.

## Host it on Railway

1. Make a new Railway project, then choose **Deploy from GitHub repo** and pick this repo.
2. Railway finds the `Dockerfile` and builds it. The container listens on `$PORT`, which defaults to 8080.
3. Under **Settings → Networking**, select **Generate Domain** to get a public URL.

To also host the presenting cut, add a second service from the same repo and set its **Root Directory** to `presenting`.

To host it somewhere else, run `docker build -t leasing-deck . && docker run -p 8080:8080 leasing-deck`, or put `index.html` on any static host.

## Update the deck

Replace `index.html` and push. Railway redeploys on each push. Keep the `noindex` meta tag in `<head>` so search engines don't list the page.
