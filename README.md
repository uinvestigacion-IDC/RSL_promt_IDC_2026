# Superprompt PRISMA 2020

Aplicación web de un solo archivo HTML que genera superprompts para redactar, sección por sección, una revisión sistemática de literatura conforme a la declaración PRISMA 2020 (27 ítems). Los prompts se copian y se usan en un modelo de lenguaje (Claude, ChatGPT, Gemini u otro).

- **Archivo:** `index.html` (115 KB, sin dependencias de instalación)
- **Institución:** Instituto de Educación Superior Público "Diseño y Comunicación" (IDC), Lima, Perú
- **Responsable:** Jefatura de la Unidad de Investigación · Mg. Mario Quiroz Martínez · 2026

---

## Funciones

| Función | Descripción |
|---|---|
| Bloque 0 | Formulario con tema, carrera profesional, línea de investigación, marco de la pregunta (PICO, PEO, PICOS, SPIDER), componentes del marco, período, idiomas, bases de datos, tipos de estudio, área, meta-análisis, revisores, registro y revista objetivo. Las etiquetas de los componentes cambian según el marco elegido. |
| Carrera y línea de investigación | Diseño de Interiores, Diseño Publicitario, Diseño de Modas, Comunicación Audiovisual, Cursos transversales y Otros (con campo para especificar). Las líneas de cada carrera y las seis líneas transversales provienen del Memorando Múltiple N.º 05/JUI/IDC/2025-II; la opción «Otra línea» admite texto libre. |
| Ruta PRISMA según el marco | Gráfico SVG integrado en la página: componentes del marco → pregunta de investigación → ocho etapas (elegibilidad, búsqueda, selección, extracción, riesgo de sesgo, síntesis, certeza, informe) con la herramienta que corresponde a cada marco. Al pulsar una etapa se abre su sección PRISMA. |
| Ayuda por campo | Botón **i** con la descripción de la información requerida y un ejemplo; el texto se adapta al marco (p. ej., S = muestra en SPIDER). El cuadro se abre al enfocar el campo. |
| Ayuda de botones | El encabezado explica la función de **Cargar Bloque 0 (.md)**, **Copiar Bloque 0 en Markdown** y **Limpiar campos**. |
| Limpiar campos | Vacía el Bloque 0, los archivos de contexto, los borradores y la extensión objetivo, previa confirmación. No modifica la galería. |
| Navegador PRISMA | 28 secciones agrupadas en 6 fases, numeradas según los ítems oficiales de PRISMA 2020. |
| Carga de archivos .md | Tres puntos de carga: Bloque 0, archivos de contexto (múltiples, también por arrastre) y borrador por sección. |
| Asignación de archivos | Cada archivo de contexto se asigna a todas las secciones, a una fase o a un ítem. |
| Modos | Protocolo (tiempo futuro), Resultados (pretérito) e Integral (el modelo decide según el material). |
| Alcance | Sección, fase completa o informe completo. |
| Opciones | Idioma de redacción (español, inglés, portugués), extensión objetivo, estándares de escritura académica, protocolo de análisis y validación de datos (Fase 4), especificación del diagrama de flujo PRISMA 2020 en SVG y filtro de estilo enciclopédico. |
| Salida | Superprompt con contador de caracteres y tokens estimados (aviso sobre 120 000 tokens), botón de copia y botón **Guardar en galería**. |
| Galería de prompts | Guarda cada prompt con tema, carrera, línea, marco, alcance, modo y fecha. Filtro por carrera (cuatro carreras, Cursos transversales y Otros), búsqueda por tema o línea, y acciones Copiar, Ver, Cargar datos y Eliminar. **Exportar galería (.md)** descarga todos los prompts agrupados por carrera. |

## Uso

1. Abra `index.html` en un navegador (Chrome, Edge, Firefox o Safari en versión actual).
2. Complete el Bloque 0 o cárguelo desde un archivo `.md`. Seleccione la carrera profesional, la línea de investigación y el marco de la pregunta. La página abre con datos de ejemplo; **Vaciar formulario** borra solo el Bloque 0 y **Limpiar campos** borra todo el trabajo en curso.
3. Revise el gráfico **Ruta PRISMA**: los componentes en ámbar están sin completar.
4. Cargue los archivos de contexto `.md` (protocolo, matriz de extracción, notas de lectura, referencias, conteos del cribado) y asigne cada uno a su ámbito.
5. Seleccione la sección en el navegador lateral o en el gráfico. Si ya tiene texto redactado, péguelo o cárguelo como borrador.
6. Elija modo, alcance e idioma.
7. Pulse **Copiar superprompt** y péguelo en el modelo de lenguaje. Pulse **Guardar en galería** para conservarlo (requiere tema y carrera).

