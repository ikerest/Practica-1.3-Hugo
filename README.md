# IAW — Práctica P1.2: Tu mini sitio web de la mano de Hugo

- Alumno: Iker Estebaranz (@ikerest)
- Módulo: Implantación de Aplicaciones Web (IAW) — 2º ASIR
- Máquina Virtual: UBUNTUUUUUASO (Ubuntu 64-bit, usuario iker)
- Servidor web: Nginx
- Perfil de GitHub (P1.1): https://github.com/ikerest

---

## 1. Instalación de Hugo en la Máquina Virtual con los comandos aportados por Jordi en su guía.

## 2. Creación del Sitio y Estructura Base

Se inicializó la estructura del sitio con configuración en YAML (hugo.yaml):

```bash
cd ~/Escritorio
hugo new site ProyectoHUGO --format yaml
cd ProyectoHUGO
```

Configuración en hugo.yaml:

```yaml
baseURL: "http://localhost:1313/"
locale: "es-es"
title: "Mini Sitio Web con Hugo - Iker Estebaranz (IAW P1.2)"
disableKinds:
  - "taxonomy"
  - "term"
```

El servidor local de desarrollo se prueba con:
```bash
hugo server -D --watch
```

## 3. Separar Código y Contenido en Markdown 

Se creó la portada en content/_index.md con su front matter, y la plantilla layouts/home.html que inyecta dinámicamente las variables de título y contenido:

```html
{{ partial "header.html" . }}
<h1>{{ .Title }}</h1>
{{ .Content }}
{{ partial "footer.html" . }}
```

## 4. Parciales y Hojas de Estilo 

Los elementos comunes (cabecera con navegación y pie de página) se crearon como parciales dentro de layouts/partials/ (header.html y footer.html). Se añadió la hoja de estilo en static/css/style.css para servirla estáticamente.

Para poner el sitio en producción con Nginx, basta con compilar con hugo y copiar el contenido de public/ a /var/www/html/ o configurar un server block en Nginx.

## 5. Páginas de Contenido Adicionales

Se añadieron las páginas content/contact.md y content/sobre-mi.md, gestionadas mediante la plantilla layouts/page.html.

## 6. Sección de Blog y Entradas

En este apartado y en el consiguiente crear el código de la página web me he apoyado un poco en la Inteligencia artificial como Gemini 4 Argon, ya que personalemnte programación es un área que no domino tanto. Se creó la sección content/posts/ con las entradas hello-world.md y practica-hugo-iaw.md. La plantilla layouts/section.html recorre los artículos usando la función range para las páginas regulares mostrando fecha formateada, resumen y enlace a cada publicación.

## 7. Enlace al Perfil de GitHub de la P1.1 

El enlace al README de perfil de GitHub (https://github.com/ikerest) se encuentra integrado en:
- El menú de navegación (header.html) en la barra superior.
- La portada (content/_index.md) en la sección obligatoria "Sobre mí".
- La página content/sobre-mi.md.
- El pie de página (footer.html).
