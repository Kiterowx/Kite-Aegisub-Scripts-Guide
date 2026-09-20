# Zagreo Glyphs

Versión **1.2.3**.

Zagreo Glyphs convierte texto uniforme o dibujos ASS en contornos animados. Comenta las fuentes e inserta y selecciona los resultados.

## Elegir un efecto

1. Selecciona las fuentes y abre **Zagreo Glyphs**.
2. Elige **Category** y pulsa **Filter**; selecciona **Effect**.
3. **Run** abre los parámetros y **Apply** genera la salida.

El catálogo reúne 230 efectos. **Help** muestra su referencia; los accesos directos se agrupan por categoría bajo `: Kite Hotkeys :/Zagreo Glyphs/`.

| Familia | Uso |
| --- | --- |
| Morph | Cambiar de fuente, interpolar dos líneas o transformar contornos. |
| Surface, Wave, Radial, Edge | Deformar superficies, ondas, centros y bordes. |
| Ink, Drip | Variaciones de tinta y goteo. |
| Path, Reveal | Recorrer el trazado o revelar partes de la forma. |
| Dissolve, Fold, Impact | Disolver, plegar o simular un impacto. |
| Contour, Shatter, Glitch, Sketch | Alterar contornos, fragmentar, introducir fallos o superponer trazos. |

## Morph de fuente y de dos líneas

**Font Morph** necesita texto y una **Target font** instalada. **Pair Morph** necesita dos fuentes: la fila de menor índice es el origen y la otra, el destino. Ambas se comentan y el resultado se inserta después de la segunda.

Los contornos se emparejan por índice y longitud. La conversión no identifica letras equivalentes por su significado.

## Controlar la deformación

| Control | Efecto |
| --- | --- |
| Strength | Intensidad según el efecto: desplazamiento, escala, giro u otra magnitud. |
| Frequency | Frecuencia espacial o cantidad, según el algoritmo. |
| Split len | Distancia de muestreo; valores pequeños añaden detalle y coste. |
| Seed | Semilla repetible para el ruido. |
| Period ms | Duración del ciclo. |
| Direction | Sentido del desplazamiento o revelado. |
| Center X% / Y% | Desplazamiento del centro respecto a la mitad del contorno. |
| Pieces / Passes | Fragmentos de Shatter o capas de Sketch. |

Los parámetros disponibles dependen de la familia. Strength = 0 no garantiza conservar la forma en todos los efectos.

## Tiempos y seguimiento

**Auto frame ranges** usa los intervalos del vídeo; **Moments only** divide la duración en la cantidad indicada. Sin tiempos de vídeo se utiliza Moments. Ratios vacío reparte la progresión entre 0 y 1.

**Preserve source motion** conserva el movimiento de origen. **Bake AE position data** suma desplazamiento de Position de After Effects; Ref frame elige la muestra de referencia desde 1. Para escala, giro y perspectiva del seguimiento utiliza [Moka Motion](moka-motion.md).

No hay un límite fijo de momentos o capas ni una confirmación de salida grande. Aumentar la cantidad produce más geometría y eventos; empieza con un intervalo breve.

## Preparar las fuentes

Instala Yutils, ASSFoundation y Aegisub-Motion. El texto debe ser uniforme: separa cambios de fuente o apariencia, saltos explícitos y mezclas de dibujo/texto. La salida de cada contorno tiene una sola apariencia.

Una línea con movimiento, giro o inclinación y sin origen explícito necesita `\org` antes de convertirla. Revisa las fuentes instaladas si falla la conversión a dibujo.

## Ejemplo: animar una banda con Wave Horizontal

En un ASS de 1280 × 720, crea una línea de 1.00 a 1.40 s con este dibujo:

```ass
{\an7\pos(500,350)\p1}m 0 0 l 240 0 240 20 0 20
```

Elige **Wave → Wave Horizontal**, Strength = 10, Frequency = 2, Scale = 120, Period ms = 900, Split len = 8 y Seed = 1985. Con vídeo cargado, usa **Auto frame ranges** y pulsa **Apply**. La cantidad de eventos depende de sus límites de fotograma; Moments = 3 solo controla la división alternativa.

<div class="shot-pair">
<figure class="ui-shot">
  <img src="../../assets/examples/zagreo-glyphs/entrada.png" alt="La fuente es una banda de 240 × 20 unidades." loading="lazy">
  <figcaption>La fuente es una banda de 240 × 20 unidades.</figcaption>
</figure>
<figure class="ui-shot">
  <img src="../../assets/examples/zagreo-glyphs/salida.png" alt="Un estado intermedio muestra la deformación de la banda." loading="lazy">
  <figcaption>Un estado intermedio muestra la deformación de la banda.</figcaption>
</figure>
</div>
