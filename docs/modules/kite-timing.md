# Timing

Versión **1.4.3** · `kite.Timing`

Combina señales de voz para los métodos Busy y Legacy de Chrono Suite. También contiene el motor de reconstrucción de Macaria Revert.

Se instala en `automation/include/kite/Timing.lua`. No añade una macro propia al menú.

## Ejemplo: clasificar archivos de señal

`classifyDataFile` reconoce nombres de VAD, silencios y keyframes. Clasificar un nombre no analiza las muestras contenidas en el archivo.

El código se ejecuta dentro de Aegisub, con el módulo instalado.

```lua
local Timing = require("kite.Timing")
assert(Timing.classifyDataFile("episodio_vad.tsv") == "vad")
assert(Timing.classifyDataFile("episodio_sil40.log") == "sil40")
assert(Timing.classifyDataFile("episodio_keyframes.txt") == "keyframes")
aegisub.debug.out("vad, sil40, keyframes\n")
```

**Salida:**

```text
vad, sil40, keyframes
```
