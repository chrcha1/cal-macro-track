# cal-macro-track

Personal nutrition + workout tracker. Data lives in `data/` as JSON. The dashboard (`dashboard.html`) loads it and renders a protein-first, meal-grouped view with a calendar to navigate historical days.

## File layout

```
cal-macro-track/
├── dashboard.html           # the page you bookmark
├── data/
│   ├── profile.json         # bio + goals
│   ├── log.json             # daily food + workouts
│   └── weight_history.json  # weight over time
├── images/                  # optional local food photos
└── README.md
```

## How to use

**Logging**: in Claude / Cowork, tell Claude what you ate. Claude writes to `data/log.json`, commits, pushes. The site auto-updates within ~30 seconds.

**Viewing**: open `dashboard.html` directly from your Mac OR open the hosted URL on any device (phone included) once Pages is set up.

## First-time hosting setup (GitHub Pages)

Run these in the folder. Only needs to be done once.

```bash
cd ~/Documents/Claude/Projects/cal-macro-track

# 1. Install GitHub CLI if you don't have it
brew install gh

# 2. Authenticate to your account (chrcha1)
gh auth login

# 3. Create the repo on GitHub and push
gh repo create cal-macro-track --public --source=. --push

# 4. Enable GitHub Pages from the main branch root
gh api -X POST "repos/chrcha1/cal-macro-track/pages" \
  -f "source[branch]=main" \
  -f "source[path]=/"
```

Once Pages is enabled (takes a minute), your site is live at:

**https://chrcha1.github.io/cal-macro-track/**

Bookmark that URL on your iPhone (Safari → Share → Add to Home Screen for an app-like icon).

## How subsequent updates flow

Every time Claude logs new food / workouts / weight:

```bash
cd ~/Documents/Claude/Projects/cal-macro-track
git add . && git commit -m "log update" && git push
```

Done. Pages redeploys automatically. Refresh your bookmark.

## Notes

- **Protein zones** are bodyweight-based (0.6 / 0.9 g/lb thresholds), no hard cap.
- **Carbs and fat** are tracked but have no target — raw numbers only.
- **Estimation bias**: overestimate intake slightly, underestimate burn (stay safely inside deficit).
- **Food photos** use `loremflickr.com` with keyword matches (real photos, stable URLs). Swap in specific URLs or drop files into `images/` and update `image_url` in `data/log.json`.
