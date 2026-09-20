# PyBridge

Versión **1.7.2** · `kite.PyBridge`

Ejecuta procesos externos, prepara argumentos y gestiona archivos temporales. Lo utilizan los backends de Python y las exportaciones con FFmpeg.

Se instala en `automation/include/kite/PyBridge.lua`. No añade una macro propia al menú.

## Ejemplo: preparar un argumento con espacios

`commandLine` construye la orden sin ejecutarla. El entrecomillado depende del sistema y del ejecutor disponible; pasa los argumentos como una lista.

```lua
local Bridge = require("kite.PyBridge")
local command = Bridge.commandLine("python", {
    "-m", "ass_png2ass", "senal de salida.svg"
})
aegisub.debug.out(command .. "\n")
```
