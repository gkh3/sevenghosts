# Image Ranker — ELO Voting Site

A simple website where visitors compare two images side-by-side and pick their favourite.
After a minimum number of comparisons, a live leaderboard shows all images ranked by ELO score.

## How it works

- Every image starts with an **ELO rating of 1000**
- Each comparison updates the winner (+) and loser (−) using the standard ELO formula
- The pairing algorithm always surfaces the **least-compared images first**, so coverage is even
- Progress and ratings are saved in the visitor's browser (`localStorage`), so they can return later
- The leaderboard unlocks once a configurable minimum number of comparisons is reached

---

## Setup

### 1. Add your images

Create an `images/` folder next to `index.html` and drop all your photos in:

```
your-repo/
├── index.html
├── README.md
└── images/
    ├── 01.jpg
    ├── 02.jpg
    └── ...
```

Any image format works (`.jpg`, `.png`, `.webp`, `.gif`).

### 2. Edit `index.html` — the CONFIG section

Open `index.html` and find the `CONFIGURATION` block near the top. Edit the `IMAGE_LIST` array to match your files:

```js
const IMAGE_LIST = [
  { id: "img1",  src: "images/01.jpg", label: "Sunset at Hanauma Bay" },
  { id: "img2",  src: "images/02.jpg", label: "Manoa Falls Trail" },
  { id: "img3",  src: "images/03.jpg", label: "Diamond Head" },
  // ... one entry per image
];
```

- **`id`** — unique string, no spaces (used internally)
- **`src`** — path to the image file (relative to `index.html`)
- **`label`** — caption shown under the image

Also adjust these settings if you like:

```js
// Number of comparisons before rankings are revealed
const MIN_COMPARISONS = 60;   // ~1.5× your image count is a good baseline

// ELO sensitivity — higher = ratings shift faster each round
const K_FACTOR = 32;          // 32 is the standard chess default

// Page heading
const PAGE_TITLE = "Which do you prefer?";
```

### 3. Remove the setup notice

Delete or comment out the `<div id="config-notice">` block in `index.html` once you're done configuring.

---

## Deploy to GitHub Pages (free hosting)

1. **Create a new GitHub repository** at https://github.com/new
   - Make it **Public** (required for free GitHub Pages)
   - Give it a name like `image-ranker`

2. **Upload your files**
   - Click **"uploading an existing file"** on the repo page
   - Drag in `index.html` and your entire `images/` folder

3. **Enable GitHub Pages**
   - Go to your repo → **Settings** → **Pages** (left sidebar)
   - Under *Source*, select **Deploy from a branch**
   - Branch: `main` / `(root)` → click **Save**

4. **Share your URL**
   - GitHub will show: `https://YOUR-USERNAME.github.io/image-ranker/`
   - It may take ~1 minute to go live the first time

---

## Notes

- **Each visitor has their own independent ratings** stored in their browser. This is a personal ranking tool, not a shared leaderboard.
- If you want a **shared, multi-user leaderboard**, you'd need a small backend (e.g. Supabase, Firebase, or a simple serverless function). Let me know if you want to extend it that way.
- To reset your own comparisons, click the **"Reset all comparisons"** button at the bottom of the page.

---

## Customisation tips

| What you want | Where to change it |
|---|---|
| Different minimum before rankings show | `MIN_COMPARISONS` in the config |
| Faster/slower ELO changes | `K_FACTOR` — try 16 (slow) or 64 (fast) |
| Page title | `PAGE_TITLE` in the config |
| Accent colour | `--accent` in the CSS `:root` block |
| Image display height | `.card-wrap img { height: ... }` in the CSS |
