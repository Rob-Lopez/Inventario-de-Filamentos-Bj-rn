# Filamentos 3D — B 3.0 Beta

PWA personal para iPhone, iPad, Mac, Android y Windows. Conserva el inventario IndexedDB, los perfiles separados por cuenta Google, la sincronización manual con Firebase, la interfaz ES/DE/EN, las fotografías, el OCR, los catálogos, las plantillas y la exportación PDF.

## Sincronización y diagnóstico

En Safari, las lecturas REST de Firebase reintentan hasta tres veces si falla fetch. Si persiste un fallo de red, se intenta la misma lectura mediante XMLHttpRequest. Esta alternativa se usa solo en Safari; Android y Windows conservan su ruta habitual. Si falla la lectura del listado de copias antiguas, el error se registra y la publicación del inventario continúa.

## Novedades B 3.0

- Actualización manual desde la nube, con opciones seguras cuando hay cambios locales pendientes.
- Modo Solo visualización por defecto y modo Master activado expresamente en el dispositivo autorizado; el ajuste se guarda por dispositivo. La protección local bloquea las acciones de edición y publicación en el dispositivo marcado como Solo visualización; el selector no impone un bloqueo global entre dispositivos.
- Vista simplificada con lista de filamentos, filtros y accesos para volver a la vista completa o actualizar desde Firebase.
- Se pueden guardar fichas de filamento vacías. Se asigna fecha de creación automáticamente; al añadir un rollo, su fecha de compra empieza en hoy y se puede cambiar.
- La ficha vacía puede editarse luego y permanece separada de otras fichas vacías.

## Historial de errores

El botón ⚠ de la barra superior abre el historial local. Registra errores JavaScript, promesas no controladas y fallos HTTP/de red de Google, Firebase y recursos de la aplicación. Cada registro incluye fecha, método y servidor cuando aplica, estado `online`, versión y navegador. Se conservan hasta 300 eventos. El historial no se sincroniza ni se publica en Firebase; se puede descargar como JSON o borrar desde la ventana.

Las lecturas GET de Firebase reintentan hasta tres veces ante fallos de red transitorios y respuestas HTTP temporales. Las escrituras no se repiten automáticamente. Un error de lectura no sustituye los datos locales.

## Publicar en GitHub Pages

1. Descomprime el ZIP y copia el contenido en la raíz del repositorio de GitHub Pages.
2. Conserva `firebase-config.js` de la base Alfa; no necesita cambios para esta actualización.
3. Publica y abre la aplicación con Internet. La caché nueva del service worker actualiza los recursos.
4. En iPhone, iPad y Mac, abre **Historial de errores** después de reproducir el fallo y descarga el registro JSON para revisar los eventos.

El modo del dispositivo y la vista simplificada se guardan localmente; no se sincronizan con las otras cuentas o dispositivos. La app carga el inventario local antes de iniciar la comprobación de Firebase. El registro de errores usa una base IndexedDB separada.
