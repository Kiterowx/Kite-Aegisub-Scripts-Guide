# Rhea Signs

Versión **2.2.1**.

Rhea Signs reúne edición de carteles, etiquetas, máscaras, perspectiva, fuentes y estilos. Su interfaz admite español, inglés y portugués.

El panel ejecuta **Perspective → Masks → Shapes → Sign → Toolbox**. Deja vacías las secciones que no uses. La selección de una operación pasa a la siguiente; un fallo posterior no revierte las operaciones ya terminadas.

## Sustituir textos con Signs Editor

1. Selecciona todas las capas del cartel y abre **Signs Editor**.
2. Elige si omites dibujos, regeneras degradados GBC o aplicas un límite de caracteres.
3. Escribe una sustitución por fila y pulsa **Execute**.

<figure class="ui-shot">
  <img src="../../assets/captures/rhea-signs-text-03.png" alt="Los textos idénticos comparten una fila. Edita la columna derecha y conserva la cantidad de filas; todas las capas del grupo reciben la sustitución." loading="lazy">
  <figcaption>Los textos idénticos comparten una fila. Edita la columna derecha y conserva la cantidad de filas; todas las capas del grupo reciben la sustitución.</figcaption>
</figure>

`\N`, `\n` y `\h` permanecen como escapes literales. Una fila requerida vacía borra el texto de ese grupo. La opción de límite está desactivada inicialmente y su valor inicial es 150.

Las etiquetas, comentarios y dibujos se conservan; el texto nuevo se reparte entre las secciones existentes. **Detect/regenerate GBC** actualiza los degradados marcados, incluso si no cambia el texto visible.

## Copiar y transformar etiquetas con Tag Editor

<figure class="ui-shot">
  <img src="../../assets/captures/rhea-tagops-02.png" alt="Copy Tags copia categorías; Keep Only retira las demás. En Resize / transform, las casillas alternan categorías respecto a las detectadas." loading="lazy">
  <figcaption>Copy Tags copia categorías; Keep Only retira las demás. En Resize / transform, las casillas alternan categorías respecto a las detectadas.</figcaption>
</figure>

| Operación | Uso |
| --- | --- |
| Copy tags | El primer evento de cada grupo Effect aporta etiquetas a los destinos. |
| Keep only | Conserva las categorías elegidas, texto y comentarios. |
| Resize / transform | Add suma; Percent multiplica por `1 + amount/100`; Transform anima hacia los valores ajustados. |
| Pos Align | Usa las dos primeras líneas para calcular el desplazamiento de los destinos. |

**Read all blocks** amplía la lectura al texto completo. **Replace** retira etiquetas equivalentes y **Append** escribe al final del bloque inicial.

En **Pos Align**, la diferencia es posición de la primera línea menos posición de la segunda. **Keep org** conserva orígenes y clips; **Move org** los desplaza con el texto.

## Crear máscaras

**from clip** convierte el contorno a dibujo local. También puedes usar las formas `square`, `rounded`, `circle` y `triangle`, o guardar una propia.

| Acción | Resultado |
| --- | --- |
| Apply Mask | Aplica la forma con las opciones del panel. |
| Create Layer | Crea una máscara por debajo del texto. Si la fuente está en capa 0, la lleva a 1. |
| Replace Mask | Sustituye la primera sección activa de dibujo. |
| Save Shape / Delete Shape | Guarda o retira geometría de la biblioteca. |

Un `iclip` aporta su contorno, sin convertirlo en el complemento del cuadro. La biblioteca `dramaturgy_masks.txt` guarda geometría, no eventos completos.

## Perspectiva y dibujos

**Copy Exact**, **Copy Static Plane** y **Copy Move Plane** copian el plano con distintos tratamientos de posición y origen. **Mass FSC** cambia escalas conservando el cuadrilátero; **Scale Quad** escala el plano. Bake/Restore Extradata permite transportar el plano en un marcador de texto.

| Shapes | Función |
| --- | --- |
| Unify Drawing Pivots | Comparte un pivote compensando las coordenadas de dibujos estáticos. |
| Place on Perimeter | Repite unidades sobre el contorno del primer dibujo. |
| Shape Color Optimizer | Reduce colores o bandas de dibujos compatibles. |

