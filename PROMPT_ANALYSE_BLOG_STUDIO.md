# Prompt Ultime — Analyse Complète Blog Studio

> Copie ce prompt et utilise-le avec Claude pour analyser ton projet Blog Studio sous tous les angles.
> Inspiré de l'architecture système de Claude Code: prompts modulaires, analyse multi-dimensionnelle, scoring automatique, plans d'action priorisés.

---

## Le Prompt

```
Tu es un architecte logiciel senior et expert en produits SaaS de niveau mondial, spécialisé en:
- Plateformes de contenu / CMS headless / Blog engines
- SEO technique et sémantique avancé
- Génération de contenu AI (LLM, prompting, streaming)
- Architecture Next.js / React / TypeScript production-grade
- Design produit et UX pour outils créatifs
- Growth engineering et monétisation SaaS

---

## TA MISSION

Analyse mon projet "Blog Studio" — une plateforme de création, pilotage et publication de contenus blog avec génération AI automatique, SEO magnétique et contrôle total paramétrable.

Procède en 8 phases séquentielles. Pour chaque phase, fournis:
1. Un **état des lieux** (ce qui existe, ce qui manque)
2. Un **score /10** du niveau actuel
3. Des **actions concrètes priorisées** (P0 = bloquant, P1 = critique, P2 = important, P3 = nice-to-have)
4. Des **exemples de code** quand pertinent
5. Un **benchmark** vs les meilleurs produits du marché (WordPress, Ghost, Contentful, Jasper AI, Surfer SEO, etc.)

---

## PHASE 1 — ARCHITECTURE & INFRASTRUCTURE (Score: /10)

Analyse:
- [ ] Structure du projet (dossiers, séparation des responsabilités)
- [ ] Stack technique (Next.js version, React, TypeScript config)
- [ ] Base de données (schéma, relations, index, migrations)
- [ ] API design (REST vs tRPC vs GraphQL, type-safety)
- [ ] Cache strategy (Redis, ISR, SWR, prompt caching)
- [ ] Error handling (boundaries, retry logic, fallbacks)
- [ ] Configuration management (env vars, feature flags)
- [ ] Monorepo vs single repo structure
- [ ] Build & bundle optimization
- [ ] Edge functions vs serverless vs server

Questions clés:
- L'architecture supporte-t-elle 100K articles sans dégradation?
- Le schéma DB est-il optimisé pour les queries SEO fréquentes?
- Y a-t-il une stratégie de prompt caching pour réduire les coûts AI?

---

## PHASE 2 — ENGINE AI & GÉNÉRATION DE CONTENU (Score: /10)

Analyse:
- [ ] Client Anthropic (configuration, modèle, streaming SSE)
- [ ] System prompts (modularité, caching, versioning)
- [ ] Workflows de génération (article complet, outline, rewrite, meta)
- [ ] Structured outputs (JSON mode pour données parsables)
- [ ] Token budget management (suivi conso, limites par plan)
- [ ] Retry & error handling API (429, 529, timeouts)
- [ ] Qualité des prompts (spécificité, few-shot, chain-of-thought)
- [ ] Multi-modèle support (fallback, A/B testing modèles)
- [ ] Streaming UX (affichage progressif, indicateurs)
- [ ] Historique & versioning des générations

Questions clés:
- Les prompts utilisent-ils le prompt caching Anthropic (blocs system cacheable)?
- Y a-t-il une pipeline: recherche → outline → rédaction → SEO → review?
- Le streaming est-il implémenté end-to-end (API → server → client)?
- Quel est le coût moyen par article généré?

Benchmark: Jasper AI, Copy.ai, Writesonic, Claude.ai Projects

---

## PHASE 3 — SEO ENGINE (Score: /10)

Analyse:
- [ ] Score SEO automatique par article (algorithme, critères, pondération)
- [ ] Meta tags (title, description, OG, Twitter Cards) — génération auto?
- [ ] Structured data / JSON-LD (Article, BreadcrumbList, FAQPage, HowTo)
- [ ] Sitemap XML dynamique (ISR, priorités, lastmod)
- [ ] Robots.txt dynamique
- [ ] Canonical URLs & gestion des doublons
- [ ] Maillage interne automatique (algorithme de suggestion)
- [ ] Analyse de densité de mots-clés
- [ ] Readability score (Flesch, Gunning Fog)
- [ ] Headings hierarchy (H1 unique, H2/H3 structurés)
- [ ] Image optimization (alt tags AI, WebP/AVIF, lazy loading, srcset)
- [ ] Core Web Vitals (LCP, FID/INP, CLS)
- [ ] URL structure (slugs propres, hiérarchie logique)
- [ ] Pagination SEO (rel=next/prev ou infinite scroll indexable)
- [ ] Multi-langue / hreflang
- [ ] Internal linking score & orphan pages detection
- [ ] Breadcrumbs avec schema markup

Questions clés:
- Le score SEO est-il comparable à Surfer SEO / Clearscope?
- Les structured data couvrent-ils tous les types de rich snippets possibles?
- Le maillage interne est-il intelligent (basé sur TF-IDF, embeddings, ou juste tags)?
- Les Core Web Vitals sont-ils monitorés en continu?

Benchmark: Surfer SEO, Clearscope, Yoast, RankMath, Ahrefs

---

## PHASE 4 — ÉDITEUR & EXPÉRIENCE DE RÉDACTION (Score: /10)

Analyse:
- [ ] Éditeur rich text (Tiptap/ProseMirror, blocs, slash commands)
- [ ] AI inline (autocomplétion, réécriture, résumé dans l'éditeur)
- [ ] Blocs de contenu (texte, image, code, embed, callout, table)
- [ ] Drag & drop des blocs
- [ ] Collaboration temps réel (Yjs, Liveblocks)
- [ ] Historique de versions (diff visuel)
- [ ] Preview responsive (desktop, tablet, mobile)
- [ ] Raccourcis clavier complets
- [ ] Mode focus / distraction-free
- [ ] Templates d'articles réutilisables
- [ ] Sauvegarde automatique (debounced)
- [ ] Import/export (Markdown, HTML, Word, Google Docs)

Questions clés:
- L'éditeur rivalise-t-il avec Notion / Ghost editor en UX?
- L'AI est-elle intégrée dans le flux d'écriture ou séparée?
- Peut-on créer des templates custom avec variables?

Benchmark: Notion, Ghost Editor, WordPress Gutenberg, Medium, Substack

---

## PHASE 5 — DASHBOARD & ANALYTICS (Score: /10)

Analyse:
- [ ] Vue d'ensemble (articles publiés, drafts, scheduled, vues totales)
- [ ] Analytics par article (vues, temps de lecture, scroll depth, bounce rate)
- [ ] Tendances temporelles (graphiques jour/semaine/mois)
- [ ] Top articles / articles en déclin
- [ ] Sources de trafic
- [ ] Suivi des positions SEO (intégration Google Search Console API)
- [ ] Suivi de la performance AI (tokens utilisés, coûts, qualité)
- [ ] Calendrier éditorial visuel
- [ ] Export des données (CSV, API)
- [ ] Notifications intelligentes (article en déclin, opportunité SEO)

Benchmark: Google Analytics, Plausible, Ghost Pro, HubSpot

---

## PHASE 6 — AUTOMATISATION & WORKFLOWS (Score: /10)

Analyse:
- [ ] Publication programmée (cron jobs, scheduled publishing)
- [ ] Auto-génération planifiée (calendrier éditorial → articles auto)
- [ ] Workflows de review (draft → review → approved → published)
- [ ] Webhooks (notifications, intégrations tierces)
- [ ] Auto-republication (mise à jour d'articles anciens, freshness)
- [ ] Distribution automatique (RSS, newsletter, réseaux sociaux)
- [ ] A/B testing des titres (AI-powered)
- [ ] Auto-traduction (multi-langue avec AI)
- [ ] Batch operations (publier/archiver/tagger en masse)
- [ ] API publique pour intégrations tierces

Questions clés:
- Peut-on mettre le blog en "pilote automatique" (génération + publication auto)?
- Les workflows sont-ils paramétrables sans code?
- Y a-t-il un système de queue robuste pour les jobs long (Inngest, Trigger.dev)?

Benchmark: Buffer, Zapier, Make, HubSpot Workflows

---

## PHASE 7 — SÉCURITÉ, PERFORMANCE & SCALABILITÉ (Score: /10)

Analyse:
- [ ] Authentication & authorization (RBAC, row-level security)
- [ ] Input validation (Zod sur toutes les frontières)
- [ ] Rate limiting (API AI, endpoints publics)
- [ ] CSRF / XSS / SQL injection protection
- [ ] Content Security Policy headers
- [ ] API key management (rotation, scoping)
- [ ] Performance: SSG/ISR pour pages publiques
- [ ] Performance: DB query optimization (N+1, index coverage)
- [ ] Performance: Image CDN + optimization pipeline
- [ ] Scalabilité: Horizontal scaling strategy
- [ ] Backup & disaster recovery
- [ ] GDPR compliance (données utilisateurs, cookies)
- [ ] Logging & monitoring (Sentry, structured logs)

Benchmark: Vercel best practices, OWASP Top 10, Cloudflare

---

## PHASE 8 — PRODUIT & MONÉTISATION (Score: /10)

Analyse:
- [ ] Onboarding flow (first article en < 5 minutes)
- [ ] Plans tarifaires (Free, Pro, Enterprise)
- [ ] Stripe integration (subscriptions, usage-based billing)
- [ ] Multi-tenant architecture (un workspace par utilisateur/team)
- [ ] White-label / custom domain
- [ ] Documentation utilisateur / Help center
- [ ] Feedback & feature requests (in-app)
- [ ] Roadmap publique
- [ ] Landing page & conversion funnel
- [ ] Email onboarding sequence

Questions clés:
- Le modèle économique est-il sustainable (coûts AI vs revenue)?
- Le pricing est-il compétitif vs Jasper AI ($49/mo), Ghost Pro ($9/mo)?
- Y a-t-il un free tier attractif pour l'acquisition?

Benchmark: Ghost Pro, Substack, Jasper AI, Copy.ai pricing

---

## LIVRABLE FINAL ATTENDU

Après les 8 phases, produis:

### 1. Tableau de Bord Projet (Scorecard)

| Phase | Score | Status | Actions P0 | Actions P1 |
|-------|-------|--------|-----------|-----------|
| Architecture | /10 | 🔴🟡🟢 | ... | ... |
| AI Engine | /10 | 🔴🟡🟢 | ... | ... |
| SEO Engine | /10 | 🔴🟡🟢 | ... | ... |
| Éditeur | /10 | 🔴🟡🟢 | ... | ... |
| Dashboard | /10 | 🔴🟡🟢 | ... | ... |
| Automation | /10 | 🔴🟡🟢 | ... | ... |
| Sécurité/Perf | /10 | 🔴🟡🟢 | ... | ... |
| Produit/Business | /10 | 🔴🟡🟢 | ... | ... |
| **TOTAL** | **/80** | | | |

### 2. Roadmap Priorisée (4 sprints)

**Sprint 1 (Semaine 1-2): Fondations** — Les P0 bloquants
**Sprint 2 (Semaine 3-4): Core Product** — AI Engine + Éditeur
**Sprint 3 (Semaine 5-6): SEO & Analytics** — Différenciation
**Sprint 4 (Semaine 7-8): Polish & Launch** — Automatisation + monétisation

### 3. Quick Wins (implémentables en < 1h chacun)

Liste de 10 améliorations rapides à fort impact.

### 4. Architecture Cible

Un diagramme ASCII de l'architecture idéale vers laquelle converger.

### 5. Prompt Library

5 prompts système optimisés pour les cas d'usage principaux:
- Génération d'article complet
- Outline structuré
- Optimisation SEO d'un article existant
- Meta description magnétique
- Réécriture / amélioration de ton

---

## CONTEXTE ADDITIONNEL

Voici le code source de mon projet Blog Studio à analyser:
[COLLE ICI TON CODE OU DÉCRIS LA STRUCTURE ACTUELLE]

Si tu n'as pas le code, commence par me poser les questions nécessaires pour
comprendre l'état actuel du projet avant de procéder à l'analyse.

Sois brutal et honnête dans tes scores. Un 3/10 honnête vaut mieux qu'un
7/10 complaisant. L'objectif est d'avoir un produit de niveau mondial.
```

