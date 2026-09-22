# BITÁCORA DE DESARROLLO, OMG SERVITECA

Este archivo mantiene continuidad entre Codex, Claude Code y futuras sesiones.

## Estados
- [ ] Pendiente
- [~] En curso
- [x] Terminado y validado
- [!] Bloqueado

## Tareas actuales

- [ ] Auditar técnicamente el Home actual antes de modificarlo.
- [ ] Mapear secciones actuales contra la nueva arquitectura UX.
- [ ] Reorganizar el Home según `OMG_UX_REDESIGN.md`.
- [ ] Mejorar tarjetas de servicios y sus acciones.
- [ ] Crear la sección “¿Qué le pasa a tu vehículo?”.
- [ ] Integrar esa orientación con servicios, WhatsApp y OSCAR cuando aplique.
- [ ] Reubicar “Deja tu opinión” fuera del recorrido comercial principal.
- [ ] Revisar jerarquía de CTA de agendamiento.
- [ ] Revisar convivencia entre OSCAR y WhatsApp.
- [ ] Revisar ubicación, horarios, mapa y CTA “Cómo llegar”.
- [ ] Revisar responsive en móvil, tablet y escritorio.
- [ ] Revisar SEO, accesibilidad y rendimiento.
- [ ] Ejecutar QA final.
- [ ] Registrar build, pruebas, commit y estado final.
- [ ] Auditar procedencia y licencia de las imágenes `img-01` a `img-16`, los logos y el personaje Oscar (ver `IMAGENES-Y-LICENCIAS.md`). Reemplazar por material propio o con licencia verificable donde no haya evidencia.
- [ ] Reclamar la ficha de Google Business Profile ("Serviteca OMG") y, una vez verificada: corregir el nombre a "OMG Serviteca", la dirección (la ficha muestra 17-57, incorrecta) y enlazar `https://omgserviteca.com`.
- [ ] Conseguir y publicar los perfiles reales de Facebook, Instagram y TikTok del negocio (se retiraron placeholders genéricos del footer).

## Decisiones confirmadas

### Dirección oficial
Cra. 1 N.º 17-47, Variante, Chía.

No modificarla basándose en directorios externos. La ficha de Google Business Profile actual muestra "17-57" — está mal, no usarla como referencia hasta corregirla.

### Git
La rama de trabajo compartida será `master`, salvo instrucción expresa del usuario. El repositorio remoto (`origin`) solo tiene `master`; no existe `main`.

### Continuidad
Codex y Claude Code pueden alternarse. Cada agente debe sincronizar el repositorio antes de trabajar y actualizar esta bitácora antes de terminar.

### Infraestructura y estado ya construido (no repetir ni deshacer)
- **Hosting**: Cloudflare Pages, proyecto `omg-serviteca-web`, despliegue automático desde `master`. Dominio propio `omgserviteca.com` comprado y conectado (Cloudflare Registrar), con `www.omgserviteca.com` como dominio adicional.
- **Redirects/SEO técnico**: regla 301 `www` → raíz (preserva query string), `<link rel="canonical">` a `https://omgserviteca.com/`, `robots.txt` y `sitemap.xml` (4 URLs: home + 3 páginas legales) en la raíz, `_headers` con cache rules.
- **Favicon / previews**: `favicon.ico` + variantes PNG, `apple-touch-icon`, y `images/og-image.jpg` (1200×630) para que WhatsApp y redes muestren vista previa con logo.
- **Contacto**: correo `omgtres@hotmail.com` visible en footer y en Contáctanos (enlace `mailto:`).
- **Imágenes**: las 16 fotos del taller viven en `images/` (extraídas de los `<img>` en base64 del HTML original) y ya están recomprimidas (JPG calidad 65 + PNG optimizado, ~13% menos peso). Pendiente sin resolver: licencia/procedencia (ver tarea arriba).
- **Google Search Console**: propiedad de dominio `sc-domain:omgserviteca.com` verificada por TXT en DNS. Sitemap enviado y en estado "Correcto". Al 17-sep-2026: 2 de 4 páginas indexadas (home y `politica-cookies`); `politica-privacidad` y `terminos-condiciones` aún no. Hay una tarea programada local (`check-omgserviteca-full-indexing`, diaria) que revisa el avance automáticamente.
- **Google Maps / Business Profile**: existe una ficha real "Serviteca OMG" (3.8★, 17 reseñas) sin reclamar, sin sitio web enlazado, y con la dirección mal escrita (17-57). El sitio ya enlaza hacia esa ficha (footer, Contacto, y `hasMap`/`sameAs` en el JSON-LD de schema.org) para reforzar la señal, a la espera de que se reclame formalmente.
- **Redes sociales**: se quitaron del footer los botones de Facebook/Instagram/TikTok porque apuntaban a las páginas genéricas de esas plataformas, no a perfiles reales del negocio. No agregarlos de nuevo sin URLs reales confirmadas.
- **Netlify**: el despliegue original (`omgserviteca.netlify.app`) está deshabilitado ("Disable project", reversible) pero no borrado — es el respaldo previo a Cloudflare.
- **Stack**: sitio estático puro. `index.html` (todo el HTML/CSS/JS del Home inline, sin build ni framework) + páginas legales sueltas (`politica-privacidad.html`, `politica-cookies.html`, `terminos-condiciones.html`, con `legal.css` compartido). No hay `package.json`, bundler ni paso de build/lint que ejecutar — "ejecutar build/lint" en `AGENTS.md` no aplica literalmente aquí; validar cambios abriendo el HTML/sirviéndolo estáticamente y revisando en navegador.

