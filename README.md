# Image Ranker — ELO Voting Site

A simple website where visitors compare two images side-by-side and pick their favorite.
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

## Notes

- **Each visitor has their own independent ratings** stored in their browser. This is a personal ranking tool, not a shared leaderboard.
- If you want a **shared, multi-user leaderboard**, you'd need a small backend (e.g. Supabase, Firebase, or a simple serverless function). Let me know if you want to extend it that way.
- To reset your own comparisons, click the **"Reset all comparisons"** button at the bottom of the page.

