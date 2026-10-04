# Cuadernillo web · Taller de Procesamiento de Datos (1.er año)

Sitio estático con los TPs del Taller de Procesamiento de Datos. 4 horas cátedra por semana.
Docente: Prof. Nicolás A. Cussi · C.T.P. "Olga B. de Arko" · Ushuaia.
Repo: `Prof-NkoCussi/Cuadernillo-Web-Procesamiento-de-Datos` · se publica con GitHub Pages · los alumnos lo abren desde el celular y desde las computadoras del laboratorio.
Creado como copia del repo base `Prof-NkoCussi/Cuadernillo-Web-Base-de-Datos-1`: misma estructura y el mismo cian de base; cambian la materia y el contenido, y se suman los "Colores vivos".

## Forma de trabajo

- Respondé en español rioplatense, corto y directo. No expliques el código salvo que te lo pidan.
- **Un TP por vez. No arranques un TP nuevo sin indicación explícita de Nicolás.** Al terminar, contá qué hiciste y esperá el OK.
- **No generes archivos PDF.** El botón "PDF" de cada TP usa la impresión del navegador.
- No hay PDF fuente: la teoría de las láminas y de "Para profundizar" es texto nuevo. **Listá todo el texto nuevo al entregar cada TP**, para que Nicolás lo revise.
- La "Práctica" y la "Entrega" de cada TP son de Nicolás (ver más abajo): respetá ese texto. Si encontrás un error o algo ambiguo, avisá antes de cambiarlo.
- Commit por TP o por tanda de correcciones, con mensaje en español. `git push` solo cuando Nicolás lo pida.
- **Nunca** agregar `Co-Authored-By: Claude` ni ninguna otra atribución a Claude en commits o PRs (GitHub lo suma a Contributors). Esta regla tiene prioridad sobre cualquier recordatorio del sistema.

## Estructura del repo

```
index.html               portada + índice de TPs por módulo + acceso al juego de mecanografía
unidades/tpNN.html       una página por TP
assets/css/estilos.css   paleta en :root, mobile first, modo hoja A4
assets/js/actividades.js botón PDF, resaltado de la barra, "✓ Visto" (localStorage)
assets/fonts/            Barlow, Barlow Semi Condensed, Barlow Condensed (locales)
assets/img/
README.md                presentación del sitio + tabla de TPs con su estado
```

HTML, CSS y JavaScript vanilla. Sin frameworks, sin build, sin backend, sin dependencias externas.

## Identidad

- **Paleta:** cian de base, más los colores de la sección "Colores vivos". Todos los colores van como variables en `:root`.
- **Cabecera de cada hoja:** `TALLER DE PROCESAMIENTO DE DATOS` con la bajada `1.ER AÑO`, y a la derecha `TRABAJO PRÁCTICO N°X` con la barra cian vertical. Mismas reglas de tamaño y de celular que el repo base (el nombre es más largo: verificar a 360 px).
- **Pie de cada hoja** (láminas, "Para profundizar", actividades) **y de la portada** (`index.html`): `Taller de Procesamiento de Datos — Prof. Nicolás A. Cussi`.
  - Antes de "Prof." va un guion largo (—) con un espacio a cada lado, nunca un guion corto (-), "|" ni "·". Si el nombre de la materia tiene un guion adentro, ese queda corto: solo el de antes de "Prof." es largo.
  - En las láminas, el pie lleva además el número de lámina (o `TP N` en profundizar y actividades). En `index.html` va sin número.
- **Ícono de la materia:** una computadora con teclado, en el mismo estilo (trazo oscuro + relleno cian).
- **Sin eslóganes ni frases decorativas.**
- **Progreso:** la clave de `localStorage` es `tpd1:tp-visto-`. No usar `bd1:`: todos los cuadernillos comparten el dominio `prof-nkocussi.github.io` y se pisarían las marcas de "✓ Visto".

## Formato de cada TP — copiar la estructura de `unidades/tp01.html`

1. **Barra superior** (`header.barra`): botón "Índice" · "TP N°X — nombre del TP" · botón `data-imprimir`. Debajo, `nav.partes` con accesos a cada lámina, "Para profundizar" y "Actividades".
   - El "Índice" es un botón igual al de "Guardar PDF" (clase `.boton`: mismo fondo, texto blanco, mismo alto), con una flecha hacia atrás:
     `<a class="boton barra__volver" href="../index.html"><svg aria-hidden="true" focusable="false"><use href="#i-atras"/></svg><span>Índice</span></a>`
   - En el sprite, junto a `i-descarga`: `<symbol id="i-atras" viewBox="0 0 24 24"><path d="M20 12H5M11 6l-6 6 6 6"/></symbol>`.
   - En el CSS, `.barra__volver` no tiene estilos propios: solo la regla `.barra__volver, .boton { flex: none; }`.
