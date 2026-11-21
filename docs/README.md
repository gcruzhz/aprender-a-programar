# Aprender a Programar

App estilo Duolingo para aprender a programar en español: lecciones cortas, ejercicios, tareas con revisión automática, puntos, racha y ligas. Primero se aprende jugando, con una terminal simulada para practicar código de verdad y un Laboratorio que instala en la computadora todo lo necesario para programar.

## Qué es

Una app de aprendizaje con 13 rutas, una por lenguaje o tema. Cada ruta tiene 4 niveles (Básico, Intermedio, Avanzado y Experto) con 20 lecciones cada uno: 80 lecciones por ruta, 1,040 en total. Las lecciones son de unos 5 minutos en un camino que se desbloquea paso a paso. Al completar una ruta se obtiene un certificado de nivel.

La app vive como artefacto web fullstack de Muse (slug: `aprender-a-programar`). El APK para Android es una reconstrucción local aparte con el mismo contenido (`~/workspace/android/programar-app/`: un solo `www/index.html` + `www/data/*.js`, localStorage y login local por cuenta) — el artefacto web no tiene URL pública, así que no se puede envolver en un WebView. La nube (Firebase) está pendiente de crear (ver abajo): hasta entonces la app es modo local y el avance NO se sincroniza entre la web y la APK.

## Rutas y contenido

| Ruta | Icono | Prompt | Tagline |
|------|-------|--------|---------|
| Introducción a la programación (`intro`) | 💡 | `prog> ` | Aprende qué es programar y cómo piensa un programador, desde cero. |
| Python (`python`) | 🐍 | `python> ` | El lenguaje más usado para empezar: claro, legible y versátil. |
| JavaScript (`javascript`) | 🟨 | `node> ` | El lenguaje de la web: páginas interactivas, servidores y apps. |
| TypeScript (`typescript`) | 🔷 | `ts> ` | JavaScript con tipos: menos errores y proyectos grandes bajo control. |
| Java (`java`) | ☕ | `java> ` | Robusto y multiplataforma: empresas, Android y sistemas grandes. |
| C# (`csharp`) | #️⃣ | `dotnet> ` | El lenguaje de .NET: apps, videojuegos con Unity y servicios. |
| Go (`go`) | 🐹 | `go> ` | Simple y rápido: servidores, nube y herramientas modernas. |
| Rust (`rust`) | 🦀 | `rust> ` | Seguro y veloz: sistemas, rendimiento y memoria bajo control. |
| Kotlin (`kotlin`) | 🅺 | `kotlin> ` | Moderno y conciso: el lenguaje oficial para Android. |
| SQL (`sql`) | 🗄️ | `sql> ` | El idioma de las bases de datos: consulta y organiza información. |
| HTML/CSS (`htmlcss`) | 🎨 | `web> ` | La base de toda página web: estructura con HTML y estilo con CSS. |
| C++ con Qt y QML — Apps para KDE (`qt-qml`) | 🖥️ | `qt> ` | C++ con Qt y QML: crea apps de escritorio y para KDE. |
| Herramientas (`herramientas`) | 🧰 | `herramientas> ` | Las herramientas que usa un programador todos los días. |

Números totales: **13 rutas × 80 lecciones = 1,040 lecciones, 5,200 ejercicios, 1,040 tareas** (una por lección).

### Cada lección

- **Teoría `detail`**: exactamente 4 bloques cortos — qué es, para qué sirve, un ejemplo concreto (con código real cuando aplica) y el error común que hay que evitar.
- **5 ejercicios**, con al menos 1 de cada tipo principal (ver abajo).
- **1 tarea** para hacer en el editor, con revisión automática (ver "Tareas").

IDs de lección estables: `<ruta>-<nivel><nn>`, por ejemplo `python-b01`, `java-i12`, `qt-qml-e20` (Básico `b01`–`b20`, Intermedio `i01`–`i20`, Avanzado `a01`–`a20`, Experto `e01`–`e20`). El avance se guarda por id, no por posición.

### Ruta C++ con Qt y QML — Apps para KDE (`qt-qml`)

Ruta pedida por Gerardo con 80 lecciones (20 por nivel, no las 20 en total propuestas al inicio). Cubre: C++ esencial para Qt (tipos, clases, señales y slots), Qt Core (QString, contenedores, archivos), Widgets (ventanas, botones, layouts), QML y Qt Quick (interfaces declarativas, propiedades, animaciones), Kirigami y KDE Frameworks, y empaquetar la app (CMake, AppImage, Flatpak), con un mini proyecto final: una app KDE sencilla con QML.

