# Estándar Jekyll: `_includes`, tema y SEO (post-coderic.io)

Referencia para portales del ecosistema Coderic que usan `remote_theme: Coderic/jekyll-theme-coderic`.

## Head y subnavegación

- Por defecto **no** versionar en el sitio `_includes/head.html` ni `_includes/subnav.html`: el tema los resuelve vía `remote_theme`.
- Si un portal necesita comportamiento exclusivo, **priorizar** subir el cambio al **tema** (un solo lugar, menos deriva). Los overrides locales solo con acuerdo explícito del equipo.
- Objetivo: **cero** `_includes/subnav.html` y **cero** `_includes/head.html` en portales salvo acuerdo explícito; la navegación de sección se define en `_data/<lang>/subnav.yml` y el include lo aporta el tema.

## Migas y fragmentos

- Si el tema no expone un partial para migas, el patrón acordado es **inlinar** el bloque Liquid/HTML en cada página de sección (evita `_includes` dedicados solo al portal).

## SEO, `<title>` y Polyglot

- El tema incluye **`sitemap.xml`** (Liquid): genera **`/sitemap.xml`** con **una URL por cada idioma** en `site.languages` (compatible con jekyll-polyglot; `jekyll-sitemap` solo repetía la URL del idioma por defecto). Cada portal debe fijar **`url`** (y **`baseurl`** si aplica) en `_config.yml`. Buenas prácticas: [Google Search Central](https://developers.google.com/search/docs?hl=es-419).
- `robots.txt` del tema (Liquid) incluye **`Sitemap: {url}/sitemap.xml`** en producción; no hace falta un `robots.txt` estático en el portal salvo reglas `Disallow` extra acordadas.
- Páginas que no deben indexarse: front matter **`sitemap: false`** (en el tema, `callback`, `profile` y `hello-world` lo declaran en su front matter).
- **`_includes/seo_resolve.html`** (tema) unifica `<title>` / meta description para: `page.net_page`, `page.i18n_source`, `page.i18n`, `page.pages_data_key` / secciones `organization` · `impact` · `governance`, y fallbacks.
- Objetivo: **cero** `_includes/head.html` en portales; cambios compartibles van al tema.

## Resumen

| Preferencia | Evitar |
|-------------|--------|
| Tema como fuente de head/subnav/sitemap/robots | Copias locales de head/subnav sin necesidad; `robots.txt` estático duplicado |
| PR al tema para cambios compartibles | Divergencia silenciosa entre portales |
| Migas inlinadas si no hay partial en tema | Includes de migas solo por un portal |
| `url` correcto en `_config.yml` | Sitemap/canonical/OG con host vacío o incorrecto |
