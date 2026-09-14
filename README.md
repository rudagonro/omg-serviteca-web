# OMG Serviteca

Respaldo recuperado del despliegue público de Netlify y preparado para versionarse en GitHub y publicarse como sitio estático.

## Estructura

- `index.html`: copia del archivo HTML servido públicamente por Netlify.
- `images/`: imágenes del sitio, extraídas del HTML original (antes venían incrustadas en base64), más favicons y la imagen `og-image.jpg` para vistas previas (WhatsApp, redes sociales).
- `favicon.ico`, `robots.txt`, `sitemap.xml`: archivos de soporte para navegadores y buscadores.

El sitio no requiere proceso de compilación: CSS y JavaScript están incrustados en `index.html`, y las imágenes viven como archivos sueltos en `images/`. La única dependencia externa de presentación es Google Fonts; los enlaces de contacto abren WhatsApp o llamadas telefónicas.

## Publicación en Cloudflare Pages

- Rama de producción: `main`
- Comando de compilación: `exit 0` (o vacío)
- Directorio de salida: `.`

Antes de publicar, revisar dirección, horarios, teléfono y enlaces reales de redes sociales.

## Cumplimiento y privacidad

- `politica-privacidad.html`: política de privacidad y tratamiento de datos.
- `politica-cookies.html`: preferencias de almacenamiento local y analítica opcional.
- `terminos-condiciones.html`: condiciones de cotización, reparación, garantía y entrega.
- `_headers`: evita que Cloudflare inyecte analítica antes del consentimiento y conserva caché prolongada para imágenes.
- `IMAGENES-Y-LICENCIAS.md`: auditoría y registro pendiente de procedencia de imágenes.

El banner carga Cloudflare Web Analytics únicamente después de la aceptación. No hay Google Analytics ni Meta Pixel en el código.
