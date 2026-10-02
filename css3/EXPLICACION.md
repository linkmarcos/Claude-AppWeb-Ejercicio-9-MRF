# Explicación del proyecto TechStore (HTML y CSS)

Partiendo de la actividad anterior (página de productos `css Ejercicio2.html`) se han
desarrollado las páginas de **Inicio**, **Servicios** y **Contacto**, manteniendo el
mismo estilo visual y la misma estructura de proyecto.

## 1. Estructura del proyecto

```
css3/
├── inicio.html            ← NUEVA: página de inicio
├── css Ejercicio2.html    ← página de productos (actividad anterior)
├── servicios.html         ← NUEVA: página de servicios
├── contacto.html          ← NUEVA: página de contacto
├── style.css              ← ÚNICA hoja de estilos para las 4 páginas
├── images/
│   ├── logo.png
│   ├── icons/             ← iconos (carrito, envío, 24h, asistencia, atención)
│   └── products/          ← fotos de los ordenadores
└── EXPLICACION.md         ← este documento
```

- No hay CSS dentro de los `.html`: ni etiquetas `<style>` ni atributos `style="..."`.
  Todas las páginas cargan el mismo archivo con
  `<link rel="stylesheet" href="style.css">`.
- Todas las páginas reutilizan las imágenes de la carpeta `images/`.

## 2. Esqueleto común de las cuatro páginas

Todas las páginas siguen exactamente la misma estructura que la página de productos:

```html
<!DOCTYPE html>
<html lang="es">
    <head> meta charset + link a style.css + title </head>
    <body>
        <div id="header"> ... </div>     <!-- aviso + menú -->
        <div id="container"> ... </div>  <!-- contenido propio de cada página -->
        <footer> ... </footer>           <!-- ventajas de la tienda -->
    </body>
</html>
```

| Elemento | Para qué sirve |
|---|---|
| `<!DOCTYPE html>` | Indica al navegador que es un documento HTML5. |
| `<html lang="es">` | Indica que la página está en español (lectores de pantalla, traductores, buscadores). |
| `<meta charset="UTF-8">` | Permite mostrar tildes, la ñ y el símbolo €. |
| `<link rel="stylesheet" href="style.css">` | Enlaza la hoja de estilos común. |
| `<title>` | Texto de la pestaña: `Inicio | TechStore MRF`, `Productos | ...`, etc. |
| `<!-- ... -->` | Comentarios HTML que separan las secciones (header, contenido, footer). |

### Header (igual en todas las páginas)

- `#notices`: barra gris con el aviso "Cerrado por mantenimiento web."
- `<nav>`: contiene el logo (`#logo`), el menú (`<ul>` con 4 `<li>`) y el icono de
  atención al cliente (`#service`).
- **Navegación entre páginas:** cada `<li>` lleva un enlace `<a href="...">` a la página
  correspondiente, por lo que **desde cualquier página se llega a todas las demás**:

| Menú | Enlace |
|---|---|
| INICIO | `inicio.html` |
| PRODUCTOS | `css%20Ejercicio2.html` |
| SERVICIOS | `servicios.html` |
| CONTACTO | `contacto.html` |

> El archivo de productos tiene un espacio en el nombre. En una URL el espacio se
> escribe como `%20`, por eso el enlace es `css%20Ejercicio2.html`.

- **Página actual:** el `<li>` de la página en la que estamos lleva `class="active"`,
  que lo pinta en blanco igual que el efecto hover. Así el usuario sabe en qué
  sección se encuentra.

### Footer (igual en todas las páginas)

Tres bloques `.icon_footer` con un icono y un texto: envío gratis, envío en 24 h y
asistencia técnica.

## 3. Contenido de cada página

### Inicio (`inicio.html`)

- `.intro`: título `<h1>` de bienvenida y un párrafo `<p>` en blanco sobre el fondo negro.
- Tres tarjetas `.card` (Productos, Servicios, Contacto). Cada una tiene:
  - `<img>` con un icono de `images/icons/`,
  - `<h2 class="name">` con el título,
  - `<p>` con una breve descripción,
  - `<a class="button">`, un botón que lleva a la sección correspondiente.

### Productos (`css Ejercicio2.html`)

Es la página de la actividad anterior: cinco tarjetas `.product` con la foto,
el nombre (`.name`), el precio (`.price`) y el botón "Añadir al carrito"
(`.add_product` > `.container_button`). Solo se han hecho correcciones básicas
(ver apartado 5).

### Servicios (`servicios.html`)

- `.intro` con `<h1>` "Nuestros servicios" y un párrafo.
- Tres tarjetas `.card` (Envío gratis, Envío en 24 h, Asistencia técnica). Tienen la
  misma estructura que las de inicio, pero en lugar de botón muestran el precio con
  la clase `.price`, la misma que usan los productos (rojo granate y en negrita).

### Contacto (`contacto.html`)

- `.intro` con `<h1>` "Contacto" y un párrafo.
- Una tarjeta `.card` con los datos de atención al cliente (teléfono, email y
  horario). `<strong>` resalta cada dato y `<br>` hace el salto de línea.
- Un formulario `<form class="card contact_form">`:
  - `<label for="...">` asociado a cada campo por su `id`: al hacer clic en el texto
    se activa el campo, y además mejora la accesibilidad.
  - `<input type="text">` para el nombre y el asunto, y `<input type="email">` para el
    correo, que el navegador valida automáticamente.
  - `<textarea>` para el mensaje.
  - El atributo `required` hace que el formulario no se envíe si falta el nombre,
    el email o el mensaje.
  - `<button type="submit" class="button">`: botón de envío con el mismo estilo que
    el resto de botones.

### Atributo `alt` de las imágenes

- Las imágenes con información (logo, fotos de productos, icono de atención al cliente)
  tienen un `alt` descriptivo.
