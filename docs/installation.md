# Instalación

Instala [DependencyControl](https://github.com/TypesettingTools/DependencyControl#installation) y conserva los archivos de Automation incluidos en Aegisub. AutoBlur utiliza las funciones de vídeo de [Aegisub de arch1t3cht](https://github.com/arch1t3cht/Aegisub).

## DependencyControl

Añade el catálogo de scripts y módulos:

```text
https://raw.githubusercontent.com/Kiterowx/Kite-Aegisub-Scripts/main/DependencyControl.json
```

Después de instalar o actualizar, reinicia Aegisub o usa **Automation → Rescan Autoload Dir**.

## Instalación manual

Descarga el [repositorio de scripts](https://github.com/Kiterowx/Kite-Aegisub-Scripts) y copia:

| Origen | Destino en Windows |
| --- | --- |
| Los scripts que necesites de `Macros/` y `Macros-Lite/` | `%APPDATA%\Aegisub\automation\autoload\` |
| La carpeta completa `Modules/kite/` | `%APPDATA%\Aegisub\automation\include\kite\` |

Los **12 módulos** se copian juntos, conservando la carpeta `kite`. Actualiza scripts y módulos a la vez y retira copias duplicadas. En una instalación portátil utiliza las rutas de Automation configuradas en ella.

Instala también las bibliotecas externas que requiera cada macro:

| Biblioteca | Módulos |
| --- | --- |
| [ASSFoundation](https://github.com/TypesettingTools/ASSFoundation) | `l0.ASSFoundation` |
| [Functional](https://github.com/TypesettingTools/Functional) | `l0.Functional` |
| [Aegisub-Motion](https://github.com/TypesettingTools/Aegisub-Motion) | `a-mo.*` |
| [Bibliotecas de arch](https://github.com/TypesettingTools/arch1t3cht-Aegisub-Scripts) | `arch.Math`, `arch.Perspective`, `arch.Util` |
| [ZF](https://github.com/TypesettingTools/zeref-Aegisub-Scripts) | `ZF.main` |
| [Akatsumekusa](https://github.com/Akatmks/Akatsumekusa-Aegisub-Scripts) | `aka.command`, para procesos externos |
| [Myaamori](https://github.com/TypesettingTools/Myaamori-Aegisub-Scripts) | `myaa.ASSParser` |
| [SubInspector](https://github.com/TypesettingTools/SubInspector) | `SubInspector.Inspector` |
| [Yutils](https://github.com/Youka/Yutils) | `Yutils.lua` |

Instala `l0.dkjson` mediante DependencyControl. Las fuentes de los estilos deben estar disponibles para Aegisub y para el renderizador que exporte el vídeo.

## Backends de Python

**AutoMask y PNG2ASS** necesitan Python de 64 bits, versión 3.10 o posterior, con pip, y Git en `PATH` para instalar desde sus repositorios.

1. Abre **AutoMask/Backend/Configure** o **PNG2ASS/Backend/Configure** y selecciona Python.
2. Ejecuta **Backend/Install or Update**.
3. Comprueba **Backend/Check**.

El instalador incorpora las bibliotecas de Python necesarias. AutoMask instala también el backend de PNG2ASS. Para SAM y LaMa, ejecuta **AutoMask/Backend/Install Models**; la reconstrucción de degradados funciona sin esos modelos.

## FFmpeg y SCXvid

Instala [FFmpeg y FFprobe](https://ffmpeg.org/download.html) y añádelos a `PATH` o configura su ejecutable en el script. Reinicia Aegisub después de cambiar `PATH`.

| Uso | Requisito |
| --- | --- |
| AutoMask, Wave2json y Scream Detector | FFmpeg. |
| Moka Motion, Snapshoter y Social Clip | FFmpeg; libass para renderizar subtítulos y libx264 para exportar H.264. |
| Social Clip | FFprobe para consultar pistas de audio. |
| Chrono Suite/Extract KF | FFmpeg y el ejecutable de consola SCXvid, configurados en Config. |
| Moka Motion/Create Video Clip | x264 es una alternativa opcional. |

Wave2json utiliza FFmpeg sin necesitar Python. PNG2ASS convierte imágenes sin requerir FFmpeg.

## Atajos y preferencias

Asigna combinaciones desde las preferencias de teclado de Aegisub. Cada macro registra sus propias acciones bajo `: Kite Hotkeys :`; el editor [Hotkeys](lite/hotkeys.md) añade migración, favoritos y acceso a preferencias compartidas.

Las preferencias compartidas se guardan en `?user/config/kite.settings.json`. Las bibliotecas de carteles, como la de Allure, tienen sus propios archivos.

## Si una macro no aparece

Vuelve a escanear Automation y revisa el registro de carga. Comprueba que los módulos estén en `include/kite`, que no haya copias duplicadas y que estén instaladas las bibliotecas declaradas por la macro. Para pedir ayuda, indica la macro, su versión, la versión de Aegisub y el error completo.