## Registro de sesiones

### 2026-09-20, preparación UX
Agente: ChatGPT

Estado:
Se realizó auditoría conceptual del recorrido comercial del Home y se definió una nueva arquitectura UX.

Documentos preparados:
- `AGENTS.md`
- `CLAUDE.md`
- `docs/OMG_UX_REDESIGN.md`
- `docs/BITACORA.md`

Pendiente:
Implementación en el repositorio y validación técnica sobre el código real.

---

### 2026-09-22, activación del paquete de coordinación y feedback
Agente: Claude Code

Tarea:
Revisar el paquete `OMG_SERVITECA_AGENT_DOCS/` (preparado por ChatGPT), dar feedback y activarlo.

Cambios:
- Corregido bug de rama: `AGENTS.md`, `CLAUDE.md` y esta bitácora referenciaban `main`, pero el repositorio solo tiene `master`. Reemplazado en los tres archivos.
- Copiados `AGENTS.md`, `CLAUDE.md`, `docs/OMG_UX_REDESIGN.md` y `docs/BITACORA.md` a la raíz del repositorio (antes solo existían dentro de `OMG_SERVITECA_AGENT_DOCS/`, sin trackear en Git).
- Agregada la sección "Infraestructura y estado ya construido" arriba, con todo lo ya resuelto (hosting, dominio, SEO técnico, Search Console, Google Business Profile, imágenes, Netlify) para que ningún agente lo repita o lo revierta sin saberlo.
- Agregadas 3 tareas pendientes reales que no estaban en la lista: licencias de imágenes, reclamo de Google Business Profile, redes sociales reales.

Archivos:
- `AGENTS.md`, `CLAUDE.md`, `docs/BITACORA.md`, `docs/OMG_UX_REDESIGN.md` (nuevos en la raíz)
- `OMG_SERVITECA_AGENT_DOCS/AGENTS.md`, `OMG_SERVITECA_AGENT_DOCS/CLAUDE.md`, `OMG_SERVITECA_AGENT_DOCS/docs/BITACORA.md` (corregidos en el paquete original)

Pruebas:
- `git branch -a` para confirmar que solo existe `master`.
- Lectura manual de los 5 archivos del paquete y verificación cruzada contra el estado real del repo (`git log`, DNS/Cloudflare, Search Console).

Resultado:
Paquete de coordinación activo en la raíz del repo. El rediseño UX de `docs/OMG_UX_REDESIGN.md` sigue pendiente de implementación (fase 1: auditoría técnica del Home actual).

Pendientes:
Ver "Tareas actuales" arriba. La carpeta `OMG_SERVITECA_AGENT_DOCS/` se dejó intacta como referencia; su contenido ya vive en las rutas finales.

Commit:
Ver commit de esta sesión en `git log`.

---

## Plantilla para nuevas sesiones

### AAAA-MM-DD, título breve
Agente: Codex / Claude Code / otro

Tarea:
Descripción.

Cambios:
- ...

Archivos:
- ...

Pruebas:
- ...

Resultado:
- ...

Pendientes:
- ...

Commit:
`HASH mensaje`
