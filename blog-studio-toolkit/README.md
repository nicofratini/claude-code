# Blog Studio Toolkit — Guide d'Installation

## Contenu du Toolkit

```
blog-studio-toolkit/
├── CLAUDE.md                          # Config projet pour Claude Code
├── AUDIT_TRACKER.md                   # Tracker de suivi (mis a jour auto)
├── PROMPT_AUDIT_CODEBASE.md           # Prompts d'audit (7 variantes)
├── .claude/commands/
│   ├── audit-complet.md               # /audit-complet — Audit 360 du projet
│   ├── weekly-review.md               # /weekly-review — Suivi hebdo
│   ├── fix-issues.md                  # /fix-issues — Corrige les issues P0/P1
│   ├── generate-article.md            # /generate-article — Genere un article AI
│   ├── seo-audit.md                   # /seo-audit — Audit SEO article
│   ├── improve-seo.md                 # /improve-seo — Ameliore SEO global
│   ├── optimize-ai.md                 # /optimize-ai — Optimise l'engine AI
│   └── new-feature.md                 # /new-feature — Implemente une feature
└── README.md                          # Ce fichier
```

## Installation

```bash
# Depuis la racine de ton projet blog-studio:
cp blog-studio-toolkit/CLAUDE.md ./CLAUDE.md
cp blog-studio-toolkit/AUDIT_TRACKER.md ./AUDIT_TRACKER.md
cp blog-studio-toolkit/PROMPT_AUDIT_CODEBASE.md ./PROMPT_AUDIT_CODEBASE.md
cp -r blog-studio-toolkit/.claude ./.claude
```

## Utilisation

### Premier audit
```bash
# Ouvre Claude Code dans ton projet
cd blog-studio
claude

# Lance l'audit complet
/audit-complet
```

### Workflow quotidien
| Commande | Quand l'utiliser |
|----------|-----------------|
| `/audit-complet` | Premier audit ou audit de reference |
| `/weekly-review` | Chaque lundi — progression + priorites |
| `/fix-issues` | Corriger les P0/P1 du tracker |
| `/generate-article` | Tester le workflow de generation AI |
| `/seo-audit` | Auditer le SEO d'un article |
| `/improve-seo` | Ameliorer le SEO technique global |
| `/optimize-ai` | Optimiser prompts, caching, streaming |
| `/new-feature` | Implementer une nouvelle feature |

### Cycle recommande
1. `/audit-complet` → Etat des lieux initial
2. `/fix-issues` → Corrige les P0 et P1
3. `/weekly-review` → Mesure la progression
4. Repete 2-3 chaque semaine