El optimizador ofrece Auto, Similar colors y Full gradient. Revisa la reducción propuesta antes de aplicarla, sobre todo en contornos pequeños o degradados suaves.

## Distribuir y revelar texto

**Typewriter** revela grafemas con alfa. **Frame** usa el mapa del vídeo; **Duration** reparte los pasos por duración. **Vertical Drop** crea un evento por grafema en un eje vertical. **Circle Text** necesita `pos` y `org`; **Curve Text** utiliza un clip vectorial como guía.

Estas distribuciones parten del estado inicial. Divide o convierte antes las líneas cuya geometría cambie durante la animación.

**Sign Builder** genera fondo, brillo y texto en tres capas y comenta las fuentes. El ancho máximo limita la caja; no reduce automáticamente un texto demasiado largo.

## Estilos y fundidos

**Font and Style Manager** sustituye fuentes, edita campos marcados y clona estilos. **Style to Tags** escribe atributos del estilo como etiquetas y permite proteger familias ya presentes.

<figure class="ui-shot">
  <img src="../../assets/captures/rhea-style-tags-02.png" alt="Marca las propiedades que quieras escribir. Keep families already used by the line protege las etiquetas existentes; Omit zero values evita añadir valores cero." loading="lazy">
  <figcaption>Marca las propiedades que quieras escribir. Keep families already used by the line protege las etiquetas existentes; Omit zero values evita añadir valores cero.</figcaption>
</figure>

**Frame Fades and Cleanup/In** y **Out** usan el fotograma actual como borde del fundido. **Clean** retira fades interiores entre grupos continuos y conserva los exteriores.

Instala ASSFoundation, Functional, Aegisub-Motion y arch.Perspective junto con los módulos compartidos.


## Ejemplo: escribir los atributos del estilo en el texto

Configura el estilo **Cartel** con Arial, tamaño 60, negrita, borde 2, sombra 0 y alineación 5. Usa relleno blanco, borde `#181818` y sombra negra.

1. Crea una línea con el texto de abajo, asígnale **Cartel** y selecciónala.
2. En el panel, elige **Style to Tags** dentro de las herramientas y pulsa **Execute**.
3. Activa **Font**, **Size**, **Bold**, **Outline**, **Primary color**, **Outline color**, **Shadow color** y **Alignment**. Conserva **Keep families already used by the line** y **Omit zero values**; pulsa **Apply**.

La línea recibe Arial, tamaño 60, negrita, borde y colores como etiquetas. Su posición permanece en (640, 360). Puedes leer esos atributos en el texto ASS sin depender únicamente del nombre del estilo.

**Entrada, campo Texto:**

```ass
{\pos(640,360)}SALIDA
```

**Salida, campo Texto:**

```ass
{\fnArial\fs60\b1\bord2\1c&HFFFFFF&\3c&H181818&\4c&H000000&\an5\pos(640,360)}SALIDA
```

## Split at Visual Changes y Simplify Drawing

**Tools → Split at Visual Changes** integra el antiguo script suelto. Selecciona una línea, carga vídeo y define una región rectangular; un clip rectangular estático puede servir de guía. Ajusta diferencia de color, porcentaje global y porcentaje por bloque. Revisa los tramos antes de generar. **Conservar animación** reajusta los tiempos de los tags; **Congelar por tramo** evalúa el primer frame de cada tramo. Puede conservar la original comentada y retirar el clip guía. Rechaza karaoke y efectos temporales no compatibles antes de escribir.

**Shapes → Simplify Drawing** reduce puntos sobre rectas y convierte Bézier cúbicas casi rectas en segmentos rectos. La tolerancia predeterminada es **0.05 unidades de dibujo en p1**, antes de escala o perspectiva; **0** elimina solo geometría colineal. Comprueba los puntos y controles originales para limitar el error de cada pasada, conserva extremos, esquinas, retrocesos, contornos separados y curvas con detalle. Los B-splines quedan intactos. Solo modifica secciones de dibujo de las líneas seleccionadas; conserva tags, texto y metadatos. Una tolerancia positiva permite una pequeña diferencia geométrica, que puede ampliarse con la escala. La rasterización de bordes puede variar ligeramente incluso con tolerancia cero.

**Tools → Remove Redundant Zero Tags** limpia únicamente tags cero que no afectan al resultado, respetando estilos, resets y animaciones.
