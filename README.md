# BridgeNurse — Vercel-ready Next.js Website

This is the root-level deployment package for the BridgeNurse Warm Editorial Storybook website.

## Important: what was fixed

The earlier ZIP nested the Next.js project inside `bridgenurse-storybook/`. This package has `package.json`, `app/`, `components/`, `public/`, and `vercel.json` **at the ZIP root**. On GitHub, upload the unzipped **contents** into your repository root; do not upload this ZIP as a file in the repository.

## Deploy on Vercel using GitHub

1. Extract the ZIP. Upload **all files and folders inside** it to the **root of the GitHub repository**.
2. In Vercel, choose **Add New > Project** and import the GitHub repository.
3. In Project Settings > Build and Deployment (or General, depending on dashboard version), use:
   - **Framework Preset**: `Next.js`
   - **Root Directory**: `./` (repository root; no nested folder)
   - **Build Command**: default (`npm run build` / `next build`)
   - **Output Directory**: default for Next.js (**do not override** it to `public`, `out`, or `.next`)
   - **Install Command**: default (`npm install`)
   - **Node.js**: 22.x (or another currently supported version compatible with this project)
4. Save, then **redeploy** with the updated repository. Check that Build Logs list routes `/` and `/about`.
5. Open the deployment's *actual* `.vercel.app` URL from the Vercel project's Domains or Deployment page.

If you already uploaded the **previous** ZIP contents into a GitHub repository under `bridgenurse-storybook/`, instead of reuploading you can set Vercel's **Root Directory** to `bridgenurse-storybook`, select **Next.js** and redeploy. The two approaches are alternatives; do not nest this new package again.

## Deploy with Vercel CLI

In this extracted directory:

```bash
npm install
npm run build
npx vercel --prod
```

If the build fails, inspect the logs and resolve the build error before opening the deployment. A 404 after a successful deployment may be caused by the wrong domain, wrong project root, or Output Directory overrides.

## Waitlist configuration

This site has a working Next.js POST route `/api/waitlist` that requires `WAITLIST_WEBHOOK_URL` configured in Vercel environment variables. Until connected, the site can display the form but **will not save submissions**; it displays an unavailable-state error. The URL must be HTTPS. Optionally configure `WAITLIST_WEBHOOK_TOKEN` for a bearer token. See `.env.example`. Do not put secrets in `NEXT_PUBLIC_` variables.

## Contents

- `app/page.jsx`: Homepage (`/`)
- `app/about/page.jsx`: About page (`/about`)
- `app/api/waitlist/route.js`: Waitlist API
- `components/StoryUI.jsx`: Interactive website UI
- `content/sourceTranslations.json`: English/Hindi/Bengali/Tamil/Indonesian content
- `app/globals.css`: Responsive design system
- `public/illustrations/`: Original SVG illustration assets

Fonts load through `next/font/google` during the server build; Vercel needs to be able to download them during installation/build. No font files are included in this package.
