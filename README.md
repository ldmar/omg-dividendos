<div align="center">
  <img src="icons/icon-512.png" alt="OMG DividendOS" width="128" />
  <h1>OMG DividendOS</h1>
  <p><b>Panel PWA para analizar, seguir y controlar los dividendos de tu cartera de CEDEARs.</b></p>
  <p>
    <img alt="PWA" src="https://img.shields.io/badge/PWA-installable-00d68f?style=flat-square" />
    <img alt="Offline" src="https://img.shields.io/badge/offline--first-Sí-3b82f6?style=flat-square" />
    <img alt="Cifrado" src="https://img.shields.io/badge/cifrado-AES--256--GCM-a855f7?style=flat-square" />
    <img alt="Sin servidor" src="https://img.shields.io/badge/backend-ninguno-8ba0b8?style=flat-square" />
    <img alt="Licencia MIT" src="https://img.shields.io/badge/licencia-MIT-00d68f?style=flat-square" />
  </p>
  <p><i>Realizado por <b>Ohmygoch</b> · v2.3</i></p>
</div>

---

## ✨ Características

- 🧠 **Parser inteligente de extractos** — arrastrás un `.xlsx`/`.csv` de tu broker (IOL, Balanz, Rava, PPI, Cocos, Bull Market…) y la app detecta fechas, tickers, número de operación, importes y emisores automáticamente.
- 🗂️ **Historial acumulativo** — cargá varios extractos sin perder los anteriores. La app fusiona los movimientos por N° de operación (o por fecha + ticker + monto) y omite los duplicados.
- 📊 **Métricas profesionales por CEDEAR** — total cobrado, promedio, mediana, coeficiente de variación, cadencia entre pagos, pagos por año, run-rate a 12 meses, consistencia y fecha estimada del próximo pago.
- 📈 **Diversificación** — índice Herfindahl (HHI), fuentes efectivas de ingreso y detección de concentración.
- 🔍 **Detección de pagos atípicos** — z-score por ticker para identificar dividendos extraordinarios o errores de carga.
- 🔔 **Seguimiento y alertas** — cargá manualmente CEDEARs que no estén en el extracto, definí su cadencia y último pago, y la app calcula la próxima fecha estimada. Panel de estados: *programado / pronto / hoy / vencido*.
- 🚨 **Notificaciones del navegador** — avisos configurables de X días antes con deduplicación diaria.
- 📅 **Calendario y heatmap** — próximos pagos estimados + mapa de calor meses × activo.
- 💼 **Posiciones y yield on cost** — cargá cantidad y precio promedio para ver tu Yield on Cost y renta anual proyectada.
- 🔐 **Seguridad real** — todos los datos se guardan cifrados con **AES-256-GCM**; la clave se deriva de tu contraseña con **PBKDF2 (150.000 iteraciones)**. La contraseña nunca se almacena.
- 📱 **PWA instalable** — funciona offline, tiene ícono propio, y se puede agregar a la pantalla de inicio en iOS y Android.
- 🖥️ **100% local** — ningún dato viaja a internet. Sin backend, sin tracking, sin telemetría.

---

## 🚀 Demo

Una vez desplegado en GitHub Pages:

```
https://ohmygoch.github.io/omg-dividendos/
```

---

## 📸 Capturas

| Resumen | Seguimiento |
|:-:|:-:|
| ![Resumen](screenshots/resumen.png) | ![Seguimiento](screenshots/seguimiento.png) |

---

## 🧑‍💻 Cómo usarla

### 1. Descargar el extracto de tu broker

1. Ingresá al **home banking** o app de tu broker.
2. Buscá **“Movimientos”**, **“Extracto de cuenta”** o **“Historial de operaciones”**.
3. Filtrá por **“Dividendos”**, **“Eventos corporativos”** o **“Renta”**.
4. Elegí un rango de **últimos 12 meses** (mínimo 6 para proyecciones confiables).
5. Exportá en formato **Excel (.xlsx)** o **CSV**.

### 2. Importarla

Arrastrá el archivo sobre la pantalla principal o usá **Cargar extracto**. La app parsea los movimientos y genera todas las métricas al instante.

### 3. Formato mínimo del archivo

| Columna | Descripción | Ejemplo |
|---|---|---|
| `Fecha` | Fecha del movimiento | `17/09/2026` |
| `Movimiento` | Texto que incluya `DIVIDENDOS` y el ticker | `... DIVIDENDOS UGP CEDEAR ULTRAPAR ...` |
| `Débito` | Importe debitado (suele ser 0) | `0,00` |
| `Crédito` | Importe acreditado (**el que se analiza**) | `6,50` |

### 4. Cargar varios extractos (historial acumulativo)

Cuando subís un archivo nuevo, la app **NO borra** los movimientos anteriores. Los **fusiona**:

- **Movimiento nuevo** → se agrega al historial.
- **Movimiento ya existente** → se omite. Se identifica por **N° de operación**; si el extracto no lo trae, por combinación de **fecha + ticker + monto**.
- **Rango de fechas** → se conserva el más amplio entre todos los extractos cargados.

**Ejemplo:** si cargás `ene–jun` y después `jul–dic`, tu historial queda con **12 meses completos**. Si volvés a cargar el primero, no se duplica nada.

