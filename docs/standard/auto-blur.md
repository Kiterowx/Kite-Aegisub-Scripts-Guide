# AutoBlur

Versión **2.1.4**.

AutoBlur estima cambios de nitidez del fondo y escribe una curva `\blur` en una línea. Necesita vídeo cargado y Aegisub de arch1t3cht.

## Elegir la muestra

1. Selecciona una línea y coloca el vídeo dentro de su intervalo.
2. Elige un punto con detalle del fondo cercano al cartel.
3. Ajusta el muestreo y pulsa **Execute**.

<figure class="ui-shot">
  <img src="../../assets/captures/autoblur-edge-01.png" alt="Patch radius amplía la zona de análisis. Quant step agrupa niveles de desenfoque y Smooth window suaviza las variaciones entre fotogramas." loading="lazy">
  <figcaption>Patch radius amplía la zona de análisis. Quant step agrupa niveles de desenfoque y Smooth window suaviza las variaciones entre fotogramas.</figcaption>
</figure>

Una superficie completamente uniforme no permite comparar el enfoque. Los cortes de escena, cambios de iluminación o texturas móviles también alteran la medida: revisa el resultado sobre el vídeo.

## Ajustar la curva

| Control | Efecto |
| --- | --- |
| Patch radius | Radio de las cinco zonas de muestra, en píxeles del vídeo; mínimo 2. |
| Max blur | Mayor desenfoque permitido; cero produce `\blur0`. |
| Curve exponent | Cambia la respuesta a la nitidez relativa. |
| Quant step | Distancia entre niveles; cero desactiva la cuantización. |
| Smooth window | Media temporal en fotogramas; 1 la desactiva. |
| Min run | Suprime tramos cortos en modo Discrete. |
| Transition | Duración de los cambios, en milisegundos. |
| Strip existing | Retira blur y be del primer bloque y de sus transformaciones. |

Las etiquetas intermedias y los resets posteriores permanecen y pueden cambiar el desenfoque en parte del texto.

## Usar seguimiento

**Use tracking data** admite Position de After Effects. Los datos deben cubrir el intervalo de fotogramas de la línea; el punto de muestra corresponde al fotograma actual. Sin seguimiento, se analiza una coordenada fija.

## Ejemplo: un fondo de enfoque constante

Selecciona un borde que permanezca inmóvil y conserve su nitidez durante toda la línea. Con **Max blur = 5** y **Quant step = 0.25**, una medida constante y no nula produce `\blur0`. Una zona con varianza cero se rechaza y deja la línea intacta.

<figure class="ui-shot">
  <img src="../../assets/examples/snapshoter/resultado.png" alt="El borde oscuro aporta contraste para comparar fotogramas; el interior de color uniforme no ofrece una referencia de nitidez." loading="lazy">
  <figcaption>El borde oscuro aporta contraste para comparar fotogramas; el interior de color uniforme no ofrece una referencia de nitidez.</figcaption>
</figure>
