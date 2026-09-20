# Selesub

Versión **2.1.8**.

Selesub busca eventos, selecciona o comenta coincidencias, elimina resultados confirmados y transfiere líneas entre archivos ASS.

## Buscar coincidencias

1. Elige **Scope = All** o **Selection** y la acción.
2. Combina los filtros exactos de Actor, Effect, Style y Layer con la consulta avanzada.
3. Pulsa **Run**. Las consultas inválidas o sin resultados regresan al formulario.

<figure class="ui-shot">
  <img src="../../assets/captures/selesub-select-01.png" alt="Visible Text busca sin etiquetas ni dibujos. Contains con SALIDA encuentra tanto SALIDA como SALIDA DE EMERGENCIA." loading="lazy">
  <figcaption>Visible Text busca sin etiquetas ni dibujos. Contains con SALIDA encuentra tanto SALIDA como SALIDA DE EMERGENCIA.</figcaption>
</figure>

| Campo u opción | Comportamiento |
| --- | --- |
| Text | Incluye etiquetas y comentarios ASS. |
| Visible Text | Retira bloques ASS y dibujos; convierte saltos y espacios duros en espacios. |
| ASS Comments | Busca en comentarios internos. |
| Duration, CPS, Character Count | Permite comparaciones numéricas. Duration se expresa en milisegundos. |
| Start / End | Compara el borde indicado; Range incluye ambos extremos. |
| Invert advanced | Invierte solo la condición avanzada. |
| Include comments | Incluye eventos Comment. |

Un filtro exacto vacío no restringe; `<empty>` busca el campo vacío. **Delete** pide confirmación. La búsqueda por texto visible no evalúa si un fade lo oculta en un fotograma.

## Gestionar valores

**Values** agrupa por Style, Actor, Effect o Layer. La lista editable contiene los valores que se van a **conservar**: elimina de ella los grupos sobre los que quieras actuar.

<figure class="ui-shot">
  <img src="../../assets/captures/selesub-values-02.png" alt="Apply actúa sobre los valores omitidos de la lista. Los valores que permanecen escritos se conservan." loading="lazy">
  <figcaption>Apply actúa sobre los valores omitidos de la lista. Los valores que permanecen escritos se conservan.</figcaption>
</figure>

**Current** usa directamente la selección inicial. **Refresh** reconstruye los grupos. Cambiar Nature o Scope regenera la lista antes de actuar; revisa las filas nuevas.

## Importar, exportar y navegar

**Export** guarda la selección de entrada, junto con estilos y datos del proyecto. Ejecuta primero la búsqueda si quieres exportar sus resultados.

**Import** añade eventos al final y solo crea estilos ausentes. Un estilo existente con el mismo nombre conserva sus propiedades, por lo que puede cambiar la apariencia del texto importado. La resolución del documento actual se mantiene.

Los atajos de Style, Actor y Effect permiten seleccionar coincidencias, saltar a la anterior/siguiente y recorrer bloques. Range selecciona hasta el inicio o fin del archivo. Instala `myaa.ASSParser` para importar y exportar.


## Ejemplo: localizar las variantes de un mismo letrero

1. Crea tres líneas con `SALIDA`, `ENTRADA` y `SALIDA DE EMERGENCIA`, en ese orden. La primera puede incluir una etiqueta como `\pos(640,360)`.
2. Elige **Scope = All**, **Action = Select**, **Field = Visible Text** y **Match = Contains**.
3. Escribe `SALIDA` en la consulta y pulsa **Run**.

Quedan seleccionadas las filas de diálogo 1 y 3. El texto y los tiempos permanecen intactos. Las etiquetas de posición de la primera línea no interfieren en la búsqueda de texto visible.

<div class="selection-result">
<table>
<thead><tr><th>Fila</th><th>Texto visible</th><th>Selección</th></tr></thead>
<tbody>
<tr class="is-selected"><td>1</td><td><mark>SALIDA</mark></td><td>Sí</td></tr>
<tr><td>2</td><td>ENTRADA</td><td>No</td></tr>
<tr class="is-selected"><td>3</td><td><mark>SALIDA</mark> DE EMERGENCIA</td><td>Sí</td></tr>
</tbody>
</table>
</div>
