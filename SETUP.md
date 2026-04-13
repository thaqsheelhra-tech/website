# HR assist — Setup & Deployment Guide

This folder is a complete static site. It deploys as-is to GitHub Pages (or Netlify, Vercel, Cloudflare Pages — any static host). Below are the three things you need to do to take it from download to live-on-your-domain:

1. Create a Google Form and wire it in
2. Push the site to GitHub Pages
3. Point your GoDaddy domain at GitHub Pages

---

## What's in this folder

```
index.html          ← Landing page (updated pricing, CTAs wired to form)
story.html          ← Our story
careers.html        ← Open roles
press.html          ← Press kit
contact.html        ← Contact details
changelog.html      ← Release notes
privacy.html        ← Privacy policy
terms.html          ← Terms of service
security.html       ← Security page
dpa.html            ← Data processing addendum
assets/
  styles.css        ← All shared styles
  reveal.js         ← Scroll-reveal animation
```

Every CTA button on the site that says **"Book a walkthrough"**, **"Start your free workspace"**, **"Start free"**, **"Begin Grove"**, or **"Talk to us"** currently points to the placeholder URL `https://forms.gle/YOUR_FORM_ID`. You'll replace this in step 1.

The pricing section has been updated: **Seedling (free) is removed**, and **Grove** and **Canopy** now each have a significantly expanded feature list.

---

## 1. Create your Google Form and map it to the site

### 1a. Build the form

1. Go to <https://forms.google.com> and click **Blank form**.
2. Give it a title like *"HR assist — Start your free workspace"* and a short description.
3. Add fields. A recommended minimum set:
   - **Full name** (short answer, required)
   - **Work email** (short answer, required — turn on *Response validation → Text → Email*)
   - **Company name** (short answer, required)
   - **Number of employees** (multiple choice: 1–10, 11–50, 51–200, 201–500, 500+)
   - **What brought you here?** (short answer, optional)
   - **Phone number** (short answer, optional)
4. Click the ⚙️ **Settings** icon:
   - Under **Responses**, turn on *Collect email addresses → Verified*.
   - Turn on *Send responders a copy of their response → When requested*.
   - Under **Presentation**, set a confirmation message like *"Thanks — we'll be in touch within one business day."*
5. Click **Send** (top right) → click the **link icon** 🔗 → tick **Shorten URL** → click **Copy**.
   - You'll get a URL like `https://forms.gle/aBcDeFgHiJkLmNoP`.

### 1b. Wire the form into the site

Open each HTML file in a text editor and replace the placeholder:

- **Find:** `https://forms.gle/YOUR_FORM_ID`
- **Replace with:** the URL you just copied (e.g. `https://forms.gle/aBcDeFgHiJkLmNoP`)

On macOS / Linux you can do this from the terminal in one shot:

```bash
cd /path/to/this/folder
# macOS
find . -name "*.html" -exec sed -i '' 's|https://forms.gle/YOUR_FORM_ID|https://forms.gle/aBcDeFgHiJkLmNoP|g' {} +
# Linux
find . -name "*.html" -exec sed -i    's|https://forms.gle/YOUR_FORM_ID|https://forms.gle/aBcDeFgHiJkLmNoP|g' {} +
```

On Windows (PowerShell):

```powershell
Get-ChildItem -Filter *.html -Recurse | ForEach-Object {
  (Get-Content $_.FullName) -replace 'https://forms.gle/YOUR_FORM_ID','https://forms.gle/aBcDeFgHiJkLmNoP' |
  Set-Content $_.FullName
}
```

### 1c. (Optional) Get responses into a Google Sheet

In Google Forms, click the **Responses** tab → click the **Sheets icon** → *Create a new spreadsheet*. Every submission now flows into a live Sheet, and you can add email alerts via *Tools → Notification rules* in the Sheet.

### 1d. (Optional) Embed the form inline instead of linking out

If you'd rather keep users on your site, in Google Forms click **Send → `< >` embed** and copy the `<iframe …>` tag. Replace any CTA link on the site with that iframe inside a dedicated page (e.g. `signup.html`) and point the buttons there instead.

---

## 2. Push the site to GitHub Pages

### 2a. Create the repository

1. Sign in to <https://github.com>.
2. Click **New repository** (top-right `+` menu).
3. Name it — if you want the URL `https://<username>.github.io` you **must** name it `<username>.github.io`. Otherwise any name works and the URL becomes `https://<username>.github.io/<reponame>`.
4. Keep it **Public**, don't add a README (you already have files), click **Create repository**.

### 2b. Upload the files

**Option A — drag and drop (easiest):**

1. On the new empty repo page, click **uploading an existing file**.
2. Drag every file and the `assets/` folder into the upload zone.
3. Scroll down, write a commit message like *"Initial site"*, click **Commit changes**.

