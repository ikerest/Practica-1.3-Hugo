---
title: "Publicando nuestro sitio estático en GitHub Pages (P1.3)"
date: 2026-11-05T16:10:00+01:00
draft: false
---

En esta tercera práctica (**IAW P1.3**) damos el salto del entorno local de nuestra máquina virtual con Nginx a la publicación directa en Internet utilizando **GitHub Pages**.

## ¿Qué aporta una página web estática en este despliegue?

Una **página web estática** se entrega al navegador exactamente tal y como está almacenada en el sistema de archivos (`HTML`, `CSS`), sin pasar por un motor de ejecución en servidor ni consultar bases de datos en tiempo real. Al combinar **Hugo** como generador y **GitHub Pages** como alojamiento obtenemos varias ventajas clave:

- **Mayor seguridad:** Al no existir backend dinámico ni base de datos en producción, desaparecen vectores de ataque clásicos como inyecciones SQL o ejecución de *web shells*.
- **Rendimiento inmediato:** Los ficheros precompilados en `html/` se sirven directamente por HTTPS con una latencia mínima.
- **Coste cero y mantenimiento sencillo:** Todo el flujo de publicación se controla mediante `git` desde la terminal (`editar → hugo → commit → push`).

## Ajustes clave realizados para GitHub Pages

1. **Configuración en `hugo.toml`:** Se definió `baseURL = "https://ikerest.github.io/Practica-1.3-Hugo/"` y `publishDir = "html"` para que Hugo genere la salida directamente en la carpeta que sirve GitHub Pages desde la rama `main`.
2. **Desactivación de Jekyll (`static/.nojekyll`):** Se incluyó el archivo vacío `.nojekyll` para que GitHub sirva los recursos estáticos de Hugo sin procesarlos con Jekyll.
3. **Rutas relativas con `relURL`:** Todas las referencias a hojas de estilo (`css/style.css`) y navegación interna usan `relURL` y `.Site.Home.RelPermalink`, garantizando que funcionen bajo la subruta `/Practica-1.3-Hugo/` sin romperse.
