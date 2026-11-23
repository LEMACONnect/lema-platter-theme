# LEMA Platter theme

The LEMA Construction look for [Platter](https://platter.studio): a theme package in Platter's `platter-brand/1` format. Platter itself ships with no LEMA content; this repository is where everything LEMA lives (the theme, logos, fonts and the notes for LEMA's own deployment).

For now this is the `theme/lema` branch of the Platter repository; it is laid out as a repository of its own so it can move to one without changes.

## Install it in Platter

Settings › Look › **Install from GitHub**, paste the link, then **Use for everyone**:

- this branch: `https://github.com/LEMACONnect/PLATTER/tree/theme/lema`
- once it has its own repository: `https://github.com/<owner>/<repo>` (or a tag: `…/tree/v1.1.0`)

A private repository needs a GitHub token with read access to its contents: paste it in the same window (it is used for that download only), or set `THEME_GITHUB_TOKEN` on the server so **Update** works later.

A deployment can also install it at start-up: `PLATTER_THEME_REPO=https://github.com/LEMACONnect/PLATTER/tree/theme/lema` with `PLATTER_BRAND=lema` (see `deploy/LEMA-DEPLOYMENT.md`).

You can still upload it as a ZIP (Settings › Look › Install package): zip this folder, or run `npm run brand -- pack` from a Platter checkout with this folder in `brands/lema`.

## What's here

| File | What |
|---|---|
| `brand.json` | the manifest: id `lema`, company, tagline, rail label, footer, contact, file names |
| `theme.css` | colours, fonts, radii and every Platter variable, light (`platter`) and dark (`platter-dark`) |
| `fonts/` | Overpass, Red Hat Text and IBM Plex Mono (SIL Open Font License: `fonts/OFL-Overpass.txt`, `fonts/OFL-Red-Hat-Text.txt`, `fonts/OFL-IBM-Plex.txt`) |
| `logo.svg`, `logo-white.svg`, `mark.svg`, `favicon.svg`, `touch-icon.png` | the LEMA logo, the cube mark and icons |
| `deploy/LEMA-DEPLOYMENT.md` | how LEMA's own Platter deployment is set up |

## Type

Titles are Overpass, bold, slightly tight (−0.01em). Body text is Red Hat Text: 400 for reading, 600 for labels and buttons, 500 at 70–82% for helper text and legends. Tags, eyebrows, figures, codes and job numbers are IBM Plex Mono. All three ship here as files, so every computer shows the same type (Ryan's choice, 2026-11-20, confirmed 2026-11-22).

## Colour

Navy `#0e3a54` for structure (the rail, primary buttons, In lines), sky `#00adef` for what needs a person (with dark navy text on it; white on sky is too faint), charcoal `#35363a` text, periwinkle `#5262a6` for allowances and changes, forest `#1c6f47` for success, gold `#f2a900` as a fill only (its text colour is `#8a5a00`), red `#c0392b` for errors. The cube's four colours make the colour line at the bottom edge of the rail; the top of the rail shows the cube mark with PLATTER under it (Platter PH12-D90).

The design system these values come from is the **LEMA Platter** design system: https://claude.ai/artifact/V8C37QM1JqGLYBPpA9ZGHa (tokens named as Platter's variables, light `platter` and dark `platter-dark`, with the Budget table components). Change values there first, then here.

## Changing it

1. Edit `theme.css` (and `brand.json` if names change). Every variable Platter reads is listed in Platter's `docs/BRANDS.md`.
2. Bump `version` in `brand.json`.
3. Push, then Settings › Look › **Update** on the deployment (or restart it when it installs from `PLATTER_THEME_REPO`).

Text colours here pass 4.5:1 on their backgrounds in both modes; the code-match dots and duration marker pass 3:1.
