# nitrate.info — marketing site

Static site for **Nitrate — Golden age streaming**. Plain HTML and one stylesheet, no
build step, no JavaScript. Deployed with GitHub Pages.

```
index.html      Landing page
privacy.html    Privacy Policy
terms.html      Terms of Service
support.html    Support / FAQ
assets/css/     site.css — all tokens and layout
assets/fonts/   Archivo Narrow (variable) + Barlow 400/600, latin subset, woff2, SIL OFL
assets/img/     App icon (SVG), favicon, apple-touch-icon, OG card
CNAME           nitrate.info
```

## Deploying

1. `git init && git add -A && git commit`
2. Push to a GitHub repo.
3. Settings → Pages → Source: *Deploy from a branch*, branch `main`, folder `/ (root)`.
4. Settings → Pages → Custom domain: `nitrate.info`, then tick **Enforce HTTPS** once the
   certificate is issued.

DNS for the apex domain — four `A` records at your registrar:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

Plus a `CNAME` for `www` → `<username>.github.io` if you want the www form to work.

Nothing here needs Jekyll; `.nojekyll` keeps Pages from processing the files.

## Point the app at these pages

`Dependencies/CharityKit/Sources/CharityKit/AppLinks.swift` in the Nitrate repo still has
`https://example.com/...` placeholders. Once this is live:

```swift
public static let terms = URL(string: "https://nitrate.info/terms.html")!
public static let privacy = URL(string: "https://nitrate.info/privacy.html")!
```

App Store Connect also needs the Privacy Policy URL and the Terms of Use (EULA) URL for
the auto-renewable subscription — both point here.

## Placeholder assets still needed

Every dashed-bordered element in the markup is an asset slot. Replace the `.ph` element
with a real `<img>` and keep the striped fill as its loading background.

| Slot | Aspect / size | Where |
|---|---|---|
| Hero still | Landscape, ≥2400px wide | `index.html` — hero, full-bleed |
| Closing still | Landscape | `index.html` — closing CTA (optional; flat panel today) |
| Posters ×12 | 2:3 | `index.html` — catalog grid |
| App screenshots ×4 | 4:3 crop | `index.html` — platform cards |

Serve them as AVIF/WebP and set `width`/`height` or `aspect-ratio` so nothing shifts.

The OG card (`assets/img/og-image.png`) is generated from the wordmark alone — regenerate
it over the real hero still when one exists.

## Deviations from the design handoff

The handoff described a product without a subscription and without ads. The app has both,
so the copy was corrected to match the shipping app rather than shipped as designed:

- **Press strip removed** — the handoff says to delete it rather than ship fake logos.
- **Support search field removed** — the handoff says not to ship a dead input.
- **Fake article counts and service-status card removed** — they were hardcoded
  placeholders. Topic cards now anchor into the FAQ on the same page.
- **No accounts** — the design's account/sign-in/email copy is gone. The app has no
  sign-up; sync runs through the user's own private iCloud database.
- **No offline downloads** — the feature isn't in the app, so all download copy is gone.
- **Ads disclosed** — the design claimed "there are no ads in Nitrate". iOS runs AdMob
  interstitials for non-members with a UMP consent form, and that is now described in
  Privacy and Terms. Mac and Apple TV genuinely show no ads, so that line survives.
- **Restorations reframed** — the design claimed the scans and restorations as our own
  work. Films are hosted and streamed by the Internet Archive; what is ours is the apps
  and the curation. Terms says so.
- **Subscription documented** — The Nitrate Society is covered in `terms.html#membership`
  with the auto-renewal disclosures Apple requires, and in `privacy.html#membership`.
- **Film count softened** — "Thousands of films" became no number at all, per the
  handoff's own rule about not claiming a figure you won't stand behind.
- **Footer** — "ALL FILMS PUBLIC DOMAIN" became "Public domain & freely licensed films",
  since some titles are licensed rather than public domain.

## Still to decide

- **Governing law / jurisdiction.** `terms.html` has no governing-law clause because it
  depends on where you operate from. Worth adding one before the site gets much traffic.
- **Effective dates.** Both legal pages read September 8, 2026 in a `<time>` element.
  Update them when the text next changes materially.
