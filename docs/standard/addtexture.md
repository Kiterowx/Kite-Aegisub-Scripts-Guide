# AddTexture

Versión **2.1.8**.

AddTexture ajusta dibujos ASS al contorno de un texto y los inserta en capas sobre el original.

## Aplicar una textura

1. Copia un dibujo ASS, un clip vectorial o filas Dialogue/Comment que contengan dibujos.
2. Selecciona los diálogos de destino y abre **AddTexture**.
3. Revisa el contenido de **ASS drawings / Dialogue lines** y pulsa **Execute**.

**Paste clipboard** vuelve a leer el portapapeles. Execute usa el contenido del cuadro: si editas una vista abreviada de un dibujo largo, tu edición sustituye al dibujo completo.

<figure class="ui-shot">
  <img src="../../assets/captures/texture-bands-01.png" alt="Preserve colors mantiene las dos bandas de la textura. Clip to text recorta su geometría al contorno de las letras y Layer offset coloca el resultado sobre el texto." loading="lazy">
  <figcaption>Preserve colors mantiene las dos bandas de la textura. Clip to text recorta su geometría al contorno de las letras y Layer offset coloca el resultado sobre el texto.</figcaption>
</figure>

| Opción | Efecto |
| --- | --- |
| Preserve colors | Conserva los colores de la textura; desactivado, usa el primario del destino. |
| Clip to text | Calcula la intersección de las formas. Desactivado, añade el contorno del texto como clip. |
| Copy alpha/fad | Copia la visibilidad y sus transformaciones a toda la textura. |
| Text simplify / Shape simplify | Simplifica el contorno del texto o la textura. Cero conserva el mayor detalle disponible. |
| Extra tags | Añade etiquetas; el valor inicial elimina borde y sombra. |
| Layer offset | Diferencia de capa no negativa respecto al original. |

La textura se escala uniformemente para cubrir el texto y se centra. Los grupos de color conservan sus posiciones relativas. Las intersecciones vacías se omiten; las líneas nuevas quedan seleccionadas.

## Preparar el dibujo

La entrada se interpreta como geometría estática. Convierte primero cualquier movimiento o perspectiva al estado que quieras pegar. **Copy alpha/fad** no reproduce transparencias independientes por carácter.

Instala ZF y ASSFoundation junto con los [módulos compartidos](../installation.md#instalacion-manual). Los originales se conservan y la inserción se puede deshacer.


## Ejemplo: rellenar un letrero con dos bandas de color

Crea una línea de 1.00 a 4.00 s en un ASS de 1280 × 720. Usa Arial, tamaño 60, negrita y alineación central.

1. Selecciona la línea `SALIDA` situada en (640, 360).
2. Pega estos dos dibujos en **ASS drawings / Dialogue lines**:

   ```ass
   {\p1\c&H00FFFF&}m 0 0 l 400 0 400 25 0 25{\p0}
   {\p1\c&H0080FF&}m 0 25 l 400 25 400 50 0 50{\p0}
   ```

3. Activa **Preserve colors** y **Clip to text**. Conserva `\bord0\shad0` y **Layer offset = 1**; pulsa **Execute**.

Se añaden dos dibujos recortados a las letras, uno por banda. Ambos conservan el intervalo de 1 a 4 segundos y se colocan una capa por encima del texto original.

**Entrada, campo Texto:**

```ass
{\pos(640,360)}SALIDA
```

### Comparación visual

<div class="shot-pair">
<figure class="ui-shot"><img src="../../assets/examples/addtexture/entrada.png" alt="El texto de entrada, a 2.00 s." loading="lazy"><figcaption>El texto de entrada, a 2.00 s.</figcaption></figure>
<figure class="ui-shot"><img src="../../assets/examples/addtexture/salida.png" alt="Dos bandas recortadas al contorno de las letras." loading="lazy"><figcaption>Dos bandas recortadas al contorno de las letras.</figcaption></figure>
</div>
