# Glassmorphic Rich Text Editor

A rich text editor wrapped in a modern **glassmorphism** UI — frosted-glass panels, floating
gradient orbs, and a dark, cinematic background — built with Next.js, React, and Tailwind CSS.

## What it does

A browser-based WYSIWYG rich text editor. Type directly into the glass panel and format text
with the floating toolbar: headings, bold, italic, underline, lists, and links — with live
active-format highlighting and keyboard shortcuts.

## Features

- **Rich text editing** — `contentEditable` surface with live toolbar state (bold / italic /
  underline / lists highlight when active)
- **Formatting toolbar** — Headings H1–H3, bold, italic, underline, bullet list, ordered list,
  and link insertion
- **Keyboard shortcuts** — Ctrl/Cmd + B (bold), Ctrl/Cmd + I (italic), Ctrl/Cmd + U (underline)
- **Glassmorphism UI** — frosted-glass editor panel over animated floating gradient orbs
  (purple, blue, pink) with a subtle noise texture and gradient mesh
- **Dark / light theme toggle** — via `next-themes`, persisted across visits
- **Fully responsive** — works on desktop and mobile screens

## Tech stack

- **Next.js 15** (App Router) + **React 19** + **TypeScript**
- **Tailwind CSS v4** (`@tailwindcss/postcss`) with `tailwindcss-animate`
- **Radix UI** primitives (`@radix-ui/*`) via shadcn/ui-style `components/ui`
- **next-themes** for theme switching
- **lucide-react** icons
- Editing engine: native `document.execCommand` API on a `contentEditable` div

## Quick start

```bash
# Install dependencies (npm or pnpm)
npm install

# Run the dev server
npm run dev

# Open http://localhost:3000
```

## Build

```bash
npm run build
npm start
```

## Project structure

```
glassmorphic-rich-text-editor/
├── app/
│   ├── layout.tsx          # Root layout + ThemeProvider
│   ├── page.tsx            # Home page → renders RichTextEditor
│   └── globals.css         # Tailwind + theme tokens
├── components/
│   ├── rich-text-editor.tsx # Editor + toolbar (contentEditable)
│   ├── theme-provider.tsx   # next-themes wrapper
│   └── ui/
│       ├── button.tsx
│       └── separator.tsx
├── lib/
│   └── utils.ts             # cn() class helper
├── public/                  # Static assets
├── next.config.mjs
├── components.json          # shadcn/ui config
└── tsconfig.json
```

## Environment variables

None — the app is fully client-side and needs no secrets or API keys.

## Deployment

The app has no API routes, server actions, or server-side data fetching, so it can be
**statically exported** and hosted anywhere static files work (GitHub Pages, Cloudflare
Pages, Netlify, Vercel).

Static export is enabled in `next.config.mjs` via `output: "export"` with
`basePath: "/glassmorphic-rich-text-editor"` for the GitHub Pages subpath.

Live demo: https://girishlade111.github.io/glassmorphic-rich-text-editor/

> Note: `basePath` is only needed for the GitHub Pages subpath. If you deploy to a root
> domain (e.g. on Vercel or Cloudflare Pages), remove the `basePath` line from
> `next.config.mjs` and rebuild.

## How it works

The editor uses the browser's native `document.execCommand` API on a `contentEditable`
element. On every keystroke/selection change it re-reads `document.queryCommandState`
for each format and stores the active set in React state, so toolbar buttons highlight
correctly as the caret moves.

---

Built by Girish Lade · https://ladestack.in
