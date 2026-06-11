---
name: astro-tailwind-cloudflare
description: Manual scaffolding of Astro + Tailwind CSS + Cloudflare Pages project when create-astro CLI fails or times out
source: auto-skill
extracted_at: '2026-06-11T04:03:35.956Z'
---

# Astro + Tailwind + Cloudflare Pages (Manual Scaffold)

## When to use
- `create-astro` CLI times out or fails (common on WSL, or when directory is not empty)
- Need a quick, reliable setup without interactive CLI prompts
- Deploying a static site to Cloudflare Pages

## Procedure

### 1. Create `package.json`
```json
{
  "name": "project-name",
  "type": "module",
  "version": "1.0.0",
  "scripts": {
    "dev": "astro dev",
    "build": "astro build",
    "preview": "astro preview"
  },
  "dependencies": {
    "astro": "^5.7.10",
    "@astrojs/tailwind": "^6.0.2",
    "@astrojs/cloudflare": "^12.3.1",
    "tailwindcss": "^3.4.17"
  }
}
```

### 2. Create `astro.config.mjs`
```js
import { defineConfig } from 'astro/config';
import tailwind from '@astrojs/tailwind';
import cloudflare from '@astrojs/cloudflare';

export default defineConfig({
  site: 'https://your-domain.com',
  output: 'static',
  adapter: cloudflare(),
  integrations: [tailwind()],
});
```

### 3. Create `tailwind.config.mjs`
```js
/** @type {import('tailwindcss').Config} */
export default {
  content: ['./src/**/*.{astro,html,js,jsx,md,mdx,svelte,ts,tsx,vue}'],
  theme: { extend: {} },
  plugins: [],
};
```

### 4. Create `tsconfig.json`
```json
{
  "extends": "astro/tsconfigs/strict",
  "compilerOptions": {
    "baseUrl": ".",
    "paths": { "@/*": ["src/*"] }
  }
}
```

### 5. Create `wrangler.toml` (for Cloudflare Pages)
```toml
name = "project-name"
compatibility_date = "2025-01-01"
compatibility_flags = ["nodejs_compat"]

[site]
bucket = "./dist"
```

### 6. Create directory structure
```
src/
  layouts/
  components/
  pages/
    index.astro
public/
```

### 7. Install and build
```bash
npm install
npm run build
```

## Troubleshooting

### `create-astro` says directory is not empty
The CLI refuses to scaffold into a non-empty directory (even hidden folders like `.qwen` count). Workaround: manually create all files as shown above.

### `ERR_MODULE_NOT_FOUND: Cannot find module 'shiki/dist/themes.mjs'`
Corrupted `node_modules`. Fix:
```bash
rm -rf node_modules package-lock.json
npm install
```

### npm install times out on WSL
Common on Windows/WSL with large dependency trees. Retry with longer timeout or use `npm install --prefer-offline` if cache is available.

## Cloudflare Pages Deployment

**Via Dashboard:**
1. Push to GitHub
2. Cloudflare Dashboard → Pages → Create project → Connect repo
3. Build command: `npm run build`
4. Build output directory: `dist`

**Via CLI:**
```bash
npx wrangler pages deploy dist --project-name=project-name
```
