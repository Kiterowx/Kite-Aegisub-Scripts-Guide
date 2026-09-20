# LineOps

Versión **1.7.4** · `kite.LineOps`

Normaliza selecciones, lee texto y etiquetas y aplica inserciones o cambios con restauración ante errores.

Se instala en `automation/include/kite/LineOps.lua`. No añade una macro propia al menú.

## Ejemplo: buscar texto sin etiquetas

`visibleText` devuelve el contenido visible de la línea y permite buscar palabras sin que las etiquetas ASS interrumpan la comparación.

El código se ejecuta dentro de Aegisub, con el módulo instalado.

```lua
local Lines = require("kite.LineOps")
local output = Lines.visibleText("{\\an8}SALIDA{\\i1} NORTE{\\i0}")
assert(output == "SALIDA NORTE")
aegisub.debug.out(output .. "\n")
```

**Salida:**

```text
SALIDA NORTE
```
