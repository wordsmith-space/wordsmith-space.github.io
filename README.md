# aslam.wordsmith — profile & rate card

A one-page profile and rate card for editorial and typesetting services, with
every call-to-action pointing to an external request form. Built to be hosted
free on GitHub Pages, with no backend, no JavaScript, and no third-party
requests.

---

## 1. The design, in one breath

The page is set like the **interior of a finely-made book** — because that is
the actual trade being sold. The hero is a title page. The section labels are
borrowed from a book's anatomy (*Prakata*, *Karya*, *Khidmat*, *Kadar*,
*Proses*, *Kolofon*). On wide screens, small roman folios sit in the margins;
the *Prakata* opens with a portrait and a two-tone line (*Seorang penulis. /
Seorang penyunting.*) over a drop-cap bio; *Karya* is split into two shelves —
the books you've written (with forthcoming titles shown as teasers) and the
books you've laid out for other publishers; and the only ornament anywhere is
the editor's red proof-mark. Paper-warm background, fountain-pen ink text, a
single proof-red accent. Type is Fraunces (display), Crimson Pro (body — the
house font), and a plain monospace for the small utility labels.

It is meant to look composed, not decorated.

---

## 2. Tech stack & why

| Layer | Choice | Reason |
|---|---|---|
| Markup | Static HTML | Nothing to execute, nothing to breach server-side |
| Styling | One CSS file | No framework, no build step |
| Scripts | **None** | Removes an entire class of client-side vulnerabilities; the CSP blocks scripts outright |
| Fonts | Self-hosted `.woff2` | No Google Fonts / CDN call → zero third-party requests, faster, privacy-friendlier |
| Hosting | GitHub Pages | Free, automatic HTTPS, no subscription |
| Form | External provider | The page only *links out*, so it collects no data itself |

The whole site is files. There is no database, no server logic, and no API
key anywhere in the repo — so the repository can safely be **public**.

---

## 3. Before you publish

**Already wired in** — edit anytime, but nothing here is required:

