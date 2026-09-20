# Macaria Revert

Versión **1.0.2**.

Macaria Revert reconstruye bases de karaoke a partir de eventos generados. Relaciona sus tiempos y posiciones para proponer líneas editables con `\k`.

## Revisar antes de reconstruir

1. Selecciona los eventos del karaoke, incluidas sus capas y fases.
2. Abre **Macaria Revert** y ajusta las tolerancias.
3. Pulsa **Preview** para leer el texto ASS completo de las bases propuestas.
4. Pulsa **Reconstruct** para insertarlas.

Los originales se conservan. Las bases se insertan comentadas, con Effect = `karaoke`, después del último diálogo seleccionado. Preview no edita ni guarda opciones; su texto es de consulta.

## Ajustes

| Control | Valor inicial y función |
| --- | --- |
| Position tolerance | 4 unidades: diferencia admitida por coordenada al relacionar fragmentos. |
| Row tolerance | 20 unidades: separación vertical admitida en una fila. |
| Time tolerance | 10 ms: separación entre límites temporales vecinos. |
| Infer word spacing | Deduce espacios a partir de medidas y separaciones. |
| Include alignment tags | Escribe la alineación deducida si difiere del estilo. |

Empieza con las tolerancias iniciales. Aumentarlas puede unir fragmentos de líneas distintas.

## Ejemplo de una base propuesta

Si reconoce A de 0 a 500 ms y B de 500 a 1000 ms, con posiciones consecutivas y fases repetidas que permitan relacionarlas, puede reconstruir:

```ass
{\k50}A{\k50}B
```

| Fragmento | Intervalo recuperado | Karaoke |
| --- | --- | --- |
| A | 0–500 ms | `\k50` |
| B | 500–1000 ms | `\k50` |

Revisa espacios, texto y tiempos antes de reutilizarla en [Alecto KFX](alecto-kfx.md). La apariencia del efecto no se reconstruye.

## Límites y acceso directo

Necesita posiciones explícitas utilizables y patrones temporales reconocibles. La selección incompleta, fragmentos superpuestos o información descartada pueden impedir recuperar una base.

**: Kite Hotkeys :/Macaria Revert/Reconstruct** ejecuta directamente con los valores predeterminados del motor. Usa la ventana para ajustar tolerancias y revisar la propuesta.
