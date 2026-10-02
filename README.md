# Superprompt PRISMA 2020

Aplicación web de un solo archivo HTML que genera superprompts para redactar, sección por sección, una revisión sistemática de literatura conforme a la declaración PRISMA 2020 (27 ítems). Los prompts se copian y se usan en un modelo de lenguaje (Claude, ChatGPT, Gemini u otro).

- **Archivo:** `superprompt-prisma-2020-idc.html` (79 KB, sin dependencias de instalación)
- **Institución:** Instituto de Educación Superior Público "Diseño y Comunicación" (IDC), Lima, Perú
- **Responsable:** Jefatura de la Unidad de Investigación · Mg. Mario Quiroz Martínez · 2026

---

## Funciones

| Función | Descripción |
|---|---|
| Bloque 0 | Formulario de 15 campos: tema, marco de la pregunta (PICO, PEO, PICOS, SPIDER), P, I/E, C, O, período, idiomas, bases de datos, tipos de estudio, área, meta-análisis, revisores, registro y revista objetivo. |
| Ayuda por campo | Botón **i** en 20 campos con la descripción de la información requerida y un ejemplo. El cuadro se abre al enfocar el campo. |
| Navegador PRISMA | 28 secciones agrupadas en 6 fases, numeradas según los ítems oficiales de PRISMA 2020. |
| Carga de archivos .md | Tres puntos de carga: Bloque 0, archivos de contexto (múltiples, también por arrastre) y borrador por sección. |
| Asignación de archivos | Cada archivo de contexto se asigna a todas las secciones, a una fase o a un ítem. |
| Modos | Protocolo (tiempo futuro), Resultados (pretérito) e Integral (el modelo decide según el material). |
| Alcance | Sección, fase completa o informe completo. |
| Opciones | Idioma de redacción (español, inglés, portugués), extensión objetivo, estándares de escritura académica, protocolo de análisis y validación de datos (Fase 4) y filtro de estilo enciclopédico. |
| Salida | Superprompt con contador de caracteres y tokens estimados (aviso sobre 120 000 tokens), botón de copia y copia del Bloque 0 en Markdown. |

## Uso

1. Abra `superprompt-prisma-2020-idc.html` en un navegador (Chrome, Edge, Firefox o Safari en versión actual).
2. Complete el Bloque 0 o cárguelo desde un archivo `.md`. La página abre con datos de ejemplo; el botón **Vaciar formulario** los elimina.
3. Cargue los archivos de contexto `.md` (protocolo, matriz de extracción, notas de lectura, referencias, conteos del cribado) y asigne cada uno a su ámbito.
4. Seleccione la sección en el navegador lateral. Si ya tiene texto redactado, péguelo o cárguelo como borrador.
5. Elija modo, alcance e idioma.
6. Pulse **Copiar superprompt** y péguelo en el modelo de lenguaje.

Los campos críticos vacíos (tema, P, I/E, O) hacen que el prompt pida al modelo proponer opciones y detenerse hasta recibir una elección. Los demás campos vacíos se completan con una propuesta marcada `[VERIFICAR]`.

## Formato del archivo Bloque 0

El cargador reconoce líneas `etiqueta: valor`, con o sin viñetas, numeración o el prefijo `>`:

```markdown
> **BLOQUE 0 — DATOS DE ENTRADA**
> 1. Tema general de la revisión: Uso de rúbricas analíticas en proyectos de diseño gráfico
> 2. Pregunta de investigación (PICO):
>    - P (Población / Problema): Estudiantes de educación superior técnica en diseño
>    - I/E (Intervención o Exposición): Retroalimentación con rúbricas digitales
>    - C (Comparación, si aplica): Calificación holística sin rúbrica
>    - O (Resultados / Outcomes): Rendimiento académico; autorregulación
> 3. Período de búsqueda: 2015–2026
> 4. Idiomas incluidos: español, inglés, portugués
> 5. Bases de datos previstas: Scopus, Web of Science, ERIC, SciELO
> 6. Tipo(s) de estudio a incluir: experimentales, cuasiexperimentales y mixtos
> 7. Área disciplinar principal: Educación superior / diseño gráfico
> 8. ¿Esperas realizar meta-análisis?: Aún no lo sé
> 9. Número de revisores: 2
> 10. Registro del protocolo: OSF Registries — pendiente
> 11. Revista objetivo: Revista Enfoques
```

El botón **Copiar Bloque 0 en Markdown** produce este mismo formato.

## Estructura del superprompt

1. Rol
2. Modo de trabajo
3. Datos de la revisión (Bloque 0)
4. Sección o secciones a redactar: tareas, formato de salida, insumos requeridos, borrador previo y lista de verificación
5. Material de referencia: contenido de los archivos delimitado con `<documento nombre="…">`
6. Reglas de integridad: prohibición de inventar estudios, autores, DOI o cifras; marcadores `[COMPLETAR]`; citas APA 7
7. Estándares de escritura académica (opcional)
8. Protocolo de análisis y validación de datos (opcional, solo con secciones de la Fase 4)
9. Filtro de estilo (opcional)
10. Entrega: texto, tablas o diagramas Mermaid, marcadores pendientes, decisiones metodológicas y, si aplica, registro de validación

## Secciones e ítems PRISMA 2020