---

## Variantes du Prompt

### Version Courte (Quick Audit)

```
Analyse mon projet Blog Studio (plateforme de création blog avec AI + SEO automatique).
Score chaque dimension /10 et donne les 3 actions prioritaires par dimension:
1. Architecture & Stack
2. AI Engine (génération, prompts, streaming)
3. SEO (score auto, structured data, maillage interne)
4. Éditeur UX
5. Automatisation (publication auto, workflows)
6. Sécurité & Performance
Sois brutal et concret. Pas de blabla, juste des actions.
```

### Version Itérative (Phase par Phase)

```
Nous allons analyser mon projet Blog Studio phase par phase.
Commence par la PHASE 1: ARCHITECTURE.
Analyse le code que je te fournis, donne un score /10,
et liste les actions P0/P1/P2 avec exemples de code.
Je te dirai "suivant" pour passer à la phase suivante.
```

### Version Compétitive (Benchmark Focus)

```
Compare mon Blog Studio aux meilleurs produits du marché:
- Ghost (CMS) — simplicité, performance, SEO natif
- Jasper AI — génération AI, templates, workflows
- Surfer SEO — optimisation SEO data-driven
- Substack — distribution, newsletter, monétisation
- Notion — éditeur, collaboration, flexibilité

Pour chaque concurrent, identifie:
1. Ce qu'ils font mieux que moi
2. Ce que je peux faire mieux qu'eux (mon avantage unique)
3. La feature killer à implémenter pour les surpasser

Mon USP cible: "Le seul outil qui combine éditeur AI + SEO automatique + publication pilote automatique dans une interface unique."
```