> 💡 Para **borrar todo** y empezar de cero, usá el botón 🗑 del encabezado. Pide **doble confirmación** y conserva tu contraseña.

### 5. Seguimiento manual

En la pestaña **Seguimiento** podés cargar CEDEARs que ya tenés en cartera y no aparezcan en el extracto:

- **Ticker**, **cadencia** (mensual / bimestral / trimestral / semestral / anual / personalizada), **último pago** y **monto esperado**.
- La app calcula la **próxima fecha estimada** y la cruza con el calendario y las alertas.
- Si un pago se atrasa más de 7 días, aparece marcado como **vencido** en rojo — ideal para reclamarle a tu broker.

### 6. Alertas

Activá las **notificaciones del navegador**, definí cuántos días antes querés que te avise y probá el sistema con el botón de test. Las notificaciones se disparan mientras la app esté abierta en alguna pestaña.

---

## 🔐 Seguridad

- **Cifrado:** AES-256-GCM (Web Crypto API nativa del navegador).
- **Derivación de clave:** PBKDF2 con SHA-256 y **150.000 iteraciones**.
- **Contraseña:** nunca se almacena. Solo se guarda un blob cifrado en `localStorage`.
- **Bloqueo de sesión:** botón 🔒 en el encabezado para cerrar la sesión al instante.
- **Limpiar datos:** botón 🗑 con **doble confirmación** — borra todo pero conserva la contraseña.

> ⚠️ **Si olvidás la contraseña, los datos no se pueden recuperar.** Es parte del diseño: sin la clave, el blob cifrado es inútil.

---

## 🛠️ Stack técnico

- **HTML + CSS + JavaScript vanilla** — sin frameworks, sin build step.
- **SheetJS (XLSX)** — lectura de archivos Excel. Cargado desde CDN, cacheado por el service worker para uso offline.
- **Web Crypto API** — cifrado AES-256-GCM y PBKDF2.
- **Notification API** — alertas nativas del sistema operativo.
- **Service Worker + Manifest** — PWA instalable y offline-first.

---

## 📁 Estructura del proyecto

```
omg-dividendos/
├── index.html          # App completa (single-file)
├── manifest.json       # Metadatos PWA (instalación)
├── sw.js               # Service worker (offline-first)
├── icons/
│   ├── generate.html   # Generador local de PNG a partir del SVG
│   ├── icon-*.png      # Íconos PWA
│   ├── icon-maskable-*.png
│   └── apple-touch-icon.png
├── README.md
├── LICENSE
└── .gitignore
```

---

## 🖼️ Generar los íconos

El repositorio incluye `icons/generate.html`. Abrilo en el navegador y descargá todos los PNG necesarios en un clic. La app ya está configurada para leerlos desde `icons/`.

Tamaños que genera:

- **PWA / Android:** 72, 96, 128, 144, 152, 192, 384, 512
- **Maskable (Android adaptativo):** 192, 512
- **Apple Touch Icon (iPhone/iPad):** 180

---

## 🌐 Deploy en GitHub Pages

1. Creá un repositorio público llamado **`omg-dividendos`**.
2. Subí todos los archivos (o cloná y pusheá).
3. Entrá a **Settings → Pages**.
4. En **Source**, elegí **Deploy from a branch** → **`main`** → **`/ (root)`**.
5. Guardá. En ~1 minuto la app estará en `https://TU_USUARIO.github.io/omg-dividendos/`.

> 💡 **HTTPS es obligatorio** para que funcionen el service worker y el prompt de instalación — GitHub Pages lo provee automáticamente.

### Alternativas de hosting

- **Netlify / Vercel / Cloudflare Pages:** arrastrás la carpeta y listo.
- **Servidor propio:** cualquier servidor estático con HTTPS sirve.

---

## 📲 Instalar la app

- **Android (Chrome / Edge):** aparece un banner de instalación o el botón **“Instalar app”** en el encabezado.
- **iPhone / iPad (Safari):** tocá **Compartir** → **Añadir a pantalla de inicio**.
- **Escritorio (Chrome / Edge):** ícono de instalación en la barra de direcciones.

Una vez instalada funciona 100% offline y se abre como una app nativa.

---

## 🧩 Compartir datos entre dispositivos

Los datos viven cifrados en el navegador donde los cargaste. Para migrar:

1. Exportá el CSV desde **↓ CSV** en el encabezado.
2. En el nuevo dispositivo, importá los movimientos nuevamente.
3. Volvé a cargar las posiciones manuales y las tenencias.

---

## 🤝 Contribuir

Se aceptan ideas y reportes. Abrí un **issue** con:

- Descripción del bug o feature.
- Pasos para reproducirlo.
- Capturas si aplica.

Pull requests bienvenidos con tests manuales documentados.

---

## 📜 Licencia

[MIT](LICENSE) © **Ohmygoch**

---

## 👤 Autor

**Ohmygoch**

- GitHub: [@ohmygoch](https://github.com/ohmygoch)

---

<div align="center">
  <sub>Hecho con 🍵 y paciencia. Si te sirve, dejame una ⭐.</sub>
</div>