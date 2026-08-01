# GaelGrounds website

Marketing site for the GaelGrounds app — a homepage plus Privacy Policy and
Terms of Service pages. Plain static HTML/CSS, no build step, no framework.

- `index.html` — homepage
- `privacy.html` — Privacy Policy
- `terms.html` — Terms of Service
- `styles.css` — shared styles (uses the app's own brand colours)
- `CNAME` — tells GitHub Pages to serve this site at `www.gaelgrounds.ie`

This is marketing content only — it describes the app's features, it doesn't
reimplement any of them (no real check-ins, accounts, or data here).

## Deploying with GitHub Pages (free)

1. Push this repo to GitHub (already done if you're reading this from there).
2. In the repo on GitHub: **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Branch: `main`, folder: `/ (root)`. Save.
5. Under **Custom domain**, enter `www.gaelgrounds.ie` and save (this matches
   the `CNAME` file already in the repo, so GitHub should pick it up
   automatically — entering it in the UI too makes sure GitHub provisions
   the HTTPS certificate for it).
6. Once the DNS step below is done and has propagated, tick **Enforce HTTPS**.

## DNS setup (at your domain registrar for gaelgrounds.ie)

Add these two records:

| Type  | Host/Name | Value                     |
|-------|-----------|---------------------------|
| CNAME | `www`     | `cormacbrannigan03.github.io` |
| A     | `@` (apex)| `185.199.108.153`          |
| A     | `@` (apex)| `185.199.109.153`          |
| A     | `@` (apex)| `185.199.110.153`          |
| A     | `@` (apex)| `185.199.111.153`          |

The `www` CNAME record is what actually serves the site. The four apex `A`
records are optional but recommended — they make `gaelgrounds.ie` (without
`www`) redirect to `www.gaelgrounds.ie` instead of not resolving at all.
Those four IPs are GitHub Pages' standard, permanent apex-domain addresses
(the same for every GitHub Pages site — not specific to this project).

DNS changes can take anywhere from a few minutes to ~24 hours to propagate,
depending on your registrar.

## Editing content

Everything is plain HTML — open any `.html` file and edit directly, no
build step required. `styles.css` is shared across all three pages via
CSS custom properties at the top of the file (`--green`, `--gold`, etc.)
matching the brand colours already used in the iOS app
(`ios/GaelGrounds/Utilities/Theme.swift` in the main GaelGrounds repo).

## Before this goes live for real

- **Contact email**: every page currently links to `hello@gaelgrounds.ie` —
  make sure that inbox exists and is actually monitored, or swap it for
  whatever address you want to use, in `index.html`, `privacy.html`, and
  `terms.html`.
- **Legal review**: the Privacy Policy and Terms of Service are drafted to
  accurately describe what the app actually collects and how the €1.99/month
  subscription works, but this isn't legal advice — worth a solicitor's
  once-over before this is the live policy backing an App Store submission,
  especially since it's handling EU/GDPR user data.
- **App Store link**: the "Coming soon" badges aren't clickable yet. Once
  the app has a real App Store listing, swap those `<span class="store-badge">`
  elements for real `<a href="...">` links to the App Store page.
