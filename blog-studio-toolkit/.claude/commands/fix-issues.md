# Corriger les Issues Identifiees

Lis le fichier `AUDIT_TRACKER.md` et traite les issues par ordre de priorite.

## Instructions

1. **Lis AUDIT_TRACKER.md** — identifie la prochaine tache non completee (status != DONE)
2. **Priorise**: P0 d'abord, puis P1, puis P2
3. **Pour chaque issue**:
   - Lis les fichiers concernes
   - Implemente la correction
   - Verifie que ca ne casse rien (lint + typecheck)
   - Marque comme DONE dans AUDIT_TRACKER.md
4. **Apres chaque correction**, fais un commit avec le format:
   `fix(scope): description courte`
5. **Continue** jusqu'a ce que toutes les P0 et P1 soient resolues

## Regles
- Ne touche PAS aux fichiers shadcn/ui (src/components/ui/)
- Lance `pnpm lint && pnpm typecheck` apres chaque modification
- Si une correction necessite une migration DB, cree-la avec `pnpm db:migrate`
- Si tu bloques, demande a l'utilisateur avant de continuer