- **Prices** — set from your rate card, in RM, priced per page: Suntingan
  struktur RM 7, Suntingan bahasa & gaya RM 6, Baca pruf RM 4, Penilaian
  manuskrip RM 300/manuskrip, Reka letak & tipografi RM 5–7. Edit them in the
  *Kadar* section. (Two services from the card aren't listed yet — Translation
  and Feature & Creative Writing; add them if you'd like.)
- **Your books** (*Karya*) — two shelves. *Tulisan saya*: Cerita-Cerita Pelik
  dari Pinggir Katil (2025) plus two 2027 teasers. *Suntingan & reka letak*:
  Manusia Moden and Wacana Psikologi. To add a book: drop the cover into
  `media/covers/`, copy a `<figure class="work …">` block into the right shelf,
  and set the src, title, and role. Tile variants: `work--flat` (flat cover
  image), `work--mockup` (transparent 3D-mockup PNG/WebP), `work--soon` (teaser,
  no cover).

**Still to fill** — each is marked with a `TODO` comment in `index.html`:

1. **Portrait** — the *Prakata* shows a placeholder "A." tile. Drop your photo
   into `media/` and follow the TODO comment to swap in an `<img>` (vertical
   4:5, ~800×1000px or larger).
2. **Tagline** — the line under your name in the hero is a placeholder
   (`Perkataan yang ditimbang…`). Replace it with your own positioning line.
3. **Form link** — three buttons point to
   `https://forms.gle/REPLACE-WITH-YOUR-FORM`. Swap in your real form URL
   (see §4); one find-and-replace covers all three.
4. **Contact links** (footer): your Threads handle, e-mail address (currently a
   placeholder domain), and WhatsApp number (`60XXXXXXXXXX`, no `+` or spaces).
5. **Optional** — `og:image` and `og:url` in the `<head>`, and a custom domain
   (see §5).

---

## 4. The request form

The page is built to **hand off** to a form, so it never touches a visitor's
data directly. Pick one:

**Google Forms — recommended.** Free, unlimited responses, and answers collect
straight into a Google Sheet. Suggested fields:

- Nama
- Cara untuk dihubungi (e-mel / WhatsApp / Threads)
- Jenis khidmat (the five services)
- Sedikit tentang naskhah (genre, panjang, status)
- Tarikh akhir yang diharapkan
- Bajet (optional)

Create the form → **Send** → link icon → copy the `forms.gle/…` URL → paste it
over `REPLACE-WITH-YOUR-FORM`.

**Tally** is a good alternative if you want a more designed form on a free tier.
**WhatsApp** is the lightest option: point the buttons at
`https://wa.me/60XXXXXXXXXX?text=Hai,%20saya%20ingin%20bertanya%20tentang%20khidmat%20suntingan`
instead of a form — fewer fields, but no structured record.

Whichever you choose, keep the form short and add a one-line PDPA note (e.g.
*"Maklumat ini digunakan hanya untuk menjawab permintaan anda."*). With this
setup, the form provider — not you — is the party storing the data.

---

## 5. Deploy to GitHub Pages

**Method A — through the website (no command line)**

1. Create a new **public** repository.
   - Name it `aslam-wordsmith` → site will live at
     `https://<username>.github.io/aslam-wordsmith/`
   - Or name it exactly `<username>.github.io` → site lives at the root
     `https://<username>.github.io/`
2. **Add file → Upload files.** Drag in everything: `index.html`,
   `styles.css`, `404.html`, `favicon.svg`, `.gitignore`, and the **`fonts/`
   and `media/` folders** (keep the folders — fonts must stay at `fonts/…` and
   images at `media/…`). Commit.
3. **Settings → Pages → Build and deployment.** Source: *Deploy from a branch*.
   Branch: `main`, folder: `/ (root)`. Save.
4. Wait a minute, then open the URL Pages shows you.

**Method B — git**

```bash
git init
git add .
git commit -m "aslam.wordsmith profile + rate card"
git branch -M main
git remote add origin https://github.com/<username>/<repo>.git
git push -u origin main
```

Then do step 3 above.

**Custom domain (optional).** Settings → Pages → Custom domain, enter it, and
tick **Enforce HTTPS**. GitHub writes a `CNAME` file into the repo; point your
domain's DNS at GitHub Pages per their instructions.

---

## 6. A note on security

What this setup already gives you:

- **No backend** — no server or database to attack.
- **No JavaScript** — the most common web-app vulnerabilities simply don't apply,
  and the Content-Security-Policy in the `<head>` blocks scripts and limits
  what may load (`default-src 'none'`, fonts/styles/images from self only).
- **No third-party requests** — nothing leaks to ad networks or CDNs.
- **HTTPS** — automatic on GitHub Pages.

**One honest limitation.** Some protections — `Strict-Transport-Security`,
`X-Frame-Options` / `frame-ancestors`, `Permissions-Policy` — only work as real
**HTTP response headers**, and GitHub Pages does not let you set those. The CSP
here is delivered via a `<meta>` tag, which covers most of it, but not those
header-only controls.

If you want them, put **Cloudflare** (free tier) in front of the site as a
proxy. You then get: *Always Use HTTPS*, HSTS, custom response-header rules (to
add the headers above), and basic WAF/DDoS protection — all at no cost. This is
optional; the site is safe to publish without it.

---

## 7. Preview locally

From this folder:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000`. (Open via a server, not by double-clicking
the file, so the fonts and CSP behave the same as in production.)

---

## 8. What's in here

```
aslam-wordsmith/
├── index.html      The page
├── styles.css      All styling and design tokens
├── 404.html        Styled "not found" page
├── favicon.svg     Editor's caret mark
├── .gitignore      Keeps OS/editor cruft out of the repo
├── fonts/
│   ├── fraunces.woff2            Display (variable)
│   ├── crimson-pro.woff2         Body
│   └── crimson-pro-italic.woff2  Body italic
├── media/          Your images go here
│   ├── README.txt               What to put where
│   └── covers/                  Book covers for the Karya section
└── README.md       This file
```

Fonts: **Fraunces** and **Crimson Pro**, both open-licensed (SIL Open Font
License).
