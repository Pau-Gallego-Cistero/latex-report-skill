---
name: renderizado-pdf
description: "Renderiza visualmente a PDF un informe LaTeX generado previamente por la skill informe. Se activa exclusivamente cuando el usuario solicita un renderizado y proporciona o hace referencia al main.tex y sus recursos. No requiere ni presupone la instalación de pdflatex, latexmk, xelatex, lualatex, TeX Live o MiKTeX. Reconstruye el documento en PDF preservando lo máximo posible la apariencia, estructura, contenido, ecuaciones, figuras, tablas, referencias, logo y estilo definidos por informe. No se activa ante una petición genérica de PDF."
---

# renderizado-pdf — Skill de renderizado visual de informes

Esta skill complementa a `informe`.

La skill `informe` es responsable de crear el documento fuente del informe, normalmente `main.tex`, junto con sus imágenes, logo y demás recursos.

La skill `renderizado-pdf` es responsable de transformar ese documento fuente y sus recursos en un PDF visualmente fiel al resultado esperado.

## Relación con la skill `informe`

El flujo previsto es:

1. `informe` crea el informe en LaTeX.
2. `informe` genera `main.tex` y reúne sus recursos.
3. `renderizado-pdf` recibe `main.tex` y todos sus recursos.
4. `renderizado-pdf` interpreta la estructura y el formato del documento.
5. `renderizado-pdf` reconstruye visualmente el documento como PDF.
6. `renderizado-pdf` comprueba el PDF resultante.
7. Se entrega el PDF final al usuario.

Esta skill no debe modificar innecesariamente el contenido científico generado por `informe`.

---

# Principio fundamental

El objetivo no es simplemente convertir texto a PDF.

El objetivo es producir un PDF que conserve visualmente, en la medida que permitan las herramientas disponibles, la apariencia que tendría el `main.tex` si se hubiera compilado mediante un motor LaTeX.

Por tanto, debe prestar especial atención a:

- estructura del documento
- portada
- título
- autor
- asignatura
- universidad
- logo
- encabezados
- secciones
- subsecciones
- párrafos
- ecuaciones
- unidades
- figuras
- tablas
- referencias
- numeración
- saltos de página
- márgenes
- espaciado
- alineación
- tipografía
- tamaño del texto
- negritas
- cursivas
- listas
- pies de figura
- distribución general de cada página

La prioridad es la fidelidad visual, no la reinterpretación creativa del diseño.

---

# Workflow

## 1. Recibir los archivos

Identifica todos los elementos necesarios para reconstruir el documento:

- `main.tex`
- `LogopequeUE.jpg`, si existe
- carpeta `Figures/`, si existe
- otros archivos gráficos utilizados
- archivos auxiliares que sean necesarios para interpretar el documento

No asumir que el informe está compuesto únicamente por `main.tex`.

Si existe una dependencia utilizada por el documento, debe localizarse antes de comenzar el renderizado.

---

## 2. Analizar `main.tex`

Leer e interpretar el documento completo.

Identificar:

- preámbulo
- paquetes utilizados
- configuración de página
- configuración tipográfica
- comandos personalizados
- variables del informe
- título
- autor
- asignatura
- universidad
- grado
- secciones
- subsecciones
- ecuaciones
- figuras
- tablas
- referencias
- listas
- saltos de página
- comandos de formato
- bloques especiales

No limitarse a extraer el texto plano.

El contenido y la estructura de LaTeX contienen información necesaria para reconstruir la apariencia del PDF.

---

## 3. Analizar la plantilla

Si `main.tex` procede de `informe`, respetar la plantilla utilizada por dicha skill.

No rediseñar el documento.

Mantener, siempre que sea posible:

- márgenes
- tamaño de página
- tamaños de letra
- colores
- jerarquía de títulos
- separación entre elementos
- posición del logo
- diseño de portada
- estilo de las figuras
- estilo de las tablas
- numeración
- espaciado
- alineaciones

La plantilla del usuario tiene prioridad sobre cualquier estilo genérico del sistema.

---

## 4. Reconstruir la portada

La portada debe conservar la estructura visual del documento original.

Comprobar:

- logo de la UEV
- título
- asignatura
- autor
- universidad
- grado
- posiciones relativas
- tamaños
- espaciado
- elementos decorativos

El logo debe utilizarse desde el archivo proporcionado.

No sustituir el logo por un icono, texto o imagen genérica si existe `LogopequeUE.jpg`.

---

## 5. Reconstruir las secciones

Mantener exactamente la jerarquía definida en `main.tex`.

Por ejemplo:

- Summary and objectives
- Principles
- Questions
- Conclusions
- References

Si el documento contiene otras secciones, conservarlas.

No cambiar nombres de secciones salvo que sea necesario para corregir un problema técnico evidente.

---

# Contenido

## Preservación del contenido

No resumir el informe.

No eliminar información para facilitar el renderizado.

No modificar:

- resultados
- valores numéricos
- ecuaciones
- conclusiones
- respuestas
- referencias
- texto científico

La tarea consiste en representar el contenido, no en reescribirlo.

