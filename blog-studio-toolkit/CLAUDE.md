# CLAUDE.md — Blog Studio AI Platform

> Lu automatiquement par Claude Code. Contient le contexte projet, les conventions,
> et les instructions pour assister le developpement.

---

## Projet

**Nom**: Blog Studio
**Type**: SaaS - Plateforme de creation, pilotage et publication de blogs AI-powered
**USP**: Le seul outil qui combine editeur AI + SEO automatique + publication pilote automatique dans une interface unique
**Status**: En developpement actif

---

## Stack Technique

| Couche | Technologie | Version |
|--------|-------------|---------|
| Framework | Next.js (App Router, RSC, Server Actions) | 14+ |
| UI | React + Tailwind CSS + shadcn/ui | 18+ |
| State | Zustand | 4+ |
| Forms | React Hook Form + Zod | - |
| Editeur | Tiptap (ProseMirror) | 2+ |
| API | tRPC (type-safe end-to-end) | 11+ |
| Auth | NextAuth.js v5 (Auth.js) | 5+ |
| DB | PostgreSQL via Supabase | - |
| ORM | Prisma | 5+ |
| Cache | Redis via Upstash | - |
| Storage | Supabase Storage | - |
| Jobs | Inngest | - |
| AI | Claude API (@anthropic-ai/sdk) | - |
| Tests | Vitest + Playwright | - |
| Deploy | Vercel | - |

---

## Architecture

```
blog-studio/
├── CLAUDE.md
├── .claude/commands/           # Slash commands Claude Code
├── src/
│   ├── app/                    # Next.js App Router
│   │   ├── (dashboard)/        # Route group: tableau de bord
│   │   │   ├── articles/       # CRUD articles
│   │   │   ├── editor/[id]/    # Editeur AI par article
│   │   │   ├── seo/            # Dashboard SEO
│   │   │   ├── media/          # Mediatheque
│   │   │   ├── analytics/      # Stats & performance
│   │   │   ├── calendar/       # Calendrier editorial
│   │   │   └── settings/       # Configuration
│   │   ├── (blog)/             # Route group: blog public
│   │   │   ├── [slug]/         # Article dynamique (ISR)
│   │   │   ├── category/[cat]/ # Pages categories
│   │   │   └── tag/[tag]/      # Pages tags
│   │   ├── api/
│   │   │   ├── trpc/[trpc]/    # tRPC handler
│   │   │   ├── ai/             # Endpoints AI (streaming SSE)
│   │   │   └── cron/           # Jobs planifies
│   │   ├── layout.tsx
│   │   └── page.tsx            # Landing / marketing
│   ├── components/
│   │   ├── ui/                 # shadcn/ui (ne pas modifier a la main)
│   │   ├── editor/             # Composants Tiptap
│   │   ├── dashboard/          # Composants dashboard
│   │   ├── seo/                # Composants SEO
│   │   └── blog/               # Composants blog public
│   ├── lib/
│   │   ├── ai/                 # Engine AI
│   │   │   ├── prompts/        # System prompts modulaires
│   │   │   ├── client.ts       # Client Anthropic
│   │   │   ├── streaming.ts    # SSE streaming
│   │   │   └── cache.ts        # Prompt caching strategy
│   │   ├── seo/                # Utilitaires SEO
│   │   ├── db/                 # Prisma client & helpers
│   │   ├── auth/               # Config auth
│   │   ├── utils/              # Utilitaires
│   │   └── validators/         # Schemas Zod
│   ├── server/
│   │   ├── routers/            # tRPC routers
│   │   └── services/           # Business logic
│   ├── hooks/                  # React hooks custom
│   ├── stores/                 # Zustand stores
│   └── types/                  # Types globaux
├── prisma/
│   ├── schema.prisma
│   ├── migrations/
│   └── seed.ts
├── tests/                      # E2E Playwright
├── public/
└── package.json
```

---

## Regles de Code

### TypeScript
- `strict: true`, `noUncheckedIndexedAccess: true` obligatoires
- Jamais de `any` — utiliser `unknown` + type narrowing
- Types Prisma generes = source de verite pour les types DB

### React / Next.js
- Server Components par defaut
- `"use client"` uniquement quand necessaire (state, events, browser APIs)
- Server Actions pour mutations simples
- tRPC pour queries complexes et mutations avec logique
- `loading.tsx` et `error.tsx` dans chaque route group

### Validation
- Zod sur TOUTES les frontieres (input user, API, env vars)
- Meme schema Zod partage entre client (form) et server (tRPC/action)

