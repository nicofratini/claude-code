# CLAUDE.md — Blog Studio AI Platform

> Ce fichier est lu automatiquement par Claude Code pour comprendre le contexte du projet.
> Inspiré de l'architecture système de Claude Code (system prompts modulaires, feature gates, multi-agents, prompt caching).

---

## Identité du Projet

**Nom**: Blog Studio
**Vision**: Plateforme de création, pilotage et publication de contenus blog de niveau mondial avec génération AI automatique, SEO magnétique, et contrôle total paramétrable.
**Philosophie**: "Un cockpit éditorial intelligent — pas un simple éditeur."

---

## Stack Technique Recommandée

### Frontend
- **Framework**: Next.js 14+ (App Router, RSC, Server Actions)
- **UI**: React 18+ avec Tailwind CSS + shadcn/ui
- **State**: Zustand (léger) ou Jotai (atomique)
- **Forms**: React Hook Form + Zod (validation)
- **Rich Editor**: Tiptap (ProseMirror) ou Novel.sh (AI-native editor)
- **Charts/Analytics**: Recharts ou Tremor

### Backend & API
- **API**: Next.js API Routes + tRPC (type-safe end-to-end)
- **Auth**: NextAuth.js v5 (Auth.js) — OAuth, magic links, RBAC
- **Database**: PostgreSQL via Supabase ou Neon
- **ORM**: Prisma (migrations, type-safe queries)
- **Cache**: Redis (Upstash) pour sessions, rate limiting, queue
- **File Storage**: Supabase Storage ou Cloudflare R2
- **Queue/Jobs**: Inngest ou Trigger.dev (background AI generation)

### AI & Génération
- **LLM Principal**: Claude API (Anthropic) — claude-sonnet-4-20250514
- **SDK**: @anthropic-ai/sdk (TypeScript)
- **Streaming**: SSE (Server-Sent Events) pour génération temps réel
- **Prompt Engine**: Système de prompts modulaires avec caching (inspiré de Claude Code)
- **SEO AI**: Génération automatique meta, slugs, structured data, internal linking
- **Image AI**: DALL-E 3 / Stable Diffusion via API pour featured images

### Infrastructure & Deploy
- **Hosting**: Vercel (Edge Functions + ISR)
- **CDN**: Vercel Edge Network ou Cloudflare
- **Monitoring**: Sentry (errors) + Posthog (analytics)
- **CI/CD**: GitHub Actions
- **Tests**: Vitest (unit) + Playwright (E2E)

---

## Architecture Projet

