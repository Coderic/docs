# Estándar Jekyll: `_includes`, tema y SEO (post-coderic.io)

Referencia para portales del ecosistema Coderic que usan `remote_theme: Coderic/jekyll-theme-coderic`.

## Head y subnavegación

- Por defecto **no** versionar en el sitio `_includes/head.html` ni `_includes/subnav.html`: el tema los resuelve vía `remote_theme`.
- Si un portal necesita comportamiento exclusivo, **priorizar** subir el cambio al **tema** (un solo lugar, menos deriva). Los overrides locales solo con acuerdo explícito del equipo.
- Objetivo: **cero** `_includes/subnav.html` y **cero** `_includes/head.html` en portales salvo acuerdo explícito; la navegación de sección se define en `_data/<lang>/subnav.yml` y el include lo aporta el tema.

## Migas y fragmentos

- Si el tema no expone un partial para migas, el patrón acordado es **inlinar** el bloque Liquid/HTML en cada página de sección (evita `_includes` dedicados solo al portal).

## SEO, `<title>` y Polyglot

- Con el `head` del tema, el `<title>` suele seguir la lógica del tema (`page.title | default: site.portal_name`, etc.).
- Títulos y descripciones **por idioma desde `_data`** requieren **extender el `head` del tema** (p. ej. condicionales con datos de página o `meta` en `ui.yml`) **o** aceptar el nombre del portal como fallback hasta un PR al tema.
- Añadir bloques `meta` en `ui.yml` por idioma sirve como **preparación**; solo mejoran SEO cuando el tema (o front matter por página) los consumen.

## Resumen

| Preferencia | Evitar |
|-------------|--------|
| Tema como fuente de head/subnav | Copias locales de head/subnav sin necesidad |
| PR al tema para cambios compartibles | Divergencia silenciosa entre portales |
| Migas inlinadas si no hay partial en tema | Includes de migas solo por un portal |
