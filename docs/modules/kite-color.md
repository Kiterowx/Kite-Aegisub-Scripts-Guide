# Color

Versión **1.2.2** · `kite.Color`

Convierte colores RGB y ASS, interpola canales y calcula luminancia, contraste y coordenadas OKLab. Incluye el editor de tramos que utiliza Zheus.

Se instala en `automation/include/kite/Color.lua`. El color ASS se escribe en orden BGR; el alfa se gestiona aparte.

## Ejemplo: convertir una paleta

```lua
local Color = require("kite.Color")
local ass = Color.fromRGB(255, 200, 87)
assert(ass == "&H57C8FF&")
assert(Color.toHex(ass) == "#FFC857")
aegisub.debug.out(ass .. "\n")
```

`normalizeStrict` devuelve nil ante un color inválido; `normalize` utiliza blanco como alternativa. Elige la función según necesites rechazar la entrada o proporcionar un valor.