```
blog-studio/
├── CLAUDE.md                    # Ce fichier — instructions projet
├── .claude/
│   └── commands/                # Commandes slash personnalisées
│       ├── generate-article.md  # /generate-article
│       ├── seo-audit.md         # /seo-audit
│       ├── publish.md           # /publish
│       └── analytics.md         # /analytics
├── src/
│   ├── app/                     # Next.js App Router
│   │   ├── (dashboard)/         # Route group dashboard
│   │   │   ├── articles/        # CRUD articles
│   │   │   ├── editor/          # Éditeur AI
│   │   │   ├── seo/             # Dashboard SEO
│   │   │   ├── media/           # Médiathèque
│   │   │   ├── analytics/       # Stats & performance
│   │   │   └── settings/        # Configuration
│   │   ├── (blog)/              # Route group blog public
│   │   │   ├── [slug]/          # Article dynamique
│   │   │   ├── category/[cat]/  # Pages catégories
│   │   │   └── tag/[tag]/       # Pages tags
│   │   ├── api/                 # API Routes
│   │   │   ├── trpc/            # tRPC handler
│   │   │   ├── ai/              # Endpoints AI (streaming)
│   │   │   ├── webhook/         # Webhooks (Stripe, etc.)
│   │   │   └── cron/            # Jobs planifiés
│   │   ├── layout.tsx           # Layout racine
│   │   └── page.tsx             # Landing page
│   ├── components/
│   │   ├── ui/                  # shadcn/ui components
│   │   ├── editor/              # Composants éditeur
│   │   ├── dashboard/           # Composants dashboard
│   │   ├── seo/                 # Composants SEO
│   │   └── blog/                # Composants blog public
│   ├── lib/
│   │   ├── ai/                  # Engine AI
│   │   │   ├── prompts/         # Templates de prompts (modulaires)
│   │   │   │   ├── system.ts    # System prompt principal
│   │   │   │   ├── article.ts   # Génération articles
│   │   │   │   ├── seo.ts       # Optimisation SEO
│   │   │   │   ├── meta.ts      # Meta descriptions
│   │   │   │   ├── outline.ts   # Plans d'articles
│   │   │   │   └── rewrite.ts   # Réécriture/amélioration
│   │   │   ├── client.ts        # Client Anthropic configuré
│   │   │   ├── streaming.ts     # Gestion SSE streaming
│   │   │   └── cache.ts         # Prompt caching strategy
│   │   ├── db/                  # Prisma client & helpers
│   │   ├── seo/                 # Utilitaires SEO
│   │   │   ├── analyzer.ts      # Analyse SEO on-page
│   │   │   ├── schema.ts        # JSON-LD structured data
│   │   │   ├── sitemap.ts       # Génération sitemap
│   │   │   ├── robots.ts        # Robots.txt dynamique
│   │   │   └── internal-links.ts # Maillage interne auto
│   │   ├── auth/                # Configuration auth
│   │   ├── utils/               # Utilitaires généraux
│   │   └── validators/          # Schémas Zod
│   ├── server/
│   │   ├── routers/             # tRPC routers
│   │   └── services/            # Business logic
│   ├── hooks/                   # React hooks custom
│   ├── stores/                  # Zustand stores
│   └── types/                   # Types TypeScript globaux
├── prisma/
│   ├── schema.prisma            # Schéma DB
│   └── migrations/              # Migrations
├── public/                      # Assets statiques
├── tests/                       # Tests E2E Playwright
├── .env.example                 # Variables d'environnement template
├── next.config.ts               # Config Next.js
├── tailwind.config.ts           # Config Tailwind
├── tsconfig.json                # Config TypeScript (strict)
└── package.json
```

---

## Principes de Développement

### Code Quality
- TypeScript strict mode obligatoire (`strict: true`, `noUncheckedIndexedAccess: true`)
- Zod pour toute validation aux frontières (input utilisateur, API externes)
- Pas de `any` — utiliser `unknown` et narrowing
- Composants serveur par défaut, `"use client"` seulement quand nécessaire
- Server Actions pour les mutations simples, tRPC pour les queries complexes

### Architecture AI (Inspirée de Claude Code)
- **Prompts modulaires**: Séparer system prompt (cacheable) et dynamic context (par requête)
- **Prompt caching**: Utiliser `cache_control: { type: "ephemeral" }` pour les blocs statiques
- **Streaming first**: Toujours streamer les réponses AI vers le client via SSE
- **Token budget**: Suivre la consommation de tokens, implémenter des limites par user/plan
- **Retry avec backoff**: Gérer 429 (rate limit) et 529 (overloaded) avec exponential backoff
- **Structured outputs**: Utiliser les structured outputs pour les données parsables (meta SEO, outlines)

### SEO Engine
- Score SEO calculé automatiquement pour chaque article (0-100)
- Checklist SEO interactive dans l'éditeur (titre, meta, headings, images alt, links)
- Génération automatique: meta description, Open Graph, Twitter Cards, JSON-LD
- Sitemap XML dynamique avec ISR
- Maillage interne automatique basé sur les tags/catégories
- Canonical URLs, hreflang pour multi-langue
- Core Web Vitals monitoring

