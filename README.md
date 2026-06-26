# Libro IVA

App para registrar ingresos y egresos, y calcular el IVA a pagar según la ley paraguaya. Todo se guarda localmente en el celular (localStorage) — no hay servidor ni base de datos.

## Subir a GitHub Pages

1. Creá un repositorio nuevo en GitHub (puede ser público o privado).
2. Subí estos archivos a la raíz del repo, manteniendo la carpeta `icons/`:
   - `index.html`
   - `manifest.json`
   - `sw.js`
   - `icons/icon-192.png`
   - `icons/icon-512.png`
   - `icons/icon-512-maskable.png`
3. En el repo, ir a **Settings → Pages**.
4. En "Build and deployment", elegir **Deploy from a branch**, rama `main`, carpeta `/ (root)`.
5. Guardar. En 1-2 minutos la app va a estar disponible en algo como:
   `https://tu-usuario.github.io/nombre-del-repo/`

## Instalar en el celular (Android Chrome)

1. Abrí la URL de GitHub Pages en Chrome.
2. Tocá el menú (⋮) → **"Instalar app"** o **"Agregar a pantalla principal"**.
   (También puede aparecer un botón ⬇️ en la cabecera de la app cuando Chrome detecta que es instalable.)
3. Listo — queda como un ícono más en el celular, funciona sin conexión.

## Actualizar la app más adelante

Cada vez que edites `index.html`, `manifest.json` o los íconos y subas los cambios a GitHub:

- Abrí `sw.js` y cambiá el número de versión en la primera línea, por ejemplo:
  `const CACHE_VERSION = 'libro-iva-v1';` → `'libro-iva-v2';`
- Esto es importante: si no cambiás la versión, los celulares que ya instalaron la app van a seguir viendo la versión vieja en caché.

## Cómo funciona el cálculo de IVA

- **10%**: IVA = monto total ÷ 11
- **5%**: IVA = monto total ÷ 21 (no ÷ 6 — verificado contra la fórmula oficial: si el 5% va incluido en el precio, la base es monto ÷ 1.05, y el IVA es la diferencia)
- **Exenta**: IVA = 0

Estos valores son automáticos pero **siempre editables** desde el botón "editar" en cada registro, por si una factura real tiene un redondeo distinto.

El cálculo de "IVA a pagar" resta el crédito fiscal (IVA de tus egresos/compras) del débito fiscal (IVA de tus ingresos/ventas), y si en un mes te queda saldo a favor, la app lo arrastra automáticamente al mes siguiente hasta consumirlo.

**Importante:** esta app es una herramienta de seguimiento personal, no un reemplazo del asesoramiento de tu contador ni de la liquidación oficial en Marangatú. Verificá siempre los montos finales antes de presentar tus declaraciones.

## Respaldo de datos

Desde el ícono ⚙️ (arriba a la derecha):
- **Exportar respaldo (.json)**: descarga todos tus datos. Guardalo en Drive o donde prefieras.
- **Importar respaldo (.json)**: reemplaza todos los datos actuales por los del archivo — usalo si cambiás de celular.
- **Exportar registro (.csv)**: exporta solo la lista de ingresos/egresos en formato Excel, útil para mandarle al contador.
