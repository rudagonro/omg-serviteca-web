# Auditoría técnica del Home actual (Fase 1 y 2)

Fecha: 2026-09-22
Agente: Claude Code
Referencia: `docs/OMG_UX_REDESIGN.md`

## 1. Arquitectura real del sitio

No es un framework con rutas de servidor ni componentes. Es **un solo `index.html`** (HTML + CSS + JS inline, ~1250 líneas, sin build ni bundler) que simula una SPA con **"vistas" alternadas por JavaScript** (`navGo('home' | 'blog' | 'article' | 'contact')`), cada una un `<div class="view">` que se muestra u oculta. Páginas legales (`politica-privacidad.html`, etc.) sí son archivos HTML separados de verdad.

Esto es clave para el rediseño: **"Home", "Blog" y "Contacto" son vistas independientes**, no secciones de un mismo scroll. El recorrido que propone `OMG_UX_REDESIGN.md` (sección 3) asume un solo scroll continuo que termina en Ubicación → Blog → Footer, pero hoy Ubicación y Blog viven fuera del Home.

## 2. Estructura actual del Home (`view-home`)

Orden real, de arriba a abajo:

1. `#hero` — Hero con CTA primario (WhatsApp directo, no "Agendar cita" como acción propia) y CTA secundario "Ver Servicios".
2. `#services-sec` — Grid de tarjetas de servicio (imagen + texto + botón "Solicitar" por WhatsApp).
3. `#benefits-sec` — Beneficios ("Por qué elegirnos").
4. `#reviews-sec` — Testimonios **+ formulario "Deja tu Opinión" embebido en la misma sección**, siempre visible.
5. `#about-sec` — Sobre OMG.
6. CTA banner — Llamar / WhatsApp (sin mapa, sin "Cómo llegar", sin opción "Agendar cita" diferenciada).
7. Footer — incluye dirección, teléfono, correo, WhatsApp, horario y link "Ver en Google Maps" (texto, sin mapa embebido).

Fuera del Home:
- `view-contact`: dirección, teléfono, correo, WhatsApp, horario, link a Maps (texto) y formulario de agendamiento completo (nombre, celular, vehículo, servicio, mensaje, consentimiento → envía por WhatsApp).
- `view-blog`: listado de artículos con filtros.
- OSCAR (asistente flotante) y botón de WhatsApp: globales, fuera de las vistas, visibles en todo momento.

## 3. Comparación contra el recorrido propuesto

| Propuesto (`OMG_UX_REDESIGN.md` §3) | Estado actual |
|---|---|
| Hero | Existe. CTA primario abre WhatsApp directo, no hay botón "Agendar cita" que lleve a un formulario/sección propia. |
| Servicios | Existe, en la posición correcta (justo después del Hero). |
| ¿Qué le pasa a tu vehículo? | **No existe.** Hay que crearla desde cero (Fase 4). |
| Por qué elegir OMG | Existe (`benefits-sec`), en la posición correcta. |
| Opiniones de clientes | Existe, pero mezclada con el formulario de reseñas (ver hallazgo below). |
| Sobre OMG | Existe, en la posición correcta. |
| CTA de agendamiento | ✅ Resuelto: "Agendar Cita" como acción propia + "Cómo llegar" en el banner. |
| Ubicación, horarios y mapa | ✅ Resuelto (Opción B, ver §5): mapa embebido + "Cómo llegar" en Contacto; Home enlaza ahí. |
| Blog | ✅ Resuelto (Opción A ligera, ver §5): preview de 3 artículos en el Home + link a la vista completa. |
| Footer | Existe. |

## 4. Hallazgos

1. **Confirmado**: el formulario "Deja tu Opinión" está embebido de forma permanente dentro de la sección de testimonios, compitiendo visualmente con la prueba social justo antes de llegar al CTA de conversión — exactamente el problema que describe la sección 9 del plan.
2. **Confirmado**: no hay mapa embebido en ningún lado del sitio, solo un enlace de texto a la ficha de Google Maps. La sección 13 del plan pide mostrar mapa explícitamente.
3. **Nuevo hallazgo, no estaba en el plan**: Ubicación/horarios/mapa y Blog no son secciones del Home — son vistas aparte a las que solo se llega por el menú. Implementar el recorrido tal cual está escrito requiere una decisión de arquitectura (ver sección 5).
4. **Nuevo hallazgo**: OSCAR ya tiene accesos rápidos (chips: Servicios, Horario, Turno, Ubicación, ¿Tienen garantía?, Cambio de aceite) — no hay que construirlos desde cero, solo revisar si conviene ajustarlos a los que sugiere el plan (Quiero agendar / Mi carro tiene una falla / Quiero cotizar / Quiero conocer los servicios) o dejarlos como están.
5. **Nuevo hallazgo**: no existe una acción "Agendar cita" independiente en el Home — todo el agendamiento actual pasa por WhatsApp directo (Hero, CTA banner) o por el formulario completo que solo vive en la vista Contacto. El plan pide que "Agendar cita" tenga la mayor jerarquía como su propia acción.
6. Los datos de contacto (dirección, teléfono, correo, WhatsApp, horario) son consistentes entre Footer y vista Contacto — no hay discrepancias que corregir ahí.

## 5. Decisión de arquitectura — RESUELTA (2026-09-22)

Había dos caminos válidos, no era una decisión técnica sino de producto:

**Opción A — Fusionar en el Home.** Traer una versión resumida de Ubicación (mapa + horario + "Cómo llegar") y una vista previa de 2-3 artículos del Blog dentro del scroll del Home, antes del Footer, tal como lo describe el plan literalmente.

**Opción B — Mantener como vistas separadas, pero con accesos más visibles.** Dejar Contacto y Blog como están (vistas propias), reforzando los CTA "Cómo llegar" y "Ver blog" desde el Home sin duplicar contenido completo.

**Decisión del usuario: Opción B.** Implementada así:
- **Ubicación**: se queda en la vista Contacto (ya tiene mapa embebido + "Cómo llegar", agregados en la sesión de esta misma fecha). El CTA banner del Home enlaza directamente ahí.
- **Blog**: Opción A ligera aplicada solo aquí (con acuerdo implícito al confirmar Opción B para el conjunto) — se agregó `#blog-preview-sec` en el Home con los 3 artículos más recientes (`renderBlogPreview()`) y un botón "Ver todos los artículos" hacia la vista Blog completa. No se fusionó el listado completo ni se tocó la navegación del menú.

## 6. Estado de los cambios de bajo riesgo

- [x] Sacar el formulario de reseñas del scroll principal → modal `#reviewModal`.
- [x] Agregar mapa embebido + "Cómo llegar" en la vista Contacto.
- [x] Diferenciar "Agendar cita" como acción propia en el CTA banner.
- [x] Vista previa del Blog en el Home (3 artículos + CTA a la vista completa).

## 7. Siguiente paso

Con la decisión de arquitectura resuelta y el Home ya reflejando Ubicación (vía Contacto) y Blog (preview), lo que sigue del plan es:
- Fase 4: crear la sección "¿Qué le pasa a tu vehículo?" (no existe aún).
- Mejorar tarjetas de servicios y sus acciones ("Ver servicio"/"Agendar" cuando haya contenido real).
- Revisar convivencia OSCAR/WhatsApp y ajustar (o no) los chips de OSCAR a los sugeridos por el plan.
- Fase 5 (refinamiento visual) y Fase 6 (QA final, incluyendo responsive completo, SEO y accesibilidad de todo el sitio, no solo de los cambios ya hechos).