### Version Technique Deep-Dive

```
Tu es un staff engineer spécialisé Next.js + AI.
Review mon code Blog Studio avec un focus sur:

1. **Performance AI**: 
   - Mes prompts utilisent-ils le prompt caching Anthropic?
   - Le streaming SSE est-il optimal (buffering, backpressure)?
   - Les structured outputs sont-ils utilisés pour les données parsables?

2. **Performance Web**:
   - Les pages blog utilisent-elles SSG/ISR correctement?
   - Les images sont-elles optimisées (next/image, srcset, lazy)?
   - Le bundle JS est-il tree-shaked correctement?

3. **Data Layer**:
   - Les queries Prisma ont-elles des index couvrants?
   - Y a-t-il des N+1 queries cachés?
   - Le cache Redis est-il utilisé stratégiquement?

4. **Type Safety**:
   - tRPC end-to-end type safety?
   - Zod sur toutes les frontières?
   - TypeScript strict + noUncheckedIndexedAccess?

Montre-moi les anti-patterns et corrige-les avec du code.
```

---

## Tips d'Utilisation

1. **Fournis toujours ton code** — Sans code, l'analyse reste théorique
2. **Utilise la version itérative** pour un audit approfondi phase par phase
3. **Commence par le Quick Audit** pour avoir une vue d'ensemble rapide
4. **Re-exécute après chaque sprint** pour mesurer la progression des scores
5. **Utilise le CLAUDE.md** comme référence permanente dans ton projet
6. **Crée des commandes slash** (`.claude/commands/`) pour les tâches récurrentes
