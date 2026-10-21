# PNG2ASS

Versión **1.7.1**.

PNG2ASS convierte imágenes y SVG en dibujos ASS mediante **kite-png2ass**. Conserva las líneas originales y permite revisar la conversión antes de insertarla.

## Convertir una imagen

1. Selecciona un diálogo y elige la imagen desde **PNG2ASS**.
2. Ajusta modo, color y posición; pulsa **Execute**.
3. Revisa el resumen y pulsa **Insert** para añadir los dibujos una capa por encima de la fuente.

Una imagen toma los tiempos de la línea activa si está seleccionada; en otro caso, del primer diálogo seleccionado.

<figure class="ui-shot">
  <img src="../../assets/captures/png2ass-example-01.png" alt="Color = source conserva los colores de la señal. Position = 0,0 coloca su lienzo en el origen del ASS; Scale controla la precisión vectorial." loading="lazy">
  <figcaption>Color = source conserva los colores de la señal. Position = 0,0 coloca su lienzo en el origen del ASS; Scale controla la precisión vectorial.</figcaption>
</figure>

## Elegir modo y precisión

| Mode | Entrada |
| --- | --- |
| auto | Detecta transparencia, máscara o color. |
| alpha | Recorta según el canal alfa. |
| white-matte | Primer plano claro sobre negro. |
| dark-matte / luma | Primer plano oscuro sobre blanco. |
| color | Separa el contenido visible en capas de color. |

SVG se convierte directamente con svgelements. **SVG decimals** controla la precisión y **Arc degrees**, la subdivisión de arcos. Se conservan las transformaciones afines anidadas, los rellenos sólidos y la opacidad. Antes de importar, se convierten a paths el texto y los objetos no compatibles; los componentes no admitidos producen un error. Blur, opacidad de grupo y bordes ASS son aproximaciones.

Los clips compatibles del SVG se aplican a la geometría antes de insertar, sin dejar tags de clip. Las curvas completamente contenidas se conservan; las intersecciones se aproximan a segmentos con una tolerancia de 1/32 de píxel del script. El blur y el borde se dibujan después del corte y pueden extenderse fuera de él.

En una imagen raster, **source + auto** solicita color; los modos explícitos de máscara toman el color del estilo. Los tags de salida se comparan con el estilo de destino: se omiten los valores redundantes y se conservan las anulaciones necesarias.

**Threshold** define la máscara binaria. **Simplify** reduce detalle de sus contornos y **Min area** descarta áreas pequeñas. **Scale** elige entre `\p1` y `\p6` sin cambiar el tamaño visible. Los preajustes VTracer afectan a la conversión de color.

**Active pos** solo lee un `\pos` estático explícito. Para posiciones heredadas o movimiento, usa coordenadas manuales.

## Convertir una secuencia

Selecciona las fuentes y varios archivos. Los nombres se ordenan por número: frame2 precede a frame10. Cada imagen corresponde a un intervalo de fotograma dentro de las líneas seleccionadas; la cantidad debe coincidir con los trabajos indicados.

Una imagen transparente deja su intervalo vacío sin desplazar las siguientes. Exporta antes GIF animados o imágenes multipágina como archivos independientes.

## Backend

El backend actual es **kite-png2ass 1.5.1**. Configura Python en **Backend/Configure**, instala con **Install or Update** y revisa **Check**. En Windows se reintentan los bloqueos breves del archivo de progreso; si persisten, se omite esa actualización sin cancelar la conversión. Los fallos al escribir el resultado siguen siendo fatales. Los avisos de líneas o caracteres permiten evaluar una salida grande antes de insertarla. Consulta la [instalación](../installation.md#backends-de-python).


## Ejemplo: convertir una señal de dos colores a dibujo ASS

La señal mide 120 × 60 píxeles: un fondo azul y una flecha blanca. Este SVG define ambos contornos:

```xml
<svg xmlns="http://www.w3.org/2000/svg" width="120" height="60">
  <path fill="#235789" d="M0 0H120V60H0Z"/>
  <path fill="#ffffff" d="M30 25H75V10L100 30L75 50V35H30Z"/>
</svg>
```

1. Guarda el código como `senal.svg`. Selecciona una línea de 1.00 a 4.00 s, ejecuta **PNG2ASS** y elige ese SVG.
2. Usa **Color = source**, **Position = 0,0**, escala de dibujo 1 y simplificación 0.
3. Pulsa **Execute**. El resumen anuncia dos líneas; pulsa **Insert**.

Se insertan un rectángulo azul y una flecha blanca. El motor SVG conserva los vértices del original y genera dos eventos ASS de 1 a 4 segundos; la línea que estaba seleccionada se conserva.

### Imagen y dibujo convertido

<div class="shot-pair">
<figure class="ui-shot"><img src="../../assets/examples/png2ass/senal.svg" alt="Señal SVG azul con una flecha blanca"><figcaption>SVG de entrada: 120 × 60 píxeles.</figcaption></figure>
<figure class="ui-shot"><img src="../../assets/examples/png2ass/salida.png" alt="Dibujo ASS azul con una flecha blanca"><figcaption>Salida ASS renderizada; recorte de 240 × 120 píxeles desde (0, 0).</figcaption></figure>
</div>
