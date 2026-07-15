# Distance Audio Model

A browser-based tool to simulate audio gain changes over distance for a looping
soundscape, with optional random one-shot sounds. It's a fully client-side
static web app built on the Web Audio API — there is no backend.

```
smpldist/
├── public/          # Deployable static site (this is what gets served/uploaded)
│   └── index.html
├── package.json
├── .gitignore
└── README.md
```

## Run locally (for testing)

Install the dev dependency once, then start the local server:

```sh
npm install
npm run dev
```

Then open http://localhost:5173 in your browser.

Loading and decoding audio files works over `http://localhost`, which is why a
local server is preferred over opening the file directly (`file://`).

> Tip: any static server works. If you'd rather not use npm, you can run
> `python -m http.server 5173 --directory public` and open the same URL.

## Deploy to a remote server

Everything in `public/` is a plain static site — HTML, CSS, and JS with no build
step — so you can host it anywhere that serves static files.

**Upload to your own server** (copy the contents of `public/` to your web root):

```sh
# via scp
scp -r public/* user@your-server:/var/www/distance-audio-model/

# or via rsync
rsync -av --delete public/ user@your-server:/var/www/distance-audio-model/
```

**Or use a static host:**

```sh
npm run deploy:vercel     # requires: npm i -g vercel  (and `vercel login`)
npm run deploy:netlify    # requires: npm i -g netlify-cli  (and `netlify login`)
```

## Note on Tailwind CSS

The UI uses the Tailwind Play CDN (`https://cdn.tailwindcss.com`), which is
convenient and requires no build step. It prints a console warning that it isn't
intended for production and depends on that CDN being reachable at runtime. For a
small internal tool this is fine. If you later want a self-contained,
production-optimized bundle, switch to the Tailwind CLI to compile a local
stylesheet.