- Los iconos decorativos que van junto a un texto que ya dice lo mismo (carrito, iconos
  del footer, iconos de las tarjetas) llevan `alt=""`, para que los lectores de
  pantalla no lean lo mismo dos veces.

## 4. Explicación de `style.css`

La hoja está organizada en tres bloques comentados: **header**, **container** y
**footer**. Todos los selectores empiezan por `body #header`, `body #container` o
`body footer`, igual que en la actividad anterior.

### Reglas generales y header

| Selector | Qué hace |
|---|---|
| `body` | Fondo negro y sin márgenes. |
| `#header nav` | Barra del menú con `display: flex`: logo (10 %), menú (80 %) e icono de atención (10 %). |
| `#header nav ul` | Lista sin viñetas (`list-style-type: none`), centrada con flex y con una línea blanca inferior. |
| `#header nav ul li` | Cada opción del menú con un ancho mínimo y un relleno. |
| `li:hover, li.active` | **Selector agrupado**: al pasar el ratón y en la página actual, fondo blanco y texto negro. |
| `#header nav ul li a` | Quita el subrayado y hereda el color del `li` (`color: inherit`). |
| `#header #notices` | Barra gris `#D9DEE3` del aviso. |

### Container (contenido de cada página)

| Selector | Qué hace |
|---|---|
| `#container` | Contenedor flex con `flex-wrap: wrap` y centrado: coloca las tarjetas en filas. |
| `.intro` | Ocupa todo el ancho (`width: 100%`), así el título queda en su propia fila. Texto blanco y centrado. |
| `.product, .card` | **Selector agrupado**: la caja gris (`#D9DEE3`) con relleno, márgenes, texto centrado y un 25 % de ancho la comparten los productos y las tarjetas nuevas. No se repite ninguna declaración. |
| `.product img` / `.card img` | Las fotos de producto ocupan el 100 % de la tarjeta y los iconos de las tarjetas miden 80 px. |
| `.name` / `.price` | Estilo del título (20 px, negrita) y del precio (22 px, granate `#800000`). Se aplican tanto a los productos como a las tarjetas de servicios. |
| `.add_product, .button` | **Selector agrupado**: el botón "Añadir al carrito" y los botones nuevos comparten borde blanco, color y fondo gris, y al pasar el ratón el fondo se vuelve blanco (`:hover`). |
| `.button` | Propiedades propias de los botones nuevos: `display: block` y `width: 100%` para ocupar todo el ancho, `box-sizing: border-box` para que el borde y el relleno no lo desborden, `font: inherit` para que `<button>` use la misma letra que la página y `cursor: pointer`. Sirve igual para `<a>` y para `<button>`. |
| `.contact_form` | El formulario es una `.card` más ancha (40 %) y con el texto a la izquierda. Como esta regla va después de `.card`, sobrescribe su ancho. |
| `.contact_form label` | Cada etiqueta en su propia línea y en negrita. |
| `.contact_form input, textarea` | Campos a todo el ancho, con relleno, borde blanco y la misma fuente que la página. |
| `.contact_form textarea` | `resize: vertical`: el mensaje solo se puede agrandar hacia abajo, sin romper el diseño. |

### Footer

| Selector | Qué hace |
|---|---|
| `footer` | Franja gris de 200 px con flex para colocar los 3 bloques en fila. |
| `.icon_footer` | Cada bloque ocupa un tercio (33 %) y centra su contenido. |
| `.icon_footer img` | Iconos de 60 px con `margin: 30px 10px 0px` (arriba, laterales, abajo). |

### Cómo se evita la redundancia

1. **Una sola hoja de estilos** para las cuatro páginas.
2. **Selectores agrupados** (`a, b { ... }`): si dos elementos se ven igual, sus
   propiedades se escriben una sola vez (`.product, .card`; `.add_product, .button`;
   `li:hover, li.active`).
3. **Reutilización de clases**: `.name` y `.price` sirven para productos y servicios, y
   `.card` sirve para inicio, servicios y contacto.
4. **Sin propiedades repetidas** dentro de una misma regla (ver correcciones).

## 5. Correcciones hechas a la actividad anterior

Se ha mantenido todo el contenido del `body` y todos los `id` y `class`. Solo se ha
corregido lo siguiente:

**HTML (`css Ejercicio2.html`)**

- Los comentarios `/*----HEADER----*/` usaban la sintaxis de CSS y por eso **se veían
  como texto** en la página. Se han cambiado a comentarios HTML `<!-- ... -->`.
- Los enlaces del menú tenían `href="#"` y no llevaban a ninguna parte. Ahora enlazan
  a las cuatro páginas.
- Se ha añadido `lang="es"`, un `<title>` coherente con el resto de páginas y el
  atributo `alt` en todas las imágenes.
- Erratas: "Windows 11 Homeg" → "Windows 11 Home", y el precio "11389,99 €" →
  "1383,99 €" (el valor de la actividad de referencia).
- `class ="icon_footer"` → `class="icon_footer"` (formato).

**CSS (`style.css`)**

- `#header nav ul`: tenía `width` dos veces (100 % y 80 %). Se deja solo `width: 80%`,
  que era la que se aplicaba.
- `#header nav ul li a`: sobraba un punto y coma (`color: inherit; ;`).
- `.product`: tenía cinco declaraciones de margen que se sobrescribían entre sí. Se
  sustituyen por `margin: 0 20px 20px`, que da el mismo resultado.
- `.add_product:hover`: repetía `border` y `color`, que ya estaban en `.add_product`.
  Ahora solo cambia el `background-color`.
- `.icon_footer img`: tres declaraciones de margen → `margin: 30px 10px 0px`.

El aspecto de la página de productos no cambia con estas correcciones.
