# razkarl.com

Static site. No build step, no dependencies, no framework. Edit HTML, push, done.

```
index.html              About (sheet 01)
projects/index.html     Project index (sheet 02)
projects/<slug>/        One folder per project — URLs match the old Webflow ones
assets/css/site.css     Every style, one file
assets/img/             Photos (see SOURCES.md)
CNAME                   Custom domain — do not delete
.nojekyll               Tells Pages to serve files as-is
404.html sitemap.xml robots.txt
```

URLs are identical to the Webflow site (`/projects/kawaz`, etc.), so nothing
you've shared or linked anywhere breaks.

---

## 1. Put it on GitHub

```bash
cd razkarl-site
git init -b main
git add .
git commit -m "Static site"
gh repo create razkarl.com --public --source=. --push
```

No `gh` CLI? Create an empty repo on github.com, then:

```bash
git remote add origin git@github.com:RazK/razkarl.com.git
git push -u origin main
```

Repo name doesn't matter for a custom domain — call it whatever. (If you ever
want the free `razk.github.io` address instead, the repo must be named exactly
`RazK.github.io`.)

## 2. Turn on Pages

Repo → **Settings** → **Pages** → Source: **Deploy from a branch** →
Branch `main`, folder `/ (root)` → **Save**.

Wait ~1 minute. It publishes at `https://razk.github.io/razkarl.com/`.
Confirm it works there before touching DNS.

## 3. DNS (whenever you're ready)

At your registrar, delete the Webflow records first, then add:

**Apex — `razkarl.com`, four A records:**

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**Subdomain — `www`, one CNAME:**

```
www  →  razk.github.io.
```

(Trailing dot, and it's your GitHub *username*, not the repo.)

Then in **Settings → Pages → Custom domain**, enter `razkarl.com` and save.
Once the check goes green, tick **Enforce HTTPS**. The certificate is issued
automatically and free — it can take up to an hour to appear.

DNS propagation is usually minutes, worst case 48h. Check with:

```bash
dig razkarl.com +short
```

## 4. Only then, cancel Webflow

Download your images first (`assets/img/SOURCES.md`) — the Webflow CDN URLs
stop working when the account closes.

---

## Still to fill in

- **Portrait and project photos** → `assets/img/SOURCES.md` has the commands
- **Project write-ups** → each `projects/<slug>/index.html` has `[bracketed]`
  placeholders in the prose block and the spec list
- **Project captions** → `projects/index.html`, the `[one-line caption]` cells
- **Your bio is from 2020** — no BlinkAid, no MS, no security research since.
  Worth a rewrite in `index.html`.
- **Email** currently points to `raz@yosigal.com`, carried over from the old
  site. Change it in the footer of every page if that's stale.

## Editing notes

Colours and type live in the `:root` block at the top of `site.css`. Change a
hex there and it propagates everywhere.

To preview locally:

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Use a server, not `file://` — the links are absolute (`/projects/`) and won't
resolve otherwise.
