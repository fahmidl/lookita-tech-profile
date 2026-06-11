# Lookita Tech - Company Profile

Landing page & company profile untuk **profile.lookita.tech**, dibangun dengan Astro + Tailwind CSS dan di-deploy di Cloudflare Pages.

## Tech Stack

- **Framework:** Astro 5
- **Styling:** Tailwind CSS 3
- **Adapter:** @astrojs/cloudflare
- **Font:** Inter (via @fontsource)

## Development

```bash
npm install
npm run dev
```

Buka `http://localhost:4321` di browser.

## Build

```bash
npm run build
```

Output ada di folder `dist/`.

## Deploy ke Cloudflare Pages

### Via Cloudflare Dashboard
1. Push repo ke GitHub
2. Di Cloudflare Dashboard → Pages → Create a project
3. Connect GitHub repo
4. Build settings:
   - **Build command:** `npm run build`
   - **Build output directory:** `dist`
5. Set custom domain: `profile.lookita.tech`

### Via Wrangler CLI
```bash
npx wrangler pages deploy dist --project-name=lookita-tech-profile
```

## Struktur Halaman

| Section | Deskripsi |
|---------|-----------|
| Hero | Headline utama + stats |
| About | Company profile + visual |
| Services | 4 layanan utama |
| Why Choose Us | 6 keunggulan |
| Blog | Preview artikel terbaru |
| Contact | Form kontak + info |
| Footer | Links + social media |
