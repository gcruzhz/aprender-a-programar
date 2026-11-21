# CHANGELOG — Aprender a Programar

Historial de la app, en orden. Fechas en hora de Ciudad de México.

## 2026-11-21 — Plan aprobado

Gerardo pide una app tipo Duolingo para aprender a programar, en español. Se acuerda primero el plan (rutas y niveles) y luego la app. El plan aprobado:

- 13 rutas: Introducción a la programación, Python, JavaScript, TypeScript, Java, C#, Go, Rust, Kotlin, SQL, HTML/CSS, C++ con Qt y QML — Apps para KDE, y Herramientas.
- Niveles Básico, Intermedio, Avanzado y Experto por ruta, con 20 lecciones por nivel: 80 lecciones por ruta, 1,040 en total, cada una de unos 5 minutos.
- Cada lección: teoría a detalle (`detail`, 4 bloques), 5 ejercicios de los 4 tipos (elegir la respuesta, completar el código, terminal simulada, ordenar los pasos) y 1 tarea con revisión automática.
- Gamificación: XP por lección, racha diaria, 6 corazones por lección, ligas semanales (Bronce a Diamante), 13 logros y certificado de nivel por ruta completada.
- Laboratorio: guías paso a paso para instalar Python, Node.js, VS Code y Git en Windows, Linux, macOS y Android (Termux).
- La ruta C++ con Qt y QML se pidió con **80 lecciones** (20 por nivel), no con las 20 en total propuestas al inicio; incluye Kirigami y empaquetado al final. Total de la app: 13 rutas × 80 lecciones = 1,040 lecciones, 5,200 ejercicios, 1,040 tareas, 4 guías de Laboratorio.

## 2026-11-21 — App construida

Se construye la app como artefacto web fullstack de Muse (`aprender-a-programar`): 13 rutas, 4 niveles por ruta, 1,040 lecciones con `detail` de 4 bloques, 5,200 ejercicios, 1,040 tareas con revisión automática (JavaScript se ejecuta en el navegador; los demás lenguajes por salida esperada o palabras clave, sin prometer ejecución real) o subida de archivo, vista Mis tareas (pendiente / hecha en la app / enviada), Laboratorio con 4 guías (Windows 11 pasos, Linux 10, macOS 10, Android/Termux 9, con pasos de Qt/Qt Creator en Windows, Linux y macOS), pestaña de Práctica, 6 corazones, XP, racha, ligas semanales, 16 logros y certificados por ruta. Login con usuario y contraseña, sesión recordada, progreso por cuenta; la primera cuenta hereda el avance hecho antes del login. Sin botón de IA en la 1.0.

El contenido vive en `~/workspace/android/programar-app/www/data/*.js` (un archivo por ruta más `labs.js`), con el contrato completo en `SCHEMA.md`: IDs de lección estables (`<ruta>-b01`…`-e20`), código real y correcto en los ejemplos, todo en español.

## 2026-11-21 — APK 2.0 (con nube)

Primera versión con Firebase: la APK 2.0 (`versionCode` 3, `versionName` 2.0, paquete `mx.gerardo.programar`, `targetSdk` 36, 3,951,340 bytes, md5 `2dac98edcccdb44f1a1d18685b819d8b`, mismo keystore permanente, firma v2 verificada) incluye la config real del proyecto `aprender-programar` y el bundle de nube (`www/cloud/firebase.bundle.js` md5 `1a841655ff6ad59fbeb9fd06fe83b4bd`, sin cambios). El perfil dice "Versión 2.0 · Nube: tu avance se sincroniza" cuando hay config. La 1.0.1 (md5 `9c803058e59783e2e9907a9aa3301196`) quedó sustituida. **Auth por correo/contraseña aún NO está activado en la consola** (no se pudo activar por API: `CONFIGURATION_NOT_FOUND`): hasta que Gerardo lo active en Authentication → Método de acceso, el registro/login en la nube falla y la app trabaja en modo local. Los logros NO se unificaron en esta versión: la APK tiene 13 y la web 16, pero las listas no son un subconjunto (ids, nombres y condiciones distintos; la web calcula los logros desde estadísticas y la APK los otorga por eventos; los de tareas y laboratorio de la web no tienen equivalente en la APK — el Lab no registra "completado" y las tareas locales no tienen "aprobada"), así que la unificación queda para después. Verificación: `tests/check-data.cjs` 44,329 checks, 0 fallos; `tests/test-app.cjs` 48/48; `curriculum.ts` web regenerado desde `www/data/` sin diferencias (0 diferencias web vs APK).

## 2026-11-21 — APK 1.0.1 (parche)