Si se detecta un posible error científico o numérico, no modificarlo silenciosamente.

---

## Texto

Conservar:

- párrafos
- saltos de línea relevantes
- negrita
- cursiva
- énfasis
- listas
- símbolos
- caracteres especiales

La conversión de LaTeX a PDF debe producir texto legible y correctamente distribuido.

Evitar que:

- las palabras se corten incorrectamente
- las líneas se superpongan
- los párrafos desaparezcan
- los caracteres especiales se pierdan
- los símbolos matemáticos aparezcan como texto incorrecto

---

# Matemáticas

Las ecuaciones tienen prioridad alta.

Interpretar correctamente expresiones LaTeX como:

- fracciones
- subíndices
- superíndices
- raíces
- integrales
- sumatorios
- productos
- letras griegas
- vectores
- matrices
- derivadas
- límites
- unidades
- símbolos científicos

Por ejemplo, una expresión como:

\[
E = mc^2
\]

debe aparecer visualmente como una ecuación matemática y no como texto literal.

---

## Ecuaciones numeradas

Si `main.tex` utiliza entornos numerados como `equation`, conservar la numeración siempre que sea posible.

Si una ecuación es referenciada posteriormente en el documento, mantener la relación entre:

- ecuación
- número
- referencia dentro del texto

No eliminar números de ecuación únicamente porque el PDF se genere mediante un método alternativo.

---

# Unidades

Prestar especial atención a expresiones generadas mediante `siunitx`.

Por ejemplo:

- `\SI{3}{\electronvolt}`
- `\SI{10}{\meter}`
- `\SI{5.2}{\angstrom}`

Deben representarse visualmente como cantidades científicas correctamente formateadas.

No mostrar comandos LaTeX al usuario.

Por ejemplo, no debe aparecer literalmente:

`\SI{3}{\electronvolt}`

sino su representación visual correspondiente.

---

# Figuras

Localizar todas las imágenes utilizadas mediante `\includegraphics` u otros comandos.

Comprobar:

- que el archivo existe
- orientación
- proporción
- tamaño
- posición
- alineación
- caption
- numeración

Las figuras deben conservar aproximadamente el tamaño definido en el documento original.

Si `informe` especificó aproximadamente `0.55\textwidth`, respetar esa proporción.

No ampliar una figura arbitrariamente hasta ocupar toda la página.

---

## Captions

Las leyendas de las figuras deben conservarse.

Mantener:

- texto
- numeración
- unidades
- posición
- alineación

Nunca eliminar una caption para simplificar el renderizado.

---

# Tablas

Reconstruir las tablas respetando:

- número de columnas
- número de filas
- contenido
- alineación
- encabezados
- unidades
- líneas
- espaciado
- posición

No convertir una tabla en un párrafo de texto.

Si una tabla es demasiado grande para una página, distribuirla de forma razonable sin perder información.

---

# Referencias

Conservar la sección de referencias.

Mantener:

- autores
- año
- título
- URL
- fuente
- numeración

No inventar referencias.

No eliminar referencias simplemente porque el sistema de renderizado no pueda reproducir exactamente el mecanismo bibliográfico de LaTeX.

Si es necesario, reconstruir visualmente las referencias como texto formateado.

---

# Logo UEV

Si `main.tex` contiene el bloque del logo de la UEV y existe `LogopequeUE.jpg`, utilizar dicho archivo.

La posición debe reproducir lo más fielmente posible la posición definida en la plantilla.

No sustituir el logo por texto.

Si el usuario ha solicitado explícitamente un informe sin logo y el logo fue eliminado por `informe`, no volver a introducirlo.

---

# Diseño de página

Respetar:

- tamaño de página
- orientación
- márgenes
- ancho de texto
- separación entre párrafos
- separación entre secciones
- posición de figuras
- posición de tablas
- saltos de página

La distribución debe parecer un documento académico real.

No generar una página con:

- texto excesivamente comprimido
- grandes espacios vacíos injustificados
- figuras deformadas
- ecuaciones cortadas
- tablas fuera del margen
- títulos aislados al final de una página

---

# Saltos de página

Los saltos de página definidos explícitamente en `main.tex` deben respetarse cuando sea posible.

También debe evitarse crear saltos de página visualmente absurdos.

Por ejemplo:

- un título de sección sin contenido debajo
- una figura separada innecesariamente de su caption
- una ecuación aislada
- una tabla partida de manera ilegible

Si el salto de página original no puede reproducirse exactamente, priorizar una composición académica limpia.

---

# Listas

Reconstruir correctamente:

- listas numeradas
- listas con viñetas
- listas anidadas

Mantener:

- orden
- contenido
- jerarquía
- sangría

---

# Formato tipográfico

Respetar, en la medida de lo posible:

- tamaño de fuente
- negrita
- cursiva
- subrayado si existe
- versalitas si existen
- símbolos especiales
- alineación
- espaciado

No utilizar una tipografía radicalmente diferente si existe una alternativa razonablemente similar disponible.

---

# Código

Si el informe contiene código Python o Mathematica:

