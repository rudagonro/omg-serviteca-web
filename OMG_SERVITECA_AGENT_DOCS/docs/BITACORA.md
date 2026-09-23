# BITÁCORA DE DESARROLLO, OMG SERVITECA

Este archivo mantiene continuidad entre Codex, Claude Code y futuras sesiones.

## Estados
- [ ] Pendiente
- [~] En curso
- [x] Terminado y validado
- [!] Bloqueado

## Tareas actuales

- [x] Auditar técnicamente el Home actual antes de modificarlo. Ver `docs/AUDITORIA_HOME.md`.
- [x] Mapear secciones actuales contra la nueva arquitectura UX. Ver `docs/AUDITORIA_HOME.md` §3.
- [!] Reorganizar el Home según `OMG_UX_REDESIGN.md`. Bloqueado: falta que el usuario decida entre Opción A/B de `docs/AUDITORIA_HOME.md` §5 (Ubicación/Blog: ¿fusionar en el Home o mantener como vistas separadas con mejor acceso?).
- [ ] Mejorar tarjetas de servicios y sus acciones.
- [ ] Crear la sección “¿Qué le pasa a tu vehículo?”.
- [ ] Integrar esa orientación con servicios, WhatsApp y OSCAR cuando aplique.
- [x] Reubicar “Deja tu opinión” fuera del recorrido comercial principal. Ahora vive en un modal (`#reviewModal`), disparado por un botón secundario en `reviews-sec` ("¿Ya eres cliente de OMG?..."). `reviews-sec` solo muestra testimonios.
- [x] Revisar jerarquía de CTA de agendamiento. Se agregó "📅 Agendar Cita" (`.cta-ban-primary`, `btn-g`) como acción principal en el banner CTA, distinta de Llamar/WhatsApp/Cómo llegar (secundarias).
- [ ] Revisar convivencia entre OSCAR y WhatsApp.
- [x] Revisar ubicación, horarios, mapa y CTA “Cómo llegar”. Se agregó mapa embebido (Google Maps `output=embed`, sin API key, con filtro dark-mode) y botón "Cómo llegar" (link de direcciones) en la vista Contacto y en el banner CTA del Home.
- [x] Revisar responsive en móvil, tablet y escritorio (para los 3 cambios de esta sesión). Verificado en 375px: sin overflow horizontal en modal, banner CTA ni mapa. Pendiente revisar el resto del sitio cuando se aborde la Fase 3 completa.
- [ ] Revisar SEO, accesibilidad y rendimiento.
- [ ] Ejecutar QA final.
- [ ] Registrar build, pruebas, commit y estado final.
- [x] Auditar procedencia y licencia de las imágenes `img-01` a `img-16`, los logos y el personaje Oscar. Resuelto 2026-09-22: son generadas con IA a partir de tomas reales del negocio, propiedad de OMG Serviteca. No aplica licencia de terceros. Ver `IMAGENES-Y-LICENCIAS.md`.
- [ ] Reclamar la ficha de Google Business Profile ("Serviteca OMG") y, una vez verificada: corregir el nombre a "OMG Serviteca", la dirección (la ficha muestra 17-57, incorrecta) y enlazar `https://omgserviteca.com`. Sin arrancar aún.
- [ ] Conseguir y publicar los perfiles reales de Facebook, Instagram y TikTok del negocio (se retiraron placeholders genéricos del footer). Sin arrancar aún.

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
- **Imágenes**: las 16 fotos del taller viven en `images/` (extraídas de los `<img>` en base64 del HTML original) y ya están recomprimidas (JPG calidad 65 + PNG optimizado, ~13% menos peso). Licencia/procedencia resuelta: generadas con IA a partir de tomas reales, propiedad de OMG Serviteca (ver `IMAGENES-Y-LICENCIAS.md`).
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

### 2026-09-22, resolución de licencias + Fase 1 y 2 del rediseño (auditoría técnica y mapeo)
Agente: Claude Code

Tarea:
Cerrar la auditoría de licencias de imágenes con la aclaración del cliente, y ejecutar las Fases 1 y 2 de `OMG_UX_REDESIGN.md` (auditoría técnica del Home actual + mapeo contra el recorrido propuesto).