### Sécurité
- Sanitization de tous les inputs (XSS, injection)
- CSRF protection via Server Actions
- Rate limiting sur les endpoints AI (Redis)
- API keys jamais exposées côté client
- Content Security Policy headers
- Validation Zod sur toutes les frontières

---

## Modèle de Données Principal

```prisma
model User {
  id            String    @id @default(cuid())
  email         String    @unique
  name          String?
  role          Role      @default(EDITOR)
  articles      Article[]
  plan          Plan      @default(FREE)
  tokensUsed    Int       @default(0)
  tokensLimit   Int       @default(50000)
  createdAt     DateTime  @default(now())
  updatedAt     DateTime  @updatedAt
}

model Article {
  id              String        @id @default(cuid())
  title           String
  slug            String        @unique
  content         Json          // Tiptap JSON
  contentHtml     String        // HTML rendu
  excerpt         String?
  featuredImage   String?
  status          ArticleStatus @default(DRAFT)
  publishedAt     DateTime?
  author          User          @relation(fields: [authorId], references: [id])
  authorId        String
  category        Category?     @relation(fields: [categoryId], references: [id])
  categoryId      String?
  tags            Tag[]
  seoScore        Int           @default(0)
  seoData         Json?         // meta, og, jsonld
  readingTime     Int?
  wordCount       Int?
  views           Int           @default(0)
  aiGenerated     Boolean       @default(false)
  aiPromptUsed    String?
  createdAt       DateTime      @default(now())
  updatedAt       DateTime      @updatedAt

  @@index([status, publishedAt])
  @@index([categoryId])
  @@index([slug])
}

model Category {
  id          String    @id @default(cuid())
  name        String    @unique
  slug        String    @unique
  description String?
  articles    Article[]
  parentId    String?
  parent      Category? @relation("CategoryTree", fields: [parentId], references: [id])
  children    Category[] @relation("CategoryTree")
}

model Tag {
  id       String    @id @default(cuid())
  name     String    @unique
  slug     String    @unique
  articles Article[]
}

model SeoAudit {
  id         String   @id @default(cuid())
  articleId  String
  score      Int
  issues     Json     // Array d'issues détectées
  suggestions Json    // Suggestions AI
  createdAt  DateTime @default(now())
}

model AnalyticsEvent {
  id        String   @id @default(cuid())
  articleId String?
  event     String   // page_view, scroll, click
  data      Json?
  createdAt DateTime @default(now())

  @@index([articleId, event])
  @@index([createdAt])
}

enum Role { ADMIN EDITOR AUTHOR VIEWER }
enum Plan { FREE PRO ENTERPRISE }
enum ArticleStatus { DRAFT REVIEW SCHEDULED PUBLISHED ARCHIVED }
```

---

## Workflows AI Clés

### 1. Génération d'Article Complète
```
Input: Sujet + ton + mots-clés cibles + longueur
→ Étape 1: Recherche & analyse concurrence (WebSearch)
→ Étape 2: Génération outline structuré (H2/H3)
→ Étape 3: Rédaction section par section (streaming)
→ Étape 4: Optimisation SEO automatique (meta, links, schema)
→ Étape 5: Suggestion d'images (prompts DALL-E)
→ Output: Article complet avec score SEO
```

### 2. SEO Audit Automatique
```
Input: Article existant
→ Analyse: titre, meta, headings, densité mots-clés, readability
→ Score: 0-100 avec détail par critère
→ Suggestions: corrections automatiques proposées
→ Action: appliquer les corrections en un clic
```

### 3. Planification Éditoriale
```
Input: Niche + objectifs + fréquence
→ Calendrier éditorial mensuel
→ Sujets avec angles uniques
→ Mots-clés cibles par article
→ Maillage interne planifié
```

---

## Variables d'Environnement

