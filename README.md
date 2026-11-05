# Práctica P1.3 IAW — Publicando mi sitio Hugo en GitHub Pages

- **Alumno:** Iker Estebaranz (`@ikerest`)
- **Curso:** 2º ASIR — Implantación de Aplicaciones Web (IAW)
- **Web publicada en GitHub Pages:** [https://ikerest.github.io/Practica-1.3-Hugo/](https://ikerest.github.io/Practica-1.3-Hugo/)
- **Repositorio del proyecto:** [https://github.com/ikerest/Practica-1.3-Hugo](https://github.com/ikerest/Practica-1.3-Hugo)
- **Mi perfil de GitHub (P1.1):** [https://github.com/ikerest](https://github.com/ikerest)

---

## ¿Qué he hecho en esta práctica?

En esta práctica P1.3 he cogido el mini sitio web que ya tenía montado en local con Nginx de la práctica anterior (P1.2) y lo he preparado para publicarlo directamente en Internet usando **GitHub Pages**.

La idea principal con la que me quedo de esta práctica es cómo funciona realmente un generador estático como Hugo cuando lo subes a un hosting como GitHub Pages: yo edito mis archivos fuente (`content/`, `layouts/`, `hugo.toml`), pruebo en local con `hugo server -D`, pero GitHub Pages no ejecuta Hugo por detrás, sino que solo sirve el HTML plano que generamos al lanzar el comando `hugo` en la terminal.

---

## Pasos que he ido siguiendo

### 1. Partir de mi web de la P1.2
He partido de la estructura que ya hice en la P1.2 (con la portada, las páginas de *Sobre mí* y *Contacto*, los parciales de cabecera y pie de página en `layouts/partials/`, el blog y el estilo de terminal en `static/css/style.css`). Antes de tocar nada he comprobado en local que todo seguía viéndose bien.

### 2. Cambiar la configuración a `hugo.toml` para GitHub Pages
Siguiendo el guion de la práctica, he pasado la configuración a `hugo.toml` para indicarle a Hugo la URL pública final con la subruta del repositorio (`baseURL`), y sobre todo el `publishDir = "html"`, para que al compilar guarde toda la web dentro de la carpeta `html/` (en lugar de `public/`):

```toml
baseURL = "https://ikerest.github.io/Practica-1.3-Hugo/"
languageCode = "es"
title = "Iker Estebaranz · Laboratorio IAW (2º ASIR)"
publishDir = "html"
disableKinds = ["taxonomy", "term"]

[params]
  description = "Sitio web estático generado con Hugo y publicado en GitHub Pages — Práctica P1.3 de Implantación de Aplicaciones Web"
  author = "Iker Estebaranz"
  github = "https://github.com/ikerest"
```

También he creado el archivo vacío `static/.nojekyll` para que, al generar la carpeta `html/`, se copie dentro y GitHub no intente procesar la web con Jekyll.

### 3. Corregir las rutas del CSS y los enlaces con `relURL`
En la P1.2 tenía puestas rutas como `/css/style.css` o `/posts/` directamente en las plantillas porque en Nginx colgaba todo de la raíz `/`. Al subirlo a GitHub Pages bajo la subruta `/Practica-1.3-Hugo/`, si dejaba eso así se iban a romper los estilos y los enlaces del menú.

Para solucionarlo (apoyándome en la IA para ver cómo funcionaba exactamente la sintaxis de las llaves de Hugo en las plantillas) he cambiado `layouts/partials/header.html` y el resto de layouts usando `{{ "css/style.css" | relURL }}` y `{{ .Site.Home.RelPermalink }}`. Así Hugo le añade sola la ruta del repositorio delante y carga el CSS a la primera.

### 4. Personalizar título, descripción y nueva entrada en el blog
En el último paso de la guía he añadido el parámetro `description` en `hugo.toml` y he metido la etiqueta `<meta name="description" content="{{ .Site.Params.description }}">` en el `header.html`. Además, he aprovechado para añadir una tercera entrada en el blog (`content/posts/despliegue-github-pages.md`) resumiendo qué es una página web estática y los pasos de este despliegue.

### 5. Generar `html/` y subir los cambios con Git
Cada vez que he hecho cambios he ejecutado:

```bash
hugo --cleanDestinationDir
```

Con esto se actualiza la carpeta `html/` con todo el sitio compilado (sin borradores) listo para que GitHub Pages lo sirva desde la rama `main` y la carpeta `/html`.

---

## Nota sobre el uso de IA

Igual que en la práctica P1.2, quiero dejar claro que para las partes más complicadas de código —como el diseño CSS estilo terminal (`static/css/style.css`), la sintaxis de las plantillas de Hugo (`relURL`, `RelPermalink`, variables de `.Site.Params`) y estructurar el texto de los posts del blog— me he apoyado en la IA (Gemini), ya que la programación y el diseño web no son mi fuerte. Eso sí, toda la configuración del despliegue, entender por qué hay que compilar en `html/` y las pruebas las he ido siguiendo paso a paso con la guía.
