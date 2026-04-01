# Prompt Master — Audit Complet de Codebase Blog Studio

> Ce prompt est concu pour etre utilise avec Claude Code directement dans le repertoire de ton projet.
> Il scanne tout, identifie tout, et produit des documents de suivi actionnables.

---

## PROMPT PRINCIPAL — Scan & Audit Complet

Copie ce prompt tel quel dans Claude Code une fois positionne dans ton projet:

```
Je veux un audit complet et brutal de cette codebase. Pas de complaisance.

## ETAPE 1 — SCAN EXHAUSTIF

Scanne l'integralite du projet et produis un inventaire precis:

### 1.1 Structure reelle
- Liste TOUS les fichiers et dossiers (arborescence complete)
- Identifie les fichiers vides, les stubs, les placeholders
- Repere les fichiers orphelins (importes nulle part)
- Verifie la coherence entre la structure prevue (CLAUDE.md) et la realite

### 1.2 Etat de chaque module
Pour CHAQUE dossier/module du projet, indique:
- Nombre de fichiers
- Lignes de code (hors commentaires/blancs)
- Status: COMPLET | PARTIEL | STUB | VIDE | MANQUANT
- Dependances manquantes

### 1.3 Configuration & Setup
- package.json: toutes les deps installees vs utilisees vs manquantes
- tsconfig.json: mode strict actif? options manquantes?
- next.config: optimisations presentes/absentes
- .env.example vs .env: variables manquantes
- Prisma schema: coherent avec le code? migrations a jour?
- ESLint/Prettier: configure correctement?

---

## ETAPE 2 — AUDIT PAR DOMAINE

### 2.1 ARCHITECTURE (Score: ?/10)
- [ ] Separation des responsabilites (clean architecture?)
- [ ] Server Components vs Client Components (ratio correct?)
- [ ] API design: type-safety end-to-end (tRPC implemente?)
- [ ] Error boundaries et error handling global
- [ ] Loading states et Suspense boundaries
- [ ] Middleware (auth, rate limiting, logging)
- [ ] Environment variables: toutes securisees?

### 2.2 BASE DE DONNEES (Score: ?/10)
- [ ] Schema Prisma complet vs partiel
- [ ] Relations correctes (FK, cascades, index)
- [ ] Migrations: propres et coherentes?
- [ ] Seed data disponible?
- [ ] Queries: N+1 detectes? index couvrants?
- [ ] Soft delete implemente?
- [ ] Audit trail (createdAt, updatedAt partout)?

### 2.3 AUTHENTIFICATION & SECURITE (Score: ?/10)
- [ ] Auth implementee (NextAuth/Auth.js)?
- [ ] RBAC (roles: Admin, Editor, Author, Viewer)
- [ ] Protection des routes (middleware)
- [ ] Rate limiting sur les endpoints sensibles
- [ ] Input validation (Zod) sur TOUTES les frontieres
- [ ] CSRF protection
- [ ] XSS prevention (sanitization des outputs)
- [ ] SQL injection impossible (ORM + parameterized)
- [ ] API keys: jamais exposees cote client?
- [ ] CSP headers configures?

### 2.4 ENGINE AI (Score: ?/10)
- [ ] Client Anthropic configure et fonctionnel
- [ ] Prompts systeme: modulaires et caches?
- [ ] Streaming SSE: implemente end-to-end?
- [ ] Structured outputs pour donnees parsables
- [ ] Token budget: suivi et limites par plan
- [ ] Retry logic (429/529) avec exponential backoff
- [ ] Workflows: generation article, outline, rewrite, meta
- [ ] Historique des generations sauvegarde
- [ ] Cout par generation affiche a l'utilisateur
- [ ] Queue/jobs pour generation longue (Inngest/Trigger.dev)

### 2.5 SEO ENGINE (Score: ?/10)
- [ ] Score SEO automatique par article (algorithme present?)
- [ ] Meta tags auto (title, description, OG, Twitter)
- [ ] JSON-LD / Structured data (Article, Breadcrumb, FAQ)
- [ ] Sitemap XML dynamique
- [ ] Robots.txt dynamique
- [ ] Canonical URLs
- [ ] Maillage interne automatique
- [ ] Alt tags sur les images
- [ ] Headings hierarchy (H1 unique, H2/H3 structures)
- [ ] URL slugs propres et SEO-friendly
- [ ] Core Web Vitals optimises
- [ ] Hreflang pour multi-langue

### 2.6 EDITEUR (Score: ?/10)
- [ ] Rich text editor (Tiptap/ProseMirror/Novel)
- [ ] Blocs de contenu (texte, image, code, embed, callout)
- [ ] AI inline (completion, rewrite dans l'editeur)
- [ ] Slash commands dans l'editeur
- [ ] Sauvegarde automatique (debounced)
- [ ] Preview temps reel
- [ ] Import/export (Markdown, HTML)
- [ ] Historique de versions
- [ ] Mode focus
- [ ] Templates d'articles
- [ ] Raccourcis clavier

### 2.7 DASHBOARD & ANALYTICS (Score: ?/10)
- [ ] Vue d'ensemble (stats globales)
- [ ] Analytics par article (vues, temps lecture)
- [ ] Graphiques temporels
- [ ] Calendrier editorial
- [ ] Top articles / articles en declin
- [ ] Suivi conso AI (tokens, couts)
- [ ] Export donnees

### 2.8 AUTOMATISATION (Score: ?/10)
- [ ] Publication programmee
- [ ] Workflow editorial (draft -> review -> publish)
- [ ] Webhooks
- [ ] Auto-generation planifiee
- [ ] Distribution (RSS, newsletter)
- [ ] Batch operations
- [ ] API publique

### 2.9 UI/UX (Score: ?/10)
- [ ] Design system coherent (shadcn/ui?)
- [ ] Responsive (mobile, tablet, desktop)
- [ ] Dark mode
- [ ] Loading skeletons partout
- [ ] Empty states bien designes
- [ ] Error states informatifs
- [ ] Toasts/notifications
- [ ] Navigation intuitive
- [ ] Accessibilite (a11y: ARIA, focus management, contraste)
- [ ] Performance percue (optimistic updates, transitions)
- [ ] Onboarding flow

### 2.10 TESTS & QUALITE (Score: ?/10)
- [ ] Tests unitaires (Vitest) — couverture?
- [ ] Tests E2E (Playwright) — scenarios critiques?
- [ ] Tests d'integration API
- [ ] CI/CD pipeline (GitHub Actions)
- [ ] Linting automatique
- [ ] Type checking strict
- [ ] Pre-commit hooks

---

## ETAPE 3 — PROBLEMES CRITIQUES

Liste TOUS les problemes trouves, classes par severite:

### BLOQUANTS (P0) — Empechent le fonctionnement
Format: [FICHIER:LIGNE] Description du probleme → Solution proposee

### CRITIQUES (P1) — Fonctionnent mais mal
Format: [FICHIER:LIGNE] Description du probleme → Solution proposee

### IMPORTANTS (P2) — Manque pour un produit pro
Format: Description → Solution proposee

### NICE-TO-HAVE (P3) — Pour un produit world-class
Format: Description → Solution proposee

---

## ETAPE 4 — FEATURES MANQUANTES vs CLAUDE.md

Compare l'etat reel du code avec ce qui est decrit dans CLAUDE.md.
Pour chaque feature listee dans CLAUDE.md:
- FAIT ✅ (avec % de completion)
- PARTIEL 🟡 (ce qui manque)
- ABSENT ❌ (a implementer)
- NON PREVU 🔵 (devrait etre ajoute)

---

## ETAPE 5 — SCORECARD FINALE

Produis ce tableau:

| Domaine | Score /10 | Status | Problemes P0 | Problemes P1 | Features manquantes |
|---------|-----------|--------|-------------|-------------|-------------------|
| Architecture | | | | | |
| Base de donnees | | | | | |
| Auth & Securite | | | | | |
| Engine AI | | | | | |
| SEO Engine | | | | | |
| Editeur | | | | | |
| Dashboard | | | | | |
| Automatisation | | | | | |
| UI/UX | | | | | |
| Tests & Qualite | | | | | |
| **TOTAL** | **/100** | | | | |

Classification:
- 0-2: INEXISTANT — A construire de zero
- 3-4: EMBRYONNAIRE — Stubs/debut d'implementation
- 5-6: FONCTIONNEL MINIMAL — Ca marche mais pas production-ready
- 7-8: SOLIDE — Production-ready avec ameliorations possibles
- 9-10: WORLD-CLASS — Niveau des meilleurs SaaS du marche

---

## FORMAT DE SORTIE

Produis ta reponse en 3 blocs distincts:
1. **INVENTAIRE** — L'etat factuel du code (pas d'opinion)
2. **DIAGNOSTIC** — Les problemes et manques (brutal et honnete)
3. **PRESCRIPTION** — Les actions a prendre dans l'ordre (priorisees)
```

