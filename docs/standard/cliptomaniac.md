# Cliptomaniac

Versión **0.4.4**.

Cliptomaniac crea, convierte y transforma clips ASS. También usa trazos guía para colocar texto, definir perspectiva y convertir animaciones a fotogramas independientes.

Abre **Cliptomaniac**, elige la acción y pulsa **Execute**. Las acciones directas se ejecutan; las demás abren opciones. **Language** cambia entre español e inglés. Los nombres siguientes corresponden a la interfaz inglesa.

## Ajustar texto y recorte

| Acción | Resultado |
| --- | --- |
| Autofit clip to text | Ajusta un clip existente al texto. |
| Create clip around text | Crea un clip aunque la línea no tenga uno. |
| Fit text to clip guide | Inserta saltos según el ancho de la guía en X o equilibra renglones con su altura en Y. |
| Text to clip | Convierte el contorno del texto o dibujo en recorte. |
| Expand clip margin | Amplía o reduce el clip según el margen. |

**Fit text to clip guide conserva la alineación y el tipo de clip.** Usa la guía para distribuir renglones. Para cambiar el tamaño del texto, utiliza **Rescale by rectangle clip**.

En Autofit y Create clip, **Margin** ajusta el margen y **Style pad** incluye borde, sombra y desenfoque. **Transform maxima** mide todos los fotogramas para cubrir la animación completa; necesita vídeo y puede tardar en líneas largas.

<figure class="ui-shot">
  <img src="../../assets/captures/clipto-options-02-01.png" alt="Autofit combina margen, división por secciones y tolerancia. Transform maxima amplía la medida al intervalo completo de la línea." loading="lazy">
  <figcaption>Autofit combina margen, división por secciones y tolerancia. Transform maxima amplía la medida al intervalo completo de la línea.</figcaption>
</figure>

## Convertir y editar contornos

| Acción | Resultado |
| --- | --- |
| Copy clip/iclip | Copia el primer recorte a los destinos correspondientes. |
| Shape to clip / Clip to shape | Convierte dibujo a clip o clip a dibujo. |
| Toggle clip/iclip | Alterna interior visible e interior oculto. |
| Rect clip to vector / Vector clip to rect | Convierte entre rectángulo y trayecto; al volver usa la caja envolvente. |
| Clip boolean with text/shape | Interseca el clip con el contorno o resta la forma al clip. |
| Extract clip as mask line | Inserta una máscara de dibujo desde el primer clip. |
| Rectangle from diagonal / Circle from 2 points | Usa el primer trazo como diagonal o diámetro. |
| New clip shape | Inicia otra forma desde el último punto. |
| Add clip points / Remove clip points | Añade puntos por distancia/cantidad o retira puntos alternos. |

### Ejemplo: conservar el área al convertir a vector

Selecciona la línea siguiente y ejecuta **Rect clip to vector**:

```ass
{\clip(400,260,880,460)}SALIDA
```

El contorno delimita la misma región de 480 × 200 unidades:

```ass
{\clip(m 400 260 l 880 260 880 460 400 460)}SALIDA
```

<figure class="ui-shot">
  <img src="../../assets/illustrations/clip-vertices.png" alt="Los cuatro vértices conservan el rectángulo. X crece hacia la derecha e Y hacia abajo." loading="lazy">
  <figcaption>Los cuatro vértices conservan el rectángulo. X crece hacia la derecha e Y hacia abajo.</figcaption>
</figure>

## Mover, girar y escalar

| Acción | Guía y resultado |
| --- | --- |
| Position at clip midpoint | Lleva la posición al centro del clip. |
| Align to clip | Lleva la posición al punto más cercano del trayecto. |
| Clip to reposition | Desplaza el conjunto según el primer trazo recto de dos puntos. |
| Clip to move | Convierte la guía en movimiento. |
| Clip to FRZ / FAX / FAY | Convierte la dirección de la guía en giro o inclinación. |
| Measure clip | Informa de longitud y ángulo de los dos primeros trazos. |
| Measure & transform clip | Anima tamaño usando dos trazos como medidas anterior/posterior. |
| Adjust by clip scale | Aplica esa proporción a las etiquetas elegidas. |
| Rescale by rectangle clip | Encaja el texto en un clip rectangular mediante Fit, Fill o Stretch. |
| Calibrate clip X / Y | Endereza el primer trazo en horizontal o vertical. |

Una guía de (100, 200) a (140, 220) representa **(+40, +20)** para Clip to reposition. Las líneas conservan su disposición relativa. **Remove guide clip** retira la referencia al terminar.

<figure class="ui-shot">
  <img src="../../assets/captures/clipto-options-25-01.png" alt="Fit mantiene el texto dentro del rectángulo; Fill cubre el área y Stretch ajusta ancho y alto por separado. Center recoloca el anclaje." loading="lazy">
  <figcaption>Fit mantiene el texto dentro del rectángulo; Fill cubre el área y Stretch ajusta ancho y alto por separado. Center recoloca el anclaje.</figcaption>
</figure>

Rescale requiere un clip rectangular. Si lo necesitas vectorial, conviértelo después del ajuste.

## Perspectiva y texto curvo

**Clip to perspective** utiliza cuatro esquinas; **Corner order** fija su correspondencia y **Origin** decide el anclaje. **Perspective to clip** reconstruye el cuadrilátero desde el plano guardado o la geometría proyectada. **Complete quadrilateral** añade el cuarto punto a una guía A–B–C.

<figure class="ui-shot">
  <img src="../../assets/captures/clipto-options-26-01.png" alt="El orden de las esquinas determina qué lados del cartel corresponden a los del plano. Revisa esa correspondencia antes de aplicar." loading="lazy">
  <figcaption>El orden de las esquinas determina qué lados del cartel corresponden a los del plano. Revisa esa correspondencia antes de aplicar.</figcaption>
</figure>

**Bezier clip to curved text** usa una Bézier cúbica para distribuir giro y espaciado por carácter. **Curve depth** controla la profundidad; **Extra fsp**, la separación adicional.

## Fotogramas y franjas

**Create strip clips** divide la región en franjas. Horizontal avanza en X y Vertical, en Y. **Create new lines** genera copias; sin él, la primera franja se aplica a la fuente. **Comment source** conserva el original comentado.

**Animated clip to FBF** convierte la animación en estados por fotograma. **Bake source** permite evaluar toda la línea o solo el clip cuando sea compatible. **Merge identical** une estados consecutivos equivalentes. **Max frames** limita las líneas resultantes después de unir; su valor inicial es 400 y **0** desactiva el límite.

<figure class="ui-shot">
  <img src="../../assets/captures/clipto-options-30-01.png" alt="Elige qué estado se evalúa y si se unen fotogramas idénticos. Max frames limita el tamaño de la salida; Comment source conserva una base comentada." loading="lazy">
  <figcaption>Elige qué estado se evalúa y si se unen fotogramas idénticos. Max frames limita el tamaño de la salida; Comment source conserva una base comentada.</figcaption>
</figure>

**Export clip track to AE** concatena las duraciones seleccionadas y muestra Position, Scale y Rotation en la consola. **Clip diagnostics** informa de tipo, dimensiones, puntos y perspectiva sin editar.

Instala ZF, ASSFoundation, Functional, Aegisub-Motion y las bibliotecas de arch. Las acciones por fotograma y Transform maxima necesitan tiempos de vídeo disponibles.