Cambios:
- `IMAGENES-Y-LICENCIAS.md`: cerrado. Las imágenes son generadas con IA a partir de tomas reales del negocio; OMG Serviteca es titular, no aplica licencia de terceros.
- Nuevo `docs/AUDITORIA_HOME.md`: mapea la estructura real del `index.html` (arquitectura de "vistas" por JS, no framework) contra el recorrido de `OMG_UX_REDESIGN.md`, con hallazgos concretos (formulario de reseñas embebido en medio de testimonios, sin mapa embebido en ningún lado, Ubicación y Blog viven en vistas separadas del Home no en el scroll principal, sin acción "Agendar cita" propia, OSCAR ya tiene chips rápidos existentes).

Archivos:
- `IMAGENES-Y-LICENCIAS.md`
- `docs/BITACORA.md`
- `docs/AUDITORIA_HOME.md` (nuevo)

Pruebas:
- Lectura completa de `index.html` (secciones, vistas, nav, OSCAR, formularios) para verificar cada hallazgo contra el código real, no contra supuestos del plan.

Resultado:
Fases 1 y 2 completas. La Fase 3 (reorganización estructural) queda **bloqueada** hasta que el usuario elija entre las opciones A/B descritas en `docs/AUDITORIA_HOME.md` §5 sobre cómo integrar Ubicación y Blog al recorrido del Home.

Pendientes:
- Decisión de arquitectura (§5 del audit) antes de tocar la estructura del Home.
- Mientras tanto, hay 3 cambios de bajo riesgo que no dependen de esa decisión y pueden hacerse ya (listados al final de `docs/AUDITORIA_HOME.md` §6): sacar el formulario de reseñas del scroll principal, agregar mapa embebido en Contacto, diferenciar "Agendar cita" como acción propia en el CTA banner.

Commit:
Ver commit de esta sesión en `git log`.

---

### 2026-09-22, Fase 3 (parcial): cambios de bajo riesgo del Home
Agente: Claude Code

Tarea:
Implementar los 3 cambios de `docs/AUDITORIA_HOME.md` §6 que no dependen de la decisión de arquitectura (Ubicación/Blog), mientras esa decisión sigue pendiente del usuario.

Cambios:
- Formulario "Deja tu Opinión" sacado del scroll principal: ahora vive en un modal (`#reviewModal`, funciones `openReviewModal()`/`closeReviewModal()`), disparado por un botón secundario en `reviews-sec`. La sección de testimonios ya no compite visualmente con un formulario siempre visible.
- "Agendar Cita" agregado como acción propia y de mayor jerarquía en el banner CTA del Home (`.cta-ban-primary`), separada de Llamar/WhatsApp/Cómo llegar.
- Mapa embebido (Google Maps `output=embed`, sin API key, con filtro dark-mode a tono con la marca) + botón "Cómo llegar" (enlace de direcciones) agregados en la vista Contacto y en el banner CTA del Home.

Archivos:
- `index.html`

Pruebas:
- Servidor estático local, verificado en navegador: modal abre/cierra, estrellas y envío por WhatsApp siguen funcionando, `navGo('contact')` desde "Agendar Cita" funciona, mapa carga (confirmado visualmente, con tema oscuro), enlaces "Cómo llegar" apuntan a Google Maps Directions con la dirección oficial.
- Sin errores de consola.
- Responsive en 375px: sin scroll horizontal en modal, banner CTA ni mapa/Contacto.
- Nota para el próximo agente: la vista previa de este entorno tiene un bug conocido — a veces muestra pantallas en negro o capturas desactualizadas con contenido embebido/lazy (mapas, imágenes), aunque el contenido real carga bien. Verificar con lectura de `window.scrollY`, `getBoundingClientRect()` o consola antes de asumir que algo está roto.

Resultado:
3 de 3 cambios de bajo riesgo completados y probados. La Fase 3 completa (reorganización estructural: Ubicación/Blog dentro del Home, nueva sección "¿Qué le pasa a tu vehículo?", tarjetas de servicio, OSCAR) sigue bloqueada/pendiente.

Pendientes:
- Decisión de arquitectura (`docs/AUDITORIA_HOME.md` §5) para continuar con Ubicación/Blog.
- Fase 4 (nueva sección "¿Qué le pasa a tu vehículo?"), Fase 5 (refinamiento visual), Fase 6 (QA final) siguen sin empezar.
- Revisar convivencia OSCAR/WhatsApp y accesibilidad/SEO del sitio completo (no solo de los 3 cambios de esta sesión).

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
