# construir — plataforma de identidad visual

editor paramétrico para que **Lista Construir** ([@listaconstruir.cedig](https://instagram.com/listaconstruir.cedig), lista estudiantil independiente de la Escuela de Diseño UDP) produzca sus propios posts sin depender de que alguien sepa diseñar.

mismo esquema que el estudio de [rastro](https://github.com/emiguerra/2026-rastro-metadatos): una página de edición maneja un *renderer* por la URL y lo muestra en vivo; lo que ves se exporta a PNG o PDF. la identidad (collage, letras recortadas, color, tratamiento de imagen) está horneada en la herramienta, así que quien hace un post elige texto, formato e imágenes, y el sistema mantiene la coherencia.

| pieza | archivo | qué hace |
| --- | --- | --- |
| editor | [taller.html](taller.html) | la herramienta: panel de controles, vista en vivo, banco de imágenes y exportación. es lo que se abre para trabajar |
| renderer | [pieza.html](pieza.html) | dibuja una pieza a tamaño real desde los parámetros de la URL. no se abre solo; lo mete el taller en un iframe |
| identidad | [identidad.html](identidad.html) | mini-manual de marca: paleta, tipografía y kit de collage *(el isotipo del cururo quedó en v1, pausado por ahora)* |
| banco | [assets/](assets/) | imágenes: stickers recortados (`stickers/`), sus originales (`ref-*.jpg`) y el índice `manifest.json` |

## cómo se usa

1. abrir **taller.html** con Live Server (no como archivo suelto — ver notas).
2. elegir formato a la izquierda: **feed 4:5**, **historia 9:16** o **16:9**.
3. editar en el panel derecho: título, info, color, imágenes.
4. para una imagen: **Elegir** abre el banco; se clickea un sticker o se **sube/arrastra** una foto propia.
5. exportar arriba: **PNG**, **PNG sin fondo** (transparente) o **PDF**.

## la identidad

- **paleta:** azul `#274DEA` (base), crema `#F4ECD8` (papel), tinta `#14151c`, y acentos amarillo `#F5D700` y magenta `#8C0041` (lima `#97BA0B` para destellos). máximo dos acentos por pieza.
- **tipografía:** Archivo Black (títulos) + Archivo (texto), de Google Fonts; se cargan solas.
- **título:** letras recortadas tipo *ransom* en papeles de color, con una palabra grande dominante y el resto chico.
- **imágenes, dos tratamientos:**
  - **duotono** — serigrafía halftone (papel + tinta + negro + trama de puntos), para fotos.
  - **sticker** — recorte sin fondo, para los elementos del banco.
- **composición:** figura/fondo con un panel de color rotado, textura de papel y sobreimpresión riso, titular cruzando la costura del panel. *(por ahora hay una sola lógica de composición; la idea es sumar más presets.)*

## el banco de imágenes

27 originales (`ref-*.jpg`, bajadas de un board de referencia) procesadas a stickers transparentes en `stickers/`; `manifest.json` es la lista **curada** (21) que lee el editor. el proceso de quita-fondo samplea el color del borde, así sirve para fondo blanco, damero quemado o fondo de color.

las fotos que subís **arrastrando en el editor** quedan guardadas en el navegador (IndexedDB), **no** en el repo: si querés versionar una foto propia, copiala a `assets/` y commiteala.

## notas

- **hay que abrirlo con Live Server** (o cualquier servidor local). el editor lee el banco con `fetch`, mete el renderer en un iframe y usa IndexedDB — nada de eso funciona abriendo el `.html` como archivo (`file://`).
- las piezas exportadas (`construir-*.png` / `.pdf`) están en `.gitignore`: son resultados, no fuente.
