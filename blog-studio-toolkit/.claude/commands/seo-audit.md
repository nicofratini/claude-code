# Audit SEO d'un Article

Effectue un audit SEO complet sur un article specifique ou sur tous les articles publies.

## Criteres d'Analyse (score /100)

### Titre (15 points)
- [ ] Longueur entre 30-60 caracteres
- [ ] Contient le mot-cle principal
- [ ] Unique (pas de doublon dans la base)
- [ ] Accrocheur (pas generique)

### Meta Description (10 points)
- [ ] Longueur entre 120-160 caracteres
- [ ] Contient le mot-cle principal
- [ ] Inclut un CTA implicite
- [ ] Unique

### Headings (15 points)
- [ ] Un seul H1
- [ ] H2/H3 hierarchiques (pas de saut)
- [ ] Mots-cles dans au moins 1 H2
- [ ] Nombre de H2 > 2

### Contenu (20 points)
- [ ] Longueur > 800 mots
- [ ] Densite mot-cle principal: 1-3%
- [ ] Readability score (Flesch) > 60
- [ ] Pas de paragraphes > 300 mots sans sous-titre
- [ ] Utilise des listes / tableaux

### Images (10 points)
- [ ] Au moins 1 image
- [ ] Toutes les images ont un alt tag descriptif
- [ ] Featured image presente
- [ ] Format optimise (WebP/AVIF)

### Liens (15 points)
- [ ] Au moins 2 liens internes
- [ ] Au moins 1 lien externe (source fiable)
- [ ] Pas de liens casses
- [ ] Anchor text descriptif (pas "cliquez ici")

### Technique (15 points)
- [ ] URL slug propre et SEO-friendly
- [ ] Canonical URL definie
- [ ] JSON-LD Article schema present
- [ ] OG tags complets (title, description, image, type)
- [ ] Twitter Card meta presentes

## Output
- Score global /100 avec detail par critere
- Liste des problemes avec severite
- Suggestions de correction AI pour chaque probleme
- Possibilite d'appliquer les corrections automatiquement

Ecris les resultats dans le champ `seoData` de l'article en base
et dans un `SeoAudit` record.
