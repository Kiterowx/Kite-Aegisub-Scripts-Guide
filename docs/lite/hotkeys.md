# Hotkeys

Versión **2.0.2**.

Hotkeys reúne la gestión de favoritos, migración de atajos y preferencias compartidas. Sus entradas son **: Kite Hotkeys :/Sync** y **Config**.

Los demás scripts registran sus acciones aunque este editor no esté instalado. Para asignar teclas nuevas, usa las preferencias de Aegisub.

## Migrar atajos

1. Abre **Sync** y revisa las rutas anteriores y propuestas.
2. Pulsa **Apply** para migrarlas o cierra para conservar el archivo.
3. Reinicia Aegisub si el cambio no aparece de inmediato.

La migración conserva teclas y contextos. Antes de escribir crea una copia con fecha y hora; si el archivo cambió durante la revisión, hay que preparar otro plan. Los cambios se basan en las rutas reconocidas y los registros de DependencyControl.

## Crear un favorito

En **Config**, elige **Source**, escribe **Favorite path** y pulsa **Add Favorite**. La ruta `Timing/Join` crea ese subgrupo bajo la raíz de favoritos. Si reutilizas una ruta, cambias la acción a la que apunta.

| Paso | Resultado |
| --- | --- |
| Source = acción de unir líneas | Se elige el comando original. |
| Favorite path = `Timing/Join` | Se guarda una ruta relativa a Favorites. |
| Recargar Automation | La macro de origen registra el favorito y su validación. |

**Remove Favorite** borra la asignación guardada; recarga para retirar una entrada ya visible. **Registered** consulta los catálogos: una acción puede seguir listada después de retirar su script.

## Preferencias compartidas

**Settings** abre las secciones guardadas en `kite.settings.json`. Elige una y pulsa **Edit** para modificar sus valores JSON. Conserva las claves y los tipos; una entrada inválida regresa al borrador.

**Save** guarda rutas y raíces del panel. Cerrar descarta esos cambios pendientes, pero no revierte favoritos que ya guardaste con Add/Remove. Puede hacer falta reabrir la macro propietaria para que lea una preferencia nueva.
