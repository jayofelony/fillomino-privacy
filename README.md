# Fillomino — public site (home page + privacy policy + terms)

These static pages satisfy Google's OAuth / Play Games verification, which requires a
publicly reachable home page **on a domain whose ownership you can verify by DNS**, that
explains the app and links to a privacy policy. A `raw.githubusercontent.com` URL and a
bare `*.github.io` subdomain do not qualify (you can't prove domain-level ownership of a
shared domain).

Target: host these at **`https://fillomino.evemarketscanner.com/`** and verify
`evemarketscanner.com` in Google Search Console.

## Files

| File | Live URL |
|---|---|
| `index.html` | `https://fillomino.evemarketscanner.com/` |
| `privacy-policy.html` | `https://fillomino.evemarketscanner.com/privacy-policy.html` |
| `terms-of-service.html` | `https://fillomino.evemarketscanner.com/terms-of-service.html` |
| `style.css`, `assets/…` | supporting files |

Contact address used in the pages: `oudshoorn.jeroen@gmail.com` (swap for a branded
support address later if you set one up).

## Step 1 — publish the files

**Option A — GitHub Pages with a custom subdomain (uses your public `fillomino-privacy` repo):**

1. Copy the contents of this `site/` folder into the **root** of
   `github.com/jayofelony/fillomino-privacy`, push to `main`.
2. Repo → **Settings → Pages → Source: "Deploy from a branch" → `main` / `(root)`**.
3. Same page → **Custom domain** → enter `fillomino.evemarketscanner.com` → Save.
   (GitHub adds a `CNAME` file to the repo and will provision HTTPS once DNS resolves.)

**Option B — your existing host:** upload the files to wherever `evemarketscanner.com`
is served, under a `fillomino.` subdomain or a `/fillomino/` path, and adjust the URLs below.

## Step 2 — DNS (at your domain registrar / DNS provider for evemarketscanner.com)

For GitHub Pages Option A, add:

```
Type   Name    Value
CNAME  fillomino   jayofelony.github.io.
```

(If your DNS won't CNAME a subdomain, use the four GitHub Pages A records for `fillomino`
instead — see GitHub's "Managing a custom domain" docs.)

Wait for it to resolve, then confirm `https://fillomino.evemarketscanner.com/` loads and
"Enforce HTTPS" is available in the Pages settings.

## Step 3 — verify the domain in Google Search Console

**Sign in as `oudshoorn.jeroen@gmail.com`** (must match the Google account that owns the
Fillomino Google Cloud project).

1. <https://search.google.com/search-console> → **Add property → Domain** →
   `evemarketscanner.com`
2. Google shows a **TXT record**. Add it at your DNS provider:
   ```
   Type  Name  Value
   TXT   @     google-site-verification=XXXXXXXXXXXXXXXXXXXX
   ```
3. Back in Search Console → **Verify**. (A Domain property covers every subdomain,
   including `fillomino.`, and both http/https — this is what the OAuth review checks.)

## Step 4 — update the OAuth consent screen (Google Auth Platform)

| Field | Value |
|---|---|
| App name | `Fillomino` |
| App home page | `https://fillomino.evemarketscanner.com/` |
| App privacy policy link | `https://fillomino.evemarketscanner.com/privacy-policy.html` |
| App terms of service link | `https://fillomino.evemarketscanner.com/terms-of-service.html` |
| Authorized domain | `evemarketscanner.com` |
| Developer contact / support email | your address |

Save, then **re-submit for verification.** This clears all five findings: unresponsive →
live page; not registered to you → Search Console **Domain** property verified by DNS;
behind a login → public; purpose not explained → `index.html`; name mismatch → the page
is titled "Fillomino".
