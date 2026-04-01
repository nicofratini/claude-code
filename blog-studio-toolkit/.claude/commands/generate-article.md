# Generation d'Article AI

Genere un article complet avec le workflow AI en 4 etapes.

## Parametres attendus
L'utilisateur doit fournir: sujet, ton, mots-cles cibles, longueur souhaitee.

## Workflow

### Etape 1 — Outline
- Genere un plan structure (H2/H3) via structured output JSON
- Inclus les mots-cles dans les headings
- Propose 5-8 sections

### Etape 2 — Redaction
- Redige chaque section individuellement
- Streaming SSE vers le client
- Ton adapte au parametre (professionnel, decontracte, expert, pedagogique)
- Longueur respectee (+/- 10%)

### Etape 3 — SEO
- Genere: meta title (< 60 chars), meta description (< 160 chars)
- Genere: OG tags, Twitter Card data
- Genere: JSON-LD Article schema
- Calcule le score SEO
- Suggere des liens internes (si articles existants)

### Etape 4 — Finalisation
- Sauvegarde en base (status: DRAFT)
- Affiche le score SEO et les suggestions
- Propose les ameliorations

## Implementation
Utilise les fichiers dans `src/lib/ai/prompts/` pour les system prompts.
Utilise le streaming SSE via `src/lib/ai/streaming.ts`.
Sauvegarde via le tRPC router `src/server/routers/article.ts`.
