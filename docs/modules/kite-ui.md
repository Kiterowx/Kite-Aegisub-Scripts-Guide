# UI

Versión **1.5.2** · `kite.UI`

Construye diálogos y selectores, conecta preferencias con Settings y publica los catálogos de acciones y favoritos que utiliza Hotkeys.

`actions.rename` migra las identidades de acciones registradas junto con sus atajos y favoritos. Permite cambiar nombres visibles sin perder las asignaciones guardadas.

Se instala en `automation/include/kite/UI.lua`. No añade una macro propia al menú.

## Ejemplo: crear un diálogo y leer su resultado

`workflow` añade título y descripción a los controles. El resultado contiene el botón pulsado y una tabla con los valores de los campos.

El código se ejecuta dentro de Aegisub, con el módulo instalado.

```lua
local UI = require("kite.UI")
local button, values = UI.workflow("Desplazamiento", "Distancia horizontal del cartel", {
    {class="label", label="X (px)", x=0, y=0, width=12},
    {class="intedit", name="dx", value=120, x=12, y=0, width=28}
}, {"Aplicar", "Cancelar"}, {ok="Aplicar", close="Cancelar"})
if button == "Aplicar" then
    aegisub.debug.out(string.format("dx=%d\n", values.dx))
end
```

**Salida:**

```text
dx=120
```

<figure class="ui-shot"><img src="../../assets/captures/module-ui-01.png" alt="Diálogo Desplazamiento creado con UI.workflow"><figcaption>Aplicar devuelve el valor 120 del campo X.</figcaption></figure>
