# GaelGrounds website

Marketing site for the GaelGrounds app — a homepage plus Privacy Policy,
Terms of Service, and Support pages. Plain static HTML/CSS, no build step,
no framework.

- `index.html` — homepage
- `privacy.html` — Privacy Policy (GDPR-oriented: legal basis for
  processing, data retention, DPC complaint rights)
- `terms.html` — Terms of Service (GAA non-affiliation, Premium billing
  terms including the EU 14-day withdrawal right, liability)
- `support.html` — Support / FAQ (account deletion, cancelling Premium,
  reporting incorrect data)
- `styles.css` — shared styles (uses the app's own brand colours), all four
  pages draw from this one stylesheet rather than duplicating styles per page
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

- **Legal review**: the Privacy Policy and Terms of Service go further than
  a first draft — GDPR Article 6 legal basis, DPC complaint rights, the EU
  14-day subscription withdrawal right, GAA non-affiliation language — but
  `terms.html`'s limitation-of-liability section is explicitly flagged
  in-page as a working draft, not solicitor-reviewed. Worth a paid legal
  review once Premium is generating real revenue; not treated as a launch
  blocker.
- **App Store link**: the "Coming soon" badges aren't clickable yet. Once
  the app has a real App Store listing, swap those `<span class="store-badge">`
  elements for real `<a href="...">` links to the App Store page.
