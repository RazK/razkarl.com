# Images

Every frame on the site shows drafting hatch until you drop the real file in.
Nothing breaks if a file is missing — the `onerror` handler removes the broken
image and leaves the hatch.

## What goes where

| File | Used on |
|---|---|
| `assets/img/portrait.jpg` | Home page, FIG. 1 (portrait crop, ~4:5) |
| `assets/img/<slug>/01.jpg`, `02.jpg` | Each project page (landscape, ~3:2) |

Slugs: `kawaz`, `bottle`, `tangible-asteroids`, `digital-knife`, `fll`,
`i-robot`, `heating`.

## Pulling your originals off Webflow

These are your own uploads, still served from Webflow's CDN. Grab them before
you cancel the plan — the URLs die with the account.

```bash
cd assets/img

# portrait (two crops exist; pick whichever you prefer)
curl -o portrait.jpg "https://uploads-ssl.webflow.com/5f5ff0e50b9becec9645e6f7/5f6152409e9ce65e2459b469_476526_3481675362442_674427849_o%20-%20Copy%20(2)-3.jpg"
curl -o portrait-alt.jpg "https://uploads-ssl.webflow.com/5f5ff0e50b9becec9645e6f7/5f6151b974ff99562957ed5a_476526_3481675362442_674427849_o%20(2)-2.jpg"
```

For the project images, the fastest route is a full mirror of the old site
while it's still up, then copy what you want out of it:

```bash
wget --mirror --page-requisites --convert-links --adjust-extension \
     --span-hosts --domains=razkarl.com,uploads-ssl.webflow.com,assets.website-files.com \
     --restrict-file-names=windows https://razkarl.com/
```

Resize before committing — anything over ~1600px wide is wasted bytes on a
static site.
