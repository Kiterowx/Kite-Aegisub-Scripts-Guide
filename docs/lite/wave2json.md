# Wave2json

Versión **1.3.6**.

Wave2json exporta la amplitud del audio en un JSON con varios niveles de detalle. Sus tres comandos están bajo **Wave2json**; no tiene ventana de configuración.

## Elegir el intervalo

| Comando | Exportación |
| --- | --- |
| Full audio | Todo el audio activo. |
| Selected span | Del inicio más temprano al fin más tardío, incluidos huecos. |
| Each selected line | Un archivo por diálogo seleccionado. |

Usa primero el archivo de audio cargado y, si no hay uno separado, el audio del vídeo. FFmpeg debe estar en `PATH`. No hace falta Python.

## Localizar el JSON

El archivo se guarda junto al ASS o, si no tiene ruta, junto al medio. El audio completo usa el nombre `Project.waveform.json`; una selección añade sus tiempos al nombre.

La exportación sustituye un JSON anterior del mismo nombre al terminar correctamente. En **Each selected line**, los archivos ya completados permanecen si falla una línea posterior.

## Interpretar los datos

FFmpeg convierte a PCM mono de 48 kHz y 16 bits. El nivel base guarda mínimo y máximo por cada 48 muestras, equivalentes a 1 ms. Los siguientes combinan pares vecinos hasta llegar a un punto.

`peaks` alterna mínimos y máximos: contiene el doble de elementos que `points`. `durationMs` refleja el audio decodificado. En selecciones, `sourceStartMs` permite situar los datos en el tiempo original.

La forma de onda sirve de entrada al [Auto Timing de Chrono Suite](../suites/chrono-suite.md#auto-timing). Sus picos representan amplitud; por sí solos no identifican palabras ni hablantes.


## Ejemplo: exportar una señal para revisar dos tramos de audio

Para revisar dónde hay señal en un audio, exporta su envolvente y compara los tramos con la línea de tiempo. En este caso, la entrada es un WAV de cinco segundos, mono, de 48000 Hz y 16 bits: contiene un tono de 240 Hz entre 0.60–1.60 s y 2.20–3.60 s, con silencio en el resto.

1. Carga el audio en Aegisub y ejecuta **Wave2json → Full audio**.
2. En el JSON, consulta el nivel con **pointMs = 1**. Cada punto guarda el mínimo y el máximo de un milisegundo.

Los 240000 valores del audio se resumen en 5000 pares de picos en el nivel más fino. La exportación contiene 14 niveles. Los picos permiten localizar los dos tramos de señal; este tono no sirve para evaluar detección de palabras o voces.

| Campo del JSON | Valor |
| --- | --- |
| durationMs | 5000 |
| sampleRate | 48000 |
| channels | 1 |
| totalSamples | 240000 |
| levels[0].pointMs | 1 |
| levels[0].points | 5000 |
| Cantidad de niveles | 14 |

<figure class="ui-shot"><img src="../../assets/illustrations/wave2json-picos.png" alt="Envolvente del nivel de 1 ms: señal en 0.60–1.60 s y 2.20–3.60 s; silencio entre ambos tramos." loading="lazy"><figcaption>Envolvente del nivel de 1 ms: señal en 0.60–1.60 s y 2.20–3.60 s; silencio entre ambos tramos.</figcaption></figure>

Cada milisegundo contiene 48 muestras del WAV. El primer tramo ocupa los puntos 600–1599 y el segundo, 2200–3599, contando desde cero. Los índices 1600–2199 corresponden a 600 ms de silencio.
