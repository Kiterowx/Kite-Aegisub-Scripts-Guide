# ShapeOptimizer

Versión **1.3.2** · `kite.ShapeOptimizer`

Analiza dibujos estáticos y propone reducciones de colores o bandas de degradado. Rhea Signs lo expone en Shapes → Shape Color Optimizer.

Se instala en `automation/include/kite/ShapeOptimizer.lua`. No añade una macro propia al menú.

## Ejemplo: leer el pivote de un dibujo

`parsePosition` obtiene un único punto de anclaje antes de transformar la geometría. Una línea con dos posiciones se rechaza por ambigüedad.

El código se ejecuta dentro de Aegisub, con el módulo instalado.

```lua
local Shape = require("kite.ShapeOptimizer")
local position = assert(Shape.geometry.parsePosition("{\\an7\\pos(320,180)\\p1}"))
assert(position.x == 320 and position.y == 180)
local invalid = Shape.geometry.parsePosition("{\\pos(10,20)\\pos(30,40)\\p1}")
assert(invalid == nil)
aegisub.debug.out(string.format("x=%d, y=%d\n", position.x, position.y))
```

**Salida:**

```text
x=320, y=180
```
