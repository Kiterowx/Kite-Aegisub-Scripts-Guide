# Chrono Suite

Versión **1.5.3**.

Chrono Suite reúne revisión de tiempos y texto, Auto Timing, importación y utilidades de edición. Abre **Chrono Suite** o usa sus acciones directas bajo `: Kite Hotkeys :/Chrono Suite/`.

La interfaz admite español, inglés y portugués. Los nombres de acción en inglés sirven como referencia para los atajos.

## Elegir el alcance

<figure class="ui-shot">
  <img src="../../assets/captures/chronosuite-main-01.png" alt="Audit Markers configura la revisión; Utility Tools elige las ediciones. Deja vacíos los selectores que no quieras ejecutar." loading="lazy">
  <figcaption>Audit Markers configura la revisión; Utility Tools elige las ediciones. Deja vacíos los selectores que no quieras ejecutar.</figcaption>
</figure>

**EXECUTE** aplica las secciones activas. **Apply to** usa toda la selección o filtra por Style, Actor, Effect o Layer con el valor de **Filter**. Auto Timing respeta ese alcance.

Las utilidades de texto suelen excluir comentarios y dibujos. Las operaciones de tiempo, etiquetas, ordenación y comentarios tienen su propio alcance.

## Revisar con marcadores

Los resultados se escriben en Effect y conservan texto y tiempos. Configura los umbrales en **Config > Audit Presets**.

| Preajuste | Revisión |
| --- | --- |
| Full Audit | Texto, composición, tiempos, CPS, huecos y estructura. |
| Ends Only / Start Only | Cercanía de cada borde a fotogramas clave. |
| Duration / Overtime | Duraciones frente a los límites respectivos. |
| CPS | Velocidad de lectura. |
| Short Gaps / Large Gaps / Both Gaps | Huecos entre líneas vecinas. |

**Single Marker** ejecuta una comprobación individual: signos, espacios, solapes, saltos, etiquetas u otros criterios. **Clear previous markers** retira las marcas anteriores. **Ignore gap on KF** omite huecos que coinciden con fotogramas clave.

### Ejemplo: revisar un hueco de 80 ms

Selecciona dos líneas con estos tiempos, elige **Short Gaps** y fija **Short gap = 100 ms**. Deja vacías las utilidades de edición.

| Línea | Inicio | Fin | Marca |
| --- | --- | --- | --- |
| Quieto. | 1.00 s | 2.00 s | `[SHORT-GAP 80ms]` |
| He oído algo. | 2.08 s | 3.40 s | `[SHORT-GAP 80ms]` |

Las marcas señalan la pareja que debes revisar al escuchar la escena; no deciden si conviene eliminar el hueco.

## Editar texto, etiquetas y tiempos

| Sección | Operaciones habituales |
| --- | --- |
| Case | Mayúsculas, minúsculas, capitalización, cursiva y alineación superior. |
| Punct / Text | Puntuación, comillas, puntos suspensivos, espacios y tartamudeo. |
| Tags / Comments | Extraer/reinsertar etiquetas, unir bloques, gestionar comentarios y pliegues. |
| Smart | Ajustar a fotogramas clave, ocultar honoríficos y completar oraciones. |
| Split / Join | Dividir, unir y distribuir saltos `\N`. |
| Time / Sort | Copiar o desplazar tiempos, encadenar y ordenar. |
| Karaoke | Convertir palabras de romaji a karaoke `\k`. |

**Remove Honorifics** encierra los sufijos en comentarios `{…}`. **Merge Tags** une bloques contiguos sin quitar comentarios. **Join Lines** conserva el orden de filas del texto y toma el inicio mínimo y el fin máximo.

<details markdown="1">
<summary>Referencia de las utilidades</summary>

Cada sección tiene un desplegable independiente. Dejarlo vacío omite la sección.

### Case

| Acción | Resultado |
| --- | --- |
| Toggle `\an8` / Toggle Italics | Alterna alineación superior / cursiva. |
| Uppercase / Lowercase | Convierte todo el texto a mayúsculas / minúsculas. |
| Title Case | Inicial mayúscula por palabra. |
| Sentence Case | Inicial mayúscula por oración. |
| Capitalize First / Lowercase First | Cambia el primer carácter visible. |

