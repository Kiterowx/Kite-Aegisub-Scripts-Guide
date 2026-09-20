# Social Clip

Versión **1.0.3**.

Social Clip recorta escenas mediante máscaras ASS y las une en un vídeo continuo. Las máscaras determinan la región visible, su movimiento y los intervalos que se exportan.

## Preparar las escenas

1. Abre un vídeo real y revisa el PlayRes del ASS.
2. Selecciona las líneas cuyos tiempos definirán las escenas.
3. Abre **Social Clip**, elige formato y centros X inicial/final y pulsa **Crear máscaras**.
4. Revisa las máscaras sobre el vídeo; ajusta tiempos y movimiento.
5. Elige **Exportar vídeo** o **Solo ASS**.

Se crea una máscara por diálogo seleccionado, con efecto `Kite Social Mask`. X iguales producen posición fija; X distintas, movimiento. Las máscaras sirven de guía y no aparecen en la exportación.

## Elegir la salida

| Perfil | Subtítulos |
| --- | --- |
| MP4 · pegados y adaptados | Pega carteles y efectos antes del recorte; recoloca y pega el diálogo después de unir escenas. |
| MP4 · pegados exactos | Renderiza la composición ASS sobre el vídeo original antes de recortar. |
| MKV · diálogo ASS flotante | Pega carteles y efectos; incluye el diálogo adaptado como pista activable. |

**Solo ASS** guarda únicamente el diálogo adaptable y comunica cuántos carteles o efectos se excluyen. **Guardar ASS adaptado** permite conservarlo junto al vídeo.

## Formato, movimiento y diálogo

| Control | Uso |
| --- | --- |
| Formato | 1080×1920, 720×1280, 1080×1350 o tamaño personalizado. |
| FPS | Origen conserva tiempos variables; 30 o 60 produce frecuencia constante. |
| CRF | Calidad H.264 de 0 a 51; valores menores suelen producir archivos mayores. |
| Relación | Expande la caja al formato o exige la misma proporción. |
| Márgenes y fuente máxima | Reservan espacio al diálogo adaptado. |
| Pista | Pista de audio desde 1. |

**Corregir Y** ajusta verticalmente máscaras poligonales compatibles. **Centrar subs X** centra el diálogo sobre su máscara y conserva su altura y fila de alineación. Un subtítulo que cruza varias escenas necesita revisión antes de centrarlo.

La caja de recorte mantiene tamaño constante por escena. Si la máscara cambia realmente de tamaño, no cabe o sale por X, se informa antes de exportar.

## Ejemplo: quitar un hueco entre escenas

Dos máscaras con intervalos 0–400 ms y 600–1000 ms producen 800 ms continuos. El corte elimina el mismo hueco del vídeo, audio y diálogo adaptado.

<figure class="ui-shot">
  <img src="../../assets/illustrations/social-clip-intervalos.svg" alt="La segunda escena empieza en 400 ms en la salida. Sus subtítulos se desplazan con ella." loading="lazy">
  <figcaption>La segunda escena empieza en 400 ms en la salida. Sus subtítulos se desplazan con ella.</figcaption>
</figure>

Los solapes dobles se reparten cerca de su mitad temporal. Ajusta antes los solapes triples o las máscaras completamente anidadas.

## Requisitos

Configura FFmpeg y FFprobe en **Config...**. FFmpeg necesita libass, libx264 y los filtros de recorte y concatenación. Las máscaras complejas se miden con ASSFoundation y SubInspector. El renderizador debe disponer de las fuentes usadas.
