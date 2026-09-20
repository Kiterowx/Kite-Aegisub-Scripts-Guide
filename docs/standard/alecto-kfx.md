# Alecto KFX

Versión **3.4.3**.

Alecto KFX adapta guías `intro`, `active` y `outro` a sílabas, grafemas, palabras o líneas completas.

## Preparar y aplicar las guías

1. Selecciona los destinos y ejecuta **Generar líneas base**.
2. Edita las guías: sus etiquetas definen la apariencia y su campo Effect identifica la fase.
3. Selecciona las guías y los destinos. Ejecuta **Validar selección** y después **Aplicar guías**. El acceso directo del menú se llama **Alecto KFX/Aplicar**.

Sin guías seleccionadas, se busca un bloque contiguo encima del primer destino. Las fases ausentes usan guías neutras.

| Comando | Resultado |
| --- | --- |
| Aplicar guías | Genera el efecto y reemplaza la salida asociada a los destinos. |
| Generar líneas base | Inserta guías editables. |
| Validar selección | Revisa entradas y estima la cantidad de eventos sin editar. |
| Limpiar FX seleccionados | Retira los efectos asociados y restaura el estado de comentario de las fuentes. |
| Configurar | Guarda tiempos predeterminados y límite de eventos. |

## Opciones en Actor

| Opción | Uso |
| --- | --- |
| `syl`, `char`, `word`, `line` | Sílabas temporizadas, grafemas, palabras o texto completo. |
| `lead=`, `tail=`, `fade=`, `stagger=` | Entrada, salida, fundido y desfase, en milisegundos. |
| `order=ltr`, `rtl`, `center`, `edges` | Orden de aparición de las unidades. |
| `group=` | Relaciona guías y destinos del mismo grupo. |
| `channel=`, `gap=` | Agrupa vecinos y reserva separación temporal. |
| `nobase`, `nofade`, `nostagger` | Desactiva base, fundido o desfase. |
| `inherit=none` | Omite las etiquetas estáticas iniciales del destino. |

Los valores de la guía tienen prioridad sobre los del destino y la configuración. Por ejemplo: `char lead=300 fade=200 stagger=40 order=edges`.

## Reaplicar y conservar la base

Mantén los identificadores de los efectos y sus datos de origen: permiten retirar la salida correcta aunque cambie de fila. El límite inicial es de 20 000 eventos; **0** lo desactiva.

Los dibujos `\p` no son destinos válidos. Para conservar la composición de texto multilínea, usa `line` o divide los renglones en eventos. La medida depende de las fuentes instaladas y de `karaskel.lua`, incluido en Aegisub.


## Ejemplo: dar entrada, activación y salida a tres sílabas

1. Crea una línea de 1.00 a 2.50 s con el texto de abajo: `Sa`, `li` y `da` duran 50 centésimas cada una.
2. Escribe en Actor `syl lead=200 tail=200 fade=100 stagger=0`. Selecciona la línea y ejecuta **Aplicar guías**.
3. Revisa las fases `intro`, `active` y `outro`. Sin guías personalizadas se usan las fases neutras; **Generar líneas base** permite crearlas y editarlas antes de aplicar.

La salida conserva la fuente como comentario y crea nueve eventos: tres de entrada, tres activos y tres de salida. La activación avanza a 1.00, 1.50 y 2.00 s; las salidas terminan a 2.70 s.

**Entrada, campo Texto:**

```ass
{\k50}Sa{\k50}li{\k50}da
```

<figure class="ui-shot"><img src="../../assets/illustrations/alecto-fases.png" alt="Cada sílaba ocupa tres eventos consecutivos. Las entradas empiezan a 0.80 s y las salidas terminan a 2.70 s." loading="lazy"><figcaption>Cada sílaba ocupa tres eventos consecutivos. Las entradas empiezan a 0.80 s y las salidas terminan a 2.70 s.</figcaption></figure>

| Sílaba | Intro | Active | Outro |
| --- | --- | --- | --- |
| Sa | 0.80–1.00 s | 1.00–1.50 s | 1.50–2.70 s |
| li | 0.80–1.50 s | 1.50–2.00 s | 2.00–2.70 s |
| da | 0.80–2.00 s | 2.00–2.50 s | 2.50–2.70 s |
