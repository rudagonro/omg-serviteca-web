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
