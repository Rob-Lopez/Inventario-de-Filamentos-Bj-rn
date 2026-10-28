# Configuración de Firebase — Filamentos 3D v3.1 Beta

Esta versión usa Google para iniciar sesión y Firebase Realtime Database para sincronizar mediante sus APIs REST; no carga el SDK JavaScript de Firebase. No usa Google Drive API. Cada cuenta solo puede acceder a /users/<su-UID>; las reglas de seguridad están en firebase-database.rules.json.

## A. Crear el proyecto gratuito

1. Entra en Firebase Console con tu cuenta Google y crea un proyecto llamado, por ejemplo, inventario-filamentos.
2. No vincules una cuenta de facturación. Selecciona el plan gratuito Spark.
3. En el proyecto, añade una aplicación web y llámala Filamentos 3D. No hace falta activar Firebase Hosting.
4. En Authentication → Sign-in method, activa Google y elige un correo de asistencia.
5. En Authentication → Settings → Authorized domains, añade exactamente `rob-lopez.github.io`. Añade solo el dominio, sin `https://` ni la ruta del repositorio.
6. En Realtime Database, crea la base de datos y copia su URL. Publica las reglas incluidas en firebase-database.rules.json.

## B. Obtener los valores de configuración

1. Abre Project settings → General → Your apps → SDK setup and configuration y copia apiKey, authDomain, projectId y appId de la aplicación web.
2. En Google Cloud Console → APIs & Services → Credentials, abre o crea el cliente OAuth de tipo **Aplicación web** asociado a este proyecto y copia su Client ID. Este dato es independiente del bloque `firebaseConfig`: aunque `firebase-config.js` cargue con HTTP 200 y contenga `apiKey` y `databaseURL`, la nube no se activa sin este Client ID.
3. En ese cliente OAuth, añade como **Authorized JavaScript origin** exactamente `https://rob-lopez.github.io`. No añadas la ruta `/Inventario-de-Filamentos-Bj-rn`.
4. Edita `firebase-config.js` manteniendo esta estructura y pega los valores correspondientes. El Client ID se coloca en `googleClientId`; la URL de Realtime Database en `databaseURL`. La aplicación también reconoce el nombre estándar `firebaseConfig` y alias comunes de estas propiedades.

El apiKey, el appId y el identificador OAuth de cliente web son identificadores públicos diseñados para estar en el código web. No pongas contraseñas, claves de cuenta de servicio, claves privadas ni archivos JSON de service account en el repositorio.

## C. Permitir el acceso de Björn

1. En Google Auth Platform → Audience, configura el tipo externo.
2. Mientras la aplicación esté en estado Testing, añade en Test users las direcciones Google de Roberto y Björn.
3. La primera vez, cada uno abre la aplicación, toca Conectar con Google, elige su cuenta y acepta iniciar sesión.
4. No se concede acceso a Drive. El nombre y correo Google identifican la cuenta; el inventario se guarda en Firebase, separado por UID.

Para uso personal con pocas personas conocidas, se puede empezar en modo de pruebas. Google puede mostrar una pantalla de advertencia y limitar quién inicia sesión. La publicación o verificación puede requerirse si se quiere quitar esa restricción o abrir el acceso a otros usuarios; no es necesaria para probar con los usuarios añadidos como testers. Revisa el estado y requisitos vigentes en Google Auth Platform antes de ampliarlo.

## D. Publicar Filamentos 3D v3.1 Beta

1. Descomprime el ZIP y copia el contenido en la raíz del repositorio de GitHub Pages.
2. El `firebase-config.js` incluido se conserva desde la Alfa. Si el archivo que ya está publicado contiene valores más recientes, conserva el publicado y reemplaza los demás archivos.
3. No borres los datos del sitio en el navegador: el inventario existente sigue en IndexedDB. El registro de errores usa otra base local separada.
4. Publica la actualización y abre la aplicación con Internet. El service worker tiene una caché nueva y precarga `diagnostics.js` junto con los recursos actuales.
5. Para revisar un fallo en Apple, pulsa el botón ⚠ de la barra superior, reproduce la conexión y descarga el registro JSON desde **Historial de errores**.

## Diagnóstico en v3.1 Beta

Si Safari no puede consultar el listado de copias antiguas durante una publicación, la aplicación registra ese fallo y continúa con el guardado principal. La limpieza de copias se vuelve a intentar después.

El botón **Historial de errores** registra localmente eventos de red, Firebase y JavaScript. No se envían a Firebase. Puedes descargar un JSON desde el historial para compartirlo durante el diagnóstico. Los GET reintentan fallos temporales; las publicaciones no se reintentan automáticamente.
