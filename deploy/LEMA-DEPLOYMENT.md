# LEMA's Platter deployment

LEMA runs its own copy of Platter on Fly.io. Platter's repository is generic: the LEMA names and settings below live only here and in the repository's GitHub variables. No secrets are written here; they stay in Fly secrets and GitHub secrets.

## Sites

| Site | Fly app | Address | Deploys from |
|---|---|---|---|
| Production | `lema-platter` | `https://lema.platter.studio` | `main` (approved releases only) |
| Staging | `platter-dev` | `https://dev.platter.studio` | `dev_2` |

Database: Fly Managed Postgres cluster `lema-platter-db` (production database, plus `platter_staging` for staging).

## GitHub repository variables (Settings › Secrets and variables › Actions › Variables)

Platter's deploy workflows read these instead of naming LEMA in the code:

| Variable | LEMA value | Used by |
|---|---|---|
| `FLY_PRODUCTION_APP` | `lema-platter` | Deploy to Fly.io (pushes to `main`) |
| `PRODUCTION_HOST` | `lema.platter.studio` | Deploy to Fly.io (certificate, `PUBLIC_URL`) |
| `FLY_STAGING_APP` | `platter-dev` | Deploy to Fly.io (pushes to `dev_2`), Fly staging setup |
| `STAGING_HOST` | `dev.platter.studio` | Deploy to Fly.io |
| `FLY_DB_CLUSTER` | `lema-platter-db` | Fly staging setup |
| `STAGING_ADMIN_EMAIL` | the staging admin's email | Fly staging setup |

Secrets stay as they are: `FLY_API_TOKEN` (production), `FLY_STAGING` (staging), `CLOUDFLARE_API_TOKEN`.

## Fly secrets on `lema-platter` (and `platter-dev` if staging should look like LEMA)

| Secret | Value | Why |
|---|---|---|
| `PLATTER_THEME_REPO` | `https://github.com/LEMACONnect/lema-platter-theme` | installs this theme at start-up when it isn't installed yet |
| `THEME_GITHUB_TOKEN` | a fine-grained GitHub token, contents: read, on this repository | the repository is private |
| `PLATTER_BRAND` | `lema` | pins the site to the LEMA theme (leave unset on staging so Settings › Look can switch) |

```bash
fly secrets set --app lema-platter PLATTER_THEME_REPO=https://github.com/LEMACONnect/lema-platter-theme THEME_GITHUB_TOKEN=<token> PLATTER_BRAND=lema
```

## In the app (an admin, once per site)

- Settings › Contracts › **Contractor**: LEMA Construction's legal name, address, licence (CGC1523064), phone, signer and title. Contracts, letters of intent, pay applications, the closeout binder and the bidder and billing pages take the company name from here.
- Settings › Look: on staging, Install from GitHub (link above), then **Use for everyone**.
- Procore: `PROCORE_COMPANY_ID` is LEMA's Procore company id (a Fly secret).

## Releasing the generic Platter to production

Platter stopped shipping `brands/lema` in the image. Before the first release that has this change reaches `main`:

1. Set the GitHub variables above.
2. Set the Fly secrets above on `lema-platter`.
3. Merge the release; on start-up the site installs this theme from GitHub and keeps the LEMA look.