### Punct / Text

| Acción | Resultado |
| --- | --- |
| Toggle ¡! / Toggle ¿? / Toggle ¡¿?! | Alterna signos de apertura. |
| Normalize Ellipsis | Unifica puntos suspensivos. |
| Add Ellipsis | Añade puntos suspensivos al final. |
| Erase Leading Ellipsis | Retira los iniciales. |
| Erase Inner Ellipsis | Retira los interiores y conserva los finales. |
| Ellipsis to Comma / Ellipsis to Period | Cambia los finales por coma / punto. |
| Unify Quotes / Latin Quotes («») | Unifica comillas / usa comillas angulares. |
| Normalize Dashes | Normaliza guiones y rayas. |
| Trim Trailing Spaces | Elimina espacios finales. |
| Remove Duplicate Letters | Elimina letras consecutivas repetidas. |
| Add Stutter / Stutter Manager | Añade tartamudeo / abre su gestor. |
| Add Ah Prefix | Añade «ah» al inicio. |

### Tags / Comments

| Acción | Resultado |
| --- | --- |
| Fold by Identifier | Pliega grupos de al menos dos líneas con el mismo identificador. |
| Extract Tags | Traslada etiquetas del texto a Effect. |
| Reinsert Tags | Devuelve etiquetas de Effect al texto y cambia punto y coma por coma dentro de los bloques. |
| Remove Tags | Retira bloques de etiquetas. |
| Merge Tags | Une bloques de etiquetas adyacentes: `{\an5}{\blur2}` pasa a `{\an5\blur2}`. Conserva comentarios y bloques separados. |
| Remove Comments | Retira comentarios internos. |
| Actor Parser | Extrae información del actor del texto. |
| Swap Comment | Alterna el estado de comentario. |
| Delete Comment Lines | Elimina filas comentadas. |
| Comments to Top / Bottom | Lleva comentarios al inicio / final de la selección. |
| Effects to Top | Lleva arriba las filas con Effect, conservando su orden relativo. |

### Smart

| Acción | Resultado |
| --- | --- |
| Bidirectional Snapping | Ajusta inicio y fin al fotograma clave más próximo dentro del alcance configurado. |
| Remove Honorifics | Encierra honoríficos japoneses en `{…}` para ocultarlos sin borrarlos de la fuente. |
| Caption Clarifier | Normaliza corchetes e indicaciones. |
| Complete Sentences | Une una oración incompleta con la siguiente si empieza en minúscula. Los solapes o continuaciones distintas se marcan `[POSSIBLE-JOIN]`. |
| Erase Blank Lines | Elimina líneas vacías. |
| Frame Effect | Escribe el fotograma inicial en Effect. |
| Copy Fold | Muestra filas ASS del pliegue de la primera línea seleccionada para copiarlas y selecciona ese pliegue. |

### Split / Join

| Acción | Resultado |
| --- | --- |
| Smart Break | Inserta `\N` si el ancho renderizado supera el disponible. |
| Split by Sentence / Comma | Divide por oración / coma. |
| Pivot `\N` | Desplaza el salto. |
| Remove `\N` | Retira los saltos y consolida espacios. |
| Join Lines | Une textos en orden de filas; abarca inicio mínimo y fin máximo y conserva metadatos de la primera fila. |
| Join Same Text | Une filas seleccionadas adyacentes con texto idéntico y estilo compatible. |
| Join Overlaps | Une grupos superpuestos, abarca sus límites y separa textos con `\N`. |
| Join Overlap Sentences | Une grupos superpuestos como oración en orden de filas; conserva la primera como base y amplía el final. |
| Divide by `\N` | Divide en cada salto existente. |

### Time / Sort