- conservar el código
- mantener su formato de bloque
- conservar indentación
- conservar saltos de línea
- utilizar una apariencia equivalente a la definida por `informe`
- evitar que las líneas se salgan del margen

El código debe aparecer como código, no como un párrafo normal.

Si el código es demasiado ancho, adaptar su tamaño o distribución de manera que siga siendo legible.

No modificar el código para conseguir que quepa.

---

# Comandos LaTeX no compatibles

No mostrar comandos LaTeX literalmente en el PDF salvo que el propio informe trate sobre código LaTeX.

Si una construcción LaTeX concreta no puede reproducirse exactamente, buscar la representación visual equivalente.

Ejemplos:

`\section{Principles}`

debe producir visualmente un encabezado equivalente a:

Principles

Y:

`\textbf{Important}`

debe producir texto visualmente equivalente a:

Important

No mostrar los comandos como contenido visible del informe.

---

# Funcionalidad no soportada

Si una característica extremadamente específica de LaTeX no puede reproducirse exactamente:

1. conservar el contenido
2. conservar la estructura
3. aproximar el aspecto visual
4. evitar errores visibles
5. no introducir contenido inventado

La fidelidad visual debe ser máxima dentro de las capacidades disponibles.

---

# No compilar LaTeX

Esta skill NO depende de que exista un compilador LaTeX.

No exigir:

- `pdflatex`
- `latexmk`
- `xelatex`
- `lualatex`
- TeX Live
- MiKTeX

No pedir al usuario que instale ninguna de estas herramientas.

El PDF debe generarse mediante las capacidades de creación/renderizado de documentos disponibles en el entorno de ejecución.

Si el entorno dispone accidentalmente de un compilador LaTeX y utilizarlo mejora significativamente la fidelidad, puede utilizarse internamente, pero no debe ser un requisito de la skill.

La ausencia de un compilador LaTeX no debe impedir el funcionamiento de esta skill.

---

# Fidelidad visual

La prioridad de fidelidad es:

1. estructura del documento
2. contenido científico
3. ecuaciones
4. figuras
5. tablas
6. portada
7. logo
8. jerarquía de títulos
9. distribución de página
10. tipografía
11. detalles menores de espaciado

No sacrificar contenido para conseguir una apariencia más sencilla.

---

# Control de calidad

Antes de entregar el PDF, realizar una comprobación visual y estructural.

Comprobar como mínimo:

- portada correcta
- título correcto
- autor correcto
- asignatura correcta
- logo presente cuando corresponde
- todas las secciones presentes
- todas las ecuaciones visibles
- ecuaciones correctamente formateadas
- todas las figuras presentes
- captions presentes
- tablas completas
- referencias presentes
- páginas correctamente ordenadas
- ausencia de texto cortado
- ausencia de elementos superpuestos
- ausencia de comandos LaTeX visibles
- ausencia de páginas completamente vacías
- márgenes razonables
- ausencia de imágenes deformadas
- ausencia de caracteres ilegibles

---

# Integridad del documento

Nunca eliminar contenido únicamente porque dificulte el renderizado.

Nunca inventar:

- resultados
- valores
- ecuaciones
- referencias
- figuras
- conclusiones

Si existe una limitación técnica, conservar el contenido y resolverla mediante una representación visual alternativa.

---

# Archivos de salida

El resultado principal debe ser:

`main.pdf`

Si el entorno requiere utilizar archivos temporales durante el proceso, no es necesario entregarlos al usuario.

Entregar únicamente los archivos finales relevantes.

Si el PDF no puede generarse por una limitación técnica real, explicar claramente qué elemento impidió completar el renderizado y entregar, cuando sea útil, los archivos fuente disponibles.

---

# Trigger

Esta skill tiene un trigger deliberadamente estricto.

Debe activarse cuando el usuario utilice explícitamente términos como:

- "renderizado"
- "renderiza el informe"
- "haz el renderizado"
- "renderiza el main.tex"
- "pásame el main.tex a PDF mediante el renderizado"
- "genera el PDF a partir del renderizado"

El término `renderizado` es el indicador principal.

No activar esta skill simplemente porque el usuario diga:

- "PDF"
- "hazme un PDF"
- "lee este PDF"
- "edita este PDF"
- "combina estos PDF"

Las tareas genéricas relacionadas con PDF pertenecen a otras skills.

---

# Objetivo final

La combinación de skills debe funcionar conceptualmente así:

`informe`
→ crea `main.tex`
→ crea/reúne logo, figuras y recursos
→ define estructura y formato académico

`renderizado-pdf`
→ lee `main.tex`
→ interpreta estructura y formato
→ utiliza todos los recursos
→ reconstruye visualmente el documento
→ genera `main.pdf`
→ comprueba el resultado
→ entrega el PDF final

El usuario no debe necesitar instalar herramientas LaTeX para utilizar `renderizado-pdf`.

El objetivo es que el PDF final sea visualmente lo más parecido posible al informe que habría producido la plantilla LaTeX de `informe`, sin depender de una compilación LaTeX real.
