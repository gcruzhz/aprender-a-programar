# Preguntas de desarrolladores — Aprender a Programar

Documento para que un desarrollador entienda la app rápido: qué es, cómo está hecha a grandes rasgos y qué se le puede preguntar. Solo contiene lo verificado; lo que aún no se sabe está marcado como pendiente.

## ¿Qué es la app?

Una app estilo Duolingo, en español, para aprender a programar jugando: Introducción a la programación, Python, JavaScript, TypeScript, Java, C#, Go, Rust, Kotlin, SQL, HTML/CSS, C++ con Qt y QML — Apps para KDE, y Herramientas. Lecciones de unos 5 minutos con teoría a detalle (4 bloques: qué es, para qué sirve, ejemplo, error común), 5 ejercicios de 4 tipos (elegir la respuesta, completar el código, terminal simulada, ordenar los pasos) y 1 tarea por lección con revisión automática o subida de archivo. 6 corazones por lección, XP, racha diaria, ligas semanales (Bronce a Diamante), 13 logros en la APK (16 en la web por ahora) y certificado al completar cada ruta. Pestaña de Práctica con ejercicios de repaso y Laboratorio con guías para instalar Python, Node.js, VS Code, Git (y Qt/Qt Creator) en Windows, Linux, macOS y Android (Termux). Sin botón de IA en la 1.0.

## ¿Dónde vive la app?

Como artefacto web fullstack de Muse (slug: `aprender-a-programar`). El código no está en este repositorio: este repo solo tiene documentación (`docs/`). El APK de Android es una reconstrucción local aparte con el mismo contenido (`~/workspace/android/programar-app/`: un solo `www/index.html` + `www/data/*.js`, localStorage y login local por cuenta) — el artefacto web no tiene URL pública, así que no se puede envolver en un WebView. La nube (Firebase) está pendiente de crear: hasta entonces la app es modo local y el avance NO se sincroniza entre la web y la APK (la web usa su propio backend; la APK usará Firebase cuando exista el proyecto).

## ¿En qué lenguaje / con qué stack está hecha?

Pendiente de documentar con detalle el stack interno del artefacto web. Lo que sí está verificado: la APK es JavaScript de una sola página (sin framework) con Capacitor 8.6.0, y su contenido vive en `www/data/*.js` (un archivo por ruta más `labs.js`), con el contrato completo en `SCHEMA.md`. El backend previsto es Firebase, compartido por la app web y la APK, con el mismo modelo que la app Checklist de Soporte en la nube y que la app de DevTools, pero con proyecto Firebase separado (`aprender-programar`, plan Spark): Firebase Auth con correo y contraseña (login por usuario con correos sintéticos `usuario@programar.local`) y Firestore con colecciones `users`, `usernames` y `progress` (las tareas viven dentro de `progress.tasks`, no hay colección aparte; reglas: cada usuario solo ve lo suyo; no hay rol de admin, todos son alumnos). La capa de nube es `www/cloud/firebase.js`, compilada con esbuild a `www/cloud/firebase.bundle.js` (md5 `1a841655ff6ad59fbeb9fd06fe83b4bd`); la APK usa caché persistente de Firestore para funcionar offline. El proyecto Firebase aún no existe (la CLI perdió la sesión); los pasos para crearlo están en el README.

## ¿Cómo funciona el login?

Cuentas con usuario y contraseña (más un nombre para los certificados). La sesión es persistente: queda guardada en el teléfono. El progreso es por cuenta. La primera cuenta creada hereda el avance hecho antes de que existiera el login (XP, lecciones y logros previos no se pierden).

Cuando exista Firebase, el login será con Firebase Auth: el usuario se resuelve a un correo sintético `usuario@programar.local`. Al registrarse se puede dejar un correo real de recuperación (opcional) para el enlace de "Olvidé mi contraseña"; sin él, una contraseña olvidada no se puede recuperar y hay que crear otra cuenta. Las cuentas locales de la 1.0 no migran automáticamente: cada usuario vuelve a registrarse en la nube con el mismo usuario y contraseña, y en el primer inicio de sesión en la nube su avance local existente se sube a Firestore si aún no hay avance en la nube.

## ¿Cómo se guarda el progreso?

Por usuario: XP total, racha diaria, lecciones completadas por ruta y nivel, logros desbloqueados (de 16), certificados y tareas. Las lecciones se desbloquean paso a paso en un camino por ruta. Cada lección tiene un id estable (`<ruta>-<nivel><nn>`, por ejemplo `python-b01`, `qt-qml-e20`) y el avance se guarda por id, no por posición.

En la versión 1.0 el progreso vive en la base del artefacto web (app web) o en localStorage (APK), sin sincronizar entre sí. Cuando exista Firebase vivirá en Firestore (`progress/{uid}`), compartido por la app web y la APK; la APK guardará además una copia local y sincronizará en vivo con `onSnapshot` al volver la conexión.

## ¿Cómo funcionan las tareas?

Cada lección trae una tarea con código inicial (`starter`) e instrucciones en español. La app la revisa de forma automática según su tipo de revisión: `js` (solo JavaScript: ejecuta el código en el navegador y compara la salida con la esperada), `output` (el usuario pega la salida de su programa y la app la compara) o `keywords` (el usuario pega su código y la app comprueba que contenga las palabras clave). Para lenguajes que no son JavaScript nunca se usa `js` y no se promete ejecución real. También se puede subir un archivo (máx. 100 KB, se guarda como texto). La vista Mis tareas muestra cada tarea como pendiente, hecha en la app o enviada (con nombre de archivo y fecha).

## ¿Qué rutas y niveles hay?