**Option B — command line:**

```bash
cd /path/to/this/folder
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

### 2c. Turn on GitHub Pages

1. In the repo, click **Settings** (top nav).
2. In the left sidebar, click **Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Under **Branch**, pick `main` and folder `/ (root)`, then click **Save**.
5. Wait 30–60 seconds, refresh the Pages settings screen. You'll see a green box: *"Your site is live at `https://<username>.github.io/<repo-name>/`"*. Click it to verify the site loads.

---

## 3. Map your GoDaddy domain to GitHub Pages

You'll need two things at the same time: **DNS records at GoDaddy** pointing to GitHub's servers, and **a custom domain setting in the GitHub repo**.

### 3a. Decide: root domain, www, or both?

Say your domain is `example.com`. You have three options:

| Setup | URL users type | What you configure |
|---|---|---|
| Root only | `example.com` | A records at GoDaddy |
| `www` only | `www.example.com` | CNAME record at GoDaddy |
| **Both (recommended)** | either works | A records **and** CNAME |

The recommended setup is both, with GitHub redirecting one to the other.

### 3b. Add DNS records at GoDaddy

1. Log in at <https://godaddy.com>, go to **My Products**, find your domain, click **DNS** (or **Manage DNS**).
2. You'll see a DNS records table. Delete any existing **A records for `@`** that GoDaddy added by default (they point to GoDaddy's parking page).
3. Click **Add** and create these records one at a time:

    **Four A records for the root domain — these are GitHub's fixed IPs:**

    | Type | Name | Value            | TTL       |
    |------|------|------------------|-----------|
    | A    | @    | 185.199.108.153  | 1 Hour    |
    | A    | @    | 185.199.109.153  | 1 Hour    |
    | A    | @    | 185.199.110.153  | 1 Hour    |
    | A    | @    | 185.199.111.153  | 1 Hour    |

    **One CNAME record for `www`:**

    | Type  | Name | Value                       | TTL    |
    |-------|------|-----------------------------|--------|
    | CNAME | www  | `<username>.github.io`      | 1 Hour |

    ⚠️ The CNAME value must end with a dot in some interfaces (e.g. `username.github.io.`). GoDaddy usually adds it automatically.

4. Click **Save**. DNS typically propagates in 10–30 minutes, occasionally up to a few hours.

### 3c. Tell GitHub about the custom domain

1. Back in your GitHub repo, go to **Settings → Pages**.
2. Under **Custom domain**, enter your domain — if you want both `example.com` and `www.example.com`, enter the **apex** (`example.com`) here. Click **Save**.
3. GitHub will add a file called `CNAME` to your repo automatically (just a text file containing your domain).
4. Wait for GitHub to check the DNS. You'll see a green check: *"DNS check successful"*. If you see a yellow warning, it usually just means DNS hasn't propagated yet — wait 10 minutes and click **Check again**.
5. Once the check passes, tick the **Enforce HTTPS** box. GitHub will issue a free Let's Encrypt SSL certificate automatically (this takes another 5–15 minutes).

### 3d. Verify

Open a fresh browser tab (or a private window) and try all four:

- `http://example.com` → should redirect to `https://example.com` ✓
- `https://example.com` → should load the site ✓
- `http://www.example.com` → should redirect ✓
- `https://www.example.com` → should load (or redirect to the apex) ✓

If any of these still show a GoDaddy parking page, you probably missed deleting an old A record in step 3b-2. Go back and check.

### 3e. Troubleshooting

- **"DNS check unsuccessful" in GitHub Pages settings** — wait 15 minutes and click *Check again*. If it still fails, run `dig example.com +short` (or use <https://dnschecker.org>) and confirm you see the four `185.199.x.153` IPs. If not, your A records haven't saved or propagated.
- **HTTPS checkbox is greyed out** — GitHub is still provisioning the certificate. Wait up to 1 hour.
- **Site works at `github.io` URL but not custom domain** — the `CNAME` file in your repo must contain exactly your domain (no `https://`, no trailing slash). Check its contents in the repo.
- **Subsequent pushes remove the custom domain** — make sure you don't delete the `CNAME` file GitHub created. It should stay committed in the repo root.

---

## What to change next

- Replace the Unsplash image URLs in `index.html` with your own product screenshots.
- Update the email addresses (`careers@`, `support@`, `hello@`, etc.) from `hrassist.example` to your real domain.
- Update the office address in `contact.html`.
- Customize copy on `story.html`, `careers.html`, and `changelog.html` to match your real situation.
- Review the legal pages (`privacy.html`, `terms.html`, `security.html`, `dpa.html`) with a lawyer before publishing — the current text is a reasonable starting draft, not legal advice.