## Ejercicios

Cada lección mezcla estos 4 tipos (mismos que la app de DevTools):

1. **Elegir la respuesta correcta** (`mc`) — opción múltiple.
2. **Completar el código** (`complete`) — rellenar la parte que falta (`___` en el código, 3 opciones).
3. **Terminal simulada** (`terminal`) — escribir la línea de código o el comando real, con el prompt propio de la ruta (`python> `, `node> `, `qt> `...). Se aceptan formas alternativas válidas (`accept`).
4. **Ordenar los pasos** (`order`) — poner en orden los 4 pasos de una tarea.

Cada lección tiene **6 corazones**: fallar ya no reinicia la lección (una lección tiene 5 ejercicios). Tras cada respuesta hay una explicación. Hay una pestaña de **🎯 Práctica** con ejercicios de repaso de las lecciones ya completadas.

## Tareas

Cada lección trae una tarea para hacer en el editor, con código inicial (`starter`) e instrucciones paso a paso en español. La app la revisa de forma automática, de tres maneras según el tipo de revisión de la tarea:

- **`js`** — solo para lecciones de JavaScript: la app ejecuta el código en el navegador y compara la salida con la esperada (ignorando espacios al inicio y al fin).
- **`output`** — el usuario escribe o pega la salida de su programa y la app la compara con la esperada (sin distinguir mayúsculas/minúsculas ni espacios extra).
- **`keywords`** — el usuario pega su código y la app comprueba que contenga todas las palabras clave pedidas (subcadenas exactas, sensibles a mayúsculas).

Para lenguajes que NO son JavaScript nunca se usa `js`: se usa `output` o `keywords`, y las instrucciones lo dicen así — la revisión es por salida esperada o por palabras clave, **sin prometer ejecución real** del código en otros lenguajes.

También se puede **subir un archivo** con la tarea (máx. 100 KB, se guarda como texto). La vista **📝 Mis tareas** muestra cada tarea en uno de tres estados: **pendiente** (sin guardar), **hecha en la app** (revisión pasada y marcada) o **enviada** (archivo subido, con nombre de archivo y fecha). Las tareas se guardan con el avance y se sincronizan con la nube cuando exista.

## Laboratorio

Pestaña **🧪 Laboratorio**: 4 guías paso a paso para instalar en la computadora todo lo necesario para programar — Python, Node.js, VS Code y Git — una por sistema operativo:

| Guía | Pasos |
|------|-------|
| Windows 11 | 11 |
| Linux | 10 |
| macOS | 10 |
| Android (Termux) | 9 |

Cada paso trae título, texto (qué hacer y por qué), comandos exactos opcionales y cómo verificar que quedó bien (por ejemplo, `python --version` debe mostrar `Python 3.x`). Las guías de **Windows, Linux y macOS incluyen además los pasos para instalar Qt y Qt Creator** (en Linux con el gestor de paquetes de la distro o el instalador en línea de Qt; en Windows/macOS con el instalador en línea), con su verificación (`qmake --version` o abrir Qt Creator y crear un proyecto de prueba). En Android se usa Termux con paquetes `pkg`.

## Gamificación

- **XP** por lección terminada.
- **Racha diaria**: días seguidos con al menos una lección.
- **Ligas semanales por XP**: Bronce a Diamante.
- **13 logros** en la APK (por ejemplo, primera lección, lección sin errores, 100 XP, racha de 7 días, ruta completada). La app web muestra 16 por ahora; los conteos se unificarán en una versión posterior.
- **Certificado de nivel** al completar cada ruta, con el nombre configurado en el perfil.

## Login y progreso

- Cuentas con **usuario y contraseña** (más el nombre que sale en los certificados).
- La sesión queda guardada en el teléfono: no hay que entrar cada vez.
- El progreso es **por cuenta**: XP, racha, lecciones, logros, certificados y tareas son de cada usuario.
- La primera cuenta que se crea **hereda el avance hecho antes del login** (XP, lecciones y logros no se pierden).

El perfil muestra "Versión 1.0.1 · Local: sin nube todavía" mientras no haya Firebase.

## Sin botón de IA en la 1.0

A diferencia de la app de DevTools (que tiene "🤖 Preguntar a la IA" con Gemini), esta app **no trae botón de IA en la versión 1.0**. Si se agrega en una versión futura, la clave la pegaría Gerardo en el Perfil y nunca iría en el código.

## Firebase — PENDIENTE DE CREAR (estado 2026-11-21)

