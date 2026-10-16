# Filamentos 3D — v1.2 Beta

PWA personal para iPhone, Android, Windows y Mac. Mantiene todos los datos en el dispositivo mediante IndexedDB y puede funcionar sin conexión después de abrirse una vez con Internet. No contiene datos de ejemplo. Si se borran los datos del navegador, también puede borrarse el inventario: guarda copias JSON con regularidad.

## Cambios de v1.2 Beta

- Consolida registros que representan el mismo producto en una sola tarjeta, conservando los datos de compra y consumo de cada bobina. Diferencias de color, material, acabado o temperaturas mantienen referencias distintas.
- La cuadrícula muestra una tarjeta por producto y el número total de bobinas en el centro. En la lista, **＋** permite añadir una o varias bobinas y **−** permite elegir cuál retirar.
- Catálogo de marcas y materiales habituales en Europa, sugerencias de nombres comerciales y elementos personalizados. Gestionar sugerencias no borra filamentos existentes.
- Plantillas completas o sin color, creadas desde un producto o manualmente; permiten aplicar, editar, duplicar y borrar.
- Selector de color sincronizado con controles de tono, saturación y luminosidad, código hexadecimal, colores sugeridos y favoritos.
- Fotografías tomadas con cámara o seleccionadas desde el dispositivo. Se comprimen localmente; se incluyen en el respaldo JSON.
- Proveedores editables por compra, con enlaces y notas.
- Exportación visual de inventario para imprimir o guardar como PDF desde el diálogo de impresión del sistema.
- Importación compatible con respaldos JSON v1.1 y migración automática de datos locales. No elimina datos guardados al actualizar los archivos.

## Actualizar el sitio existente en GitHub Pages

1. Antes de actualizar, abre la aplicación v1.1 en el mismo dispositivo y exporta una copia JSON como precaución.
2. Descarga y descomprime el ZIP v1.2 Beta.
3. En el repositorio existente `Rob-Lopez/Inventario-de-Filamentos-Bj-rn`, reemplaza los archivos publicados por el contenido de este ZIP. Sube `index.html`, `app.js`, `styles.css`, `sw.js`, el manifiesto, iconos y la carpeta `assets` directamente a la raíz. No subas solo el ZIP ni una carpeta contenedora.
4. Confirma los cambios en la rama `main`. GitHub Pages seguirá publicando desde `main` y `/(root)`.
5. En cada teléfono, abre el mismo enlace del sitio con Internet y espera a que cargue v1.2. Si sigue apareciendo v1.1, cierra completamente la PWA y vuelve a abrirla. El service worker usa una caché nueva para descargar la actualización.
6. Revisa inventario, cantidades y fotografías. No borres los datos del navegador ni desinstales la aplicación antes de comprobarlos.

**La actualización de archivos no borra IndexedDB.** La aplicación consolida duplicados equivalentes al iniciar: une sus bobinas individuales sin perder fechas, pesos, precios, proveedores ni consumos. Mantiene los datos separados en cada navegador/dispositivo.

## Instalación

- **Android:** abre el enlace con Chrome o Samsung Internet y usa el menú del navegador → **Instalar aplicación** o **Añadir a pantalla de inicio**.
- **iPhone:** abre el enlace en Safari → **Compartir** → **Añadir a pantalla de inicio**.
- Para descargar los archivos offline, abre la aplicación con Internet al menos una vez antes de usar el modo avión.

## PDF y respaldos

**Exportar inventario PDF** abre el diálogo de impresión del navegador. Elige **Guardar como PDF** (Android/Windows/Chrome) o la opción PDF de Compartir/Imprimir disponible en Safari. El informe se genera localmente, también sin conexión, y muestra resumen, referencias agrupadas por marca, fotos o bobinas ilustradas y detalle de cada bobina.

El respaldo **JSON** es el formato que conserva los datos editables, incluidas fotos, plantillas, proveedores y catálogos. Debido a las fotografías puede ocupar más espacio; la aplicación reduce las imágenes antes de guardarlas. Guarda el JSON fuera del dispositivo (por ejemplo, en Drive) y no lo subas al repositorio público.

## Protección de datos y límites

- El inventario no se sincroniza automáticamente entre dispositivos. Cada teléfono conserva su propia base local.
- Borrar los datos del navegador puede borrar también el inventario. Exporta copias JSON con regularidad y antes de cambiar de teléfono.
- No compartas públicamente el respaldo JSON: contiene fotos y datos personales del inventario.
- La lectura OCR permanece local y depende del idioma y la calidad de la etiqueta; revisa los campos reconocidos.
- La exportación PDF utiliza la impresión integrada en el sistema. En iPhone, el destino PDF se elige desde la hoja de impresión/compartir de Safari.

## Comprobaciones de esta entrega

Se validan sintaxis JS, manifest, recursos offline, migración y agrupación, cálculos de peso/precio, importación JSON anterior, controles de rollo, selector de color y generación de HTML de impresión. Esta versión sigue siendo Beta hasta que se pruebe en Samsung Internet/Chrome y Safari de iPhone.

## Archivos

`index.html`, `app.js`, `styles.css`, `manifest.webmanifest`, `sw.js`, iconos y `assets/` (Tesseract.js, modelo OCR local y licencias).
