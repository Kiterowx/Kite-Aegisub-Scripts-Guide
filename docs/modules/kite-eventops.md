# EventOps

Versión **1.3.1** · `kite.EventOps`

Comparte operaciones de eventos: tartamudeo, fundidos por fotograma, limpieza de fades interiores y mezcla de textos.

Se instala en `automation/include/kite/EventOps.lua`. No añade una macro propia al menú.

## Ejemplo: retirar un fade interior

Al enlazar dos líneas, el fade de salida de la primera puede crear un parpadeo. `adjustFade` permite ponerlo en cero conservando el fade de entrada.

El código se ejecuta dentro de Aegisub, con el módulo instalado.

```lua
local Events = require("kite.EventOps")
local output, changed = Events.adjustFade("{\\fad(100,200)}SALIDA", false, true)
assert(output == "{\\fad(100,0)}SALIDA")
assert(changed == 1)
aegisub.debug.out(output .. "\n")
```

**Salida:**

```text
{\fad(100,0)}SALIDA
```