El proyecto Firebase nuevo y separado es **`aprender-programar`**, pero **aún no existe**: la CLI de Firebase perdió la sesión y no se pudo crear desde el sandbox. Hasta que exista, la app trabaja en **modo local** (cuentas y avance solo en el teléfono) y la nube web ↔ APK **NO sincroniza** entre sí: la app web usa su propio backend y la APK usará Firebase cuando exista el proyecto.

El modelo previsto es el mismo que el de Checklist de Soporte y el de DevTools:

- **Proyecto Firebase nuevo y separado:** `aprender-programar` (plan Spark, gratis). No se reutiliza el proyecto de Checklist (`checklist-soporte`) ni el de DevTools (`devtools-aprender`).
- **Autenticación:** Firebase Auth con correo y contraseña. El login sigue siendo usuario y contraseña: el usuario se resuelve a un correo sintético `usuario@programar.local` (igual que Checklist y DevTools). Al registrarse se puede dejar un correo real de recuperación (opcional) para el enlace de "Olvidé mi contraseña"; sin él, una contraseña olvidada no se puede recuperar y hay que crear otra cuenta.
- **Datos en Firestore:** colecciones `users/{uid}` (usuario, nombre, correo real), `usernames/{usuario}` (para resolver el login) y `progress/{uid}` (XP, racha, lecciones, logros, tareas — las tareas viven dentro de este documento, `progress.tasks`, no hay colección aparte). Reglas en `firestore.rules`: cada usuario solo ve y escribe lo suyo. No hay rol de admin en esta app: todos son alumnos.
- **Offline:** la APK usa caché persistente de Firestore: funciona sin internet y sincroniza al volver la conexión (igual que Checklist y DevTools). La capa de nube es `www/cloud/firebase.js`, compilada con esbuild a `www/cloud/firebase.bundle.js` (md5 `1a841655ff6ad59fbeb9fd06fe83b4bd`).
- **Migración de cuentas locales:** Firebase Auth no puede reutilizar las contraseñas guardadas en modo local (solo existen hashes, no las contraseñas). Cada usuario vuelve a registrarse en la nube con el mismo usuario y contraseña; en el primer inicio de sesión en la nube, el avance local existente se sube a Firestore si aún no hay avance en la nube (si ya hay avance en la nube, manda el de la nube).

### Pasos exactos que debe hacer Gerardo

1. **Re-autenticar la CLI de Firebase** con su cuenta (en el sandbox: `firebase login --reauth`), **o crear el proyecto `aprender-programar` directamente en** https://console.firebase.google.com (botón "Agregar proyecto", nombre del proyecto `aprender-programar`).
2. **Activar Auth por correo/contraseña**: en la consola, Compilación → Authentication → Método de acceso → habilitar "Correo electrónico/contraseña".
3. **Crear Firestore y publicar las reglas**: en la consola, Compilación → Firestore Database → Crear base de datos, y luego en la pestaña Reglas pegar el contenido de `firestore.rules` (del código en `~/workspace/android/programar-app/firestore.rules`) y publicar. Por consola: el `firebase deploy` por CLI falla en el sandbox por la ruta Node → proxy (igual que pasó con DevTools).
4. **Registrar la app web y pegar la config real en `www/firebase-config.js`**: en la consola, Configuración del proyecto → "Tus apps" → agregar app web `</>`; copiar los valores (`apiKey`, `authDomain`, `projectId`, `storageBucket`, `messagingSenderId`, `appId`) y pegarlos en `www/firebase-config.js` (la plantilla con placeholders está en `www/firebase-config.example.js`). El archivo real **NO se sube a GitHub** (está en `.gitignore`): la apiKey web es pública por diseño, pero el resto de la config no tiene por qué versionarse. El bundle NO embebe la configuración (se lee de `window.PROGRAMAR_FIREBASE_CONFIG` en runtime), así que su md5 no cambia con la config.
5. **Si cambia `www/cloud/firebase.js`, reconstruir el bundle** con `pnpm build:cloud` (esbuild → `www/cloud/firebase.bundle.js`), correr `npx cap sync` y **recompilar la APK** (mismo `appId` y mismo keystore, `versionCode` 3). La app instalada usa el bundle, no el `.js`.

## Instalación de la APK

