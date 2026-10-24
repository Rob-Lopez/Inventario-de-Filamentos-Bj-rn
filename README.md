# Filamentos 3D — v2.1 Beta

PWA personal para iPhone, iPad, Mac, Android y Windows. Conserva el inventario IndexedDB, los perfiles separados por cuenta Google, la sincronización manual con Firebase, la interfaz ES/DE/EN, las fotografías, el OCR, los catálogos, las plantillas y la exportación PDF.

## Sincronización y diagnóstico

Si Safari no puede consultar el listado de copias antiguas, la aplicación registra el error y continúa con la publicación del inventario. La limpieza se vuelve a intentar en una publicación posterior.

## Historial de errores

El botón ⚠ de la barra superior abre el historial local. Registra errores JavaScript, promesas no controladas y fallos HTTP/de red de Google, Firebase y recursos de la aplicación. Cada registro incluye fecha, método y servidor cuando aplica, estado `online`, versión y navegador. Se conservan hasta 300 eventos. El historial no se sincroniza ni se publica en Firebase; se puede descargar como JSON o borrar desde la ventana.

Las lecturas GET de Firebase reintentan hasta tres veces ante fallos de red transitorios y respuestas HTTP temporales. Las escrituras no se repiten automáticamente. Un error de lectura no sustituye los datos locales.

## Publicar en GitHub Pages

1. Descomprime el ZIP y copia el contenido en la raíz del repositorio de GitHub Pages.
2. Conserva `firebase-config.js` de la base Alfa; no necesita cambios para esta actualización.
3. Publica y abre la aplicación con Internet. La caché nueva del service worker actualiza los recursos.
4. En iPhone, iPad y Mac, abre **Historial de errores** después de reproducir el fallo y descarga el registro JSON para revisar los eventos.

La app carga el inventario local antes de iniciar la comprobación de Firebase. El registro de errores usa una base IndexedDB separada.
