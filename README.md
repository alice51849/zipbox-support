# Zipbox support site

The public support, privacy and terms pages for **Zipbox** (App Store:
`Zipbox: Unzip RAR, ZIP & 7z`), in all 50 App Store locales.

    index.html     what Zipbox does, privacy promise, contact
    support.html   getting started, FAQ, troubleshooting
    privacy.html   privacy policy and paid-download handling
    terms.html     terms of use
    samples/       sample archives for App Review (unlisted, linked only from
                   the review notes)
    sitemap.xml, robots.txt, .nojekyll

Every page is a single self-contained file: inline CSS, inline JavaScript and
inline translations. There is no framework, CDN, web font, analytics or
cookie. These public pages are opened by the system outside Zipbox; the app
itself makes no network request. The language is picked from the browser and
can be changed with the selector in the header or with `?lang=<locale>`; the
choice is remembered in `localStorage` only.

## Do not hand-edit the HTML

`index.html`, `support.html`, `privacy.html` and `terms.html` are generated.
Edit the copy in `../marketing/src/copy/*.json`, then:

    python3 marketing/build.py     # rewrites docs/*.html and the metadata pack
    python3 marketing/validate.py  # 50 locales, field limits, banned wording

`marketing/make_samples.py` regenerates `samples/`.

## Publishing

Either serve this folder from the app repository (Settings → Pages → Source:
`main` / `/docs`), or copy it into a repository named `zipbox-support` and
serve from its root. Both give the canonical URLs the pages and the App Store
metadata already point at:

    https://alice51849.github.io/zipbox-support/
    https://alice51849.github.io/zipbox-support/support.html   -> ASC Support URL
    https://alice51849.github.io/zipbox-support/privacy.html   -> ASC Privacy Policy URL
    https://alice51849.github.io/zipbox-support/              -> ASC Marketing URL

If the site ends up on a different path, change `SITE` at the top of
`marketing/build.py` and re-run it: the canonical tags, the sitemap and all 50
locales of `supportUrl` / `privacyPolicyUrl` come from that one constant.

## Contact

`hourstag.app@gmail.com` is the only address that may appear on this site or in
the app. `marketing/validate.py` fails the build if any other address appears
anywhere under `marketing/` or `docs/`.