Los campos críticos vacíos (tema y los componentes de población/muestra, intervención/exposición/fenómeno y resultados/evaluación) hacen que el prompt pida al modelo proponer opciones y detenerse hasta recibir una elección. Los demás campos vacíos se completan con una propuesta marcada `[VERIFICAR]`.

## Marcos de la pregunta

| Marco | Componentes | Uso | Riesgo de sesgo / calidad | Síntesis | Certeza |
|---|---|---|---|---|---|
| PICO | P, I, C, O | Intervenciones con comparador | RoB 2 · ROBINS-I | Meta-análisis o SWiM | GRADE |
| PEO | P, E, O | Exposiciones sin intervención asignada | ROBINS-E · JBI · Newcastle-Ottawa | Meta-análisis de asociación o narrativa | GRADE |
| PICOS | P, I, C, O, S (diseño) | PICO con restricción del diseño de estudio | Según el diseño S | Meta-análisis por diseño o SWiM | GRADE |
| SPIDER | S (muestra), PI, D, E, R | Síntesis cualitativa o de métodos mixtos | CASP · JBI-QARI · MMAT | Síntesis temática o meta-agregación | GRADE-CERQual |

Combinación de bloques de búsqueda: PICO `P AND I (AND O)`; PEO `P AND E AND O`; PICOS `P AND I AND O` con S como filtro de diseño; SPIDER `(S AND PI) AND (D OR E) AND R`, complementada con otra estrategia por su menor sensibilidad (Methley et al., 2014).

## Formato del archivo Bloque 0

El cargador reconoce líneas `etiqueta: valor`, con o sin viñetas, numeración o el prefijo `>`. Las líneas de componentes aceptan el formato de cualquier marco (`P — Población…`, `PI — Fenómeno de interés…`, `R — Tipo de investigación…`). Una carrera o línea que no figura en las listas se carga como «Otros» u «Otra línea» con el texto leído.

```markdown
> **BLOQUE 0 — DATOS DE ENTRADA**
> 1. Tema general de la revisión: Uso de rúbricas analíticas en proyectos de diseño gráfico
> 2. Carrera profesional: Diseño Publicitario
> 3. Línea de investigación: Identidad corporativa y branding
> 4. Marco de la pregunta: PICO
> 5. Pregunta de investigación (PICO):
>    - P — Población o problema: Estudiantes de educación superior técnica en diseño
>    - I — Intervención: Retroalimentación con rúbricas digitales
>    - C — Comparación (si aplica): Calificación holística sin rúbrica
>    - O — Resultados (outcomes): Rendimiento académico; autorregulación
> 6. Período de búsqueda: 2015–2026
> 7. Idiomas incluidos: español, inglés, portugués
> 8. Bases de datos previstas: Scopus, Web of Science, ERIC, SciELO
> 9. Tipo(s) de estudio a incluir: experimentales, cuasiexperimentales y mixtos
> 10. Área disciplinar principal: Educación superior / diseño gráfico
> 11. ¿Esperas realizar meta-análisis?: Aún no lo sé
> 12. Número de revisores: 2
> 13. Registro del protocolo: OSF Registries — pendiente
> 14. Revista objetivo: Revista Enfoques
```

El botón **Copiar Bloque 0 en Markdown** produce este mismo formato. Con PICOS y SPIDER, el diseño de estudio (S o D) aparece entre los componentes y no como línea separada. También se reconocen los archivos con el formato anterior (`P (Población / Problema)`, `I/E (Intervención o Exposición)`).

## Estructura del superprompt

1. Rol, con carrera profesional y línea de investigación
2. Modo de trabajo
3. Datos de la revisión (Bloque 0): componentes del marco, pregunta preliminar construida con ellos e indicaciones de uso del marco (bloques de búsqueda, herramientas de sesgo, síntesis y certeza)
4. Sección o secciones a redactar: tareas, formato de salida, insumos requeridos, borrador previo y lista de verificación
5. Material de referencia: contenido de los archivos delimitado con `<documento nombre="…">`
6. Reglas de integridad: prohibición de inventar estudios, autores, DOI o cifras; marcadores `[COMPLETAR]`; citas APA 7
7. Estándares de escritura académica (opcional)
8. Protocolo de análisis y validación de datos (opcional, solo con secciones de la Fase 4)
9. Diagrama de flujo PRISMA 2020 en SVG (opcional, cuando el alcance incluye los ítems 8 o 16)
10. Filtro de estilo (opcional)
11. Entrega: texto, tablas, diagrama SVG u otros diagramas en Mermaid, marcadores pendientes, decisiones metodológicas y, si aplica, registro de validación

