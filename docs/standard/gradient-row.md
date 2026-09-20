# Gradient Row

Versión **1.8.9**.

Gradient Row reparte colores por grafema o genera copias del cartel recortadas en franjas.

## Elegir el modo

| Gradient Type | Resultado |
| --- | --- |
| Char Line | Un degradado independiente por línea. |
| Char Selection | Un degradado continuo por las líneas seleccionadas. |
| Horizontal / Vertical | Franjas que avanzan por el ancho / alto. |
| Rotated | Franjas según el ángulo indicado. |

Los modos Char editan las líneas. Los espaciales comentan las fuentes y seleccionan las copias generadas.

<figure class="ui-shot">
  <img src="../../assets/captures/gradient-character-01.png" alt="Char Line reparte la paleta entre las letras. Desactiva Inline color stops para usar las muestras del panel; Color slots elige los canales." loading="lazy">
  <figcaption>Char Line reparte la paleta entre las letras. Desactiva Inline color stops para usar las muestras del panel; Color slots elige los canales.</figcaption>
</figure>

## Paleta y controles

**Add+** añade un color y **Rem-** retira el último, con un mínimo de dos. Las páginas muestran ocho muestras y conservan sus cambios al usar **Previous/Next**.

- **Acceleration = 1** interpola linealmente; valores mayores prolongan los colores iniciales.
- **Pixels per strip** fija el grosor de franja. Aumentarlo reduce la cantidad de eventos.
- **Inline color stops** usa colores explícitos antes o entre letras como referencias, en los modos Char.

En `{\c&H000000&}AB{\c&HFFFFFF&}CD`, las referencias están en A y C. Los colores de transformaciones no son referencias estáticas. Los espacios normales consumen una posición; `\N`, `\n` y `\h` se conservan sin consumirla.

## Franjas y perspectiva

Los modos espaciales admiten ausencia de clip, un rectángulo o un vector de cuatro esquinas antes del texto. Los clips inversos, múltiples, intermedios o animados se rechazan.

La geometría se prepara para un estado del cartel. Revisa toda su duración si se mueve o cambia de perspectiva. [Cliptomaniac](cliptomaniac.md#fotogramas-y-franjas) permite convertirlo primero a estados por fotograma.

Instala ASSFoundation, Aegisub-Motion y arch.Perspective. SubInspector es opcional y permite medir el texto renderizado.


## Ejemplo: colorear un letrero de rojo a azul

Usa un ASS de 1280 × 720 y un estilo con Arial, tamaño 60, negrita, escala 100 % y espaciado 0.

1. Selecciona `SALIDA` y elige **Gradient Type = Char Line**.
2. Desactiva **Inline color stops**. Marca solo `\c`, fija aceleración 1 y las paradas `#FF0000` y `#0000FF`.
3. Pulsa **Execute**.

La salida sigue siendo una sola línea y contiene seis colores, uno por letra. **Horizontal** distribuye el color sobre el ancho renderizado: conserva la fuente como comentario y genera tantas franjas como requieran el ancho y Pixels per strip.

**Entrada, campo Texto:**

```ass
SALIDA
```

**Salida, campo Texto:**

```ass
{\c&H0000FF&}S{\c&H3300CC&}A{\c&H660099&}L{\c&H990066&}I{\c&HCC0033&}D{\c&HFF0000&}A
```

### Comparación visual

<div class="shot-pair">
<figure class="ui-shot"><img src="../../assets/examples/gradient-row/entrada.png" alt="Texto con el color del estilo." loading="lazy"><figcaption>Texto con el color del estilo.</figcaption></figure>
<figure class="ui-shot"><img src="../../assets/examples/gradient-row/salida.png" alt="Char Line: seis colores entre rojo y azul." loading="lazy"><figcaption>Char Line: seis colores entre rojo y azul.</figcaption></figure>
</div>