---

## PROMPTS DE SUIVI (a utiliser apres l'audit initial)

### Suivi Sprint — A utiliser chaque semaine

```
Relis le fichier AUDIT_TRACKER.md et mets-le a jour:
1. Marque comme DONE les taches que j'ai completees (verifie dans le code)
2. Recalcule les scores par domaine
3. Identifie les nouvelles regressions ou problemes introduits
4. Propose les 5 prochaines taches prioritaires pour cette semaine
5. Mets a jour la progression globale (%)
```

### Deep-Dive par Module — Quand tu veux approfondir un domaine

```
Focus sur le module [NOM_DU_MODULE].
1. Lis CHAQUE fichier de ce module
2. Analyse la qualite du code ligne par ligne
3. Identifie: bugs, anti-patterns, code mort, imports inutiles, types manquants
4. Propose des refactorings concrets avec le code avant/apres
5. Verifie la coherence avec les autres modules qui en dependent
```

### Test de Fonctionnalite — Verifier qu'une feature marche

```
Teste la fonctionnalite [NOM_FEATURE]:
1. Identifie tous les fichiers impliques (composants, API, DB, lib)
2. Trace le flux complet: UI → action → API → DB → reponse → UI
3. Cherche les edge cases non geres
4. Verifie les loading/error states
5. Verifie la validation des inputs
6. Cherche les failles de securite
7. Donne un verdict: PRET | PRESQUE | CASSE | MANQUANT
```

### Audit Performance — Optimisation

```
Audit de performance:
1. Identifie les composants marques "use client" inutilement
2. Cherche les re-renders excessifs (dependencies incorrectes dans useEffect/useMemo)
3. Verifie l'utilisation correcte de SSG/ISR/SSR sur chaque route
4. Cherche les imports dynamiques manquants (lazy loading)
5. Verifie les tailles de bundle (images non optimisees, deps lourdes)
6. Cherche les queries DB non optimisees (N+1, index manquants, select trop large)
7. Verifie le prompt caching AI (blocs system caches?)
```

### Audit SEO Technique

```
Audit SEO technique complet:
1. Verifie chaque page publique: meta title, description, OG tags, canonical
2. Inspecte le sitemap: toutes les pages incluses? priorites correctes?
3. Verifie le robots.txt: rien de bloque par erreur?
4. Cherche les structured data manquants (JSON-LD)
5. Verifie la hierarchie des headings sur chaque template
6. Cherche les liens casses (internes et externes)
7. Verifie le score Lighthouse estime par page
8. Verifie les images: alt tags, lazy loading, formats optimises
```
