# Prompt d'Audit Complet — Blog Studio

> Ce fichier contient le prompt principal + les prompts de suivi.
> A utiliser avec Claude Code directement dans le repertoire du projet blog-studio.

---

## MODE D'EMPLOI

1. Copie tout le dossier `blog-studio-toolkit/` a la racine de ton projet blog-studio
2. Renomme/deplace les fichiers:
   - `CLAUDE.md` → racine du projet
   - `.claude/commands/*` → `.claude/commands/` a la racine
   - `AUDIT_TRACKER.md` → racine du projet
3. Ouvre Claude Code dans le dossier blog-studio
4. Lance: `/audit-complet` pour le premier audit
5. Ensuite: `/weekly-review` chaque semaine pour suivre la progression

---

## PROMPT 1 — PREMIER AUDIT COMPLET

Copie ce prompt dans Claude Code:

```
Effectue un audit complet et brutal de cette codebase Blog Studio.
Lis CLAUDE.md pour comprendre la vision du projet, puis analyse tout le code reel.

## ETAPE 1 — INVENTAIRE FACTUEL

Scan chaque dossier et fichier du projet. Pour chaque module, indique:
- Nombre de fichiers et lignes de code
- Status: COMPLET | PARTIEL | STUB | VIDE | MANQUANT
- Dependances utilisees vs installees vs manquantes

Verifie specifiquement:
- package.json: deps installees mais jamais importees? deps manquantes?
- tsconfig.json: strict mode? noUncheckedIndexedAccess?
- next.config: optimisations?
- prisma/schema.prisma: coherent avec le code?
- .env.example: toutes les variables documentees?

## ETAPE 2 — AUDIT PAR DOMAINE (score chaque domaine /10)

### 2.1 ARCHITECTURE
- Separation des responsabilites clean?
- Server Components vs Client Components (ratio)?
- tRPC type-safety end-to-end?
- Error boundaries et error handling?
- Loading states et Suspense boundaries?
- Middleware (auth, rate limiting)?

### 2.2 BASE DE DONNEES
- Schema Prisma complet?
- Relations, cascades, index?
- Migrations propres?
- Seed data?
- Queries: N+1? index couvrants?

### 2.3 AUTH & SECURITE
- Auth implementee (NextAuth)?
- RBAC (roles)?
- Protection routes (middleware)?
- Rate limiting endpoints AI?
- Validation Zod sur TOUTES les frontieres?
- XSS/CSRF/injection protection?
- API keys server-only?

### 2.4 ENGINE AI
- Client Anthropic configure?
- Prompts modulaires et caches?
- Streaming SSE end-to-end?
- Structured outputs pour donnees parsables?
- Token budget par user/plan?
- Retry 429/529 avec backoff?
- Workflows: generation, outline, rewrite, meta?
- Queue/jobs pour generation longue?

### 2.5 SEO ENGINE
- Score SEO auto par article?
- Meta tags auto (title, description, OG, Twitter)?
- JSON-LD structured data?
- Sitemap XML dynamique?
- Robots.txt?
- Canonical URLs?
- Maillage interne auto?
- Alt tags images?
- Headings hierarchy?
- Core Web Vitals?

### 2.6 EDITEUR
- Rich text (Tiptap/ProseMirror)?
- AI inline (completion, rewrite)?
- Blocs de contenu?
- Sauvegarde auto?
- Preview temps reel?
- Import/export?
- Templates?

### 2.7 DASHBOARD & ANALYTICS
- Vue d'ensemble stats?
- Analytics par article?
- Graphiques?
- Calendrier editorial?
- Suivi conso AI?

### 2.8 AUTOMATISATION
- Publication programmee?
- Workflow editorial (draft→review→publish)?
- Auto-generation planifiee?
- RSS/newsletter?
- Batch operations?

### 2.9 UI/UX
- Design system coherent (shadcn/ui)?
- Responsive?
- Dark mode?
- Loading skeletons?
- Empty states?
- Error states?
- Toasts/notifications?
- Accessibilite (a11y)?
- Onboarding?

### 2.10 TESTS & QUALITE
- Tests unitaires (couverture)?
- Tests E2E?
- CI/CD pipeline?
- Linting?
- Type checking strict?
- Pre-commit hooks?

## ETAPE 3 — PROBLEMES PAR SEVERITE

### P0 — BLOQUANTS (empechent le fonctionnement)
Format: [FICHIER:LIGNE] Probleme → Solution

### P1 — CRITIQUES (fonctionnent mais mal)
Format: [FICHIER:LIGNE] Probleme → Solution

### P2 — IMPORTANTS (manque pour un produit pro)
Format: Description → Solution

### P3 — NICE-TO-HAVE (pour world-class)
Format: Description → Solution

## ETAPE 4 — COMPARAISON CLAUDE.md vs REALITE

Pour chaque feature de CLAUDE.md:
- FAIT ✅ (% completion)
- PARTIEL 🟡 (ce qui manque)
- ABSENT ❌ (a implementer)

## ETAPE 5 — SCORECARD FINALE

| Domaine | Score /10 | Status | P0 | P1 | Features manquantes |
|---------|-----------|--------|-----|-----|-------------------|
| Architecture | | | | | |
| DB | | | | | |
| Auth/Securite | | | | | |
| Engine AI | | | | | |
| SEO | | | | | |
| Editeur | | | | | |
| Dashboard | | | | | |
| Automatisation | | | | | |
| UI/UX | | | | | |
| Tests | | | | | |
| **TOTAL** | **/100** | | | | |

Echelle: 0-2 INEXISTANT | 3-4 EMBRYONNAIRE | 5-6 MINIMAL | 7-8 SOLIDE | 9-10 WORLD-CLASS

## ETAPE 6 — ECRIS LE RESULTAT

Ecris tout le resultat dans AUDIT_TRACKER.md en utilisant le template fourni.
Sois BRUTAL et HONNETE. Un 2/10 vrai vaut mieux qu'un 7/10 faux.
```

