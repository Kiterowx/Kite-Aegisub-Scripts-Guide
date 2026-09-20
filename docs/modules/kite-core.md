# Core

Versión **1.1.0** · `kite.Core`

Validación numérica, copias de tablas, redondeo y operaciones básicas de texto.

Se instala en `automation/include/kite/Core.lua`. No añade una macro propia al menú.

## Ejemplo: formatear coordenadas sin decimales sobrantes

`formatNumber` redondea a tres decimales y devuelve texto listo para una etiqueta. `clamp` limita un valor a un intervalo.

El código se ejecuta dentro de Aegisub, con el módulo instalado.

```lua
local Core = require("kite.Core")
local value = Core.formatNumber(12.34567, 3)
assert(value == "12.346")
assert(Core.clamp(1.2, 0, 1) == 1)
aegisub.debug.out(value .. "\n")
```

**Salida:**

```text
12.346
```