Se corrige la tarea `javascript-e13` ("Texto seguro", JavaScript Experto): la longitud de `"<b>Hola</b>"` es 11, no 12; las instrucciones y la salida esperada decían 12 y marcaban mal una respuesta correcta. APK 1.0.1 (`versionCode` 2, `versionName` 1.0.1, paquete `mx.gerardo.programar`, `targetSdk` 36, 3,951,348 bytes, md5 `9c803058e59783e2e9907a9aa3301196`, mismo keystore permanente, firma v2 verificada). La 1.0 (md5 `66da6fbb3a1a929f2f4ff2a6494b2b7e`) quedó sustituida. El cambio también se aplicó en el espacio web. Verificación: `tests/check-data.cjs` 44,329 checks, 0 fallos; `tests/test-app.cjs` 48/48; las 80 tareas JavaScript ejecutan y dan la salida esperada (80/80).

## 2026-11-21 — APK 1.0

Se entrega la APK 1.0 (`versionCode` 1, `versionName` 1.0, paquete `mx.gerardo.programar`, `targetSdk` 36, 3,951,348 bytes, md5 `66da6fbb3a1a929f2f4ff2a6494b2b7e`, firmada con keystore permanente `~/workspace/android/keys/programar-release.keystore`, alias `programar`, SHA-256 `CE:C3:A3:F2:8B:68:16:98:F4:31:62:BB:42:D8:95:43:A0:57:B0:82:0A:43:8A:54:25:AE:0B:4E:98:97:FA:DE`, firma v2 verificada). No es un envoltorio del artefacto web (no tiene URL pública): es una reconstrucción local aparte con el mismo contenido (`www/index.html` + `www/data/*.js`, localStorage, login local por cuenta). Verificada estructuralmente (badging, firma, contenido empaquetado); sin probar aún en un teléfono real. El avance NO se sincroniza entre la web y la APK 1.0 (no hay Firebase todavía).

Verificación de la 1.0: `tests/check-data.cjs` **44,329 checks, 0 fallos**; `tests/test-app.cjs` (jsdom, datos reales) **48/48**. Bundle de Firebase `www/cloud/firebase.bundle.js` md5 `1a841655ff6ad59fbeb9fd06fe83b4bd`.

## 2026-11-21 — Firebase creado (Auth pendiente de activar)

El proyecto Firebase `aprender-programar` (plan Spark) **ya existe**: creado por CLI el 2026-11-21, con Firestore creado en la región `nam5` y las reglas de `firestore.rules` publicadas por CLI, y la app web "Aprender a Programar" registrada (App ID `1:584182094137:web:37c4a7e9f6741696e9f0e8`). La config real quedó en `www/firebase-config.js` (no se sube a GitHub) y la APK 2.0 ya la incluye. **Falta activar Auth por correo/contraseña en la consola** (Authentication → Método de acceso → Correo/contraseña → Habilitar → Guardar): la activación por API falló con `CONFIGURATION_NOT_FOUND` tras varios intentos, así que solo se puede hacer por consola. Sin ese paso, el login en la nube falla y la app sigue en modo local.

## 2026-11-21 — Firebase pendiente de crear

El proyecto Firebase nuevo y separado es `aprender-programar` (plan Spark), con Firebase Auth (usuario y contraseña, correos sintéticos `usuario@programar.local`), Firestore (`users`, `usernames`, `progress` con las tareas dentro de `progress.tasks`) y caché offline en la APK. La capa de nube está lista en el código (`www/cloud/firebase.js` + bundle esbuild, reglas en `firestore.rules`, config placeholder en `www/firebase-config.js`), pero **el proyecto aún no existe: la CLI de Firebase perdió la sesión** y no se pudo crear desde el sandbox. Hace falta `firebase login --reauth` con la cuenta de Gerardo, o crear el proyecto en console.firebase.google.com, y después: activar Auth por correo/contraseña, crear Firestore y publicar las reglas por consola, registrar la app web y pegar la config real en `www/firebase-config.js`, y recompilar la APK (mismo `appId` y keystore, `versionCode` 3). Hasta entonces la app es modo local y la nube web ↔ APK no sincroniza. Los pasos exactos están en el README.

## 2026-11-21 — Documentación y GitHub

Se crea la documentación en `docs/` (README.md, PREGUNTAS-DEVS.md y este CHANGELOG.md). Gerardo creó el repositorio público `gcruzhz/aprender-a-programar` (vacío; la Muse GitHub App no puede crear repositorios). El repo contiene solo la documentación; el código de la app vive en el artefacto web y el de la APK en `~/workspace/android/programar-app/`. Los docs se suben solo con la aprobación de Gerardo.

## Pendiente

- Activar Auth por correo/contraseña en la consola de Firebase (sin eso el login en la nube de la APK 2.0 falla) y unificar los logros: la APK tiene 13 y la web 16, con listas e ids distintos y mecanismos diferentes (ver entrada 2.0).
- Verificación de sincronización web ↔ APK con una cuenta real en un navegador o teléfono (pendiente; falta el ciclo completo: registrar, completar una lección, salir y volver a entrar).
- Detalle del stack interno del artefacto web.
- Pruebas de Gerardo en teléfono real (APK 1.0.1: instalar la APK, registro/login, completar una lección, tarea JS y por archivo, Laboratorio, Práctica, 6 corazones, ligas/logros/certificado, y cuando exista Firebase, la sincronización web ↔ APK).
