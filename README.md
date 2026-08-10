# Otto Fly — putting the site live

Two accounts only: **GitHub** (holds the code and serves the site) and
**Afrihost** (holds the domain and the email). Nothing else, nothing monthly.

---

## What's in this folder

| File | What it is |
|---|---|
| `index.html` | The whole website — home, work and contact |
| `media/` | The four case-study videos and their poster images |
| `og-image.png` | The picture that appears when the link is shared on WhatsApp |
| `favicon.svg`, `favicon-32.png`, `apple-touch-icon.png` | The little icon in the browser tab |
| `CNAME` | Tells GitHub the site answers to ottofly.co.za — **do not delete** |
| `.nojekyll` | Stops GitHub reprocessing the files — **do not delete** |

Upload **everything**, including the two files starting with a dot.

---

## Step 1 — Make a GitHub account

Go to github.com and sign up. Free plan. Use an email you'll keep access to.

## Step 2 — Create the repository

1. Click the **+** top right → **New repository**
2. Name it `ottofly-site`
3. Set it to **Public**
4. Leave every checkbox alone
5. **Create repository**

> **Why public?** GitHub only serves websites from public repositories on the
> free plan. This costs you nothing in privacy — a website's code is already
> visible to anyone who visits it. No passwords or client data live in here.

## Step 3 — Upload the files

1. On the empty repository page click **uploading an existing file**
2. Drag in everything from this folder, including the `media` folder
3. At the bottom click **Commit changes**

Uploading takes a minute or two — the videos are about 4 MB in total.

## Step 4 — Switch the website on

1. In the repository click **Settings** (top right)
2. Left sidebar → **Pages**
3. Under *Source* choose **Deploy from a branch**
4. Branch: **main**, folder: **/ (root)** → **Save**

Wait two or three minutes, then reload. GitHub shows a link like
`https://yourname.github.io/ottofly-site/`. **Open it and check the site works.**
Do not go further until it does.

## Step 5 — Tell GitHub about the domain

Still in **Settings → Pages**, under *Custom domain*, enter:

```
ottofly.co.za
```

Click **Save**. It will complain that DNS isn't configured. That's expected —
that's the next step.

## Step 6 — Point the domain at GitHub, in Afrihost

Log in to **Afrihost ClientZone**, find `ottofly.co.za`, and open its
**DNS / zone editor**.

**⚠️ Before you touch anything, photograph or copy the whole existing record
list.** If there are `MX` records there, they run your email. Leave every MX
and TXT record exactly as it is. You are only adding A and CNAME records.

Add **four A records** on the root (the host field is usually `@` or blank):

| Type | Host | Points to |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

Then **one CNAME** for www:

| Type | Host | Points to |
|---|---|---|
| CNAME | www | `yourname.github.io` |

Replace `yourname` with your actual GitHub username. Keep the dot on the end if
Afrihost's form adds one.

If an existing A record or a "parking" record already sits on `@`, delete that
one first — it's Afrihost's holding page and it will fight with these.

## Step 7 — Wait, then lock it down

DNS usually settles in 15–60 minutes, occasionally up to 24 hours.

Go back to **Settings → Pages**. Once the green tick appears next to the domain,
tick **Enforce HTTPS**. That gives you the padlock, free, automatically.

Then open **https://ottofly.co.za** and check:

- [ ] Home page loads and the OTTO mark draws itself in the sky
- [ ] Work page plays all four videos
- [ ] Contact form opens your mail app when submitted
- [ ] Padlock showing in the address bar
- [ ] `www.ottofly.co.za` also works

---

## Making changes later

Open the repository, click the file, click the pencil icon, edit, then
**Commit changes**. The live site updates in about a minute.

To replace a video: go into `media/`, use **Add file → Upload files**, and give
the new file the same name as the old one.

---

## About the contact form

GitHub Pages serves files but cannot run code, so the form cannot email anyone
by itself. Instead, when someone submits it, their own mail app opens with every
answer already filled in and addressed to `jean@ottofly.co.za`. They press send.

It works, it costs nothing, and it needs no third service. The trade-off is that
a visitor without a mail app set up will fall back to the phone, email and
WhatsApp links shown beside the form.

If you'd rather enquiries arrive silently without the visitor pressing send in
their own mail app, that needs either a form service or Afrihost shared hosting
with PHP. Say the word and it's a small change.

---

## Email

Your email is not affected by any of this, **provided you left the MX records
alone in Step 6**. If mail stops arriving, an MX record was deleted — restore it
from the copy you made and it will come back.