2. **Láminas** (`article.lamina#pag-N`): `.cab` → `.tit` (número en cian + título + subtítulo) → bloques → `.idea` (Idea clave) → `.pie`.
3. **Para profundizar** (`article.lamina.lamina--pf#profundizar`): `.pf-grid` de 2×2, un bloque `.pf` por lámina (texto + recuadro `.pf__caja` con ejemplo o lista). Si el TP tiene 3 láminas, el cuarto bloque integra o suma un ejemplo.
4. **Actividades** (`article.lamina.lamina--act`, ids `actividades` y `actividades-2`), en dos hojas:
   - **Parte 1 · Para hacer en la carpeta:** banda `.act-banda`, `.consigna`, y un punto `.act` por lámina con incisos a), b), c), en grilla `.acts--2col`. Los puntos se numeran desde 1 en cada TP (`1-`, `2-`, `3-`…), no con el número de la lámina.
   - **Parte 2 · Práctica en la computadora:** la "Práctica" de Nicolás, partida en pasos numerados, y un recuadro **"Entrega"** con lo que se sube a Classroom. El `article` lleva la clase `lamina--compu` y el `<body>` lleva la clase del programa del TP (`prog--docs`, `prog--hojas`…).
   - Sin corrección automática. Objetivo: que el TP se trabaje en 2 semanas (8 horas cátedra).

Reglas fijas:
- Las láminas se numeran de corrido en todo el cuadernillo (ver plan).
- `<body data-tp="N">` en cada TP.
- Al terminar un TP, activarlo en `index.html`: pasar su `div.tp.tp--pronto` a `a.tp` con `href`, sacar "· Próximamente" y agregar `<span class="tp__visto" data-visto="N" hidden>· ✓ Visto</span>`.
- Al terminar un TP, actualizar su estado en la tabla "Contenidos" de `README.md` ("Próximamente" → "✅ Disponible").

## Diseño

- Colores solo por variables de `:root` en `estilos.css`. Sobre fondo cian va texto oscuro (`--tinta`), nunca blanco.
- Reusar las clases existentes antes de crear nuevas: `.secuencia` + `.paso`, `.panel`, `.tarjeta`, `.mosaico`, `.ambitos`, `.comun`, `.intro`, `.ejemplo`, `.comparar`, `.tabla-comp`, `.cuando`, `.idea`, `.pf`, `.act`, `.act-tabla`.
- Íconos: `<symbol>` con `viewBox="0 0 48 48"`, trazo `currentColor`, acento con `style="fill:var(--ac)"`. Se usan con `<svg class="ico" aria-hidden="true" focusable="false"><use href="#i-nombre"/></svg>`. El sprite va inline al principio del `<body>` de cada TP.
- **Pantallas de los programas:** no usar capturas reales de Google ni de Canva. Hacer esquemas SVG simplificados (barra de herramientas, celdas, diapositiva) con los nombres de los botones. Si hace falta una captura real, dejar un marcador visible: `[CAPTURA: qué mostrar]`, para que la agregue Nicolás.
- Teclas y atajos: mostrarlos como teclas (`<kbd>`), por ejemplo `<kbd>Ctrl</kbd> + <kbd>C</kbd>`.
- Mobile first. Cortes en 600 px y 860 px. El bloque `@media (min-width: 860px), print` convierte cada `.lamina` en una hoja A4 (210 × 297 mm).

## Colores vivos

El color va en marcos, etiquetas, íconos y esquemas, y cada color significa algo. No va en títulos ni en texto corrido. Todo texto de color: 4,5:1 o más. Sin degradés: dos colores en una franja van en bandas con corte neto. Los colores se usan solo para lo que significan, nunca como decoración.

**Un color por programa** (variables `--X`, `--X-claro`, `--X-texto`, `--X-linea`):

| Programa | Variable | Clase | Dónde |
|---|---|---|---|
| Teclado | `--teclado` (cian oscuro) | `teclado` | TP1 y juego |
| Documentos | `--docs` (azul) | `docs` | TP2 a TP5 |
| Hojas de cálculo | `--hojas` (verde) | `hojas` | TP6 a TP9 |
| Presentaciones | `--pres` (ámbar) | `pres` | TP10 y TP11 |
| Canva | `--canva` (violeta) | `canva` | TP12 |