La numeración se ajusta según las opciones activas.

### Especificación del diagrama PRISMA en SVG

La sección indica al modelo:

- Plantilla PRISMA 2020 para revisiones nuevas, de una columna o de dos («otros métodos») según las fuentes declaradas.
- Lienzo (`viewBox`, ancho 900 o 1660 px), `<title>` y `<desc>` accesibles y fondo blanco.
- Bandas de etapa Identificación, Cribado e Incluidos (sin la etapa «Elegibilidad» de PRISMA 2009), encabezado amarillo y colores definidos.
- Posición, ancho y texto exacto de cada caja, con `n = …` por fuente y por motivo de exclusión.
- Tipografía, longitud de línea, cálculo de la altura de las cajas y elementos prohibidos (`foreignObject`, scripts, fuentes web).
- Marcador de flecha y trazado de conectores verticales y horizontales.
- Comprobación aritmética de cada etapa; las discrepancias se marcan `[VERIFICAR]` sin corregir cifras.
- En modo protocolo, todos los valores como `n = [COMPLETAR]`.
- Entrega del código en un bloque `svg`, una tabla de conteos y el resultado de las comprobaciones.

## Secciones e ítems PRISMA 2020

| Fase | Secciones | Ítems |
|---|---|---|
| 1. Título y resumen | Título; resumen estructurado (PRISMA 2020 for Abstracts) | 1–2 |
| 2. Introducción | Justificación; objetivos y preguntas | 3–4 |
| 3. Métodos | Elegibilidad; fuentes; estrategia de búsqueda (PRISMA-S); selección; extracción; ítems de datos; riesgo de sesgo; medidas del efecto; síntesis; sesgo de notificación; certeza | 5–15 |
| 4. Resultados | Selección (diagrama de flujo en SVG); características; riesgo de sesgo; resultados individuales; síntesis; sesgos de notificación; certeza | 16–22 |
| 5. Discusión | Interpretación; limitaciones; implicaciones | 23a–23d |
| 6. Otra información | Registro y protocolo; financiamiento y conflictos de intereses; disponibilidad de datos | 24–27 |

### Diferencias con el skill `prisma-sr`

La herramienta sigue la numeración y los criterios de Page et al. (2021) cuando difieren del skill de origen:

- La Discusión ocupa el ítem 23 (23a–23d); el registro es el ítem 24; financiamiento, 25; conflictos de intereses, 26; disponibilidad de datos, 27.
- El diagrama de flujo tiene tres etapas (identificación, cribado, incluidos), no las cuatro de PRISMA 2009.
- El riesgo de sesgo usa RoB 2 para ensayos aleatorizados y ROBINS-I para estudios no aleatorizados, en lugar de la escala de Jadad.
- Para síntesis sin meta-análisis se aplica SWiM; para hallazgos cualitativos, GRADE-CERQual.

## Publicación en GitHub Pages

1. Cree un repositorio y suba `index.html` (y este `README.md`).
2. En **Settings → Pages**, seleccione la rama `main` y la carpeta raíz.
3. La página queda disponible en `https://<usuario>.github.io/<repositorio>/`.

## Almacenamiento y privacidad

- El contenido del formulario, los archivos cargados y los borradores se guardan en el `localStorage` del navegador (clave `prisma-sp-v1`), asociado al dominio donde se abre la página. No se envían a ningún servidor.
- La galería de prompts usa una clave aparte (`prisma-sp-gallery-v1`): **Limpiar campos** no la borra. Solo se elimina con **Eliminar**, **Vaciar galería** o al borrar los datos del sitio.
- Cada navegador y cada dominio conservan datos independientes: la galería guardada en un equipo no aparece en otro. Use **Exportar galería (.md)** para respaldarla o compartirla.
- El `localStorage` admite unos 5 MB. Los prompts que incluyen archivos de contexto extensos ocupan más espacio; si se llena, la página lo avisa al guardar.
- Los archivos cargados se incluyen como texto dentro del superprompt; revise su contenido antes de pegarlo en un servicio externo.