### AI Engine — Principes Critiques
- **Prompts modulaires**: system prompt (cache) + dynamic context (par requete)
- **Prompt caching**: `cache_control: { type: "ephemeral" }` sur blocs statiques
- **Streaming first**: toujours streamer via SSE, jamais attendre la reponse complete
- **Token budget**: tracker conso par user, limiter par plan (FREE: 50K/mois, PRO: 500K, ENTERPRISE: illimite)
- **Retry backoff**: 429 → wait, 529 → backoff exponentiel (2s, 4s, 8s, 16s)
- **Structured outputs**: JSON mode pour meta SEO, outlines, donnees structurees
- **Modele**: claude-sonnet-4-20250514 par defaut, configurable via env

### SEO Engine
- Score SEO auto calcule a chaque sauvegarde (0-100)
- Checklist SEO dans l'editeur (titre < 60 chars, meta < 160, H1 unique, alt imgs)
- Generation auto: meta description, OG tags, Twitter Cards, JSON-LD
- Sitemap XML dynamique via ISR
- Maillage interne auto base sur categories + tags + similarite semantique
- Canonical URLs sur chaque page

### Securite
- API keys JAMAIS exposees cote client (`ANTHROPIC_API_KEY` = server only)
- Rate limiting Redis sur `/api/ai/*`
- Input sanitization (DOMPurify pour HTML user-generated)
- CSP headers dans next.config
- Zod validation = premiere ligne de defense

---

## Modele de Donnees (Prisma)

### Tables principales
- `User` — id, email, name, role (ADMIN/EDITOR/AUTHOR/VIEWER), plan (FREE/PRO/ENTERPRISE), tokensUsed, tokensLimit
- `Article` — id, title, slug (unique), content (Tiptap JSON), contentHtml, excerpt, status (DRAFT/REVIEW/SCHEDULED/PUBLISHED/ARCHIVED), seoScore, seoData (JSON), aiGenerated, publishedAt
- `Category` — id, name, slug, description, parentId (self-relation pour arborescence)
- `Tag` — id, name, slug, articles (many-to-many)
- `SeoAudit` — id, articleId, score, issues (JSON), suggestions (JSON)
- `AnalyticsEvent` — id, articleId, event, data (JSON), createdAt

### Index critiques
- `Article`: (status, publishedAt), (slug), (categoryId), (authorId)
- `AnalyticsEvent`: (articleId, event), (createdAt)

---

## Feature Flags

```typescript
// src/lib/features.ts
export const FEATURES = {
  AI_GENERATION: true,          // Generation articles AI
  SEO_AUTO_AUDIT: true,         // Audit SEO automatique
  MULTI_LANGUAGE: false,        // Multi-langue (future)
  EDITORIAL_CALENDAR: true,     // Calendrier editorial
  ANALYTICS_DASHBOARD: true,    // Dashboard analytics
  AUTO_INTERNAL_LINKING: true,  // Maillage interne auto
  IMAGE_AI_GENERATION: false,   // Generation images AI (future)
  VOICE_TO_ARTICLE: false,      // Voix vers article (future)
  AUTO_PUBLISH: false,          // Publication auto (future)
  AB_TESTING_TITLES: false,     // A/B test titres (future)
} as const
```

---

## Commandes Dev

```bash
pnpm dev              # Dev server (port 3000)
pnpm build            # Build production
pnpm lint             # ESLint
pnpm typecheck        # tsc --noEmit
pnpm test             # Vitest
pnpm test:e2e         # Playwright
pnpm db:push          # Push schema sans migration
pnpm db:migrate       # Migration Prisma
pnpm db:studio        # GUI Prisma Studio
pnpm db:seed          # Seed data
```

---

## Conventions

### Nommage
- Fichiers: `kebab-case.tsx`
- Composants: `PascalCase`
- Fonctions/variables: `camelCase`
- Types: `PascalCase`
- Constantes: `SCREAMING_SNAKE_CASE`
- Routes API: `/api/kebab-case`

### Git
- Conventional commits: `type(scope): description`
- Types: feat, fix, refactor, docs, test, chore, perf
- Branches: `feature/`, `fix/`, `refactor/`

### Imports (ordre)
```typescript
// 1. Externes
import { NextRequest } from "next/server"
// 2. Lib internes
import { db } from "@/lib/db"
// 3. Composants
import { ArticleCard } from "@/components/blog/article-card"
// 4. Types
import type { Article } from "@prisma/client"
```

---

## Workflows AI

### Generation article
```
Sujet + ton + mots-cles + longueur
→ 1. Outline structure (H2/H3) — structured output JSON
→ 2. Redaction section par section — streaming SSE
→ 3. Optimisation SEO auto (meta, links, schema)
→ 4. Score SEO calcule
→ Article complet dans l'editeur
```

### Audit SEO
```
Article existant
→ Analyse: titre, meta, headings, densite, readability
→ Score 0-100 avec detail
→ Suggestions AI de correction
→ Apply en 1 clic
```

---

## Metriques Cibles

- SEO Score moyen > 85/100
- LCP < 2.5s, INP < 200ms, CLS < 0.1
- Generation article < 60s
- Cout AI par article < $0.15
- Test coverage > 80%
