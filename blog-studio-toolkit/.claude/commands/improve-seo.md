# Ameliorer le SEO Global

Analyse et ameliore le SEO technique du projet Blog Studio.

## Actions

### 1. Structured Data
- Verifie que chaque page publique a son JSON-LD
- Types: Article, BreadcrumbList, WebSite, Organization
- Verifie avec le schema Google (schema.org)

### 2. Sitemap
- Verifie que le sitemap XML est genere dynamiquement
- Inclut toutes les pages publiees avec priorites correctes
- lastmod correspond a la date de derniere modification reelle

### 3. Robots.txt
- Verifie que robots.txt est correct
- Bloque: /api/, /(dashboard)/, /editor/
- Autorise: /(blog)/, /sitemap.xml

### 4. Meta Tags
- Verifie chaque layout.tsx pour les meta par defaut
- Verifie les generateMetadata() dynamiques
- Verifie les OG images (taille 1200x630)

### 5. Performance SEO
- Verifie les images: next/image, lazy loading, srcset
- Verifie le SSG/ISR sur les pages blog
- Verifie les Core Web Vitals (bundle size, fonts, CSS)

### 6. Maillage Interne
- Verifie le composant de liens internes automatiques
- Verifie l'algorithme de suggestion (tags, categories, similarite)
- Verifie les breadcrumbs avec schema markup

## Output
Pour chaque point, indique: OK / A CORRIGER / MANQUANT
Corrige automatiquement ce qui peut l'etre.
Cree des issues dans AUDIT_TRACKER.md pour le reste.