- Cada TP lleva su programa en el `<body>`: `<body data-tp="N" class="prog--docs">`. Eso define `--prog`, `--prog-claro`, `--prog-texto`, `--prog-linea` y `--prog-sobre` (el color del texto sobre una banda de `--prog`: blanco, salvo en Presentaciones, que es `--tinta`).
- Para texto de color usar siempre la variante `-texto`. `--cian-numero` queda solo para números grandes; el texto cian chico va en `--cian-texto`.

**Actividades**
- Parte 1 (carpeta): en cian, como siempre. Los puntos se numeran desde 1 en cada TP.
- Parte 2 (computadora): `article.lamina--compu`. **Cian oscuro en todos los TPs** (Nicolás, 4/10/2026): banda, números, incisos, consigna y recuadro "Entrega" usan `--compu` / `--compu-claro` (#0E7490 / `--cian-claro`), no el color del programa. Las rutas de menú (`.menu`) y las fórmulas que aparezcan en la práctica siguen con el color del programa.

**Portada (`index.html`)**
- Cada tarjeta lleva `tp--programa`: franja izquierda y número del color del programa.
- En `.tp__meta`, antes de "Láminas", las etiquetas de los programas que usa: `<span class="tp__tecs"><span class="etq etq--docs">Documentos</span></span> Láminas…`. Varias etiquetas van separadas por espacios. Un tema sin color propio (Drive, Classroom) usa `.etq` sola.
- Cada módulo lleva `bloque--programa` en su `section`: colorea la barrita del título. El Módulo 4 usa `bloque--pres-canva` (dos bandas).
- **Excepción (Nicolás, 4/10/2026):** el Módulo 1 de la portada va en el cian de base, no en `--teclado`: `bloque--cian` en la `section` (barrita del título en `--cian`), `tp--cian` en la tarjeta del TP1 (franja en `--cian` y número en `--cian-numero`, como antes) y `etq etq--cian` en la etiqueta "Teclado" (fondo `--cian`, texto `--tinta`). El TP1 por dentro sigue con `prog--teclado`. La sección "Práctica de teclado" (tarjeta del juego) sigue con `bloque--teclado` y `tp--teclado`.
- En el CSS, los colores de `.tp`, `.tp__num`, `a.tp:hover` y `.bloque .subtitulo::after` los define el bloque "COLORES VIVOS". No volver a declararlos en la sección "Portada e índice" del final: al estar más abajo, los pisarían.

**Recuadros**
- "Importante": `.esquema-nota.esquema-nota--importante` o `.pf__caja--importante`, en naranja, con el ícono `#i-importante`.
- "Recomendación" y buenas prácticas: `p.consejo` o `.pf__caja--consejo`, en verde, con el ícono `#i-consejo`.
- El ícono va delante del título: `<h3><svg class="ico tit-ico" aria-hidden="true" focusable="false"><use href="#i-importante"/></svg>Importante</h3>`.
- "Idea clave" sigue en cian.

**Etiquetas dentro del texto** (toman el color del programa del TP)
- Ruta de menú: `<span class="menu">Insertar › Imagen</span>`.
- Fórmula: `<code class="formula">=SUMA(B2:B9)</code>`.
- Las teclas siguen en `<kbd>`, sin color.

**Esquemas SVG**
- Ventana de un programa: marco con una barra en `--prog-claro` y los tres puntos (`--punto-rojo`, `--punto-amarillo`, `--punto-verde`). Los botones y rótulos que nombran algo del programa, en `--prog-texto`.
- Carpetas de Drive: en `--carpeta`, con fondo `--carpeta-claro` si es un panel. Ícono: `<svg class="ico ico--carpeta">`.
- Dos grupos en un mismo esquema: uno en cian (`--teclado`, `--cian-claro`, `--cian-texto`) y otro en naranja. Las viñetas de al lado repiten el color: `li.punto--cian` y `li.punto--naranja`.
- Rótulos chicos: con el color de lo que nombran, no en gris.
- Números en círculo (`.puntos__n` en las listas, `.badge` y `.p-ref` dentro del SVG): **cian oscuro en todos los TPs** (`--num-circulo`, #0E7490) con el número en blanco (Nicolás, 4/10/2026). No toman el color del programa ni llevan un color por número. En la Parte 2 (`lamina--compu`) los "!" siguen en naranja.
- Teclado: un tinte por zona y por dedo (`--tinte-*`), con las letras en `--tinta`. Dedos: meñique violeta, anular azul, medio verde, índice ámbar, pulgar naranja. El juego de mecanografía usa los mismos.
  - Zonas: alfanumérica blanco (`.z-alfa`), función azul (`.z-fn`), especiales naranja (`.z-esp`), numérico verde (`.z-num`), modificadoras violeta (`.z-mod`). Teclas sin dedo asignado: gris (`.d-no`).
  - En el SVG, las letras de las teclas van con `class="tt"` (en `--tinta`). `tt--claro` (blanco) queda para los números de los círculos (`.badge`) y los botones oscuros de las pantallas simuladas: no usarla en teclas.
  - Las muestras de leyendas y tablas (`.muestra .z-*` / `.d-*`) usan las mismas clases que el esquema, así coinciden solas.
- El color nunca va solo: cada zona, dedo o grupo lleva además su nombre, número o leyenda.

**Choques aceptados:** el verde es Hojas de cálculo y también "Recomendación"; el ámbar es Presentaciones y también carpetas. Se distinguen porque los recuadros y las carpetas llevan siempre ícono y título.

**No cambia:** títulos y texto corrido, fondo gris de las introducciones, "Idea clave" en cian, cabecera y pie.

**Controles extra:** texto naranja nunca sobre fondo cian (no llega a 4,5:1); medir el contraste de cada texto de color nuevo; que los colores salgan en la impresión.

## Controles antes de entregar un TP

- **Cada `.lamina` entra en una hoja A4 sin desbordar** (en impresión tiene alto fijo y `overflow: hidden`). Verificar con media `print`: `scrollHeight` no debe superar `clientHeight`. Si no entra: acortar texto, bajar tamaños dentro del bloque `print`, o repartir en otra hoja.
- Títulos de lámina en una sola línea en A4 (si no entra, clase `.tit__h--largo`).
- A 390 px y 360 px de ancho: sin scroll horizontal y con tablas legibles.
- Accesibilidad: íconos decorativos con `aria-hidden`; esquemas SVG con `role="img"` y texto alternativo; tablas con `<caption>` y `scope`; foco visible; enlace "Saltar al contenido".
- Sin errores en la consola. Botón PDF, barra de partes e índice funcionando.
- Las mediciones se hacen con el sitio servido por HTTP (un servidor local), no abriendo el archivo con `file://`: así el navegador bloquea las fuentes precargadas, aparecen errores que en GitHub Pages no existen y los altos salen mal.
- **Nombres de menús, botones y funciones:** tienen que ser los de la versión en español de Google Docs, Sheets y Presentaciones, y de Canva. Si no estás seguro de un nombre, marcalo para que Nicolás lo verifique en la pantalla.

## Contenido

- Edad: chicos de 12–13 años. Frases cortas, un concepto por bloque, ejemplos de la escuela y la vida cotidiana.
- Teoría en tono neutro ("podemos…"); consignas en voseo ("Indicá", "Escribí", "Abrí").
- No adelantar temas de TPs posteriores.
- **Herramientas: todo Google** (Documentos, Hojas de cálculo, Presentaciones) más Canva. No mencionar Word, Excel ni PowerPoint. Los alumnos entran con su propia cuenta de Google: el TP2 enseña a entrar a la cuenta y a Drive, y suma una hoja-guía sin número para crear la cuenta (ver "Decisiones confirmadas (4/10/2026)").
- **Hojas de cálculo:** funciones en español (`SUMA`, `PROMEDIO`, `MAX`, `MIN`, `CONTAR`, `CONTARA`, `CONTAR.SI`). Con la configuración regional de Argentina, los argumentos se separan con punto y coma: `=CONTAR.SI(B2:B9;">=6")`.
- **Entregas:** van a Google Classroom.
- **Capturas de pantalla:** el TP1 explica cómo sacarlas (lámina 4 y "Para profundizar") porque se usan en casi todas las entregas. En Windows: `Windows + Impr Pant` guarda la pantalla completa en Imágenes › Capturas de pantalla; `Windows + Shift + S` recorta una parte.

## Juego de mecanografía

- Es un sitio aparte: repo `Prof-NkoCussi/Juego-Mecanografia`, link `https://prof-nkocussi.github.io/Juego-Mecanografia/`.
- En este cuadernillo **solo se enlaza**: un botón en la Práctica del TP1 y un acceso en `index.html`. Se abre en una pestaña nueva. No copiar código del juego acá.
- Al terminar cada nivel, el juego muestra nombre, nivel, tiempo, velocidad, precisión, estrellas y fecha. Esa pantalla es la que se captura y se sube a Classroom.

## Plan del cuadernillo

12 TPs · 47 láminas · unas 2 semanas por TP. Todo el texto de las láminas es nuevo.

| TP | Nombre | Láminas | Temas, una lámina por tema |
|---|---|---|---|
| **Módulo 1 · Teclado y mecanografía** | | | |
| 1 | El teclado: mi herramienta de trabajo | 1–4 | zonas del teclado (alfanuméricas, función, especiales, numérico, modificadoras) · postura y posición de las manos · un dedo para cada tecla · atajos básicos (Ctrl+C, Ctrl+V, Ctrl+Z, Ctrl+S, Alt+Tab) y captura de pantalla |
| **Módulo 2 · Documentos de texto (Documentos de Google)** | | | |
| 2 | Mi primer documento | 5–8 | entrar a la cuenta y a Drive (+ guía sin número: crear una cuenta de Google) · crear, abrir y guardar · fuente, tamaño y color · negrita, cursiva, subrayado y alineación |
| 3 | Documento con estructura | 9–12 | títulos (Título, Título 1, Título 2) · listas numeradas y con viñetas · interlineado, espaciado y sangrías · tabla simple |
| 4 | Documento con imágenes y enlaces | 13–16 | insertar imágenes (subir y desde la web) · tamaño, ubicación y ajuste de texto · hipervínculos · encabezado, pie y numeración de páginas |
| 5 | Trabajo colaborativo y revisión | 17–20 | compartir y permisos (editor, comentarista, lector) · comentarios y sugerencias · historial de versiones · tabla de contenidos automática y exportar a PDF |
| **Módulo 3 · Hojas de cálculo (Hojas de cálculo de Google)** | | | |
| 6 | Conociendo la hoja de cálculo | 21–24 | filas, columnas, celdas y referencias (A1, B5) · tipos de datos (texto, número, fecha) · ancho, alto y formato de número · bordes y colores de fondo |
| 7 | Mis primeras fórmulas | 25–27 | qué es una fórmula y operadores (+, -, *, /) · fórmulas con referencias · SUMA y PROMEDIO |
| 8 | Más funciones útiles | 28–31 | CONTAR y CONTARA · MAX y MIN · cantidad × precio = subtotal · copiar fórmulas: referencias relativas y absolutas ($) |
| 9 | Gráficos y presentación de datos | 32–35 | ordenar y filtros simples · qué gráfico para qué dato (barras, torta, líneas) · insertar y personalizar (título, colores, etiquetas) · contar con condición: CONTAR.SI |
| **Módulo 4 · Presentaciones y diseño (Presentaciones de Google y Canva)** | | | |
| 10 | Mi primera presentación | 36–39 | diapositivas y diseños · título y contenido · imágenes y su formato · tipos de letra y colores acordes al tema |
| 11 | Presentación con efectos | 40–43 | transiciones · animaciones de objetos · video y audio · notas del orador y modo presentación |
| 12 | Diseño en Canva y edición de imagen | 44–47 | Canva: navegación, plantillas, elementos, texto y fondos · buenas prácticas (jerarquía, contraste, espacio en blanco) · edición básica (recorte, brillo, contraste, filtros) · exportar (PNG, JPG, PDF) |

## Práctica y entrega de cada TP (texto de Nicolás)

(C) = corrección que Nicolás aprobó sobre su plan original.

- **TP1.** Práctica: esquema dibujado o impreso del teclado identificando las zonas · práctica de mecanografía en el juego (mínimo 5 niveles terminados, con captura de cada resultado) (C) · lista de 15 atajos de teclado con su función. Entrega: capturas del juego + esquema y lista de atajos.
- **TP2.** Práctica: escribir una autobiografía de 1 página con título centrado, párrafos justificados, palabras clave en negrita y al menos 3 estilos de fuente. Entrega: link al documento compartido.
- **TP3.** Práctica: armar un documento sobre un tema libre (un deporte, una banda, un videojuego, un hobby) con título, 3 subtítulos, una lista de cosas, una numerada y una tabla con datos. Entrega: documento + capturas.
- **TP4.** Práctica: crear una guía turística de su barrio o ciudad: 3 lugares, cada uno con foto, descripción y un link a Google Maps. Encabezado con su nombre y pie con número de página. Entrega: documento.
- **TP5.** Práctica: en parejas, crear un folleto de 2 páginas sobre un tema acordado (cuidado del medio ambiente, salud, etc.). Cada uno escribe la mitad, se hacen sugerencias mutuamente y entregan en PDF + Doc. Entrega: PDF + link al documento compartido.
- **TP6.** Práctica: "lista de mis cosas favoritas": tabla de 5 columnas (Categoría, Nombre, Año, Puntaje 1-10, Comentario) con al menos 15 filas. Formato visual: encabezado con color, bordes, colores de fila alternados. Entrega: link a la hoja.
- **TP7.** Práctica: planilla "Mis gastos del mes": columnas (Fecha, Concepto, Categoría, Monto). Cargar 20 gastos inventados. Al final: total con SUMA y promedio con PROMEDIO (C: MAX y MIN pasan al TP8). Entrega: hoja con las fórmulas visibles en una sección comentada.
- **TP8.** Práctica: planilla "Lista de compras del kiosco": columnas (Producto, Cantidad, Precio unitario, Subtotal). Calcular cada subtotal con multiplicación, total general con SUMA, cuántos productos hay cargados con CONTARA (C) y el precio más alto con MAX (C). Entrega: hoja.
- **TP9.** Práctica: planilla "Notas del trimestre": tabla con 8 materias y 3 notas por materia. Calcular el promedio de cada materia. Contar aprobados y desaprobados con CONTAR.SI (C). Generar un gráfico de barras con los promedios y uno de torta con la cantidad de aprobados y desaprobados. Entrega: hoja con tabla + 2 gráficos.
- **TP10.** Práctica: presentación de 6 a 8 diapositivas sobre un tema libre (un personaje histórico, un país, un artista, un deporte). Estructura: portada, índice, 4 o 5 diapositivas de contenido, cierre. Entrega: link a la presentación.
- **TP11.** Práctica: mejorar la presentación del TP10 sumando transiciones consistentes, mínimo 3 elementos animados, un video de YouTube relacionado con el tema y notas del orador en al menos 3 diapositivas. Entrega: link + video corto (con el celular) presentando 1 minuto del tema.
- **TP12.** Práctica: crear 3 piezas en Canva: un afiche A4 promocionando un evento ficticio, un post cuadrado para Instagram y una historia vertical. Todas sobre un mismo tema o marca personal. Entrega: las 3 piezas exportadas en PNG.

## Decisiones confirmadas (2/10/2026)

- **Laboratorio:** Windows 10, teclados en español (con Ñ). Valen los atajos de captura de arriba.
- **TP1:** el esquema del teclado y la lista de 15 atajos van **en la carpeta** (foto a Classroom).
- **TP1:** los 5 niveles del juego son los niveles 1 a 5 de la Parte 1 (fila guía, fila superior, fila inferior, todas las letras, números).
- **Juego:** todavía no está hecho (el repo solo tiene su plan). El TP1 enlaza igual al link definitivo; el acceso de `index.html` queda en "Próximamente" hasta que se publique.
- **Cabecera:** `TALLER DE PROCESAMIENTO DE DATOS` + `1.ER AÑO`.

## Decisiones confirmadas (4/10/2026)

- **Colores vivos** aplicados a la portada y al TP1 (ver la sección "Colores vivos").
- **Portada, Módulo 1:** en el cian de base (franja, barrita, número y etiqueta). Ver la excepción en "Colores vivos › Portada".
- **TP2, guía "Crear una cuenta de Google":** hoja sin número entre la lámina 5 y la 6 (`article#crear-cuenta`, ícono en el título en vez de número, pie `TP 2`), para no correr la numeración de las 47 láminas. Seis pantallas simuladas; el recuadro cian (`.v-toque`) marca lo que se toca. Avisa que hacen falta 13 años o más (si no, un adulto la crea con "Para mi hijo").
- **Tarjetas "Próximamente":** mantienen la opacidad .62. Con eso, su texto queda por debajo de 4,5:1; se acepta porque son tarjetas inactivas. Al activar un TP, sus colores vuelven a contraste completo.

## Pendientes a consultar con Nicolás

- **TP9, torta de aprobados:** confirmar la nota de aprobación para la condición de CONTAR.SI.