- **APK 1.0.1** (actual): paquete `mx.gerardo.programar`, `versionCode` 2, `versionName` 1.0.1, `targetSdk` 36, 3,951,348 bytes, md5 `9c803058e59783e2e9907a9aa3301196`, firma v2 verificada con apksigner. La 1.0 (md5 `66da6fbb3a1a929f2f4ff2a6494b2b7e`) quedó sustituida por este parche, que corrige la tarea `javascript-e13` (la longitud de `"<b>Hola</b>"` es 11, no 12).
- **Keystore permanente**: `~/workspace/android/keys/programar-release.keystore`, alias `programar`, SHA-256 del certificado `CE:C3:A3:F2:8B:68:16:98:F4:31:62:BB:42:D8:95:43:A0:57:B0:82:0A:43:8A:54:25:AE:0B:4E:98:97:FA:DE`. La configuración de firma vive en `keys/programar-keystore.properties` (permisos 600) y se usa vía `signingConfigs.release` en `android/app/build.gradle`. **Nunca** usar el keystore debug: se regenera en cada reinicio de la VM y cambia la firma, así que Android bloquea las actualizaciones.
- Se instala como actualización sobre versiones futuras con el mismo keystore; cambiar de firma exigiría desinstalar la app una vez.
- La APK está en `~/workspace/your_files/aprender-a-programar.apk`. El APK compilado vive en `android/app/build/outputs/apk/release/app-release.apk` dentro de `~/workspace/android/programar-app/`.

## Desarrollo

Código en `~/workspace/android/programar-app/`:

- `www/index.html` — la app completa (una sola página, sin framework).
- `www/data/*.js` — un archivo por ruta (`intro.js`, `python.js`, `javascript.js`, `typescript.js`, `java.js`, `csharp.js`, `go.js`, `rust.js`, `kotlin.js`, `sql.js`, `htmlcss.js`, `qt-qml.js`, `herramientas.js`) más `labs.js` (las 4 guías de Laboratorio). Cada archivo hace `window.PROGRAMAR_ROUTES.push({...})` (salvo `labs.js`, que usa `window.PROGRAMAR_LABS`). Estos archivos son la **fuente única del contenido**: la app web y la APK usan los mismos IDs y los mismos textos.
- `www/cloud/firebase.js` + `www/cloud/firebase.bundle.js` — capa de nube (Firebase Auth + Firestore + caché offline).
- `www/firebase-config.js` — config real del proyecto (placeholder hasta que exista Firebase; NO se sube a GitHub). Plantilla: `www/firebase-config.example.js`.
- `firestore.rules` — reglas de Firestore listas para publicar por consola.
- `SCHEMA.md` — contrato de datos completo (rutas, lecciones, ejercicios, tareas, Laboratorio, reglas duras).
- `tests/` — `check-data.cjs` (validador de contenido) y `test-app.cjs` (pruebas jsdom con datos reales).
- `android/` — proyecto Capacitor 8.6.0 / Gradle (la APK).

### Cómo regenerar contenido

El contenido se escribe o se edita directamente en `www/data/*.js`, siguiendo el contrato de `SCHEMA.md`: todo en español, código real y correcto (que corra tal cual en su intérprete/compilador; si es pseudocódigo, dilo en el texto), `detail` con exactamente 4 bloques, 5 ejercicios por lección (mínimo 1 `mc`, 1 `complete`, 1 `terminal` y 1 `order`), 1 tarea por lección con revisión `js` (solo JavaScript), `output` o `keywords` (los demás lenguajes). Después de editar, verificar cada archivo con `node --check <archivo>` y correr el validador (abajo). Para agregar una ruta nueva: crear `www/data/<id>.js` con la misma estructura y registrar el `<script>` en `www/index.html` junto a las otras rutas.

### Tests

```bash
cd ~/workspace/android/programar-app
node tests/check-data.cjs   # validador de contenido
node tests/test-app.cjs     # pruebas jsdom con datos reales
```

Verificación de la 1.0.1: `tests/check-data.cjs` **44,329 checks, 0 fallos**; `tests/test-app.cjs` (jsdom, datos reales) **48/48**.

### Build de la APK

Toolchain en `~/workspace/android/` (JDK 21 Temurin en `jdk21/`, Android SDK en `sdk/`). Entorno listo en `~/workspace/android/env.sh` (hay que hacer `source` antes). Lecciones del toolchain (detalle en `~/AGENTS.md`):