| Acción | Resultado |
| --- | --- |
| Copy Times | Copia tiempos de una línea a otras. |
| Time Picker | Selecciona por intervalo. |
| Sort by Length / CPS | Ordena por longitud visible / velocidad de lectura. |
| Sort Odd Even | Ordena según el valor numérico par o impar de Effect. |
| Count CPS | Muestra CPS promedio. |
| Import Text | Importa texto externo para sustitución controlada. |
| Kite Timing | Aplica márgenes adaptables, encadenado y protección de bordes con los valores de Config. |
| Shift First | Desplaza la selección para alinear la primera línea con el inicio de la segunda. |
| Start Snap Back / Forward | Lleva el inicio al fotograma clave anterior / siguiente. |
| End Snap Back / Forward | Lleva el fin al fotograma clave anterior / siguiente. |
| Add Lead-In Left / Right | Mueve el inicio atrás / adelante según el paso configurado. Si la anterior está encadenada a hueco cero, mueve también su fin. Con hueco positivo, el desplazamiento hacia atrás se detiene al tocarla. |
| Add Lead-Out Left / Right | Mueve el fin atrás / adelante y desplaza el inicio de la siguiente si están encadenadas. |
| Chain Left / Right | Extiende inicio / fin hasta la vecina dentro de la distancia máxima configurada. |

### Karaoke

**Romaji Karaoker (Word → `\k`)** genera karaoke de romaji por palabra con etiquetas `{\k}`.

</details>

### Ejemplo: encadenar dos líneas

Elige **Chain Right** con una distancia máxima de al menos 300 ms:

| Línea | Inicio | Fin anterior | Fin resultante |
| --- | --- | --- | --- |
| ¿Lo tienes? | 1.00 s | 1.80 s | 2.10 s |
| Casi. | 2.10 s | 3.50 s | 3.50 s |

La primera se extiende hasta la siguiente. Úsalo cuando pueda permanecer visible durante ese hueco.

## Auto Timing

<figure class="ui-shot">
  <img src="../../assets/captures/chrono-auto-timing-02.png" alt="Method elige Lazy o Busy. Mode decide si se detecta voz, se añaden márgenes o se ajustan los tiempos actuales." loading="lazy">
  <figcaption>Method elige Lazy o Busy. Mode decide si se detecta voz, se añaden márgenes o se ajustan los tiempos actuales.</figcaption>
</figure>

| Método | Entrada |
| --- | --- |
| Lazy | JSON de picos de [Wave2json](../lite/wave2json.md). |
| Busy | Silencios, VAD, flux, envolvente RMS y forma de onda opcional, mediante [Timing](../modules/kite-timing.md). |
| Legacy | Grupos de silencio desde su ventana independiente. |

**Raw voice** ajusta a la voz sin márgenes ni fotogramas clave. **Full + polish** añade márgenes, encadenado y ajuste a keyframes. **Post current** aplica esos ajustes a los tiempos actuales. Los dos últimos necesitan los fotogramas clave del vídeo.

Empieza por Raw voice para revisar la detección. **Search ±** amplía la búsqueda fuera de la línea; **Smoothing**, **Bridge gaps** y **Drop islands** controlan suavizado, microsilencios y señales breves. Ampliar mucho la búsqueda puede incluir una voz vecina.

**Busy Files...** reúne las señales de [Chrono Generators](https://github.com/Kiterowx/Chrono-Generators-Scripts). **Reload waveform cache** relee un JSON modificado. Las marcas `[TM-...]` indican casos para revisar, como voz ausente, solape o CPS alto.

## Importar y preparar medios

**Data Import** transfiere texto, actor, Effect o etiquetas desde el material pegado por coincidencia temporal. **Same Layers** restringe por capa; **Text as {...}** coloca el texto importado en comentarios. **Song Sync** usa una línea Comment de capa 50 como referencia.

**Extract KF** necesita FFmpeg y SCXvid, configurados en Config. **Scream Detector** usa FFmpeg para marcar intensidad elevada con `[SCREAM]`; no reconoce emociones ni hablantes.

## Propiedades y limpieza

**Properties and Cleanup** edita título y créditos. **Clean the whole subtitle file** afecta a todo el archivo: retira rutas, datos extra, eventos comentados y comentarios internos; vacía Actor y Effect y elimina diálogos vacíos. Conserva una copia editable si esos campos contienen trabajo pendiente.

**Text Replacer** sustituye texto conservando etiquetas. **Remover Assistant** retira solo los elementos elegidos. **mpv QC** importa observaciones y sugerencias temporizadas.
