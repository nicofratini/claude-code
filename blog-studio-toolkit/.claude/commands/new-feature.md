# Implementer une Nouvelle Feature

Implemente une nouvelle fonctionnalite dans Blog Studio en respectant l'architecture.

## Checklist Pre-Implementation

1. **Verifie CLAUDE.md** — la feature est-elle prevue? feature flag existant?
2. **Verifie AUDIT_TRACKER.md** — y a-t-il des dependances ou pre-requis?
3. **Identifie les fichiers a creer/modifier** — liste-les avant de coder

## Workflow

### 1. Schema DB (si necessaire)
- Modifie `prisma/schema.prisma`
- Cree une migration: `pnpm db:migrate --name <nom>`
- Mets a jour les types generes

### 2. Backend
- Cree/modifie le tRPC router dans `src/server/routers/`
- Ajoute la validation Zod dans `src/lib/validators/`
- Ajoute la business logic dans `src/server/services/`

### 3. Frontend
- Server Component par defaut
- `"use client"` seulement si necessaire
- Utilise les composants shadcn/ui existants
- Ajoute loading.tsx et error.tsx

### 4. Tests
- Au minimum: 1 test unitaire par service
- E2E si c'est un flow utilisateur critique

### 5. Post-Implementation
- `pnpm lint && pnpm typecheck`
- Mets a jour AUDIT_TRACKER.md
- Commit: `feat(scope): description`

## Regles
- Respecte les conventions de CLAUDE.md
- Pas de `any` TypeScript
- Zod sur toutes les frontieres
- Server Components par defaut
