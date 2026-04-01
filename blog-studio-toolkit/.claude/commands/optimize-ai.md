# Optimiser l'Engine AI

Analyse et optimise le systeme de generation AI du Blog Studio.

## Checks

### 1. Prompt Caching
- Verifie que les system prompts utilisent `cache_control: { type: "ephemeral" }`
- Separe les blocs statiques (cacheables) des blocs dynamiques (par requete)
- Estime les economies de tokens

### 2. Streaming
- Verifie le flux complet: API Anthropic → Server → SSE → Client
- Verifie la gestion du backpressure
- Verifie les indicateurs UI (loading, streaming, complete)

### 3. Structured Outputs
- Verifie que les outlines utilisent le JSON mode
- Verifie que les meta SEO utilisent le JSON mode
- Verifie le parsing et la validation (Zod) des outputs

### 4. Error Handling
- Verifie le retry logic (429 rate limit, 529 overloaded)
- Verifie le backoff exponentiel (2s, 4s, 8s, 16s max)
- Verifie les messages d'erreur user-friendly

### 5. Token Budget
- Verifie le tracking de tokens par user
- Verifie les limites par plan (FREE/PRO/ENTERPRISE)
- Verifie l'affichage de la conso dans le dashboard

### 6. Qualite des Prompts
- Review chaque prompt dans src/lib/ai/prompts/
- Verifie: specificite, few-shot examples, chain-of-thought
- Propose des ameliorations

## Output
Corrige les problemes trouves et mets a jour AUDIT_TRACKER.md.
