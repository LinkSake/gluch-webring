# GLUCH Webring

El anillo de sitios personales de la comunidad del GLUCH, el Grupo de Usuarios
de Linux Chihuahua.

Sitio: `https://linksake.github.io/gluch-webring/`

## Unirte

1. Revisa los requisitos en la página del anillo.
2. Agrega tu sitio al **final** de `data/members.yaml` con un pull request:

   ```yaml
   - slug: mi-blog                 # corto, único, solo a-z, 0-9 y guiones; no cambia
     name: Mi blog
     url: https://ejemplo.com/     # con https
     author: Tu nombre             # opcional
     description: De qué trata.    # opcional
   ```

   Si no usas GitHub, abre un issue con el formulario "Unirme al anillo".
3. Cuando se fusione, copia tu widget desde la página del anillo y pégalo en tu
   sitio.

El build de cada pull request valida la lista: un slug repetido o inválido, o
una URL sin https, hacen que falle.

## Cómo funciona

Este repo solo tiene la configuración, la lista de miembros y el diseño. Todo
lo demás viene del módulo de Hugo
[`hugo-webring`](https://github.com/LinkSake/hugo-webring) (versión fijada en
`go.mod`): las redirecciones `/ring/<slug>/next/` y `/ring/<slug>/previous/`,
`/random/`, `/members.json` y la revisión semanal de miembros.

| Archivo | Qué es |
| --- | --- |
| `hugo.toml` | Configuración del sitio y del anillo |
| `data/members.yaml` | Miembros, en el orden del anillo |
| `content/_index.md` | Texto de "Qué es" en la página principal |
| `layouts/baseof.html`, `layouts/home.html` | Diseño propio de este anillo |
| `assets/css/theme.css`, `assets/css/gluch.css` | Colores y estilos |
| `static/fonts/` | Oswald y JetBrains Mono (SIL Open Font License) |
| `.github/workflows/hugo.yaml` | Build y deploy a GitHub Pages en cada push a `main` |
| `.github/workflows/check-pr.yaml` | Build de prueba en cada pull request |
| `.github/workflows/check-members.yaml` | Revisión semanal de miembros (lunes) |

## Desarrollo

Versiones en `.tool-versions` (asdf o mise): Hugo y Go.

```sh
hugo server
```

Para actualizar el módulo: `hugo mod get github.com/LinkSake/hugo-webring@<versión>`.
