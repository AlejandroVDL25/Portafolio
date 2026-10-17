# Portafolio de Alejandro Villafuerte Díaz Leal

Sitio estático (un solo `index.html`, sin compilación) publicado en Vercel desde este repositorio.

## Qué se agregó a la versión original

El diseño, la escena 3D, la esfera de etiquetas, la terminal, la línea de tiempo, el modal por capas y el generador de CV en PDF se conservan sin cambios. Se añadió:

- **Niveles honestos de habilidad**: cada etiqueta marca experiencia práctica, conocimientos básicos o en desarrollo, con leyenda.
- **Contexto de uso**: cada grupo de habilidades indica dónde se aplicó.
- **Casos de estudio** dentro del modal de cada proyecto: objetivo, contribución, resultado y desafíos técnicos.
- **Sección Servicios** para clientes, con botón de cotización que preselecciona el formulario.
- **Formulario de contacto** con validación que prepara el mensaje por correo o WhatsApp (sin servidor ni almacenamiento).
- **Mensajes para reclutadores y clientes**, aviso de privacidad y enlace para saltar al contenido.
- **SEO**: URL canónica, imagen para compartir (`og.png`), datos estructurados, `robots.txt`, `sitemap.xml` y página `404.html`.
- **Encabezados de seguridad** en `vercel.json`.
- **Enlace de GitHub corregido** a `github.com/AlejandroVDL25` (el anterior daba error 404).
- **LinkedIn real** tomado del enlace del CV (`alejandro-villafuerte-díaz-leal-40837843a`); el anterior no correspondía al perfil. Si `DATA.linkedin` se deja vacío, LinkedIn se oculta en todo el sitio y en el PDF.
- **OTDR eliminado**: no aparece en el CV; la medición se describe con medidor de potencia óptica.
- **Error corregido del original**: las tarjetas aún no visibles tenían una proyección 3D que cubría la página y bloqueaba los botones "Descargar CV" y "Escribir por WhatsApp" del inicio al cargar. Ahora no captan clics hasta aparecer.

## Cómo actualizar el contenido

Todo el contenido vive en el objeto `DATA`, al inicio del `<script>` principal (entre `/*DATA-START*/` y `/*DATA-END*/`). El CV en PDF se genera a partir de esos mismos datos, así que se actualiza solo.

- **Niveles**: en `DATA.levels`, escribe el nombre exacto de la etiqueta con `"basico"` o `"desarrollo"`. Lo que no aparezca se muestra como experiencia práctica.
- **Dónde se aplicó**: campo `where` de cada grupo en `DATA.skills`.
- **Casos de estudio**: campo `caseStudy` de cada proyecto (`goal`, `role`, `result`, `challenges`).
- **Servicios**: arreglo `DATA.services` (íconos de https://lucide.dev).
- **Contacto**: `email`, `phone`, `phoneRaw`, `linkedin`, `github` y `githubUser`.

## Publicar

Sube los cambios a este repositorio (`git push`) y Vercel vuelve a publicar automáticamente. Si cambias de dominio, actualiza la URL en `index.html` (canonical, `og:url`, `og:image` y datos estructurados), `robots.txt` y `sitemap.xml`.

## Pruebas

```
pip install playwright && playwright install chromium
python -m http.server 8767
python tests/test_site.py
```

`tests/route_local.py` sirve copias locales de three.js, lucide y jsPDF para probar sin conexión; para probar con internet, quita la línea `pg.route(...)` del script. Para probar la versión publicada: `BASE_URL=https://portafolio-alexvdl.vercel.app/ python tests/test_site.py`.