```env
# App
NEXT_PUBLIC_APP_URL=http://localhost:3000
NODE_ENV=development

# Database
DATABASE_URL=postgresql://...

# Auth
NEXTAUTH_SECRET=
NEXTAUTH_URL=http://localhost:3000

# AI
ANTHROPIC_API_KEY=sk-ant-...
AI_MODEL=claude-sonnet-4-20250514
AI_MAX_TOKENS=4096
AI_TEMPERATURE=0.7

# Storage
SUPABASE_URL=
SUPABASE_ANON_KEY=
SUPABASE_SERVICE_KEY=

# Cache
UPSTASH_REDIS_URL=
UPSTASH_REDIS_TOKEN=

# Analytics
NEXT_PUBLIC_POSTHOG_KEY=
SENTRY_DSN=

# SEO
NEXT_PUBLIC_SITE_URL=https://yourblog.com
NEXT_PUBLIC_SITE_NAME=Blog Studio
```

---

## Commandes de Développement

```bash
# Développement
pnpm dev                    # Serveur dev Next.js
pnpm db:push               # Push schema Prisma
pnpm db:migrate             # Migration Prisma
pnpm db:studio              # Prisma Studio (GUI DB)
pnpm db:seed                # Seed données initiales

# Tests
pnpm test                   # Vitest unit tests
pnpm test:e2e               # Playwright E2E
pnpm test:coverage          # Coverage report

# Build & Deploy
pnpm build                  # Build production
pnpm start                  # Start production
pnpm lint                   # ESLint
pnpm typecheck              # tsc --noEmit
```

---

## Conventions

### Nommage
- **Fichiers**: kebab-case (`article-editor.tsx`)
- **Composants**: PascalCase (`ArticleEditor`)
- **Fonctions/variables**: camelCase (`getArticleBySlug`)
- **Types/Interfaces**: PascalCase (`ArticleWithSeo`)
- **Constantes**: SCREAMING_SNAKE_CASE (`MAX_TOKEN_BUDGET`)
- **Routes API**: kebab-case (`/api/ai/generate-article`)

### Git
- Format commit: `type(scope): description` (conventional commits)
- Types: feat, fix, refactor, docs, test, chore, perf
- Branches: `feature/`, `fix/`, `refactor/`
- PR requise pour merge sur main

### Imports
```typescript
// 1. Packages externes
import { NextRequest } from "next/server"
import Anthropic from "@anthropic-ai/sdk"

// 2. Lib internes
import { db } from "@/lib/db"
import { generateArticle } from "@/lib/ai/client"

// 3. Composants
import { ArticleCard } from "@/components/blog/article-card"

// 4. Types
import type { Article } from "@prisma/client"
```

---

## Feature Gates (Inspiré de Claude Code)

Utiliser des feature flags pour déploiement progressif:

```typescript
// lib/features.ts
export const FEATURES = {
  AI_GENERATION: env.FEATURE_AI_GENERATION === "true",
  SEO_AUTO_AUDIT: env.FEATURE_SEO_AUTO_AUDIT === "true",
  MULTI_LANGUAGE: env.FEATURE_MULTI_LANGUAGE === "true",
  EDITORIAL_CALENDAR: env.FEATURE_EDITORIAL_CALENDAR === "true",
  ANALYTICS_DASHBOARD: env.FEATURE_ANALYTICS_DASHBOARD === "true",
  AUTO_INTERNAL_LINKING: env.FEATURE_AUTO_INTERNAL_LINKING === "true",
  IMAGE_AI_GENERATION: env.FEATURE_IMAGE_AI_GENERATION === "true",
  VOICE_TO_ARTICLE: env.FEATURE_VOICE_TO_ARTICLE === "true",
} as const
```

---

## Métriques de Succès

- **SEO Score moyen** > 85/100 sur tous les articles publiés
- **Core Web Vitals**: LCP < 2.5s, FID < 100ms, CLS < 0.1
- **Temps de génération** article complet < 60 secondes
- **Coût AI** par article < $0.15 (avec prompt caching)
- **Uptime** > 99.9%
- **Test coverage** > 80%
