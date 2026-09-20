# Snapshoter

Versión **1.6.8**.

Snapshoter extrae PNG del vídeo cargado: fotogramas, secuencias, rectángulos y máscaras con alfa. Conserva los eventos del ASS.

## Elegir la captura

<figure class="ui-shot">
  <img src="../../assets/captures/snapshoter-example-01.png" alt="Clip crop usa la geometría del ASS. Rectangle crop extrae su caja; las opciones alfa conservan la forma visible del clip o dibujo." loading="lazy">
  <figcaption>Clip crop usa la geometría del ASS. Rectangle crop extrae su caja; las opciones alfa conservan la forma visible del clip o dibujo.</figcaption>
</figure>

| Capture | Resultado |
| --- | --- |
| Selected lines | Capturas en los instantes elegidos de cada línea, sin subtítulos. |
| Frame list | Fotogramas escritos, ordenados y sin duplicados. |
| Frame sequence | Intervalo completo de la selección, incluidos huecos. |
| Clip crop | Recorte rectangular o alfa de clips/dibujos. |
| Manual rectangle | Caja X/Y/W/H en píxeles del vídeo. |
| Densest subtitle frame | Primer fotograma con más eventos seleccionados superpuestos. |

**Timing** elige punto medio, inicio/final, inicio/centro/final o fotograma actual. El final de un evento es exclusivo.

## Clips y transparencia

**Rectangle crop** usa el rectángulo envolvente de un clip normal estático. **Clip alpha** admite clips inversos y animación compatible con libass; **Drawing alpha** utiliza los dibujos como máscara. Crop recorta el área visible y Full frame conserva el tamaño del vídeo.

Las coordenadas del clip pasan de PlayRes a píxeles del vídeo. **Padding** amplía recortes rectangulares; no amplía las salidas alfa.

## Secuencias y archivos

Activa **No subtitles**, **With subtitles** o **Subtitles only**. With subtitles renderiza todos los eventos visibles del intervalo; la selección define los tiempos. Subtitles only produce fondo transparente.

Los PNG se guardan en **Snapshots**, junto al proyecto guardado, con la carpeta del script o vídeo como alternativa. **All images in Snapshots** evita las subcarpetas de lotes. Configura FFmpeg en **Config...**; necesita libass para subtítulos y alfa.

Frame list acepta `120`, `F120` o `120f, 130f`. Los números empiezan en cero; `120-130` no se expande como intervalo.


## Ejemplo: extraer solo el rectángulo del letrero

1. Usa PlayRes de 1280 × 720 y carga un vídeo de la misma resolución y selecciona una línea de 1.00 a 4.00 s con el clip rectangular de abajo.
2. Elige **Capture = Clip crop**, **Clip output = Rectangle crop** y **Timing = Midpoint**, con **Padding = 0**.
3. Desactiva la inclusión del texto en el nombre y pulsa **Execute**.

Se guarda un PNG de 480 × 200 píxeles correspondiente al punto medio de la línea, 2.50 s. El ASS queda intacto. El ancho sale de 880 − 400 y la altura, de 460 − 260.

**Entrada, campo Texto:**

```ass
{\clip(400,260,880,460)}SALIDA
```

<figure class="ui-shot"><img src="../../assets/examples/snapshoter/resultado.png" alt="Recorte de 480 por 200 píxeles del letrero"><figcaption>PNG producido por Clip crop en el punto medio de la línea.</figcaption></figure>
