# Inventario Filamentos 3D — v1.1 Beta

PWA personal para registrar bobinas, consumo, cantidades, precios y temperaturas. Los datos permanecen en el dispositivo, en IndexedDB. Incluye OCR local en inglés con Tesseract.js y copia de seguridad JSON.

## Publicar gratis en GitHub Pages

1. Crea una cuenta gratuita de GitHub si aún no tienes una.
2. Crea un repositorio público llamado `inventario-filamentos`.
3. Descomprime esta carpeta y sube **todo su contenido** a la raíz del repositorio. Conserva la carpeta `assets` y sus archivos.
4. En GitHub, abre **Settings → Pages**. En **Build and deployment**, selecciona **Deploy from a branch**, rama `main` y carpeta `/ (root)`, luego guarda.
5. Espera a que GitHub publique el sitio. La URL será similar a `https://TU-USUARIO.github.io/inventario-filamentos/`.
6. Abre la URL con conexión en línea una vez para que el navegador descargue la aplicación y los recursos OCR (unos veinte megabytes antes de la compresión de red). En la siguiente visita ya podrá abrir y trabajar sin conexión.

El repositorio será público con GitHub Free. Esto publica el código de la aplicación, pero no el inventario: cada dispositivo guarda sus propios datos localmente.

## Instalar

### iPhone

Abre el enlace en **Safari** → **Compartir** → **Añadir a pantalla de inicio** → activa **Abrir como app web** → **Añadir**.

### Android

Abre el enlace en Chrome → menú **⋮** → **Instalar aplicación** o **Añadir a pantalla de inicio**.

## Pruebas recomendadas

- Añade un filamento manualmente; prueba los dos modos de vista y filtros por marca, material, color y disponibilidad. En la lista, usa + para agregar un rollo repetido y − para quitar el último, con confirmación.
- Cambia el número de columnas y vuelve a cargar la aplicación para verificar que se guarda.
- Añade rollos con precios distintos; los botones rápidos copian el peso y precio del último rollo y puedes modificarlos en la ficha. Prueba los acabados visuales normal, metálico, brillante, mate, transparente y multicolor.
- Registra consumos, prueba rollos agotados y revisa cantidades y estadísticas.
- Exporta una copia JSON, impórtala después de confirmar el reemplazo y revisa los datos.
- Abre la PWA con conexión una vez; después activa modo avión y vuelve a abrirla. Comprueba navegación, datos y OCR.
- Verifica en Safari del iPhone la instalación, cámara/selector de fotos y funcionamiento sin conexión.

## Cambios de v1.1 Beta

- En la vista de lista, **＋** añade un rollo con peso y precio inicial copiados del último rollo de ese filamento. La fecha se pone en hoy; los datos se pueden corregir en la ficha.
- **−** quita el último rollo después de mostrar una confirmación; si queda uno solo, no permite dejar el filamento sin rollos.
- El número de rollos aparece en grande al centro de cada bobina.
- Acabados visuales: normal, metálico, brillante, mate, transparente y multicolor. Se puede dar un nombre propio a otro acabado y escoger el estilo visual más parecido.
- La vista previa cambia al ajustar color o acabado.

## Estado de verificación

Esta entrega se mantiene como **Beta** hasta probarse en los teléfonos de destino. Se comprobaron sintaxis JavaScript, manifest, archivos offline, cálculo de cantidades/precios y los seis gráficos de acabados. La compatibilidad final de instalación, uso sin conexión y OCR debe confirmarse en Samsung y Safari de iPhone.

## Datos y límites

- No hay cuenta ni sincronización. Cada dispositivo conserva un inventario independiente.
- Exporta copias JSON antes de cambiar de teléfono o borrar datos del navegador.
- El OCR corre localmente, con modelo inglés. Puede fallar en etiquetas pequeñas, brillantes, curvas o con texto en otros idiomas; revisa los datos reconocidos antes de guardarlos.
- Las bobinas ilustradas son generadas por la aplicación; no se guardan imágenes por filamento.
- El número de columnas se conserva en este dispositivo. Con quince columnas, los detalles de cada bobina quedan pequeños en una pantalla estrecha.
- Para publicar una actualización, sube la nueva versión de los archivos al mismo repositorio. El service worker cambia de caché por versión y reclama la aplicación nueva; cierra y vuelve a abrir la PWA si aún ves la versión anterior.

## Contenido

- `index.html`, `styles.css`, `app.js`: aplicación.
- `manifest.webmanifest`, `sw.js`, iconos: instalación y modo sin conexión.
- `assets/`: motor OCR, modelo de idioma y licencias de terceros.
