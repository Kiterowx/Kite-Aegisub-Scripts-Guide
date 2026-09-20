# Settings

Versión **1.0.1** · `kite.Settings`

Guarda preferencias por namespace y sección en `?user/config/kite.settings.json`. Migra formatos anteriores y comprueba claves y tipos al editar una sección compartida.

Se instala en `automation/include/kite/Settings.lua`. [Hotkeys](../lite/hotkeys.md#preferencias-compartidas) ofrece su editor desde Settings.

## Ejemplo: leer una tabla de datos

`parseLiteralTable` interpreta tablas literales sin ejecutar código Lua. Sirve para leer formatos heredados.

```lua
local Settings = require("kite.Settings")
local values = assert(Settings.parseLiteralTable('{ step = 10, enabled = true }'))
assert(values.step == 10 and values.enabled == true)
aegisub.debug.out(string.format("step=%d\n", values.step))
```

Para persistir opciones, `open` crea el almacén, `values` consulta una sección, `update` modifica sus valores y `write` los guarda. Comprueba el resultado de escritura antes de dar por guardada la configuración.
