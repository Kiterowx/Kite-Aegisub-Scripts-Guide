# Zheus Colormanager

Versión **4.7.4**.

Zheus Colormanager gestiona colores por actor, reemplazos, degradados de cuatro esquinas y cambios temporales. También compara paletas y ofrece perfiles de visión del color.

## Asignar colores por actor

Selecciona las líneas, abre **Colores por actor** y ajusta relleno, borde y sombra. Las páginas de ocho actores conservan sus cambios al navegar.

| Aplicar como | Resultado |
| --- | --- |
| Etiquetas, con auto-limpieza | Retira colores anteriores de los canales editados y reitera la paleta después de resets. Conserva el secundario. |
| Etiquetas, sin auto-limpieza | Cambia la base y conserva colores sólidos posteriores, que pueden prevalecer. |
| Estilos | Genera estilos por actor y estilo de origen, conservando tipografía, márgenes y formato. |
| Limpiar | Retira colores sólidos y degradados de los cuatro canales, incluidas sus transformaciones. |

**Actores** permite renombrar, fusionar o vaciar nombres de la selección. **Lista**, **Conflictos**, **Importar** y **Exportar** se abren desde el selector del gestor.

## Sustituir colores y editar tramos

**Cambiar colores** enumera valores explícitos de los canales elegidos, incluidos destinos de transformaciones y esquinas VSF. **Actualizar** relee la selección después de cambiar el filtro. Las sustituciones se aplican una vez: rojo → azul y azul → verde no convierte el rojo inicial en verde.

**Editor de tramos** modifica colores y fronteras por grafema. Permite dividir, unir y cambiar de canal conservando el texto. Protege los canales animados frente a una sustitución estática.

## Programar cambios con Transiciones de color

1. Selecciona las líneas y escribe los fotogramas de control, por ejemplo `120f, 150f`.
2. Indica el fundido en milisegundos o fotogramas, como `240ms` o `6f`.
3. Elige las sustituciones de cada control y aplica el programa completo.

El fundido se centra en el control y puede atravesar el corte entre líneas sin reiniciarse. Cero produce un cambio instantáneo. La duración en fotogramas sigue el mapa temporal del vídeo.

Transiciones de color necesita colores sólidos uniformes en los canales afectados. Los cambios intermedios, transformaciones previas de color, VSF o fundidos superpuestos requieren preparar las líneas o usar el editor de tramos.

## Degradados VSF

`\1vc`, `\2vc`, `\3vc` y `\4vc` corresponden a los cuatro canales. Las esquinas se ordenan: superior izquierda, superior derecha, inferior izquierda e inferior derecha.

Se escriben como etiquetas. Necesitan **VSFilterMod o un renderizador compatible**; libass no muestra estas extensiones. Para degradados compatibles con libass, usa [Gradient Row](../standard/gradient-row.md).

## Comparar y adaptar paletas

**Daltonismo → Auditar** presenta contraste, luminancia y diferencias entre actores sin modificar subtítulos. Los perfiles Daltonismo, Universal, Protanopía, Deuteranopía, Tritanopía, Monocromo y Alto contraste proponen otras paletas. **Calibrar** guarda preferencias en Personalizado.

Revisa **Preservar alfa**, **Forzar bord y shad** e **Incluir dibujos** antes de aplicar. Las simulaciones son aproximaciones: la legibilidad final depende también del fondo, la opacidad y el borde presente en el vídeo.

## Guardar paletas

Las paletas por actor y las accesibles se pueden exportar e importar. Conservan nombres Unicode y actores vacíos. Los ajustes y perfiles personalizados se guardan entre sesiones.


## Ejemplo: asignar una paleta estable al narrador

1. Selecciona la línea cuyo actor es `Narrador`.
2. Abre **Gestor → Colores por Actor** y fija relleno `#FFC857`, borde `#20242C` y sombra `#000000`.
3. En **Aplicar como**, elige **Etiquetas**. Mantén la limpieza activada y pulsa **Aplicar**.

El texto conserva sus palabras y tiempos. El relleno, el borde y la sombra quedan escritos en ASS, cuyo orden de componentes de color es BGR.

**Entrada, campo Texto:**

```ass
La puerta se abre.
```

**Salida, campo Texto:**

```ass
{\c&H57C8FF&\3c&H2C2420&\4c&H000000&}La puerta se abre.
```

### Comparación visual

<div class="shot-pair">
<figure class="ui-shot"><img src="../../assets/examples/zheus-colormanager/entrada.png" alt="Color inicial del narrador." loading="lazy"><figcaption>Color inicial del narrador.</figcaption></figure>
<figure class="ui-shot"><img src="../../assets/examples/zheus-colormanager/salida.png" alt="Relleno #FFC857 con borde #20242C." loading="lazy"><figcaption>Relleno #FFC857 con borde #20242C.</figcaption></figure>
</div>

Los atajos Colores por actor, Colores de 4 esquinas, Renombrar o fusionar actores y Transiciones de color explican su acción. Los nombres anteriores conservan sus asignaciones al recargar el script.