| Fase | Secciones | Ítems |
|---|---|---|
| 1. Título y resumen | Título; resumen estructurado (PRISMA 2020 for Abstracts) | 1–2 |
| 2. Introducción | Justificación; objetivos y preguntas | 3–4 |
| 3. Métodos | Elegibilidad; fuentes; estrategia de búsqueda (PRISMA-S); selección; extracción; ítems de datos; riesgo de sesgo; medidas del efecto; síntesis; sesgo de notificación; certeza | 5–15 |
| 4. Resultados | Selección (diagrama de flujo); características; riesgo de sesgo; resultados individuales; síntesis; sesgos de notificación; certeza | 16–22 |
| 5. Discusión | Interpretación; limitaciones; implicaciones | 23a–23d |
| 6. Otra información | Registro y protocolo; financiamiento y conflictos de intereses; disponibilidad de datos | 24–27 |

### Diferencias con el skill `prisma-sr`

La herramienta sigue la numeración y los criterios de Page et al. (2021) cuando difieren del skill de origen:

- La Discusión ocupa el ítem 23 (23a–23d); el registro es el ítem 24; financiamiento, 25; conflictos de intereses, 26; disponibilidad de datos, 27.
- El diagrama de flujo tiene tres etapas (identificación, cribado, incluidos), no las cuatro de PRISMA 2009.
- El riesgo de sesgo usa RoB 2 para ensayos aleatorizados y ROBINS-I para estudios no aleatorizados, en lugar de la escala de Jadad.
- Para síntesis sin meta-análisis se aplica SWiM; para hallazgos cualitativos, GRADE-CERQual.

## Publicación en GitHub Pages

1. Cree un repositorio y suba `superprompt-prisma-2020-idc.html`. Puede renombrarlo `index.html` para que sea la página de inicio.
2. En **Settings → Pages**, seleccione la rama `main` y la carpeta raíz.
3. La página queda disponible en `https://<usuario>.github.io/<repositorio>/`.

## Almacenamiento y privacidad

- El contenido del formulario, los archivos cargados y los borradores se guardan en el `localStorage` del navegador, asociado al dominio donde se abre la página. No se envían a ningún servidor.
- Cada navegador y cada dominio conservan datos independientes. Borrar los datos del sitio elimina el trabajo guardado.
- Los archivos cargados se incluyen como texto dentro del superprompt; revise su contenido antes de pegarlo en un servicio externo.

## Requisitos técnicos

- Navegador con JavaScript habilitado.
- Conexión a internet solo para las tipografías (Literata, Public Sans, JetBrains Mono desde Google Fonts). Sin conexión se usan las fuentes del sistema.
- Formatos de carga aceptados: `.md`, `.markdown` y `.txt` en UTF-8.

## Referencias

Campbell, M., McKenzie, J. E., Sowden, A., Katikireddi, S. V., Brennan, S. E., Ellis, S., Hartmann-Boyce, J., Ryan, R., Shepperd, S., Thomas, J., Welch, V., & Thomson, H. (2020). Synthesis without meta-analysis (SWiM) in systematic reviews: Reporting guideline. *BMJ, 368*, l6890. https://doi.org/10.1136/bmj.l6890

Page, M. J., McKenzie, J. E., Bossuyt, P. M., Boutron, I., Hoffmann, T. C., Mulrow, C. D., Shamseer, L., Tetzlaff, J. M., Akl, E. A., Brennan, S. E., Chou, R., Glanville, J., Grimshaw, J. M., Hróbjartsson, A., Lalu, M. M., Li, T., Loder, E. W., Mayo-Wilson, E., McDonald, S., … Moher, D. (2021). The PRISMA 2020 statement: An updated guideline for reporting systematic reviews. *BMJ, 372*, n71. https://doi.org/10.1136/bmj.n71

Rethlefsen, M. L., Kirtley, S., Waffenschmidt, S., Ayala, A. P., Moher, D., Page, M. J., Koffel, J. B., & PRISMA-S Group. (2021). PRISMA-S: An extension to the PRISMA statement for reporting literature searches in systematic reviews. *Systematic Reviews, 10*, 39. https://doi.org/10.1186/s13643-020-01542-z

Sterne, J. A. C., Hernán, M. A., Reeves, B. C., Savović, J., Berkman, N. D., Viswanathan, M., Henry, D., Altman, D. G., Ansari, M. T., Boutron, I., Carpenter, J. R., Chan, A.-W., Churchill, R., Deeks, J. J., Hróbjartsson, A., Kirkham, J., Jüni, P., Loke, Y. K., Pigott, T. D., … Higgins, J. P. T. (2016). ROBINS-I: A tool for assessing risk of bias in non-randomised studies of interventions. *BMJ, 355*, i4919. https://doi.org/10.1136/bmj.i4919

Sterne, J. A. C., Savović, J., Page, M. J., Elbers, R. G., Blencowe, N. S., Boutron, I., Cates, C. J., Cheng, H.-Y., Corbett, M. S., Eldridge, S. M., Emberson, J. R., Hernán, M. A., Hopewell, S., Hróbjartsson, A., Junqueira, D. R., Jüni, P., Kirkham, J. J., Lasserson, T., Li, T., … Higgins, J. P. T. (2019). RoB 2: A revised tool for assessing risk of bias in randomised trials. *BMJ, 366*, l4898. https://doi.org/10.1136/bmj.l4898

---

Jefatura de la Unidad de Investigación · Mg. Mario Quiroz Martínez · 2026
Instituto de Educación Superior Público "Diseño y Comunicación" · Lima, Perú
