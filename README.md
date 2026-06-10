# Pala — marketing website

The marketing site and legal pages for **Pala**, a free padel scorekeeper for
Apple Watch & iPhone by Moobytes. Lives at **https://playpala.app**.

Plain static HTML/CSS/JS — **no build step, no dependencies.** Just files.

## Structure

```
index.html                    Landing page
how-padel-scoring-works.html  Cornerstone SEO guide (padel scoring)
support.html                  Help / FAQ        (App Store support URL)
privacy.html                  Privacy Policy     (App Store privacy URL)
terms.html                    Terms of Use       (App Store EULA/policy URL)
404.html                      Branded not-found page
styles.css  app.js            Shared design system + progressive-enhancement JS
robots.txt  sitemap.xml       SEO / crawlability (AI crawlers allowed)
llms.txt                      Summary for LLM/AI answer engines (GEO)
site.webmanifest              PWA manifest
assets/                       Logos, favicons, OG image, app screenshots
.do/app.yaml                  DigitalOcean App Platform spec
```

## Local preview

```bash
python3 -m http.server 8150
# open http://localhost:8150
```

## Deploy — DigitalOcean App Platform (auto-deploy on push)

1. Push this repo to GitHub (`main`).
2. DO → **App Platform → Create App → GitHub** → pick this repo, branch `main`.
3. It auto-detects a **Static Site**. No build command. Output dir `/`,
   index `index.html`, error doc `404.html`. (All captured in `.do/app.yaml`.)
4. Deploy. Every push to `main` redeploys automatically.

Or, reproducibly with the CLI:
```bash
doctl apps create --spec .do/app.yaml
```

### Custom domain (playpala.app on OVH)
In the DO app → **Settings → Domains**, add `playpala.app`. DO shows the DNS
records — add them at **OVH**. DO auto-issues a free Let's Encrypt certificate
once DNS resolves. Free tier covers it ($0).

## App Store Connect URLs
Once live, point App Store Connect at:
- Privacy Policy → `https://playpala.app/privacy.html`
- Support → `https://playpala.app/support.html`
- Marketing → `https://playpala.app/`

(Don't switch ASC to these until the site is actually serving — a 404 on the
privacy URL fails App Review.)

## Updating the app screenshots
The hero/OG screenshots in `assets/` are exported from the iOS app's App Store
screenshots. When you re-shoot them, replace `assets/screen-iphone.png` /
`assets/screen-watch.png` and re-run the OG-image compose step, then commit.

---
© Moobytes · contact: bmo.dev@moobytes.io