- **JDK 21 obligatorio**: Capacitor 8 / AGP 8.13 exigen JDK 21 (source release 21); con JDK 17 el build falla con `invalid source release: 21`.
- **Proxy y CA**: Java no sale a internet por defecto; hay que pasarle a la JVM `-Djava.net.preferIPv4Stack=true` y el proxy con usuario/clave de `$https_proxy`, más la CA del proxy importada en el cacerts del JDK. La CA puede rotar al reiniciar la VM: correr `~/workspace/android/refresh-ca.sh` y después parar el daemon de Gradle (`./gradlew --stop`) antes de reintentar. `JAVA_TOOL_OPTIONS=-Djava.net.preferIPv4Stack=true` ya está en `env.sh`; el proxy del daemon va por `systemProp.*` en `android/gradle.properties`.
- **Gradle tras un reinicio**: `/root/.gradle` se vacía y el wrapper no puede descargar su distribución por el proxy; descargar el zip con curl a `/root/.gradle/wrapper/dists/<dist>/<hash>/gradle-<ver>-all.zip` y verificar con `unzip -t` (en DevTools: gradle-8.14.3-all.zip, 224,584,249 bytes).
- **pnpm, no npm**: `npm install` falla con `EPERM chown`; usar pnpm standalone (`~/.local/share/pnpm/bin/pnpm`).
- **Nunca `pnpm dlx cap sync`**: `dlx` resuelve `cap` a un paquete npm ajeno; usar siempre `npx cap sync` (el CLI local del proyecto).
- **Si cambia `www/cloud/firebase.js`, reconstruir el bundle** con `pnpm build:cloud` y volver a correr `npx cap sync` antes de compilar: la app instalada usa el bundle, no el `.js`.

```bash
source ~/workspace/android/env.sh
cd ~/workspace/android/programar-app
pnpm build:cloud        # solo si cambió www/cloud/firebase.js
npx cap sync            # copia www/ a android/app/src/main/assets/public
cd android
./gradlew assembleRelease
# APK en app/build/outputs/apk/release/app-release.apk
```

Verificar la APK con `apksigner verify --print-certs` (firma v2 y SHA-256 del certificado) y `md5sum`.

## Este repositorio

Este repo contiene **solo la documentación** de la app (`docs/`). El código de la app vive en el artefacto web de Muse y el de la APK en `~/workspace/android/programar-app/` (no hay código en este repo, así que no hay nada que compilar desde aquí). El repo lo creó Gerardo (vacío) y **solo lleva documentación: NUNCA binarios ni `firebase-config.js` con valores reales**. Repo: https://github.com/gcruzhz/aprender-a-programar

## Estado actual (2026-11-21)

- Plan aprobado y app construida el mismo día: 13 rutas × 80 lecciones = 1,040 lecciones, 5,200 ejercicios, 1,040 tareas, 4 guías de Laboratorio. La ruta C++ con Qt y QML (80 lecciones) se agregó a petición de Gerardo, que la pidió con 80 lecciones en vez de las 20 propuestas al inicio.
- APK 1.0.1 entregada el 2026-11-21: paquete `mx.gerardo.programar`, `versionCode` 2, firmada con keystore permanente (SHA-256 `CE:C3:A3:F2:8B:68:16:98:F4:31:62:BB:42:D8:95:43:A0:57:B0:82:0A:43:8A:54:25:AE:0B:4E:98:97:FA:DE`), md5 `9c803058e59783e2e9907a9aa3301196`. Parche sobre la 1.0 (md5 `66da6fbb3a1a929f2f4ff2a6494b2b7e`) que corrige la tarea `javascript-e13`. Verificada estructuralmente (badging, firma, contenido empaquetado); sin probar aún en un teléfono real. El avance NO se sincroniza entre la web y la APK 1.0.1 (no hay Firebase todavía).
- Proyecto Firebase `aprender-programar` **pendiente de crear** (la CLI perdió la sesión; hace falta `firebase login --reauth` con la cuenta de Gerardo, o crearlo en la consola). Código de nube listo (`www/cloud/firebase.js` + bundle md5 `1a841655ff6ad59fbeb9fd06fe83b4bd`, reglas en `firestore.rules`, config placeholder en `www/firebase-config.js`).
- Documentación en este repositorio (`docs/`), lista para subir a GitHub con la aprobación de Gerardo.

## Pendiente / por definir

- Crear el proyecto Firebase `aprender-programar` (pasos exactos arriba), activar Auth, publicar las reglas, pegar la config real y compilar la APK 2.0 con nube.
- Verificar la sincronización web ↔ APK con una cuenta real en un navegador o teléfono (registrar, completar una lección, salir y volver a entrar).
- Detalle del stack interno del artefacto web (pendiente de documentar; no inventado aquí).
- Pruebas de Gerardo en teléfono real: instalar la APK, registro/login, completar una lección, tarea JS y por archivo, Laboratorio, Práctica, 6 corazones, ligas/logros/certificado, y (cuando exista Firebase) la sincronización web ↔ APK.
