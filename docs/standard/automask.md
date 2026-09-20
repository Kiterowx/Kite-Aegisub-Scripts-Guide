# AutoMask

Versión **2.5.5**.

AutoMask reconstruye una superficie del fotograma actual y la convierte en relleno, dibujo o clip ASS mediante el backend **kite-automask**.

## Definir la región

1. Carga el vídeo y sitúalo en el fotograma que quieras reconstruir.
2. Selecciona los diálogos que servirán de fuente. Dibuja un clip alrededor de cada región.
3. Abre **AutoMask**, revisa superficie y tinta y pulsa **Apply**.

Cada región usa el mismo fotograma. Para una superficie en movimiento, aplica después el seguimiento necesario.

| Comando | Uso |
| --- | --- |
| AutoMask | Abre el editor para revisar o pintar las máscaras. |
| Find surface inside clip | Busca la superficie dentro de un clip normal con margen. |
| Classic AutoGrask | Reconstruye papel claro con tinta oscura desde un clip normal, sin editor. |

## Reconstruir y comparar

<figure class="ui-shot">
  <img src="../../assets/captures/automask-editor.png" alt="Revisa el área y la tinta antes de Apply. Las vistas Original, Mask, Fill y Vector permiten comparar la región, la reconstrucción y sus dibujos." loading="lazy">
  <figcaption>Revisa el área y la tinta antes de Apply. Las vistas Original, Mask, Fill y Vector permiten comparar la región, la reconstrucción y sus dibujos.</figcaption>
</figure>

**Region + / −** corrige la superficie; **Ink + / −**, los defectos. **Detect ink** vuelve a detectar la tinta y **Rebuild** recalcula el relleno. **Refine with SAM** usa los puntos o la caja que marques.

| Engine | Operación |
| --- | --- |
| Automatic | Elige entre degradado e inpainting. |
| Full AutoMask | Reconstruye mediante inpainting. |
| Improved AutoGrask | Ajusta un degradado de color. |
| Classic AutoGrask | Usa el ajuste para papel claro. |

## Elegir la salida

| Output | Cambio en el ASS |
| --- | --- |
| ASS fill | Sustituye las fuentes por dibujos de relleno con sus tiempos y propiedades. |
| Shape | Inserta un contorno una capa por encima y conserva la fuente. |
| `\clip` / `\iclip` | Sustituye el recorte y conserva el texto y las demás etiquetas. |

Los clips son coordenadas absolutas. El editor admite clips inversos; Inside y Classic requieren normales. Convierte los clips animados al estado deseado antes de usarlos. Los dibujos de entrada necesitan geometría estática, `\pos` explícito y `\an7`.

## Instalar el backend

Configura Python en **Backend/Configure**, ejecuta **Install or Update** y comprueba **Check**. **Install Models** descarga los modelos de SAM y LaMa; los degradados funcionan sin ellos. Consulta la [instalación](../installation.md#backends-de-python).

## Ejemplo: cubrir las letras de un letrero

Dibuja una guía alrededor del letrero, elige **Whole clip**, **Automatic** y **ASS fill**. Corrige las letras omitidas con **Ink +** y pulsa **Rebuild** antes de aplicar. El color y el contorno dependen del fotograma y de la región elegida.

<div class="shot-pair">
<figure class="ui-shot">
  <img src="../../assets/examples/automask/entrada.png" alt="La tinta ocupa parte de la superficie que se va a reconstruir." loading="lazy">
  <figcaption>La tinta ocupa parte de la superficie que se va a reconstruir.</figcaption>
</figure>
<figure class="ui-shot">
  <img src="../../assets/examples/automask/salida.png" alt="El relleno ASS cubre esa región. Comprueba el resto del intervalo si el fondo cambia." loading="lazy">
  <figcaption>El relleno ASS cubre esa región. Comprueba el resto del intervalo si el fondo cambia.</figcaption>
</figure>
</div>
