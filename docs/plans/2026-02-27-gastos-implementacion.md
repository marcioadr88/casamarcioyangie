# Gastos Marcio y Angie - Plan de Implementación Completo

> **Para Claude:** REQUIRED SUB-SKILL: Usar superpowers:executing-plans para implementar este plan tarea por tarea.

**Objetivo:** Implementar una app web mobile-first para rastrear gastos del hogar compartidos entre Marcio y Angie.

**Arquitectura:** MVP con un único archivo HTML + localStorage (rápido), luego migración a Vite + Firebase Firestore.

**Tech Stack:** HTML5, CSS3, Vanilla JavaScript, Firebase Firestore, Vite

---

## FASE 1: MVP Básico con localStorage

### Tarea 1: HTML Base con Estructura Mobile-First
- Reemplazar index.html con estructura completa
- Incluir Google Fonts, variables CSS, layout flexbox
- Crear 3 contenedores para tabs y modal para formulario

### Tarea 2: Funciones Clave de Utilidad
- Implementar fmt(n) para formatear montos como "Gs. X.XXX"
- Implementar getMonthEntries() para filtrar por mes
- Implementar getMonthName() y getWeekday() para nombres en español

### Tarea 3: Persistencia con localStorage
- Crear función guardar() que serializa entries a JSON
- Crear función cargar() que deserializa desde localStorage
- Llamar cargar() al iniciar, guardar() después de cambios

### Tarea 4: Sistema de Renderizado Base
- Implementar render() que despacha según currentTab
- Crear funciones vacías renderResumen(), renderMovimientos(), renderDeudas()
- Agregar event listeners para botones de tab

### Tarea 5: Formulario Modal para Agregar Entradas
- Crear HTML del formulario con selectores de tipo, categoría, monto, usuario
- Implementar abrirModal() y cerrarModal()
- Agregar soporte para categoría personalizada ("otro")

### Tarea 6: Función para Guardar Entrada
- Implementar guardarEntrada() con validación de monto
- Crear objeto con id (timestamp), type, category, amount, who, description, date
- Agregar a entries array, guardar a localStorage, renderizar

### Tarea 7: Renderizar Tab Movimientos
- Implementar entryHtml(e) que genera tarjeta de entrada
- Mostrar todas las entradas del mes, ordenadas por fecha descendente
- Agregar botones de editar y eliminar

### Tarea 8: Renderizar Tab Resumen
- Mostrar totales: total gasto, Marcio, Angie
- Crear gráfico de barras por categoría
- Mostrar últimas 3 entradas
- Agregar navegación de meses (anterior/siguiente)

### Tarea 9: Renderizar Tab Deudas
- Filtrar deudas por estado (pendiente/pagada)
- Mostrar total de deuda pendiente
- Agregar botón para marcar como pagada/pendiente

### Tarea 10: Estilos CSS Finales y Responsive
- Completar todos los estilos CSS inline
- Hacer responsive para mobile (320px+)
- Pulir UX con transiciones y estados de botones

---

## FASE 2: Migración a Vite + Firebase (Después)

### Tarea 11: Configurar Vite
- Crear package.json, vite.config.js
- Mover index.html a src/index.html

### Tarea 12: Separar en módulos
- Crear src/main.js (state + render)
- Crear src/firebase.js (Firestore integration)
- Crear src/ui.js (event handlers)
- Crear src/style.css (estilos separados)

### Tarea 13: Firebase Firestore
- Reemplazar localStorage con Firestore
- Colección: "entries" con documentos por entrada
- Autenticación: usuario elige nombre una vez

### Tarea 14: Sincronización en Tiempo Real
- Usar onSnapshot() en entries collection
- Actualizar estado automáticamente cuando hay cambios
- Implementar para los dos usuarios

---

## Nota de Seguridad (Tarea 7-9)
En renderizado: usar textContent para contenido de usuario, sanitizar descripciones
que puedan venir de entrada del usuario para evitar XSS. Considerar usar DOMPurify
si es necesario.

---

## Commits Esperados

1. feat: estructura HTML base con tabs y modal
2. feat: agregar funciones de utilidad
3. feat: persistencia con localStorage
4. feat: sistema de renderizado
5. feat: formulario modal
6. feat: guardar entradas
7. feat: tab Movimientos
8. feat: tab Resumen
9. feat: tab Deudas
10. feat: estilos CSS finales
11. feat: setup Vite
12. feat: separar en módulos
13. feat: integración Firebase Firestore
14. feat: sincronización en tiempo real

