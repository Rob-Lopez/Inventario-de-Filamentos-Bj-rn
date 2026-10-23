# Configuración de la nube — Filamentos 3D v1.3 Beta

Esta versión usa Google para iniciar sesión y Firebase Realtime Database para sincronizar. No usa Google Drive API. Cada cuenta solo puede acceder a /users/<su-UID>; las reglas de seguridad están en firebase-database.rules.json.

## A. Crear el proyecto gratuito

1. Entra en Firebase Console con tu cuenta Google y crea un proyecto llamado, por ejemplo, inventario-filamentos.
2. No vincules una cuenta de facturación. Selecciona el plan gratuito Spark.
3. En el proyecto, añade una aplicación web y llámala Filamentos 3D. No hace falta activar Firebase Hosting.
4. En Authentication → Sign-in method, activa Google y elige un correo de asistencia.
5. En Authentication → Settings → Authorized domains, añade el dominio publicado de GitHub Pages, por ejemplo rob-lopez.github.io. Añade solo el dominio, sin https:// ni la ruta del repositorio.
6. En Realtime Database, crea la base de datos y copia su URL. Publica las reglas incluidas en firebase-database.rules.json.

## B. Obtener los valores de configuración

1. Abre Project settings → General → Your apps → SDK setup and configuration y copia apiKey, authDomain, projectId y appId de la aplicación web.
2. En Google Cloud Console → APIs & Services → Credentials, abre el cliente OAuth de tipo Web application que usa Google Sign-In. Copia su Client ID.
3. En ese cliente OAuth, añade como Authorized JavaScript origins el origen de GitHub Pages, por ejemplo https://rob-lopez.github.io. No pongas la ruta /Inventario-de-Filamentos-Bj-rn.
4. Edita firebase-config.js y pega los valores correspondientes. databaseURL es la URL copiada al crear Realtime Database.

El apiKey, el appId y el identificador OAuth de cliente web son identificadores públicos diseñados para estar en el código web. No pongas contraseñas, claves de cuenta de servicio, claves privadas ni archivos JSON de service account en el repositorio.

## C. Permitir el acceso de Björn

1. En Google Auth Platform → Audience, configura el tipo externo.
2. Mientras la aplicación esté en estado Testing, añade en Test users las direcciones Google de Roberto y Björn.
3. La primera vez, cada uno abre la aplicación, toca Conectar con Google, elige su cuenta y acepta iniciar sesión.
4. No se concede acceso a Drive. El nombre y correo Google identifican la cuenta; el inventario se guarda en Firebase, separado por UID.

Para uso personal con pocas personas conocidas, se puede empezar en modo de pruebas. Google puede mostrar una pantalla de advertencia y limitar quién inicia sesión. La publicación o verificación puede requerirse si se quiere quitar esa restricción o abrir el acceso a otros usuarios; no es necesaria para probar con los usuarios añadidos como testers. Revisa el estado y requisitos vigentes en Google Auth Platform antes de ampliarlo.

## D. Publicar la v1.3 Beta

1. Configura primero firebase-config.js y verifica en Firebase que Google Authentication y Realtime Database estén activos.
2. Descomprime el ZIP y reemplaza en la raíz de GitHub Pages los archivos de la versión anterior por el contenido del ZIP. No subas una carpeta contenedora.
3. Conserva la base de datos local del navegador. No borres almacenamiento, cookies ni datos del sitio.
4. Abre la URL con Internet. La v1.3 carga primero el perfil local; después comprueba una versión pequeña en Firebase. Si coincide el identificador, no descarga el inventario ni las fotos.
5. Para publicar cambios, pulsa Guardar en la nube y espera el mensaje de confirmación. Los cambios locales nunca se suben automáticamente.

## E. Límites y funcionamiento

- En el plan Spark, Realtime Database incluye 1 GB almacenado, 10 GB de descargas al mes y hasta 100 conexiones simultáneas. Al superar la cuota gratuita, el producto puede quedar desactivado para el resto del mes; no vincules facturación si el proyecto debe permanecer sin coste.
- Las fotos están comprimidas por la aplicación y se incluyen en el JSON sincronizado. Las copias históricas consumen espacio; se conservan cinco por cuenta por defecto, ajustable entre una y veinte. Solo se crea una copia al publicar cambios.
- IndexedDB conserva el inventario y los cambios offline. La base de datos web de Firebase no sustituye esa cola local si se cierra la app sin conexión.
- La sincronización al abrir consulta primero la revisión. Descarga el contenido completo solo si hay una versión nueva y no existen cambios locales pendientes.
- Si dos dispositivos cambian datos distintos, se combinan. Si ambos cambiaron el mismo dato, la app pide elegir qué versión conservar en esos campos. El resto de cambios se mantiene.
- Con la cuenta desconectada, el perfil local permanece en el dispositivo. Cambiar de cuenta abre el perfil separado de esa cuenta.
- Las copias JSON manuales siguen siendo el respaldo independiente recomendado.
- La sesión de Google puede requerir reconexión. El inicio de sesión necesita Internet; el inventario local sigue disponible sin conexión.

## Pruebas antes de usar con el inventario principal

Usa primero dos cuentas y datos de prueba: conectar cada cuenta, cambiar de cuenta en el mismo navegador, abrir la misma cuenta en dos dispositivos, guardar desde un dispositivo, sincronizar desde el otro, editar el mismo campo sin publicar para verificar el diálogo de conflicto, activar o desactivar historial, restaurar una versión y probar modo avión. Mantén el JSON de la v1.2 hasta completar la migración.
