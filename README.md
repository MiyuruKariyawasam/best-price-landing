# MyBestPrice — Pre-Launch Landing Page

Static landing page for `mybestprice.lk`, used before the beta to collect **seller registrations** and **buyer waitlist sign-ups**.

| File | Purpose |
|---|---|
| `index.html` | Landing page (single file, no build step) |
| `privacy.html` | Pre-launch privacy notice (linked from both forms) |
| `CNAME` | Custom domain for GitHub Pages (`mybestprice.lk`) |
| `.nojekyll` | Tells GitHub Pages to serve files as-is (no Jekyll processing) |

## Before publishing

1. Create the two forms (questions and wording are in `docs/launch/FORMS_AND_PRIVACY_NOTICE.md` in the private MyBestPrice project, not in this repo).
2. In `index.html`, replace these placeholders:
   - `SELLER_FORM_URL`: seller registration form link (4 links)
   - `BUYER_FORM_URL`: buyer waitlist form link (3 links)
   - `FACEBOOK_URL`, `INSTAGRAM_URL`, `TIKTOK_URL`, `WHATSAPP_CHANNEL_URL`: social links (remove any you don't have yet)
3. In `privacy.html`, replace `[DATE]`, `[FOUNDER FULL NAME]`, `[Tally / Google]` and `[21]`.
4. Optional: add an `og:image` (1200×630) once the logo is ready, for nicer WhatsApp/Facebook link previews.

## Preview locally

Open `index.html` in a browser, or run a local server from this folder:

```bash
npx serve .
```

## Deploy to GitHub Pages (free, recommended for the landing page)

This repo (`best-price-landing`) is **public** so GitHub Pages is free. It contains only the landing page files. The main MyBestPrice project (business docs, code) stays **private** and separate.

1. **Public repo:** `MiyuruKariyawasam/best-price-landing` (already created). Push changes to `main`.
2. **Turn on Pages:** repo → **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main`, folder `/ (root)` → Save.
3. **Verify the domain** (prevents others from claiming it): your GitHub profile → **Settings → Pages → Add a verified domain** → `mybestprice.lk` → add the TXT record GitHub shows (`_github-pages-challenge-MiyuruKariyawasam.mybestprice.lk`) at your DNS provider → **Verify**.
4. **Point DNS to GitHub Pages** at your DNS provider:

   | Type | Name | Value |
   |---|---|---|
   | A | `@` (mybestprice.lk) | `185.199.108.153` |
   | A | `@` | `185.199.109.153` |
   | A | `@` | `185.199.110.153` |
   | A | `@` | `185.199.111.153` |
   | AAAA | `@` | `2606:50c0:8000::153` |
   | AAAA | `@` | `2606:50c0:8001::153` |
   | AAAA | `@` | `2606:50c0:8002::153` |
   | AAAA | `@` | `2606:50c0:8003::153` |
   | CNAME | `www` | `miyurukariyawasam.github.io` |

   *Check these IP addresses against GitHub's current "Managing a custom domain for your GitHub Pages site" documentation before adding them.*
5. Back in **Settings → Pages**, confirm the custom domain shows `mybestprice.lk`, wait for the DNS check to pass, then tick **Enforce HTTPS** (the certificate can take up to about an hour).
6. Test on a phone: `https://mybestprice.lk` and `https://www.mybestprice.lk` load, both form links open, and `privacy.html` works.

**Where is DNS managed?** Use whatever DNS service your .lk registrar provides. If it doesn't offer easy DNS editing, use **Cloudflare's free DNS** (records set to "DNS only", the grey cloud) while still hosting on GitHub Pages. Cloudflare will be needed anyway for the beta website (`api.`, `media.`, `staging.` subdomains and image CDN).

**Note:** GitHub Pages isn't meant for running a commercial online service. A pre-launch information page with links to external forms is fine. The beta website itself runs on MyBestPrice's own server (see the infrastructure plan in the main project).

## Alternative: Cloudflare Pages (free)

1. Cloudflare dashboard → **Workers & Pages** → **Create** → **Pages** → **Upload assets** (or connect a Git repo with output directory `landing`; no build command).
2. **Custom domains** → add `mybestprice.lk` (DNS must be on Cloudflare).
3. Works with a private repo, so a separate public repo isn't needed.

When the beta website (Next.js) launches, it replaces this page on `mybestprice.lk`.
