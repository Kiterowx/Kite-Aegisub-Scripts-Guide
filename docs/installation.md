# Instalación

El orden es: **Aegisub y DependencyControl → bibliotecas del entorno → módulos de terceros → scripts y módulos Kite → programas externos según el uso**. Los módulos de terceros se instalan antes de copiar los scripts a `autoload`; una dependencia ausente puede impedir que la macro llegue a aparecer en el menú.

### 1. Aegisub y DependencyControl

La distribución recomendada es [Aegisub de arch1t3cht — Migration Release 04](https://github.com/arch1t3cht/Aegisub/releases/tag/migration04-01), basada en [TypesettingTools/Aegisub](https://github.com/TypesettingTools/Aegisub). AutoBlur usa funciones de vídeo de la versión de arch1t3cht. Se conservan las carpetas y bibliotecas de Automation incluidas en Aegisub.

Si DependencyControl no aparece o falla después de instalar Aegisub Migration, puede repararse con la [versión 0.9.1](https://github.com/TypesettingTools/DependencyControl/releases/tag/v0.9.1):

1. Descargar **[DependencyControl-v0.9.1.zip](https://github.com/TypesettingTools/DependencyControl/releases/download/v0.9.1/DependencyControl-v0.9.1.zip)** desde los assets de la versión. Los enlaces **Source code** contienen el repositorio, no el paquete de instalación.
2. Cerrar Aegisub y extraer el contenido del paquete en `%APPDATA%\Aegisub\automation`, fusionando sus carpetas `autoload` e `include` con las existentes. No debe quedar otro nivel `automation\automation`.
3. Abrir Aegisub y comprobar que esté disponible **DependencyControl → Install Script** dentro de Automation. Para recargar scripts también se puede usar **Automation → Rescan Autoload Dir**.

Se utiliza la carpeta del perfil de usuario, no la de `Program Files`, donde las actualizaciones pueden fallar por permisos. Una instalación portátil debe usar sus rutas de Automation configuradas. En Linux la ruta habitual es `~/.aegisub/automation`; en macOS, `~/Library/Application Support/Aegisub/automation`.

La versión 0.9.1 corrige un caso de **Bad DependencyControl record** causado por módulos instalados manualmente cuya versión no se podía interpretar. No corrige una ruta equivocada ni instala programas externos. En Aegisub 3.4 o posterior, el paquete actual de DependencyControl para Windows/macOS incorpora sus componentes necesarios: ya no requiere instalar por separado DownloadManager, BadMutex ni PreciseTimer. Otras bibliotecas aún pueden necesitar **requireffi**, que se instala como dependencia de ZF. [Instrucciones oficiales](https://github.com/TypesettingTools/DependencyControl/blob/v0.9.1/README.md).

### 2. Bibliotecas del entorno

Estas bibliotecas se comprueban aparte de la lista anterior:

| Componente | Dónde se obtiene y cuándo se necesita |
| --- | --- |
| `karaskel.lua`, `utils.lua`, `aegisub.re`, `aegisub.unicode`, `aegisub.clipboard` y cargador de MoonScript | Forman parte del entorno de Automation de Aegisub. Se conservan los archivos de su distribución; no se buscan como módulos de este catálogo. |
| [Yutils](https://github.com/Youka/Yutils) | Obligatorio para Zagreo Glyphs y **ZF main** —usado por AddTexture, Cliptomaniac, Moka Motion y PNG2ASS—; también se usa en operaciones de curvas de ASSFoundation. Si falta, se copia [src/Yutils.lua](https://github.com/Youka/Yutils/blob/T1/src/Yutils.lua) como `automation/include/Yutils.lua`. No está incluido en todas las versiones de Aegisub. Requiere LuaJIT; libpng solo se necesita para su lector de PNG. |
| [LuaJSON](https://github.com/harningt/luajson) (`json`) | Lo necesitan **Line** de Aegisub-Motion y Smart Split de Chrono para leer las ondas. Si falta, se copian `json.lua` y la carpeta `json` del directorio [lua del proyecto](https://github.com/harningt/luajson/tree/master/lua) a `automation/include`. Necesita LPeg (`lpeg`), incluido en el entorno Lua de las distribuciones recomendadas. Se conserva completa la carpeta `json`: dkjson no sustituye su API. |
| Fuentes tipográficas | Deben estar disponibles tanto para Aegisub como para el renderizador usado al exportar. |
| VSFilterMod | Los degradados de cuatro esquinas de Zheus requieren un renderizador compatible con esas extensiones. Instalar un módulo Lua no añade ese soporte a libass. |

### 3. Módulos de terceros desde DependencyControl

En **DependencyControl → Install Script** se elige el desplegable **Modules:**. **Automation Scripts:** es otro selector y contiene macros, no las bibliotecas de esta tabla. El nombre suele ir seguido de la versión y, si procede, del canal.

Se instala **aka.command** como dependencia común de los módulos Kite. Después se añaden los módulos de los scripts elegidos según la [tabla por script](https://github.com/Kiterowx/Kite-Aegisub-Scripts/blob/main/docs/es/Dependencies.md#dependencias-por-script). **dkjson** viene en el paquete de DependencyControl; Allure lo declara expresamente. No hace falta instalar todas las bibliotecas del catálogo para usar una sola macro.

| Nombre en **Modules** | Identificador en el código | Catálogo de origen |
| --- | --- | --- |
| **ZF main** | `ZF.main` | [zeref](https://github.com/TypesettingTools/zeref-Aegisub-Scripts) · [feed](https://raw.githubusercontent.com/TypesettingTools/zeref-Aegisub-Scripts/main/DependencyControl.json) |
| **ASSFoundation** | `l0.ASSFoundation` | [ASSFoundation](https://github.com/TypesettingTools/ASSFoundation) · [feed](https://raw.githubusercontent.com/TypesettingTools/ASSFoundation/master/DependencyControl.json) |
| **(Almost) Functional Suite** | `l0.Functional` | [Functional](https://github.com/TypesettingTools/Functional) · [feed](https://raw.githubusercontent.com/TypesettingTools/Functional/master/DependencyControl.json) |
| **Line** | `a-mo.Line` | [Aegisub-Motion](https://github.com/TypesettingTools/Aegisub-Motion) · [feed](https://raw.githubusercontent.com/TypesettingTools/Aegisub-Motion/DepCtrl/DependencyControl.json) |
| **LineCollection** | `a-mo.LineCollection` | [Aegisub-Motion](https://github.com/TypesettingTools/Aegisub-Motion) · [feed](https://raw.githubusercontent.com/TypesettingTools/Aegisub-Motion/DepCtrl/DependencyControl.json) |
| **Log** | `a-mo.Log` | [Aegisub-Motion](https://github.com/TypesettingTools/Aegisub-Motion) · [feed](https://raw.githubusercontent.com/TypesettingTools/Aegisub-Motion/DepCtrl/DependencyControl.json) |
| **Tags** | `a-mo.Tags` | [Aegisub-Motion](https://github.com/TypesettingTools/Aegisub-Motion) · [feed](https://raw.githubusercontent.com/TypesettingTools/Aegisub-Motion/DepCtrl/DependencyControl.json) |
| **ArchMath** | `arch.Math` | [arch1t3cht](https://github.com/TypesettingTools/arch1t3cht-Aegisub-Scripts) · [feed](https://raw.githubusercontent.com/TypesettingTools/arch1t3cht-Aegisub-Scripts/main/DependencyControl.json) |
| **Perspective** | `arch.Perspective` | [arch1t3cht](https://github.com/TypesettingTools/arch1t3cht-Aegisub-Scripts) · [feed](https://raw.githubusercontent.com/TypesettingTools/arch1t3cht-Aegisub-Scripts/main/DependencyControl.json) |
| **Util** | `arch.Util` | [arch1t3cht](https://github.com/TypesettingTools/arch1t3cht-Aegisub-Scripts) · [feed](https://raw.githubusercontent.com/TypesettingTools/arch1t3cht-Aegisub-Scripts/main/DependencyControl.json) |
| **SubInspector** | `SubInspector.Inspector` | [SubInspector](https://github.com/TypesettingTools/SubInspector) · [feed](https://raw.githubusercontent.com/TypesettingTools/SubInspector/master/DependencyControl.json) |
| **aka.command** | `aka.command` | [Akatsumekusa](https://github.com/Akatmks/Akatsumekusa-Aegisub-Scripts) · [feed](https://raw.githubusercontent.com/Akatmks/Akatsumekusa-Aegisub-Scripts/master/DependencyControl.json) |
| **ASS Parser** | `myaa.ASSParser` | [Myaamori](https://github.com/TypesettingTools/Myaamori-Aegisub-Scripts) · [feed](https://raw.githubusercontent.com/TypesettingTools/Myaamori-Aegisub-Scripts/master/DependencyControl.json) |
| **dkjson** | `l0.dkjson` | [DependencyControl](https://github.com/TypesettingTools/DependencyControl) · [feed](https://raw.githubusercontent.com/TypesettingTools/DependencyControl/v0.9.1/DependencyControl.json) |
| **DataWrapper** | `a-mo.DataWrapper` | [Aegisub-Motion](https://github.com/TypesettingTools/Aegisub-Motion) · [feed](https://raw.githubusercontent.com/TypesettingTools/Aegisub-Motion/DepCtrl/DependencyControl.json) |
| **polyclipping** | `zpolyclipping.polyclipping` | [zeref](https://github.com/TypesettingTools/zeref-Aegisub-Scripts) · [feed](https://raw.githubusercontent.com/TypesettingTools/zeref-Aegisub-Scripts/main/DependencyControl.json) |
| **zimg** | `zimg.main` | [zeref](https://github.com/TypesettingTools/zeref-Aegisub-Scripts) · [feed](https://raw.githubusercontent.com/TypesettingTools/zeref-Aegisub-Scripts/main/DependencyControl.json) |
| **Transform** | `a-mo.Transform` | [Aegisub-Motion](https://github.com/TypesettingTools/Aegisub-Motion) · [feed](https://raw.githubusercontent.com/TypesettingTools/Aegisub-Motion/DepCtrl/DependencyControl.json) |
| **petzkuLib** | `petzku.util` | [petzku](https://github.com/petzku/Aegisub-Scripts) · [feed](https://raw.githubusercontent.com/petzku/Aegisub-Scripts/refs/heads/master/DependencyControl.json) |
| **DataHandler** | `a-mo.DataHandler` | [Aegisub-Motion](https://github.com/TypesettingTools/Aegisub-Motion) · [feed](https://raw.githubusercontent.com/TypesettingTools/Aegisub-Motion/DepCtrl/DependencyControl.json) |
| **ShakeShapeHandler** | `a-mo.ShakeShapeHandler` | [Aegisub-Motion](https://github.com/TypesettingTools/Aegisub-Motion) · [feed](https://raw.githubusercontent.com/TypesettingTools/Aegisub-Motion/DepCtrl/DependencyControl.json) |
| **requireffi** | `requireffi.requireffi` | [ffi-experiments](https://github.com/TypesettingTools/ffi-experiments) · [feed](https://raw.githubusercontent.com/TypesettingTools/ffi-experiments/master/DependencyControl.json) |

Por ejemplo, `l0.Functional` se busca como **(Almost) Functional Suite** y `myaa.ASSParser` como **ASS Parser**. **ArchMath** corresponde a `arch.Math`; no es el módulo **Math** de Aegisub-Motion.

Si falta un catálogo, su enlace **feed** se añade desde **Manage Feeds**. Se revisan los avisos de confianza y se actualiza la lista. Un módulo ya instalado puede no aparecer en el selector de instalación: se comprueba en las opciones de actualización de DependencyControl. Las dependencias que requieran esas bibliotecas se resuelven desde sus propios feeds; no es necesario instalar la macro Aegisub-Motion para obtener **LineCollection**, por ejemplo.

La tabla también incluye dependencias indirectas: **petzkuLib** se instala con **aka.command**; **polyclipping**, **zimg** y **requireffi**, con **ZF main**; **Transform**, con **Line**. **DataWrapper** solo se necesita para el tracking de AutoBlur y añade **DataHandler** y **ShakeShapeHandler**. **SubInspector** forma parte de las dependencias de **ASSFoundation**, aunque no todas sus funciones lo utilicen.

<a id="instalacion-manual"></a>

### 4. Copiar la carpeta de Automation

El [repositorio](https://github.com/Kiterowx/Kite-Aegisub-Scripts) contiene una sola estructura de instalación:

```text
automation/
├── autoload/           22 scripts públicos (.lua y .moon)
└── include/
    └── kite/          12 módulos compartidos
```

Se copia la carpeta `automation` sobre `%APPDATA%\Aegisub\automation`, fusionando el contenido. También se pueden copiar sus dos carpetas por separado:

| Origen en el repositorio | Destino en Aegisub |
| --- | --- |
| `automation/autoload/` | `%APPDATA%\Aegisub\automation\autoload\` |
| `automation/include/kite/` | `%APPDATA%\Aegisub\automation\include\kite\` |

Para una instalación parcial, se dejan en la copia de `autoload` solo los scripts que se vayan a usar y se conserva completa la carpeta `include/kite`. Los archivos `.moon` se copian tal cual. Las bibliotecas de `include` no van dentro de `autoload`.

Al actualizar, se reemplazan scripts y módulos Kite juntos. Se retiran las copias antiguas de esas mismas macros para evitar registros duplicados y se reinicia Aegisub o se vuelve a escanear Automation. Las demás bibliotecas que ya haya en `include` se conservan.

El feed de Kite sirve para instalar y actualizar las macros y sus módulos desde DependencyControl:

```text
https://raw.githubusercontent.com/Kiterowx/Kite-Aegisub-Scripts/main/DependencyControl.json
```

### 5. Programas externos según la herramienta

Estos programas se instalan fuera de DependencyControl. Solo se necesitan para las funciones indicadas.

| Programa | Uso |
| --- | --- |
| [Python](https://www.python.org/downloads/) de 64 bits, 3.10 o posterior, con pip | Backends de AutoMask y PNG2ASS. |
| [Git](https://git-scm.com/downloads), disponible en `PATH` | Instalar o actualizar esos backends desde GitHub. |
| [FFmpeg y FFprobe](https://ffmpeg.org/download.html) | AutoMask, Wave2json, Scream Detector de Chrono y exportaciones de Moka Motion, Snapshoter y Social Clip. FFprobe permite consultar pistas y metadatos. Para renderizar ASS y exportar H.264 se necesita una compilación con libass y libx264. |
| SCXvid, ejecutable de consola | **Chrono Suite/Extract KF**, junto con FFmpeg. Se indican ambas rutas en **Chrono Suite/Config → SCXvid**. |
| x264, ejecutable de consola | Alternativa opcional en **Moka Motion/Create Video Clip**. |

FFmpeg se añade a `PATH` o se selecciona en la configuración del script. Tras cambiar `PATH`, se reinicia Aegisub. En Windows se mantiene PowerShell disponible para ejecutar procesos externos. Wave2json no necesita Python; PNG2ASS no necesita FFmpeg para convertir imágenes.

### Backends de Python

Para AutoMask o PNG2ASS:

1. En **AutoMask/Backend/Configure** o **PNG2ASS/Backend/Configure**, seleccionar el intérprete de Python.
2. Ejecutar **Backend/Install or Update** y después **Backend/Check**.
3. Para EfficientSAM y LaMa, usar también **AutoMask/Backend/Install Models**. La reconstrucción de degradados funciona sin esos modelos.

El instalador incorpora OpenCV y las demás bibliotecas de Python. AutoMask instala también PNG2ASS; FFmpeg y SCXvid se instalan aparte. Desde una terminal se pueden usar estos comandos, solo para el backend necesario:

```text
python -m pip install --upgrade "git+https://github.com/Kiterowx/kite-png2ass.git"
python -m pip install --upgrade "git+https://github.com/Kiterowx/kite-automask.git"
```

El Python usado en la terminal debe ser el mismo seleccionado en Aegisub. Los detalles están en la [guía de dependencias](https://github.com/Kiterowx/Kite-Aegisub-Scripts/blob/main/docs/es/Dependencies.md).

## Consultar dependencias en el código

Los `.lua` y `.moon` se pueden abrir con un editor de texto. Cerca del inicio suele estar el bloque `DependencyControl`, con los nombres de módulo y sus versiones mínimas. También se pueden buscar `require`, `requireModules` e `include`. Por ejemplo, `a-mo.LineCollection` se instala como **LineCollection**, aunque el identificador y el nombre del archivo sean distintos.

En [DependencyControl.json](https://github.com/Kiterowx/Kite-Aegisub-Scripts/blob/main/DependencyControl.json), cada script declara `requiredModules`. Cuando aparece un módulo `kite.*`, se sigue su entrada en `modules` para consultar sus dependencias. Las bibliotecas de terceros también pueden requerir otros módulos. Una carga dentro de `pcall` puede corresponder a una función opcional; se contrasta con la guía del script antes de instalarla. No hace falta editar esos bloques para instalar una dependencia.

## Problemas de instalación

| Síntoma | Qué revisar |
| --- | --- |
| DependencyControl no aparece | Usar el ZIP de la versión, comprobar la ruta de usuario y los errores de carga en Automation. Evitar carpetas anidadas de más y copias antiguas del Toolbox en otra ruta de autoload. |
| **Bad DependencyControl record** | Actualizar al paquete 0.9.1 y volver a cargar. Si persiste, conservar el mensaje completo: hay otras causas posibles aparte de la corregida en esa versión. |
| `module '…' not found` o una macro no aparece | Buscar el identificador en la tabla, instalar el módulo correspondiente y revisar `include/kite`. Para `Yutils` o bibliotecas incluidas con Aegisub, revisar su instalación por separado. |
| Un módulo no sale en **Modules:** | Comprobar si ya está instalado, si su feed está añadido y habilitado, y si hay un aviso de confianza o un fallo de red. Revisar también que se esté usando **Modules:** y no **Automation Scripts:**. |
| Error HTTP, TLS o al descargar | Revisar conexión, proxy, antivirus y acceso al feed indicado por el error. El registro de DependencyControl está en la carpeta `log` del perfil de Aegisub. |
| Error de DLL, FFI o carga de una biblioteca nativa | Comprobar la compatibilidad del módulo con la versión y arquitectura de Aegisub. Reinstalar el paquete completo adecuado; cambiar de nombre una DLL no resuelve esa incompatibilidad. |
| Función inexistente en `kite.UI` u otro módulo Kite | Actualizar también los 12 módulos de `include/kite`; copiar solo la macro puede mezclar versiones incompatibles. |
| Entradas duplicadas en Automation | Buscar copias de la misma macro en las rutas de autoload configuradas. Conservar una sola copia activa. |
| El backend funciona en la terminal, pero falla en Aegisub | Comparar la ruta del intérprete, ejecutar **Backend/Check** y comprobar que pip instaló en ese mismo Python. |
| No se encuentra FFmpeg, FFprobe o SCXvid | Revisar el ejecutable configurado o `PATH` y reiniciar Aegisub tras cambiarlo. No se instalan con los módulos Lua. |

## Inicio, memoria y caché

Cada macro de `autoload` se carga al iniciar o volver a escanear Automation. Aegisub crea un entorno Lua por script, de modo que las bibliotecas usadas por varias macros pueden cargarse en varios entornos. El tiempo y la memoria dependen del conjunto instalado y del equipo; no hay un coste fijo por archivo.

Para reducir la carga, se mantienen en `autoload` solo las macros necesarias. Las demás pueden guardarse fuera de todas las rutas de autoload configuradas. Se conservan los módulos que necesiten las macros activas: estar en `include` no los convierte en macros que se ejecuten por sí solas.

DependencyControl guarda los catálogos descargados en `%APPDATA%\Aegisub\cache\l0.DependencyControl\feeds` con la configuración predeterminada. Esa caché evita repetir descargas; borrarla en cada inicio puede provocar más trabajo de red. La primera consulta de feeds, una actualización o una conexión lenta pueden añadir espera. Esta caché es distinta de la de audio/vídeo de Aegisub y de los modelos descargados por AutoMask.

La política de actualización se guarda en `%APPDATA%\Aegisub\config\l0.DependencyControl.json`. En `updates.mode`, `auto-update` permite comprobaciones automáticas; `dependency-resolution` instala lo requerido sin las comprobaciones periódicas; `user-requested` limita la actividad a las acciones solicitadas en el Toolbox. Este último modo exige instalar manualmente las dependencias que falten. `off` también impide instalaciones. Los valores y sus efectos se describen en la [documentación de DependencyControl](https://github.com/TypesettingTools/DependencyControl/blob/v0.9.1/README.md#configuration).

## Atajos y preferencias

Las combinaciones se asignan desde las preferencias de teclado de Aegisub. Cada macro registra sus acciones bajo `: Kite Hotkeys :`; [Hotkeys](lite/hotkeys.md) añade migración, favoritos y acceso a preferencias compartidas.

Las preferencias compartidas se guardan en `?user/config/kite.settings.json`. Las bibliotecas de carteles, como la de Allure, tienen sus propios archivos.
