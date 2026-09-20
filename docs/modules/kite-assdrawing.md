# AssDrawing

Versión **1.0.3** · `kite.AssDrawing`

Valida trayectos ASS y transforma sus coordenadas. Lo usan las herramientas de clips, máscaras, seguimiento y exportación.

Se instala en `automation/include/kite/AssDrawing.lua`. No añade una macro propia al menú.

## Ejemplo: trasladar un contorno

`mapCoordinates` transforma cada par de coordenadas. La validación rechaza un comando `l` que solo tenga una coordenada.

El código se ejecuta dentro de Aegisub, con el módulo instalado.

```lua
local Drawing = require("kite.AssDrawing")
local input = "m 0 0 l 100 0 100 40 0 40"
local output = Drawing.mapCoordinates(input, function(x, y)
    return x + 20, y + 10
end, 2)
assert(output == "m 20 10 l 120 10 120 50 20 50")
assert(not Drawing.validatePath("m 0 0 l 10"))
aegisub.debug.out(output .. "\n")
```

**Salida:**

```text
m 20 10 l 120 10 120 50 20 50
```
