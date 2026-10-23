# Filamentos 3D — v1.3 Beta

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

El ZIP incluye firebase-config.js vacío. Debes completar sus valores y configurar Firebase siguiendo CONFIGURAR_FIREBASE.md. Sin esa configuración, la aplicación funciona localmente, pero no puede iniciar sesión ni sincronizar. No vincules una cuenta de facturación si el proyecto debe permanecer en el plan gratuito Spark.

## Actualizar desde v1.2

1. Guarda antes una copia JSON desde la v1.2, como protección adicional.
2. Descomprime el ZIP y configura Firebase.
3. Sustituye los archivos de la raíz publicada en GitHub Pages por los archivos del ZIP; conserva la base de datos de Firebase y no borres los datos del navegador.
4. Abre la misma URL con Internet. La v1.3 mantiene IndexedDB y el service worker cambia a una caché nueva.
5. Prueba primero con datos de prueba. Al conectar por primera vez ofrece conservar/subir o descargar los datos existentes; revisa la selección antes de aceptar.

## Instalación y seguridad

- Android: abre el enlace con Chrome o Samsung Internet y elige Instalar/Añadir a pantalla de inicio.
- iPhone: abre el enlace con Safari y elige Compartir → Añadir a pantalla de inicio.
- Abre una vez con Internet para guardar los recursos offline. El inicio de sesión y la sincronización necesitan Internet.
- No publiques respaldos JSON ni claves privadas en GitHub. El identificador de cliente OAuth y la configuración web Firebase son públicos; las reglas de base de datos protegen los datos por UID.
- El plan Spark tiene cuotas. Si se exceden, Firebase puede detener el producto hasta el siguiente ciclo mensual. Consulta CONFIGURAR_FIREBASE.md.

## Estado de verificación

Código, configuración, reglas, service worker y rutas de almacenamiento revisados. El flujo real de Google/Firebase requiere completar la configuración del propietario y probarse con dos cuentas; no se puede validar sin un proyecto Firebase configurado. Sigue siendo Beta hasta completar pruebas en Chrome/Samsung Internet y Safari/iPhone.
