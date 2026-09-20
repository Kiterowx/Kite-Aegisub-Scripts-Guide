# AssContext

Versión **1.1.3** · `kite.AssContext`

Resuelve estilo, alineación, márgenes, posición y estado temporal de una línea ASS. También conserva el reloj de animaciones al dividir eventos y proporciona Style to Tags.

Se instala en `automation/include/kite/AssContext.lua`. Es una biblioteca utilizada por los scripts de carteles y efectos.

## Ejemplo: evaluar una posición en movimiento

`explicitPosition` recibe texto, duración y tiempo relativo, en milisegundos. A mitad de este movimiento, la posición es (150, 200).

```lua
local Context = require("kite.AssContext")
local x, y = Context.explicitPosition("{\\move(100,200,200,200)}SALIDA", 1000, 500)
assert(x == 150 and y == 200)
aegisub.debug.out(string.format("x=%d, y=%d\n", x, y))
```

Esta función consulta una posición explícita. Para resolver también estilos y márgenes, crea el contexto del documento con `fromSubtitles`.