## Requisitos técnicos

- Navegador con JavaScript habilitado.
- Conexión a internet solo para las tipografías (Literata, Public Sans, JetBrains Mono desde Google Fonts). Sin conexión se usan las fuentes del sistema.
- Formatos de carga aceptados: `.md`, `.markdown` y `.txt` en UTF-8.

## Referencias

Campbell, M., McKenzie, J. E., Sowden, A., Katikireddi, S. V., Brennan, S. E., Ellis, S., Hartmann-Boyce, J., Ryan, R., Shepperd, S., Thomas, J., Welch, V., & Thomson, H. (2020). Synthesis without meta-analysis (SWiM) in systematic reviews: Reporting guideline. *BMJ, 368*, l6890. https://doi.org/10.1136/bmj.l6890

Cooke, A., Smith, D., & Booth, A. (2012). Beyond PICO: The SPIDER tool for qualitative evidence synthesis. *Qualitative Health Research, 22*(10), 1435–1443. https://doi.org/10.1177/1049732312452938

Instituto de Educación Superior Público "Diseño y Comunicación", Unidad de Investigación. (2025). *Memorando Múltiple N.º 05/JUI/IDC/2025-II: Convocatoria a participar en actividades de investigación e innovación tecnológica* [Documento interno]. Lima, Perú.

Methley, A. M., Campbell, S., Chew-Graham, C., McNally, R., & Cheraghi-Sohi, S. (2014). PICO, PICOS and SPIDER: A comparison study of specificity and sensitivity in three search tools for qualitative systematic reviews. *BMC Health Services Research, 14*, 579. https://doi.org/10.1186/s12913-014-0579-0

Page, M. J., McKenzie, J. E., Bossuyt, P. M., Boutron, I., Hoffmann, T. C., Mulrow, C. D., Shamseer, L., Tetzlaff, J. M., Akl, E. A., Brennan, S. E., Chou, R., Glanville, J., Grimshaw, J. M., Hróbjartsson, A., Lalu, M. M., Li, T., Loder, E. W., Mayo-Wilson, E., McDonald, S., … Moher, D. (2021). The PRISMA 2020 statement: An updated guideline for reporting systematic reviews. *BMJ, 372*, n71. https://doi.org/10.1136/bmj.n71

Rethlefsen, M. L., Kirtley, S., Waffenschmidt, S., Ayala, A. P., Moher, D., Page, M. J., Koffel, J. B., & PRISMA-S Group. (2021). PRISMA-S: An extension to the PRISMA statement for reporting literature searches in systematic reviews. *Systematic Reviews, 10*, 39. https://doi.org/10.1186/s13643-020-01542-z

Sterne, J. A. C., Hernán, M. A., Reeves, B. C., Savović, J., Berkman, N. D., Viswanathan, M., Henry, D., Altman, D. G., Ansari, M. T., Boutron, I., Carpenter, J. R., Chan, A.-W., Churchill, R., Deeks, J. J., Hróbjartsson, A., Kirkham, J., Jüni, P., Loke, Y. K., Pigott, T. D., … Higgins, J. P. T. (2016). ROBINS-I: A tool for assessing risk of bias in non-randomised studies of interventions. *BMJ, 355*, i4919. https://doi.org/10.1136/bmj.i4919

Sterne, J. A. C., Savović, J., Page, M. J., Elbers, R. G., Blencowe, N. S., Boutron, I., Cates, C. J., Cheng, H.-Y., Corbett, M. S., Eldridge, S. M., Emberson, J. R., Hernán, M. A., Hopewell, S., Hróbjartsson, A., Junqueira, D. R., Jüni, P., Kirkham, J. J., Lasserson, T., Li, T., … Higgins, J. P. T. (2019). RoB 2: A revised tool for assessing risk of bias in randomised trials. *BMJ, 366*, l4898. https://doi.org/10.1136/bmj.l4898

Thomas, J., & Harden, A. (2008). Methods for the thematic synthesis of qualitative research in systematic reviews. *BMC Medical Research Methodology, 8*, 45. https://doi.org/10.1186/1471-2288-8-45

---

Jefatura de la Unidad de Investigación · Mg. Mario Quiroz Martínez · 2026
Instituto de Educación Superior Público "Diseño y Comunicación" · Lima, Perú
