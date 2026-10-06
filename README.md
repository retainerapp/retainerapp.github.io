# Retainer — website

Plain static HTML for GitHub Pages. No build step, no framework, no dependencies.
Edit a file, commit, and it is live in about a minute.

```
index.html              → /                      the Retainer landing page
privacy.html            → /privacy               ← App Store Connect: Privacy Policy URL
support.html            → /support               ← App Store Connect: Support URL
404.html                                         shown for any unknown URL
styles.css                                       every page shares this
favicon.svg                                      the Retainer mark; follows light/dark itself
apple-touch-icon.png                             180px app icon, for home-screen bookmarks
icon-light.svg, icon-dark.svg                    the app icon on the page, light and dark
.nojekyll                                        skip Jekyll; we are serving plain HTML
```

## Where it lives

**https://retainerapp.github.io** — served by GitHub Pages from the repository
`retainerapp/retainerapp.github.io`, owned by the free GitHub organisation `retainerapp`.

- Because the repository is named `<organisation>.github.io`, the site is served at the top of
  the domain — which is what the links assume (`/styles.css`, `/privacy.html`). Served one folder
  down, as an ordinary repository would be, every link and the stylesheet would break.
- **Publishing is pushing.** Commit to `main`, push, and it's live in a minute or two. HTTPS is
  automatic on github.io.
- Support address: **retainerapp@icloud.com**, an iCloud alias. Reply *from the alias*, not a
  personal address.
- Commits here are signed `Retainer <retainerapp@icloud.com>` (set in this repository's own git
  config), so no personal address appears in the public history.

App Store Connect needs two of these addresses:

| Field | Address |
|---|---|
| Privacy Policy URL | https://retainerapp.github.io/privacy.html |
| Support URL | https://retainerapp.github.io/support.html |

## A custom domain, later

If a domain is ever bought: add a `CNAME` file here containing just the domain, point its DNS at
GitHub Pages (four A records on the apex to 185.199.108.153, .109.153, .110.153 and .111.153, and a
`www` CNAME to `retainerapp.github.io`), set the domain under the repository's Settings → Pages,
and tick **Enforce HTTPS** once the certificate is issued. The links already assume the top of a
domain, so nothing else changes. Don't add a `CNAME` file before the domain exists — GitHub will
try to serve the site there and stop serving it at github.io.

## Adding things

**A page** — copy an existing file, keep the `<head>` and the header/footer blocks, change
the middle. There is no templating, so the `<head>` is duplicated per page by design: it is
the price of having no build step, and it is about fifteen lines.

## Design notes

The Retainer identity: the R1 mark — two ticks, one ink and one vermilion, overlapping, with
a third tone where they cross — on warm cream. Every colour at the top of `styles.css` is the
same value as the app's Retainer theme (`Theme/Palette.swift`, `.retainer`), so change it in
one and change it in the other.

**Vermilion means a check-in**, as it does in the app: the activity squares, the underline on
a link. It is never body text on cream — that's 3.1:1. Muted grey (`#696660`, 4.9:1) is the
lightest text colour allowed for anything small.

**The mark in the header is inline SVG**, so it follows the colour scheme: in dark mode the
first tick turns cream and the crossing turns pale, per the handoff's Ink colourway. The
vermilion tick never changes. Every page carries the mark and the name: the site is Retainer's
and nothing else's. The one place a person is named is the privacy policy's "Who this policy is
from", because UK data protection law requires it to say who is responsible.

**No web fonts.** The type is Apple's rounded system face — the app's own — read from the
visitor's device (`ui-rounded`), with the system sans elsewhere. Nothing is downloaded from a
font CDN, which matters on a site whose privacy page promises nobody is watching.

Light and dark are both defined, via `prefers-color-scheme`, entirely in custom properties
at the top of `styles.css`.
