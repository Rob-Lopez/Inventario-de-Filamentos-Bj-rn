# Filamentos 3D — v1.3.1 Beta

PWA personal para iPhone, Android, Mac y Windows. Conserva las funciones de v1.2: inventario local IndexedDB; lista, cuadrícula y ficha; bobinas individuales; cantidades y precios; catálogos, plantillas, fotos comprimidas, OCR local, PDF y respaldo JSON.

## Sincronización

- Acceso con cuenta Google mediante Firebase Authentication. No accede a Google Drive.
- Cada cuenta tiene un inventario independiente en Firebase Realtime Database.
- El inventario local sigue en IndexedDB y funciona sin Internet.
- Al abrir, carga primero los datos locales y consulta únicamente la revisión remota. Si la revisión coincide, no descarga el inventario ni las fotos.
- Las modificaciones se guardan localmente. Solo se publican al pulsar «Guardar en la nube».
- Los cambios independientes se combinan; si dos dispositivos cambian el mismo dato, la app pide elegir qué versión conservar en esos campos.
- Historial automático de versiones al publicar, activado por defecto: conserva cinco copias, configurable entre una y veinte. Se puede desactivar. El historial usa el espacio gratuito compartido del proyecto.
- Cambiar de cuenta abre otro perfil local y otra ruta privada en la nube. No se mezclan los inventarios.

## Antes de publicar

La corrección acepta `window.FILAMENTS_FIREBASE_CONFIG`, `window.firebaseConfig`, `window.FIREBASE_CONFIG` y la variable estándar `const firebaseConfig`. También reconoce alias de propiedades. Requiere `apiKey`, `databaseURL` y el `googleClientId` del cliente OAuth web. Este último no suele venir en el objeto que Firebase muestra como configuración web. Si ya tienes un `firebase-config.js` válido, consérvalo al sustituir los demás archivos. Si falta una propiedad, la aplicación lo indica por nombre. La aplicación usa Firebase Authentication y Realtime Database mediante REST; no necesita descargar el SDK Firebase. No vincules una cuenta de facturación si el proyecto debe permanecer en el plan gratuito Spark.

## Actualizar desde v1.3 Beta

1. Conserva una copia JSON por seguridad.
2. Descomprime el ZIP. Conserva el `firebase-config.js` ya configurado; el del ZIP es una plantilla vacía.
3. Copia los demás archivos del ZIP a la raíz publicada en GitHub Pages. No borres los datos del navegador ni la base de datos Firebase.
4. Abre la URL con Internet y recarga. La v1.3.1 conserva IndexedDB y fuerza una caché nueva para JavaScript, HTML y configuración.
5. Comprueba la franja superior. Si falta un dato, indicará el nombre. Prueba primero con datos de prueba.

## Instalación y seguridad

- Android: abre el enlace con Chrome o Samsung Internet y elige Instalar/Añadir a pantalla de inicio.
- iPhone: abre el enlace con Safari y elige Compartir → Añadir a pantalla de inicio.
- Abre una vez con Internet para guardar los recursos offline. El inicio de sesión y la sincronización necesitan Internet.
- No publiques respaldos JSON ni claves privadas en GitHub. El identificador de cliente OAuth y la configuración web Firebase son públicos; las reglas de base de datos protegen los datos por UID.
- El plan Spark tiene cuotas. Si se exceden, Firebase puede detener el producto hasta el siguiente ciclo mensual. Consulta CONFIGURAR_FIREBASE.md.

## Estado de verificación

Código, configuración, reglas, service worker y rutas de almacenamiento revisados. El flujo real de Google/Firebase requiere completar la configuración del propietario y probarse con dos cuentas; no se puede validar sin un proyecto Firebase configurado. Sigue siendo Beta hasta completar pruebas en Chrome/Samsung Internet y Safari/iPhone.
