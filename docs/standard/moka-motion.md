# Moka Motion

Versión **3.7.6**.

Moka Motion aplica seguimiento de Mocha/After Effects, importa máscaras y perspectiva, corrige secuencias por fotograma y exporta material para tracking.

## Aplicar movimiento

1. Carga el vídeo y selecciona los diálogos de destino.
2. Abre **Motion/Apply Motion** y pega los datos AE Transform o la ruta de su archivo.
3. Ajusta **First data row**, **Reference row** y la correspondencia temporal; elige los canales y aplica.

<figure class="ui-shot">
  <img src="../../assets/captures/moka-example-01.png" alt="Reference row define la muestra neutra. X/Y, Scale y Rotation eligen qué componentes del seguimiento se aplican al cartel." loading="lazy">
  <figcaption>Reference row define la muestra neutra. X/Y, Scale y Rotation eligen qué componentes del seguimiento se aplican al cartel.</figcaption>
</figure>

| Control | Uso |
| --- | --- |
| First data row | Primera muestra de la lista interpretada, contando desde 1. |
| Reference row | Muestra neutra dentro de los datos ya recortados. |
| Selection timeline | Un seguimiento para todo el intervalo, incluidos los huecos. |
| Restart on each line | Reinicia los datos en cada línea. |
| Clips only | Transforma recortes y conserva la geometría del texto. |
| Compact linear motion | Usa movimiento compacto cuando los datos y etiquetas lo permiten. |

Las dimensiones exportadas se convierten a PlayRes. La sincronización estricta rechaza datos incompletos o incompatibles con los tiempos del vídeo. **Utilities/Inspect Mocha Data** permite revisar formato, canales y muestras antes de aplicar.

**Motion/Revert Motion** aplica la inversa con los mismos datos, referencia y opciones. No recupera precisión perdida por redondeo.

## Importar formas y perspectiva

**Shapes/Create Clip**, **Create Inverse Clip** y **Create Vector Drawing** leen máscaras AE, Bezier antiguo o Shake RotoShape. **Placement** decide si reemplazan las fuentes o insertan líneas nuevas; Source/Target W/H relacionan sus coordenadas.

**Perspective/Apply Power Pin** necesita las cuatro esquinas de CC Power Pin o Corner Pin. Revisa el origen y los canales de perspectiva, posición, clips, borde y sombra.

<figure class="ui-shot">
  <img src="../../assets/captures/moka-apply-power-pin-01.png" alt="Power Pin usa las cuatro esquinas del plano. Origin mode decide cómo tratar el origen de la perspectiva." loading="lazy">
  <figcaption>Power Pin usa las cuatro esquinas del plano. Origin mode decide cómo tratar el origen de la perspectiva.</figcaption>
</figure>

## Corregir y reducir una secuencia

**Track Refinery** trabaja sobre eventos por fotograma con posición explícita.

| Operación | Resultado |
| --- | --- |
| Analyze | Informa de pasos, ciclos y posibles muestras duplicadas. |
| Smooth / Denoise | Suaviza todo el seguimiento o sus anomalías. |
| Repair Duplicate Frame | Corrige una muestra repetida detectada. |
| Retarget Start / End | Recoloca un extremo y conserva gradualmente el otro. |

Revisa pausas y zigzags intencionales antes de corregirlos. **Utilities/Optimizer** une estados compatibles con tolerancia Exact, Conservative o Subpixel; protege etiquetas que dependen de la duración.

## Exportar para tracking

**Create Video Clip** genera un MP4 H.264 sin audio. **Create Exact PNG Sequence** conserva una imagen por fotograma con su numeración de origen. El intervalo abarca la selección completa, incluidos los huecos.

Configura FFmpeg y, si lo necesitas como alternativa, x264 en **Utilities/Trim Settings**. Para material con tiempos variables, la secuencia PNG conserva la correspondencia por fotogramas; el MP4 usa frecuencia constante.

## Ejemplo: trasladar un cartel

Con la referencia en (640, 360), una muestra en (690, 360) aporta un desplazamiento de 50 unidades en X si la exportación y el ASS comparten resolución. Selecciona X/Y y desactiva los demás canales para aplicar solo esa traslación.

<div class="shot-pair">
<figure class="ui-shot">
  <img src="../../assets/examples/moka-motion/entrada.png" alt="Cartel antes del seguimiento, en (640, 360)." loading="lazy">
  <figcaption>Cartel antes del seguimiento, en (640, 360).</figcaption>
</figure>
<figure class="ui-shot">
  <img src="../../assets/examples/moka-motion/salida.png" alt="La muestra desplaza el cartel 50 unidades a la derecha sin cambiar su altura." loading="lazy">
  <figcaption>La muestra desplaza el cartel 50 unidades a la derecha sin cambiar su altura.</figcaption>
</figure>
</div>
