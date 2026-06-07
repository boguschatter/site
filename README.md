# bogusch@tter — setup guide

From downloaded files to live at boguschatter.com. Top to bottom, no skipping steps.

---

## step 1 — set up your folder

After downloading, you'll have a folder that looks like this:

```
boguschatter/
├── index.html
└── README.md
```

Create an `images` folder inside it so it becomes:

```
boguschatter/
├── index.html
├── README.md
└── images/
```

---

## step 2 — add your photos

Drop your work photos into the `images/` folder. A few rules:

- **No spaces in filenames.** Use hyphens or underscores instead.
  `beer-box-face.jpg` ✓ — `beer box face.jpg` ✗
- JPG or PNG both work. JPG is smaller/faster for photos.
- Shoot or crop square if you can — the gallery tiles are square. Non-square images will be cropped to fit but nothing gets distorted.

---

## step 3 — add your works to the site

Open `index.html` in a text editor. VS Code is free and good — download at code.visualstudio.com if you don't have one.

Search for this line (Cmd+F on Mac, Ctrl+F on Windows):

```
const works = [
```

You'll see placeholder entries below it. Delete those and replace them with your actual works, one block per piece. Copy this template for each one:

```js
{
  id: "2025-01",
  title: "beer box face",
  file: "images/2025-01-beer-box-face.jpg",
  medium: "house paint, sharpie on beer box",
  year: 2025,
  dims: '12" x 9"',
  available: true,
  price: "$200",
  desc: "Whatever you want to say about this one."
},
```

Notes:
- `id` — use `"YYYY-NN"` format (year + count within that year). It's just a label, but it keeps things readable and self-organizing
- `file` — must match the exact filename in your `images/` folder. Use the same `YYYY-NN-title.jpg` convention there too
- `available` — `true` if for sale, `false` if sold
- `price` — `"$200"` or `"inquire"` or `"sold"`
- **Newest work always goes at the TOP of the list** — array order = gallery order, full stop
- Don't forget the **comma** after the closing `}` on each entry (except the very last one)

Save the file when done.

---

## step 4 — put it on GitHub

You already have a GitHub account — good.

### create the repo

1. Go to github.com and log in
2. Click the **+** in the top right → **New repository**
3. Name it `boguschatter`
4. Set it to **Public**
5. Leave everything else unchecked — no README, no .gitignore
6. Click **Create repository**

### upload your files

On the repo page, click **uploading an existing file**.

Drag your entire folder contents into the upload area — `index.html`, `README.md`, and your whole `images/` folder. GitHub lets you drag a folder straight in.

Write a commit message like `initial upload` and click **Commit changes**.

---

## step 5 — turn on GitHub Pages

1. In your repo, click **Settings** (top tab bar)
2. Click **Pages** in the left sidebar
3. Under **Source**, select **Deploy from a branch**
4. Set branch to `main`, folder to `/ (root)`
5. Click **Save**

GitHub builds your site in about 60 seconds. A URL will appear at the top of the Pages settings:

```
https://yourusername.github.io/boguschatter
```

Open it. Your site is live.

---

## step 6 — connect boguschatter.com

Done in two places: GitHub and your domain registrar (Namecheap, GoDaddy, wherever you bought it).

### in GitHub

1. Go to **Settings → Pages**
2. Find the **Custom domain** field, type `boguschatter.com`, click **Save**
3. Check **Enforce HTTPS** once it appears (may take a few minutes)

### in your domain registrar's DNS settings

Add these records (values are the same everywhere — exact steps vary by registrar):

**4 A records for the root domain:**

| Type | Host | Value |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

**1 CNAME record for www:**

| Type | Host | Value |
|------|------|-------|
| CNAME | www | yourusername.github.io |

DNS propagation takes anywhere from a few minutes to 24 hours. Once done, boguschatter.com loads your site with free HTTPS.

---

## adding new work later

1. Drop the new photo in `images/`
2. Open `index.html`, find `const works = [`
3. Paste a new entry block at the **top** of the list
4. Save
5. Go to your GitHub repo → click `index.html` → click the pencil (edit) icon → paste your changes → commit

That's it. No terminal required.

---

## marking a piece as sold

Find its entry and change:
```js
available: true,
price: "$200",
```
to:
```js
available: false,
price: "sold",
```
Sold pieces stay in the gallery as archive.

---

## making the contact form actually send emails (optional, later)

Right now the form shows a confirmation but doesn't email you. Easiest fix:

1. Go to formspree.io, sign up free (50 messages/month on free tier)
2. Create a form, get your endpoint URL
3. It's a 4-line code swap — come back here and ask when you're ready

---

## that's it.

One HTML file. One images folder. No framework, no monthly fee, no algorithm.
