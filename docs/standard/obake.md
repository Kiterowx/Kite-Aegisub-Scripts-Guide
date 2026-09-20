# Obake

Versión **0.4.5**.

Obake crea cadenas de transformaciones, animaciones, capas y secuencias de estados. Abre **Obake**, elige una acción y pulsa **Execute**. El panel admite español e inglés.

Los atajos conservan los nombres de acción. En el selector inglés aparecen estas descripciones:

| Acción | Nombre en el selector |
| --- | --- |
| Apply chain | build t() chain |
| Retime transforms | retime t() tags |
| In-Out tags | create in/out t() tags |
| Gunfight of Tags | randomize numeric tags / FBF |
| ZigZag lines | alternate selected lines by frames |
| Animation FX | apply animation presets |
| Border layers | create border layers |
| Color preset | apply color-layer preset |

## Cadenas de transformaciones

**Apply chain** escribe un estado inicial y destinos `\t`. Cada fila contiene tiempo y etiquetas sin llaves. **Previous/Next** recorre las páginas; **Add+** duplica la última fila y **Rem-** la retira.

<figure class="ui-shot">
  <img src="../../assets/captures/obake-blur-chain-02.png" alt="La primera parada fija el estado inicial. La segunda lleva blur a 5 durante los primeros 1000 ms de la línea." loading="lazy">
  <figcaption>La primera parada fija el estado inicial. La segunda lleva blur a 5 durante los primeros 1000 ms de la línea.</figcaption>
</figure>

| Shape | Tiempos |
| --- | --- |
| Manual keyframes | Usa las filas en porcentaje o milisegundos. |
| Once | Va del primer estado al último. |
| Out and back | Reparte ida y vuelta en dos mitades. |
| Yoyo | Repite la cantidad de ciclos indicada. |
| Pulse | Usa Value como duración de cada medio ciclo. |
| Steps | Crea destinos interpolados sucesivos. |

**Delay** retrasa la animación dentro del evento en los modos automáticos. **Strip existing \t** retira las transformaciones anteriores. **Retime transforms** es otra acción: adapta los tiempos explícitos de las transformaciones a la duración actual de la línea.

## Animaciones y capas

**Animation FX** ofrece blur, fade, escala, aparición, cambios de color, temblor y división de texto. Step, Amount, aceleración y colores se usan según el preajuste. **Border Pulse** y **Glow Pulse** realizan una transición, pese a sus nombres.

**Border layers** crea un relleno y hasta cuatro bordes activos. Sus grosores se acumulan: B1 = 1 y B2 = 2 producen bordes de 1 y 3. **Color preset** separa relleno/borde o genera brillo, sombra y doble borde.

<figure class="ui-shot">
  <img src="../../assets/captures/obake-action-7-02.png" alt="Activa solo los bordes que necesitas. Cada tamaño se suma al anterior y el relleno queda sobre las capas de borde." loading="lazy">
  <figcaption>Activa solo los bordes que necesitas. Cada tamaño se suma al anterior y el relleno queda sobre las capas de borde.</figcaption>
</figure>

## Combinar o alternar estados

| Acción | Entrada y resultado |
| --- | --- |
| In-Out tags | Dos líneas por valor de Effect; crea una transición y comenta las fuentes. |
| Gunfight of Tags | Varía etiquetas numéricas o de color dentro del rango y la semilla elegidos. |
| ZigZag lines | Alterna dos o más estados en orden de filas durante su intervalo combinado. |

In-Out necesita pares con estilo, capa, márgenes y propiedades no animables compatibles. Un Effect vacío también forma un grupo: cuatro líneas vacías no se dividen automáticamente en dos pares.

Gunfight puede dividir una fuente por fotogramas o tratar la selección como una secuencia existente. ZigZag conserva el reloj original de las etiquetas temporales: usa tiempos coincidentes si los estados deben compartir la misma fase.

Instala ASSFoundation y Aegisub-Motion. Las acciones por fotograma necesitan las conversiones temporales del vídeo.


## Ejemplo: desenfocar un letrero durante su primer segundo

Crea una línea de 1.00 a 4.00 s con el texto de abajo.

1. Selecciona el cartel y abre **build t() chain**.
2. Elige la unidad de milisegundos y **Manual keyframes**. En la primera parada escribe tiempo `0` y `\blur0`; en la segunda, `1000` y `\blur5`.
3. Activa **Strip existing \t** y pulsa **Execute**.

La transformación anterior se sustituye por `\t(0,1000,\blur5)`. El blur inicial queda en cero y llega a cinco al cabo de un segundo. La etiqueta inicial `\blur0` queda repetida porque la cadena añade su propio estado inicial; ambas etiquetas fijan el mismo valor.

**Entrada, campo Texto:**

```ass
{\pos(640,360)\blur0\t(0,1000,\blur1)}SALIDA
```

**Salida, campo Texto:**

```ass
{\pos(640,360)\blur0\blur0\t(0,1000,\blur5)}SALIDA
```

### Comparación visual

<div class="shot-pair">
<figure class="ui-shot"><img src="../../assets/examples/obake/entrada.png" alt="Transformación anterior, a 1.60 s." loading="lazy"><figcaption>Transformación anterior, a 1.60 s.</figcaption></figure>
<figure class="ui-shot"><img src="../../assets/examples/obake/salida.png" alt="Nueva cadena de blur, a 1.60 s: 600 ms desde el inicio." loading="lazy"><figcaption>Nueva cadena de blur, a 1.60 s: 600 ms desde el inicio.</figcaption></figure>
</div>
