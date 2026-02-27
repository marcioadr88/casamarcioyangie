# CLAUDE.md

Este archivo guía a Claude Code (claude.ai/code) al trabajar con el código de este repositorio.

## Idioma

Toda la comunicación, comentarios en código, nombres de variables en español, mensajes de commit, documentación y respuestas al usuario deben estar en **español**.

## Descripción del proyecto

**Gastos Marcio y Angie** — App web mobile-first para rastrear gastos del hogar compartidos en tiempo real entre Marcio y Angie.

En producción: `gastosmarcioyangie.web.app`

## Arquitectura actual

La app es un **único archivo HTML** (`index.html`) con todo el CSS y JS inline. Sin herramientas de build, sin frameworks, sin package manager.

- **Almacenamiento**: localStorage (clave: `casa_entries`) — entradas guardadas como array JSON
- **Estado**: Variables globales JS (`entries`, `currentType`, `currentCat`, `currentWho`, `currentTab`, `viewMonth`, `viewYear`)
- **Renderizado**: Manipulación manual del DOM con `innerHTML` y template literals
- **Generación de IDs**: `Date.now().toString()`

## Arquitectura planeada (aún no implementada)

Migrar a:
- **Build tool**: Vite
- **Base de datos**: Firebase Firestore con `onSnapshot` para sincronización en tiempo real
- **Hosting**: Firebase Hosting
- **Estructura**: Separar en `src/main.js`, `src/firebase.js`, `src/ui.js`, `src/style.css`

## Reglas de dominio

- **Usuarios**: Solo Marcio y Angie. Sin sistema de auth — el usuario elige su nombre una vez, guardado en localStorage.
- **Moneda**: Guaraníes paraguayos (Gs.) — solo enteros, sin decimales. Formato: `Gs. 1.234.567`
- **Tipos de entrada**: `gasto`, `ahorro`, `deuda` (se puede marcar como `pagada`)
- **Categorías por defecto**: `hogar` 🏠 | `comida` 🛒 | `servicios` 💡 | `transporte` 🚌 | `salud` 💊 | `otro` 📦
- **Categorías dinámicas**: Al seleccionar "otro", el usuario puede ingresar un nombre personalizado con emoji opcional (usar emoji genérico por defecto si no provee uno)
- **Pagador por defecto**: Marcio
- **Tabs**: Resumen (totales + barras por categoría + últimos 3), Movimientos (lista completa), Deudas (pendientes/pagadas)
- **Navegación de meses**: `cycleMonth()` actualmente solo retrocede

## Sistema de diseño

- **Mobile-first**, optimizado para iPhone Safari, compatible con PWA
- **Paleta**: `--bg: #F5F0E8`, `--accent: #C94F2C` (rojo), `--green: #2C7A4B`, `--gold: #E8A020`, `--ink: #1A1208`
- **Tipografía**: DM Serif Display (títulos) + DM Sans (cuerpo) — cargadas desde Google Fonts
- **Sin librerías de UI externas**
- **Referencia de diseño**: `referencia.html` (si existe) muestra el diseño inicial aprobado

## Patrones clave

- `fmt(n)` formatea montos como `Gs. X.XXX`
- `getMonthEntries()` filtra el array de entradas por `viewMonth`/`viewYear`
- `entryHtml(e)` genera el HTML de una tarjeta de entrada (usado en Resumen y Movimientos)
- `render()` despacha a `renderResumen()`, `renderMovimientos()` o `renderDeudas()` según `currentTab`
- El formulario modal usa estado global (`currentType`, `currentCat`, `currentWho`) seteado por handlers de botones
