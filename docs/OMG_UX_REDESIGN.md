# OMG SERVITECA
## Plan maestro de reorganización UX, arquitectura de información y conversión

Versión: 1.1
Sitio: www.omgserviteca.com

## 1. Objetivo
Reorganizar la experiencia del Home para que el visitante entienda qué hace OMG, encuentre el servicio que necesita, reciba orientación si desconoce la falla y llegue rápidamente a agendamiento o contacto.

No realizar un rebranding ni reconstruir el sitio sin necesidad.

## 2. Antes de editar
Leer `AGENTS.md` y `docs/BITACORA.md`.
Analizar stack, rutas, componentes, estilos, assets, formularios, SEO, analítica, WhatsApp y OSCAR.
Ejecutar el proyecto localmente si el entorno lo permite.
Reutilizar componentes existentes.
No inventar datos comerciales.

Dirección oficial confirmada:
Cra. 1 N.º 17-47, Variante, Chía.

## 3. Recorrido propuesto
HERO
↓
SERVICIOS
↓
¿QUÉ LE PASA A TU VEHÍCULO?
↓
POR QUÉ ELEGIR OMG
↓
OPINIONES DE CLIENTES
↓
SOBRE OMG
↓
CTA DE AGENDAMIENTO
↓
UBICACIÓN, HORARIOS Y MAPA
↓
BLOG
↓
FOOTER

WhatsApp debe permanecer accesible. OSCAR debe complementar el recorrido.

## 4. Hero
Mantener la propuesta “Expertos en cuidar tu vehículo” si sigue siendo el contenido oficial.
CTA principal: “Agenda tu cita”.
CTA secundario: “Ver servicios”.
El CTA secundario debe llevar a Servicios mediante navegación clara.

## 5. Servicios
Debe aparecer inmediatamente después del Hero.
Mantener los servicios oficiales existentes.
Las tarjetas deben ser accionables. Cuando exista contenido real, permitir “Ver servicio” y “Agendar”.
No crear páginas vacías.

## 6. Nueva sección, ¿Qué le pasa a tu vehículo?
Crear una experiencia para usuarios que conocen el síntoma pero no el nombre del servicio.

Opciones iniciales:
- Hace un ruido extraño.
- Se encendió un testigo.
- Vibra al conducir.
- Se va hacia un lado.
- El aire no enfría.
- Tiene problemas al frenar.
- Necesita mantenimiento.
- No sé qué tiene.

Orientar, no afirmar diagnósticos definitivos.
Relacionar cada selección con servicios existentes, OSCAR, WhatsApp o agendamiento.

## 7. Por qué elegir OMG
Ubicar beneficios después de Servicios y orientación por síntomas.
Usar información verificable existente.
No inventar certificaciones, cifras o garantías.

## 8. Opiniones
Mantener testimonios reales.
La sección debe aportar confianza antes del CTA comercial.

## 9. Deja tu opinión
Sacar el formulario del recorrido principal del prospecto.
Mantenerlo accesible mediante una acción secundaria como:
“¿Ya eres cliente de OMG? Cuéntanos tu experiencia”.
Puede abrir modal, sección secundaria o ruta existente según la arquitectura.

## 10. Sobre OMG
Ubicar después de servicios, beneficios y testimonios.
Priorizar fotografías reales.
Mantener el contenido institucional breve en Home.

## 11. CTA de conversión
Crear una sección clara después de generar confianza.
Acciones:
- Agendar cita.
- Hablar por WhatsApp.
- Cómo llegar.

“Agendar cita” debe tener la mayor jerarquía.

## 12. OSCAR
Presentar accesos rápidos cuando la implementación actual lo permita:
- Quiero agendar.
- Mi carro tiene una falla.
- Quiero cotizar.
- Quiero conocer los servicios.

OSCAR no debe competir visualmente con WhatsApp ni emitir diagnósticos definitivos.

## 13. Ubicación
Mostrar dirección, horarios, teléfono, WhatsApp, mapa y “Cómo llegar”.
Evaluar lazy loading del mapa.

## 14. Blog
Ubicar hacia el final del Home.
Mostrar pocos artículos relevantes y un CTA hacia el contenido completo.

## 15. Header y navegación
Priorizar una navegación corta.
Ejemplo conceptual:
Inicio, Servicios, Nosotros, Blog, Contacto, Agendar cita.
Adaptar al contenido real del proyecto.

## 16. Jerarquía
Primaria: Agendar cita.
Secundarias: Ver servicios, WhatsApp.
Terciarias: Conocer OMG, Blog, Dejar opinión.

## 17. Responsive
Revisar al menos 320, 375, 390, 430, 768, 1024, 1280 y 1440 px.
Prestar especial atención a 375, 390 y 430 px.
Comprobar navegación, cards, botones, formularios, OSCAR, WhatsApp, mapas, imágenes y ausencia de scroll horizontal.

## 18. Animaciones
Usar movimiento con función clara.
Evitar scroll hijacking, parallax excesivo y animaciones permanentes que dificulten lectura.
Respetar `prefers-reduced-motion`.

## 19. Imágenes
Priorizar material real de OMG.
Revisar resolución, recorte, peso, lazy loading y alt text.
No sustituir fotografías reales por imágenes genéricas sin justificación.

## 20. SEO y rendimiento
Preservar title, description, canonical, Open Graph, headings, enlaces internos, sitemap, robots y datos estructurados existentes.
No cambiar URLs indexadas sin necesidad.
Revisar LCP, CLS, INP, imágenes, fuentes, scripts y recursos bloqueantes.

## 21. SEO local
Mantener consistencia de nombre, dirección, teléfono y horarios.
Revisar Schema.org existente sin inventar datos.

## 22. Accesibilidad
Revisar contraste, teclado, focus, labels, semántica, alt text, headings, modales, formularios y errores.

## 23. Analítica
Si existe analítica, conservarla.
Cuando sea compatible con la solución actual, medir acciones como:
`click_agendar`, `click_whatsapp`, `click_servicio`, `click_como_llegar`, `problema_vehiculo_selected`, `oscar_open`, `oscar_option_selected`.

No instalar una plataforma nueva sin revisar la existente.

## 24. Proceso
Fase 1: auditoría técnica.
Fase 2: mapeo de secciones.
Fase 3: reorganización estructural.
Fase 4: nueva experiencia “¿Qué le pasa a tu vehículo?”.
Fase 5: refinamiento visual.
Fase 6: QA.

Registrar avances y pendientes en `docs/BITACORA.md`.

## 25. Validación final
Comprobar que:
- el visitante entiende rápidamente qué hace OMG;
- encuentra los servicios;
- recibe orientación si desconoce la falla;
- ve un CTA claro;
- puede agendar fácilmente desde móvil;
- WhatsApp está accesible;
- OSCAR ayuda sin distraer;
- “Deja tu opinión” no compite con la conversión;
- ubicación y horarios son fáciles de encontrar;
- se mantiene la identidad;
- no existen errores nuevos;
- SEO y responsive siguen funcionando.

## 26. Entrega del agente
Registrar en la bitácora:
- archivos modificados;
- componentes creados o reutilizados;
- cambios UX;
- responsive;
- SEO;
- integraciones;
- dependencias;
- pruebas;
- pendientes;
- commit.

Después, cumplir el protocolo Git definido en `AGENTS.md`.
