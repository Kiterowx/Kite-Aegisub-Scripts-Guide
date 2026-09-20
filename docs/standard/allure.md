# Allure

Versión **1.2.4**.

Allure guarda composiciones de carteles y transforma sus capas alrededor de un pivote común. El panel ofrece **Makeup** para la biblioteca y **Posing** para la geometría.

## Guardar e insertar con Makeup

1. Guarda el ASS, selecciona las capas y activa la línea de referencia.
2. Escribe un nombre y elige **Save style**, **Save group** o **Save both**.
3. Pulsa **Makeup**. Después selecciona los destinos, abre el registro y usa **Insert preset**.

| Registro | Contenido y uso |
| --- | --- |
| `[TAG]` | Tratamiento adaptable a texto nuevo. **Create from targets** necesita un destino por espacio de texto; **Replace selected layers**, un grupo completo de capas. |
| `[GROUP]` | Eventos completos: texto, dibujos, etiquetas, campos, capas y diferencias temporales. Cada destino recibe un grupo. |

La biblioteca consta de `Makeup Library.index.json` y la carpeta `Makeup Library`, junto al subtítulo. Copia ambos al trasladarla. Para carteles compuestos solo por dibujos, usa **Save group**.

## Mover, girar y cambiar tamaño con Posing

<figure class="ui-shot">
  <img src="../../assets/captures/allure-move-01.png" alt="Move X = 120 y Move Y = −40 desplazan el cartel. Relative resize = 0 conserva el tamaño; el pivote solo interviene al girar o redimensionar." loading="lazy">
  <figcaption>Move X = 120 y Move Y = −40 desplazan el cartel. Relative resize = 0 conserva el tamaño; el pivote solo interviene al girar o redimensionar.</figcaption>
</figure>

El giro y el cambio de tamaño usan el centro del grupo, la primera línea o un punto personalizado. El centro se obtiene de las posiciones y extremos de movimiento. **Relative resize = −50** reduce el conjunto a la mitad.

Las posiciones, movimientos, orígenes, clips y dibujos se transforman juntos. Un clip rectangular estático girado pasa a vectorial. Si el clip rectangular está animado, conviértelo antes a fotogramas independientes.

## Configuración y límites

**Config** guarda idioma, pasos de atajos, pivote y modo de giro. El panel admite español e inglés.

Revisa la adaptación de clips al cambiar mucho el texto o usar perspectiva. Un grupo exacto conserva los desplazamientos temporales de sus capas; un destino demasiado corto se rechaza. Instala `l0.dkjson` y las fuentes utilizadas.


## Ejemplo: recolocar un cartel sin editar sus etiquetas a mano

1. Selecciona la línea situada en (640, 360).
2. En **Posing**, conserva **Transform selection**, escribe **X = 120** e **Y = -40** y deja giro y tamaño en cero.
3. Pulsa **Posing**.

La posición pasa a (760, 320): 120 píxeles a la derecha y 40 hacia arriba. La operación conserva texto, estilo, actor y tiempos.

**Entrada, campo Texto:**

```ass
{\pos(640,360)}SALIDA
```

**Salida, campo Texto:**

```ass
{\pos(760,320)}SALIDA
```

### Comparación visual

<div class="shot-pair">
<figure class="ui-shot"><img src="../../assets/examples/allure/entrada.png" alt="Posición inicial (640, 360)." loading="lazy"><figcaption>Posición inicial (640, 360).</figcaption></figure>
<figure class="ui-shot"><img src="../../assets/examples/allure/salida.png" alt="Posición final (760, 320), con el mismo recorte de imagen." loading="lazy"><figcaption>Posición final (760, 320), con el mismo recorte de imagen.</figcaption></figure>
</div>
