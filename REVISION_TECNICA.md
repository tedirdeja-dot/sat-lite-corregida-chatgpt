# Revisión técnica de SatelliteWallpaper 4.1.6

## Cambios realizados
- Evitado un posible `NullPointerException` al leer el registro de intentos de `SharedPreferences`: se usa `orEmpty()` en lugar de `!!`.
- Canal de notificación configurado con importancia LOW para mejorar su visibilidad como servicio en primer plano. Nota: Android conserva la importancia del canal existente; para una instalación previa puede requerirse cambiar la importancia desde ajustes o crear un canal nuevo.
- GitHub Actions compilando con Gradle 8.10.2, JDK 17 y Android SDK 35, sin depender de un `gradlew` ausente. Ejecuta compilación, pruebas unitarias y lint, y publica el APK.

## Riesgos pendientes de pruebas en dispositivo
- Android puede restringir servicios de primer plano y capturas WebView en segundo plano, dependiendo de versión y fabricante.
- El filtro de imágenes rechaza pantallas casi blancas, pero no puede garantizar que todas las imágenes aceptadas correspondan a nubes reales.
- El watchdog de cinco minutos libera el estado de la descarga; deben probarse capturas bloqueadas y cambios de vista simultáneos.
- La clave de firma incluida en el proyecto tiene contraseña pública; no sirve para distribuir una versión release con seguridad de firma robusta. No se ha cambiado para preservar la posibilidad de actualizar instalaciones previas.

## Alcance
Revisión estática. No se ha podido ejecutar Android Gradle Plugin ni probar la APK en emulador o dispositivo en este entorno. La compilación definitiva se comprueba en GitHub Actions.
