# Valentine's Day Interactive Website — Plan

## Overview
Build a playful, romantic Valentine-themed single-page interactive website using **Nuxt 3** (Vue 3, Composition API) + **TailwindCSS**. The site reads a `name` from the URL query (`/love?name=Anisha`) and delivers a storytelling love card experience with animations.

---

## Todo Items

- [x] **1. Scaffold Nuxt 3 project** — `npx nuxi init`, install dependencies (tailwindcss, @nuxtjs/tailwindcss)
- [x] **2. Configure TailwindCSS** — tailwind.config, add romantic color palette (pink/red/warm gradients)
- [x] **3. Create `pages/love.vue`** — reads `name` from `useRoute().query`, passes to child components
- [x] **4. Create `components/HeroLove.vue`** — hero section with "For {{name}}" heading, subtitle, animated hearts background
- [x] **5. Create `components/LoveQuote.vue`** — random romantic quote from predefined array on each load
- [x] **6. Create `components/LoveStory.vue`** — step-by-step timeline (First Meet → Memories → Today → Forever) with scroll animations
- [x] **7. Create `components/LoveMessage.vue`** — personal emotional paragraph with typing animation
- [x] **8. Create `components/LoveButton.vue`** — "Click if you love me ❤️" button, hearts burst + "I love you {{name}} forever" on click
- [x] **9. Add floating hearts background animation** — continuous random floating hearts via CSS
- [x] **10. Add background music toggle** — Play/Pause button for soft romantic music
- [x] **11. Global layout & styling polish** — smooth scroll, mobile-first responsive, micro-interactions (hover, sparkles, glowing)
- [x] **12. Test & verify** — run dev server, confirm all sections work with `?name=` param
- [x] **13. Write review summary** — add review section to this file

---

## Architecture

```
f14/
├── nuxt.config.ts
├── tailwind.config.ts
├── pages/
│   └── love.vue
├── components/
│   ├── HeroLove.vue
│   ├── LoveQuote.vue
│   ├── LoveStory.vue
│   ├── LoveMessage.vue
│   └── LoveButton.vue
├── public/
│   └── music.mp3  (placeholder or external link)
├── assets/
│   └── css/
│       └── main.css  (global animations)
└── tasks/
    └── todo.md
```

## Key Decisions
- **No extra animation libraries** — pure CSS animations + Vue transitions keep it simple and dependency-light
- **TailwindCSS** for all styling — romantic color palette via `extend.colors`
- **Single page (`/love`)** — all 5 components stacked vertically with smooth scroll
- **Music** — use a free royalty-free romantic music URL or placeholder

---

## Review

### Summary of Changes

All 13 tasks completed successfully. The project is a fully functional Nuxt 3 Valentine's Day website.

### Files Created

| File | Purpose |
|------|---------|
| `package.json` | Nuxt 3 + TailwindCSS dependencies |
| `nuxt.config.ts` | Nuxt config with TailwindCSS module, Google Fonts, global CSS |
| `tailwind.config.ts` | Romantic color palette (rose, blush, candy, deep) + custom animations |
| `tsconfig.json` | TypeScript config extending Nuxt |
| `app.vue` | Root app with `<NuxtPage />` |
| `assets/css/main.css` | Global CSS — floating hearts keyframes, typing cursor, scroll reveal, sparkle effects, music button, timeline line |
| `pages/index.vue` | Redirects `/` → `/love?name=My Love` |
| `pages/love.vue` | Main page — reads `?name=` query param, renders all 5 sections |
| `components/HeroLove.vue` | Hero section — "For {{name}} ❤️" with floating decorative hearts |
| `components/LoveQuote.vue` | Random romantic quote (8 quotes) with scroll-reveal animation |
| `components/LoveStory.vue` | 4-step timeline (First Meet → Memories → Today → Forever) with IntersectionObserver scroll animations |
| `components/LoveMessage.vue` | Personal emotional message with character-by-character typing animation |
| `components/LoveButton.vue` | "Click if you love me ❤️" button with heart burst particles + reveal message |
| `components/FloatingHearts.vue` | Continuous random floating hearts background (spawns every 2s) |
| `components/MusicToggle.vue` | Fixed play/pause music button (bottom-right corner) |

### Key Design Decisions

1. **Zero extra animation libraries** — all animations are pure CSS + Vue reactivity (IntersectionObserver for scroll reveals, setInterval for typing)
2. **Minimal dependencies** — only `nuxt`, `vue`, `vue-router`, `@nuxtjs/tailwindcss`
3. **SSR-compatible** — all components work with server-side rendering
4. **Mobile-first** — responsive breakpoints (sm/md) with mobile fallbacks for timeline
5. **Music via CDN** — uses a Pixabay royalty-free track, no local file needed

### How to Run

```bash
cd f14
npm install
npm run dev
```

Then open: `http://localhost:3000/love?name=Anisha`
