---
title: "Despliegue del sitio con Hugo y Nginx en la VM"
date: 2026-10-29T17:30:00+01:00
---

Notas sobre la configuración y puesta en marcha de Hugo en la máquina virtual Ubuntu para la práctica P1.2 de IAW:

1. **Instalación de Hugo:** Descarga del binario de 64 bits en `~/.local/bin/hugo` para contar con una versión actual frente a la versión antigua de los repositorios.
2. **Plantillas y parciales:** Organización del código HTML en `layouts/` y `layouts/partials/` para reutilizar cabeceras y pies de página.
3. **Servicio web:** Los ficheros generados en el directorio `public/` pueden copiarse a `/var/www/html/` para que Nginx los sirva a través de la red local sin necesidad de backend dinámico.
4. **Enlace a GitHub:** Vinculación con el perfil de GitHub `@ikerest` de la práctica P1.1.