13 rutas: Introducción a la programación, Python, JavaScript, TypeScript, Java, C#, Go, Rust, Kotlin, SQL, HTML/CSS, C++ con Qt y QML — Apps para KDE, y Herramientas. Cada una con 4 niveles (Básico, Intermedio, Avanzado y Experto) de 20 lecciones cada uno: 80 lecciones por ruta, 1,040 en total, cada una con 5 ejercicios y 1 tarea. La ruta C++ con Qt y QML cubre C++ esencial para Qt, Qt Core, Widgets, QML y Qt Quick, Kirigami y KDE Frameworks, y empaquetado (CMake, AppImage, Flatpak).

## ¿Qué es el Laboratorio?

La pestaña 🧪 Laboratorio trae 4 guías paso a paso para instalar en la computadora todo lo necesario para programar (Python, Node.js, VS Code y Git): Windows (11 pasos), Linux (10 pasos), macOS (10 pasos) y Android con Termux (9 pasos). Las guías de Windows, Linux y macOS incluyen además instalar Qt y Qt Creator, con verificación (`qmake --version` o crear un proyecto de prueba en Qt Creator). El contenido vive en `www/data/labs.js` (`window.PROGRAMAR_LABS`).

## ¿Hay APK?

Sí. La APK 1.0 se entregó el 2026-11-21 (paquete `mx.gerardo.programar`, `versionCode` 1, `versionName` 1.0, `targetSdk` 36, 3,951,348 bytes, md5 `66da6fbb3a1a929f2f4ff2a6494b2b7e`, firmada con keystore permanente `~/workspace/android/keys/programar-release.keystore`, alias `programar`, SHA-256 `CE:C3:A3:F2:8B:68:16:98:F4:31:62:BB:42:D8:95:43:A0:57:B0:82:0A:43:8A:54:25:AE:0B:4E:98:97:FA:DE`, firma v2 verificada). Es una reconstrucción local aparte, no un envoltorio del artefacto web. Es modo local: sin Firebase todavía, así que el avance no sincroniza con la web. Verificación de la 1.0: `tests/check-data.cjs` 44,329 checks, 0 fallos; `tests/test-app.cjs` (jsdom, datos reales) 48/48. Pendiente de pruebas en un teléfono real. La APK con nube será la 2.0 (`versionCode` 2, mismo `appId` y keystore) cuando se cree el proyecto Firebase `aprender-programar`.

## ¿Cómo se compila la APK?

Toolchain en `~/workspace/android/` (JDK 21 Temurin, Android SDK; entorno en `~/workspace/android/env.sh`). Comandos, desde `~/workspace/android/programar-app/`:

```bash
source ~/workspace/android/env.sh
pnpm build:cloud        # solo si cambió www/cloud/firebase.js
npx cap sync            # copia www/ a android/app/src/main/assets/public
cd android && ./gradlew assembleRelease
```

La APK queda en `android/app/build/outputs/apk/release/app-release.apk`. Lecciones del toolchain (detalle en `~/AGENTS.md`): JDK 21 obligatorio (Capacitor 8 / AGP 8.13); Java necesita el proxy con IPv4 forzado y la CA del proxy en el cacerts (la CA rota al reiniciar la VM: `refresh-ca.sh` + `./gradlew --stop`); tras un reinicio `/root/.gradle` se vacía y hay que descargar Gradle con curl; usar pnpm (npm falla con `EPERM chown`); nunca `pnpm dlx cap sync` (usar `npx cap sync`); si cambia `www/cloud/firebase.js`, reconstruir el bundle con `pnpm build:cloud` antes de `cap sync`. La firma usa el keystore permanente (`keys/programar-keystore.properties`, permisos 600) vía `signingConfigs.release`; nunca el keystore debug, que se regenera en cada reinicio de la VM y cambia la firma.

## ¿Cómo se agrega una ruta o una lección?

Se edita o se crea un archivo en `www/data/*.js` siguiendo el contrato de `SCHEMA.md`: un archivo por ruta que hace `window.PROGRAMAR_ROUTES.push({...})`, con 4 niveles de 20 lecciones; cada lección con `id` estable, título, intro, `detail` de exactamente 4 bloques, 5 ejercicios (mínimo 1 `mc`, 1 `complete`, 1 `terminal` y 1 `order`) y 1 tarea con revisión `js` (solo JavaScript), `output` o `keywords`. Todo en español y con código real y correcto. La ruta nueva se registra con su `<script>` en `www/index.html` junto a las otras. Después: `node --check` por archivo y los tests (`node tests/check-data.cjs` y `node tests/test-app.cjs`).

## ¿Qué se le puede preguntar a un dev que revise la app?

- Cómo agregar una ruta o una lección nueva (contenido y niveles).
- Cómo funciona la terminal simulada (qué comandos valida y cómo).
- Cómo funciona la revisión automática de tareas (ejecución JS en el navegador, salida esperada, palabras clave) y la subida de archivos.
- Cómo se calculan XP, racha y ligas, y dónde vive esa lógica.
- Cómo se hace el despliegue del APK y qué permisos necesita (internet).
- Cómo se respalda o se migra el progreso de los usuarios.
- Cómo se crea el proyecto Firebase `aprender-programar` y se publica `firestore.rules` por consola.

## Enlaces

- App web: artefacto `aprender-a-programar` en Muse.
- Repo (documentación): https://github.com/gcruzhz/aprender-a-programar (creado por Gerardo, vacío; docs listos en `docs/`, se suben solo con su aprobación).
- Proyecto Firebase: `aprender-programar` (pendiente de crear; consola https://console.firebase.google.com).
