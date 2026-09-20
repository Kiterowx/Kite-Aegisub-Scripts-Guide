# Field Group Manager

Versión **1.1.8**.

Field Group Manager agrupa eventos por un campo y asigna un valor a cada grupo. Por ejemplo, puede dar una capa distinta a cada actor.

## Definir la correspondencia

<figure class="ui-shot">
  <img src="../../assets/captures/field-layers-02.png" alt="Cada fila de New values corresponde al grupo de su izquierda. Refresh list reconstruye la lista y descarta las asignaciones editadas." loading="lazy">
  <figcaption>Cada fila de New values corresponde al grupo de su izquierda. Refresh list reconstruye la lista y descarta las asignaciones editadas.</figcaption>
</figure>

1. Elige **Group by**, **Write field** y **Scope**.
2. En **Parallel list**, escribe un valor de destino por grupo. **Single value** aplica el mismo a todos.
3. Revisa las filas y pulsa **Execute**.

Los grupos de texto se ordenan alfabéticamente; números y tiempos, numéricamente. Editar la columna izquierda no renombra los grupos. Cambiar campos, alcance o filtros regenera la lista antes de ejecutar.

## Campos y valores especiales

| Campo | Entrada |
| --- | --- |
| Actor, Effect, Style, Text | Texto literal. Style asigna un nombre, sin crear un estilo. |
| Layer, márgenes | Enteros no negativos; margen cero usa el del estilo. |
| Start, End | Milisegundos o tiempos como `0:00:01.50`. El inicio no puede superar el fin. |
| Comment | `Comment` / `Dialogue`, `yes` / `no` o `1` / `0`. |

**Include empty source** incluye campos vacíos; **Include comments**, diálogos comentados. Un destino `<mixed>` indica valores distintos: dejarlo intacto omite ese grupo. Una fila vacía borra texto o asigna cero a un campo numérico.

Usa `\N` para saltos dentro de Text: cada fila física del cuadro corresponde a una asignación. Al terminar quedan seleccionadas las líneas modificadas.


## Ejemplo: separar por capas al narrador y a un personaje

1. Crea dos líneas de 1.00 a 4.00 s, en la capa 0 y con el mismo estilo: `Hola.`, con Actor `Ana`, y `La puerta se abre.`, con Actor `Narrador`. Selecciona ambas.
2. Elige **Group by = Actor**, **Write field = Layer**, **Mode = Parallel list** y **Scope = Selection**. Pulsa **Refresh list**.
3. Frente a `Ana` escribe `5`; frente a `Narrador`, `10`. Pulsa **Execute**.

Ana pasa a la capa 5 y Narrador a la 10. Si ambas líneas coinciden en posición e intervalo, pueden superponerse al quedar en capas distintas. La operación cambia metadatos, sin recolocar el texto. El informe confirma dos grupos y dos líneas actualizados, sin grupos omitidos. La correspondencia depende del orden visible de la lista; revísalo después de cambiar el campo de origen.

| Actor | Capa inicial | Capa final |
| --- | --- | --- |
| Ana | 0 | 5 |
| Narrador | 0 | 10 |
