# Cuadernillo web · Taller de Procesamiento de Datos (1.er año)

Sitio estático con los TPs del Taller de Procesamiento de Datos. 4 horas cátedra por semana.
Docente: Prof. Nicolás A. Cussi · C.T.P. "Olga B. de Arko" · Ushuaia.
Repo: `Prof-NkoCussi/Cuadernillo-Web-Procesamiento-de-Datos` · se publica con GitHub Pages · los alumnos lo abren desde el celular y desde las computadoras del laboratorio.
Creado como copia del repo base `Prof-NkoCussi/Cuadernillo-Web-Base-de-Datos-1`: misma estructura, misma paleta, cambia la materia y el contenido.

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

- **Paleta:** la misma de Base de Datos. No tocar las variables de color de `:root`.
- **Cabecera de cada hoja:** `TALLER DE PROCESAMIENTO DE DATOS` con la bajada `1.ER AÑO`, y a la derecha `TRABAJO PRÁCTICO N°X` con la barra cian vertical. Mismas reglas de tamaño y de celular que el repo base (el nombre es más largo: verificar a 360 px).
- **Pie de cada hoja:** `Taller de Procesamiento de Datos - Prof. Nicolás A. Cussi` + número de lámina (o `TP N` en profundizar y actividades).
- **Ícono de la materia:** una computadora con teclado, en el mismo estilo (trazo oscuro + relleno cian).
- **Sin eslóganes ni frases decorativas.**
- **Progreso:** la clave de `localStorage` es `tpd1:tp-visto-`. No usar `bd1:`: todos los cuadernillos comparten el dominio `prof-nkocussi.github.io` y se pisarían las marcas de "✓ Visto".

## Formato de cada TP — copiar la estructura de `unidades/tp01.html`

1. **Barra superior** (`header.barra`): "← Índice" · "TP N°X — nombre del TP" · botón `data-imprimir`. Debajo, `nav.partes` con accesos a cada lámina, "Para profundizar" y "Actividades".
2. **Láminas** (`article.lamina#pag-N`): `.cab` → `.tit` (número en cian + título + subtítulo) → bloques → `.idea` (Idea clave) → `.pie`.
3. **Para profundizar** (`article.lamina.lamina--pf#profundizar`): `.pf-grid` de 2×2, un bloque `.pf` por lámina (texto + recuadro `.pf__caja` con ejemplo o lista). Si el TP tiene 3 láminas, el cuarto bloque integra o suma un ejemplo.
4. **Actividades** (`article.lamina.lamina--act`, ids `actividades` y `actividades-2`), en dos hojas:
   - **Parte 1 · Para hacer en la carpeta:** banda `.act-banda`, `.consigna`, y un punto `.act` por lámina con incisos a), b), c), en grilla `.acts--2col`.
   - **Parte 2 · Práctica en la computadora:** la "Práctica" de Nicolás, partida en pasos numerados, y un recuadro **"Entrega"** con lo que se sube a Classroom.
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

## Controles antes de entregar un TP

- **Cada `.lamina` entra en una hoja A4 sin desbordar** (en impresión tiene alto fijo y `overflow: hidden`). Verificar con media `print`: `scrollHeight` no debe superar `clientHeight`. Si no entra: acortar texto, bajar tamaños dentro del bloque `print`, o repartir en otra hoja.
- Títulos de lámina en una sola línea en A4 (si no entra, clase `.tit__h--largo`).
- A 390 px y 360 px de ancho: sin scroll horizontal y con tablas legibles.
- Accesibilidad: íconos decorativos con `aria-hidden`; esquemas SVG con `role="img"` y texto alternativo; tablas con `<caption>` y `scope`; foco visible; enlace "Saltar al contenido".
- Sin errores en la consola. Botón PDF, barra de partes e índice funcionando.
- **Nombres de menús, botones y funciones:** tienen que ser los de la versión en español de Google Docs, Sheets y Presentaciones, y de Canva. Si no estás seguro de un nombre, marcalo para que Nicolás lo verifique en la pantalla.

## Contenido

- Edad: chicos de 12–13 años. Frases cortas, un concepto por bloque, ejemplos de la escuela y la vida cotidiana.
- Teoría en tono neutro ("podemos…"); consignas en voseo ("Indicá", "Escribí", "Abrí").
- No adelantar temas de TPs posteriores.
- **Herramientas: todo Google** (Documentos, Hojas de cálculo, Presentaciones) más Canva. No mencionar Word, Excel ni PowerPoint. Los alumnos entran con su propia cuenta de Google: el TP2 enseña a entrar a la cuenta y a Drive, no a crear la cuenta.
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
| 2 | Mi primer documento | 5–8 | entrar a la cuenta y a Drive · crear, abrir y guardar · fuente, tamaño y color · negrita, cursiva, subrayado y alineación |
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

## Pendientes a consultar con Nicolás

- **TP9, torta de aprobados:** confirmar la nota de aprobación para la condición de CONTAR.SI.
