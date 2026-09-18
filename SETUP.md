# Setup — Cannabis & Veterinary Reference (prototype app)

This repo has two parts:
1. **`index.html`** — a single-page lookup app (species → condition → studied dose range, evidence tier, source). No build step, no dependencies beyond two Google Fonts loaded from CDN.
2. **The markdown knowledge base** (`README.md`, `01`–`07` `.md` files) — the underlying literature review the app's data was drawn from. `data/conditions.json` and `data/app-data.json` are the machine-readable versions; `app-data.json` is what the app actually reads.

## Option A — Host it on GitHub Pages (recommended for a clinic demo)

1. Create a new GitHub repository (public or private — Pages works on both, private requires GitHub Pro/Team/Enterprise for Pages).
2. Unzip this archive and push its contents to the repo root:
   ```bash
   git init
   git add .
   git commit -m "Cannabis & veterinary reference prototype"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```
3. On GitHub: **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main` / `(root)` → Save.**
4. GitHub will give you a URL like `https://<your-username>.github.io/<your-repo>/` within a minute or two. Open it — the app fetches `data/app-data.json` over HTTPS, which works fine on Pages.

No further configuration needed. Any time you edit `data/app-data.json` and push, the live site updates automatically (usually within ~1 minute).

## Option B — Run it locally before pushing

Because the app loads its data with `fetch('data/app-data.json')`, opening `index.html` directly from disk (double-clicking it) will fail in most browsers — they block `fetch` on the `file://` protocol. Run a tiny local server instead:

```bash
cd cannabis-vet-kb
python3 -m http.server 8000
# then open http://localhost:8000 in your browser
```

or, with Node installed:

```bash
npx serve .
```

## Editing the data

- Edit `data/app-data.json` to add/change species, conditions, dose ranges, evidence tiers, or reference-page text (Legal & Regulatory / THC Toxicity). The app re-reads this file on every load — no rebuild step.
- `data/conditions.json` is kept as the original flat data export referenced from the markdown knowledge base; it isn't read by the app itself. If you want a single source of truth, you can delete it and point anything referencing it at `app-data.json` instead, or keep both in sync manually.
- Evidence tiers are defined once in `app-data.json` under `meta.tiers` (`A`–`D`, plus `R` for regulatory-status entries) and rendered automatically as the legend at the bottom of every condition view.

## Before showing this to a clinic

- This is a **prototype**: the dosing data reflects what's in the published literature as of September 2026, not a maintained formulary. Treat any specific number as a starting point for a conversation with the vet, not an answer to hand a client.
- Read `01-legal-regulatory.md` before any live demo involving state-specific claims — several state veterinary boards differ on what a vet may legally recommend.
- The Livestock/Food Animals tab intentionally shows no dose — that's correct, not a bug. No cannabinoid ingredient is currently approved for food-producing animals in the US.

## Repo structure

```
cannabis-vet-kb/
├── index.html                     # the app (search, per-species lookup, Cancer/Oncology, dose calculator)
├── data/
│   ├── app-data.json              # data the app reads (species, oncology topic, reference pages, source links, calc fields)
│   └── conditions.json            # original flat data export (reference only, not read by the app)
├── README.md                      # knowledge-base index (this is a *different* README — see note below)
├── SETUP.md                       # this file
├── 01-legal-regulatory.md         # Costa Rica (Ley 10113, SENASA, CPMVCR) first; US federal status as background
├── 02-canine.md
├── 03-feline.md
├── 04-equine.md
├── 05-livestock-food-animals.md
├── 06-toxicity-emergency.md
├── 08-oncology.md                 # cancer/oncology — clearly separates the one real trial from preclinical findings
└── 07-sources.md
```

> Note: GitHub renders `README.md` on the repo's front page by default. If you'd rather the repo landing page describe the *app* instead of the knowledge base, rename the current `README.md` to something like `KNOWLEDGE-BASE.md` and rename this `SETUP.md` to `README.md`.
