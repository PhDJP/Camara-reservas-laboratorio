# Capturador de cámara externo

Esta página debe servirse desde un origen HTTPS que no pertenezca a Apps Script. El servicio HTML de Apps Script bloquea `navigator.mediaDevices.getUserMedia()` dentro de su iframe; por eso la aplicación abre esta página en otra ventana y recibe la foto mediante `postMessage`.

## Configuración

1. Aloja `index.html` en un dominio HTTPS accesible para las personas usuarias. No se necesita un servidor que guarde datos: la foto se mantiene en memoria y se envía a la aplicación solo después de que la persona elige «Usar esta foto».
2. Abre la aplicación publicada y obtén el valor exacto de `window.location.origin` desde la consola del navegador.
3. Sustituye `https://script.googleusercontent.com` en `ALLOWED_PARENT_ORIGINS` por ese origen exacto.
4. En las propiedades del proyecto de Apps Script, establece `CAMARA_URL` con la URL HTTPS completa de esta página.
5. Despliega la actualización de Apps Script y prueba la captura desde un teléfono y un computador con cámara.

La aplicación acepta mensajes solo desde el origen configurado de esta página, desde la ventana que ella misma abrió y con el identificador aleatorio de esa captura. No cambies esas verificaciones ni uses `postMessage` con el destino `*`.
