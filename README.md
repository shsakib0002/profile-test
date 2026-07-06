# Md. Sakib Hasan — Portfolio

A premium, enterprise-style personal portfolio built with Next.js 14, TypeScript, Tailwind CSS, and Framer Motion — designed for applications to AWS, Microsoft, Cisco, Huawei, Nokia, Ericsson, Oracle, and similar companies.

## Tech stack

- Next.js 14 (App Router) + TypeScript
- Tailwind CSS v3
- Framer Motion
- next-themes (dark/light mode, dark by default)
- IBM Plex Sans & IBM Plex Mono — self-hosted via `@fontsource`, zero external font requests
- lucide-react icons

## Getting started

```bash
npm install
npm run dev
```

Open http://localhost:3000.

## Editing content

Everything on the page — name, role, bio, experience, skills, certifications, projects, education, timeline, and stats — comes from **`lib/data.ts`**. Edit that one file and the whole site updates.

A few things still need your input (marked `TODO` in that file):

- `siteConfig.url` — your deployed domain, once you have one
- `siteConfig.github` / `githubUsername` — wasn't listed on your CV; add it to light up the GitHub Activity section with your real repo/follower counts and contribution graph
- Certification `credentialUrl` fields — add your Credly / Huawei / Red Hat verification links if you have them and the "Verify credential" link will appear automatically (it's hidden when the field is empty, so nothing looks broken in the meantime)

## Résumé

`public/resume.pdf` is already your real CV, so the "Download Résumé" buttons work right now. Replace that file whenever you update your CV — keep the filename `resume.pdf`, or update `siteConfig.resumeUrl` in `lib/data.ts` if you rename it.

## Notable implementation details

- **GitHub Activity** fetches your public GitHub stats server-side (revalidated hourly) and embeds a live contribution graph — no API key needed. Falls back gracefully to zeros if the username isn't set yet or the API is unreachable, so it never breaks the build.
- **Contact form** is UI-only (validates input and shows a success state) — wire the `handleSubmit` function in `components/sections/resume-contact.tsx` to a service like Formspree, Resend, or your own API route before relying on it to receive real messages.
- **LinkedIn** doesn't have a public embeddable activity widget, so it's surfaced as a direct link in Contact and the footer rather than a fake embed.
- `prefers-reduced-motion` is respected throughout (network graphic, scroll reveals, hero entrance).
- Full SEO pass: metadata API, Open Graph/Twitter cards, `sitemap.ts`, `robots.ts`, and JSON-LD `Person` structured data in the layout.

## Deployment

**Vercel** (zero config):
```bash
npx vercel
```

**Netlify**: connect the repo in the Netlify dashboard — it auto-detects Next.js via its official Next.js runtime — or run `netlify init` from this folder.

## Project structure

```
app/                    routes, root layout, metadata, sitemap, robots
components/
  sections/             one file per homepage section
  ui.tsx                shared Button / Card / Badge / SectionHeading / StatusDot / AnimatedCounter
  navbar.tsx, footer.tsx, theme-provider.tsx
lib/
  data.ts               ← all real content lives here — start here
  motion.ts             shared Framer Motion variants
  utils.ts
public/
  resume.pdf            your real CV
```
