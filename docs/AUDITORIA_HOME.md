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
| CTA de agendamiento | Existe como banner, pero sin "Agendar cita" como acción propia ni "Cómo llegar". |
| Ubicación, horarios y mapa | **Vive en una vista separada (`Contacto`), no en el Home.** No hay mapa embebido, solo un link de texto. |
| Blog | **Vive en una vista separada, no en el Home.** |
| Footer | Existe. |

## 4. Hallazgos

1. **Confirmado**: el formulario "Deja tu Opinión" está embebido de forma permanente dentro de la sección de testimonios, compitiendo visualmente con la prueba social justo antes de llegar al CTA de conversión — exactamente el problema que describe la sección 9 del plan.
2. **Confirmado**: no hay mapa embebido en ningún lado del sitio, solo un enlace de texto a la ficha de Google Maps. La sección 13 del plan pide mostrar mapa explícitamente.
3. **Nuevo hallazgo, no estaba en el plan**: Ubicación/horarios/mapa y Blog no son secciones del Home — son vistas aparte a las que solo se llega por el menú. Implementar el recorrido tal cual está escrito requiere una decisión de arquitectura (ver sección 5).
4. **Nuevo hallazgo**: OSCAR ya tiene accesos rápidos (chips: Servicios, Horario, Turno, Ubicación, ¿Tienen garantía?, Cambio de aceite) — no hay que construirlos desde cero, solo revisar si conviene ajustarlos a los que sugiere el plan (Quiero agendar / Mi carro tiene una falla / Quiero cotizar / Quiero conocer los servicios) o dejarlos como están.
5. **Nuevo hallazgo**: no existe una acción "Agendar cita" independiente en el Home — todo el agendamiento actual pasa por WhatsApp directo (Hero, CTA banner) o por el formulario completo que solo vive en la vista Contacto. El plan pide que "Agendar cita" tenga la mayor jerarquía como su propia acción.
6. Los datos de contacto (dirección, teléfono, correo, WhatsApp, horario) son consistentes entre Footer y vista Contacto — no hay discrepancias que corregir ahí.

## 5. Decisión pendiente antes de la Fase 3 (reorganización estructural)

Hay dos caminos válidos y NO es una decisión técnica sino de producto — la dejo para el usuario:

**Opción A — Fusionar en el Home.** Traer una versión resumida de Ubicación (mapa + horario + "Cómo llegar") y una vista previa de 2-3 artículos del Blog dentro del scroll del Home, antes del Footer, tal como lo describe el plan literalmente. El botón "Blog" del menú pasaría a ser un anclaje al Home en vez de una vista aparte (o se mantiene la vista completa del Blog para "ver todos los artículos").

**Opción B — Mantener como vistas separadas, pero con accesos más visibles.** Dejar Contacto y Blog como están (vistas propias), y en su lugar reforzar los CTA "Cómo llegar" y "Ver blog" dentro del CTA banner del Home, sin duplicar contenido. Menos trabajo, menos riesgo de romper algo que ya funciona (SEO de esas páginas, por ejemplo — aunque son vistas JS, no URLs distintas, así que no hay impacto de indexación real en ningún caso).

Mi recomendación: **Opción B** para el mapa/ubicación (agregar el mapa embebido y "Cómo llegar" directamente en la vista Contacto, que ya visita quien busca esa información) y **Opción A ligera** solo para el Blog (2-3 tarjetas de preview antes del footer del Home, enlazando a la vista Blog completa) — es el balance más cercano a la intención del plan sin reescribir la navegación del sitio.

## 6. Siguiente paso

Con esta auditoría lista, la Fase 3 (reorganización estructural) puede empezar en cuanto se resuelva la decisión de la sección 5. Mientras tanto, hay cambios de bajo riesgo que no dependen de esa decisión y se pueden hacer ya:
- Sacar el formulario de reseñas del scroll principal (dejar solo los testimonios en `reviews-sec`; mover el formulario a un modal o acción secundaria "¿Ya eres cliente? Cuéntanos tu experiencia").
- Agregar mapa embebido + "Cómo llegar" en la vista Contacto.
- Diferenciar "Agendar cita" como acción propia en el CTA banner (hoy solo hay Llamar/WhatsApp).