---

## PROMPT 2 — SUIVI HEBDOMADAIRE

```
Lis AUDIT_TRACKER.md et mets-le a jour:
1. Verifie dans le code quelles taches ont ete completees → marque DONE
2. Recalcule les scores par domaine
3. Identifie les regressions (nouveau code qui cree des problemes)
4. Liste les 5 priorites pour la semaine prochaine
5. Calcule la progression globale en %
6. Resume en 5 lignes: fait, reste, blocages
```

---

## PROMPT 3 — DEEP-DIVE MODULE

```
Focus sur le module [NOM].
1. Lis CHAQUE fichier
2. Analyse qualite ligne par ligne: bugs, anti-patterns, code mort, types manquants
3. Propose refactorings avec code avant/apres
4. Verifie coherence avec les modules dependants
5. Mets a jour AUDIT_TRACKER.md
```

---

## PROMPT 4 — TEST FONCTIONNEL

```
Teste la fonctionnalite [NOM]:
1. Identifie tous les fichiers impliques
2. Trace le flux: UI → action → API → DB → reponse → UI
3. Cherche les edge cases non geres
4. Verifie loading/error states
5. Verifie validation inputs
6. Cherche failles securite
7. Verdict: PRET | PRESQUE | CASSE | MANQUANT
```

---

## PROMPT 5 — AUDIT PERFORMANCE

```
Audit performance:
1. Composants "use client" inutiles
2. Re-renders excessifs (deps useEffect/useMemo incorrectes)
3. SSG/ISR/SSR correct sur chaque route
4. Imports dynamiques manquants (lazy loading)
5. Bundle size (images, deps lourdes)
6. Queries DB non optimisees (N+1, index, select trop large)
7. Prompt caching AI (blocs system caches?)
```

---

## PROMPT 6 — AUDIT SEO TECHNIQUE

```
Audit SEO technique:
1. Chaque page publique: meta title, description, OG, canonical
2. Sitemap: toutes pages incluses? priorites?
3. Robots.txt: rien bloque par erreur?
4. JSON-LD structured data manquants
5. Hierarchie headings par template
6. Liens casses
7. Images: alt, lazy loading, formats
8. Score Lighthouse estime
```

---

## PROMPT 7 — BOOTSTRAP FEATURE

```
Implemente [FEATURE] dans Blog Studio:
1. Verifie CLAUDE.md pour les conventions
2. Schema DB si necessaire (prisma/schema.prisma + migration)
3. Backend: tRPC router + validation Zod + service
4. Frontend: Server Component par defaut, shadcn/ui
5. Loading.tsx + error.tsx
6. Test minimum
7. pnpm lint && pnpm typecheck
8. Mets a jour AUDIT_TRACKER.md
9. Commit: feat(scope): description
```
