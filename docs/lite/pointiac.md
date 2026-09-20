# Pointiac

Versión **1.1.7**.

Pointiac añade dos círculos a cada diálogo seleccionado: uno al principio y otro al final. Las fuentes se conservan y los marcadores quedan seleccionados.

## Colocar las marcas

<figure class="ui-shot">
  <img src="../../assets/captures/pointiac-markers-01.png" alt="X/Y coloca el primer círculo. Offset X desplaza el segundo y Layer + suma una diferencia a la capa de origen." loading="lazy">
  <figcaption>X/Y coloca el primer círculo. Offset X desplaza el segundo y Layer + suma una diferencia a la capa de origen.</figcaption>
</figure>

1. Selecciona las líneas y abre **Pointiac**.
2. Elige color, posición, separación horizontal y capa.
3. Pulsa **Execute** y revisa los extremos del intervalo.

Offset X admite positivos, negativos y cero. Con X = 100 y Offset X = −20, las marcas quedan en X = 100 y X = 80.

## Duración de los marcadores

Con tiempos de vídeo, se utiliza el primer fotograma visible y el que contiene el último milisegundo anterior al fin. Los fragmentos se limitan al intervalo de la fuente y respetan la duración variable de los fotogramas.

Si no hay conversiones utilizables, **FPS** define la duración alternativa. Los marcadores pueden coincidir en una línea muy corta.

## Ejemplo sin tiempos de vídeo

Para una fuente de 1 a 3 s, **FPS = 25**, X/Y = 100/100, Offset X = 20 y Layer + = 1:

| Elemento | Intervalo | Posición | Capa si la fuente usa 0 |
| --- | --- | --- | --- |
| Fuente | 1.00–3.00 s | Conserva la original | 0 |
| Marca inicial | 1.00–1.04 s | (100, 100) | 1 |
| Marca final | 2.96–3.00 s | (120, 100) | 1 |

Cada marca ocupa 40 ms en este cálculo alternativo. Con vídeo, manda su mapa temporal.
