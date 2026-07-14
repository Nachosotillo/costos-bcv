# Costos BCV — PWA

Calculadora de costo unitario e IVA de productos según la tasa oficial del BCV.
Funciona como app instalable en el celular (PWA), sin pasar por Play Store / App Store.

## Qué hace
- Trae la tasa oficial del BCV (USD/VES) desde DolarAPI al abrir, al volver a la app y cada 30 min.
- Calcula por producto: costo en Bs, PVP sin IVA (con margen opcional), IVA y precio final.
- IVA configurable (16 % por defecto) e IGTF 3 % opcional.
- Agrega/elimina productos. Todo se guarda en el dispositivo (localStorage).
- Cachea la última tasa y el shell para uso offline.

## Archivos
- `index.html` — la app completa (HTML + CSS + JS, sin build).
- `manifest.webmanifest` — metadata de la PWA.
- `sw.js` — service worker (offline).
- `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` — íconos.

> Importante: el service worker y "Agregar a pantalla de inicio" solo funcionan sobre **HTTPS**.
> GitHub Pages y Vercel ya sirven HTTPS, así que basta con desplegar.

## Opción A — GitHub Pages
1. Crea un repo (ej. `costos-bcv`) y sube estos archivos a la raíz.
2. Settings → Pages → Source: `Deploy from a branch` → branch `main`, carpeta `/ (root)`.
3. Espera ~1 min. Tu URL será `https://TU_USUARIO.github.io/costos-bcv/`.

## Opción B — Vercel (drag & drop)
1. vercel.com → Add New → Project → importa el repo, o arrastra la carpeta.
2. Sin framework, sin build command. Deploy.
3. Te da una URL HTTPS lista.

## Instalar en el celular
- **Android (Chrome):** abre la URL → menú ⋮ → "Agregar a pantalla de inicio" / "Instalar app".
- **iPhone (Safari):** abre la URL → botón Compartir → "Agregar a inicio".

## Cambiar la fuente de la tasa (opcional)
En `index.html`, dentro de `fetchRate()`, se usa:
`https://ve.dolarapi.com/v1/dolares/oficial`  (campo `promedio`).
Alternativa: pyDolarVenezuela (`https://pydolarve.org/`) si algún día necesitas cambiar de proveedor.

## Idea de mejora (tu stack)
Si quieres notificación push cuando el BCV cambie, un workflow de **n8n** con cron diario
(~4:40 p.m. Caracas) puede consultar la API y avisarte por Telegram/Gmail cuando `promedio` cambie.
