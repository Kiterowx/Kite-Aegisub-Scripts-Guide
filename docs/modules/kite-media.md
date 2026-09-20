# Media

Versión **1.4.0** · `kite.Media`

Resuelve rutas del proyecto e intervalos de fotogramas usando los tiempos del vídeo, tanto de frecuencia constante como variable.

Se instala en `automation/include/kite/Media.lua`. No añade una macro propia al menú.

## Ejemplo: consultar el fotograma de un instante

La conversión usa el mapa temporal del vídeo abierto. Comprueba que esté disponible antes de utilizar el resultado.

```lua
local Media = require("kite.Media")
local frame = assert(Media.frameFromMs(1000), "Carga un vídeo con tiempos disponibles")
aegisub.debug.out(string.format("1000 ms -> %d f\n", frame))
```
