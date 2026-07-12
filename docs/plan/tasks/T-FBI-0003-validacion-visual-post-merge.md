---
id: T-FBI-0003
title: "Validación visual del informe tras el merge de las dos líneas de trabajo"
type: qa
weight: 3
version: ""
status: in_progress
effort_unit: h
estimated_effort: 0
remaining_effort: 0
actual_effort: 0
created_at: 2026-07-12
updated_at: 2026-07-12
original_ref: ""
---

# T-FBI-0003: Validación visual del informe tras el merge de las dos líneas de trabajo

## 🎯 Objetivo de Negocio
El merge `decbd2e` reconcilió dos líneas divergentes del informe (ALERTA de pérdida bloqueada + formato condicional vs. Valor de Adquisición + limpieza de medidas + columnas nuevas), unificando además los esquemas PBIR a 2.8.0 y resolviendo ~90 conflictos en visuales. La resolución fue mayormente automática (esquema→entrante, layout/filtros→estado actual), así que hace falta una pasada visual deliberada para confirmar que no quedó nada roto o perdido.

## 📍 Contexto Técnico
- Merge: `decbd2e` (+ fix `d5f3fd2` por columnas duplicadas Ticker/Ingreso/Dividendos en `Saldo.tmdl` que impedían abrir el modelo).
- Zonas de mayor riesgo: página **Transacciones** (tabla principal `d0707eca`: se unieron a mano la columna ALERTA y las medidas Impuestos Retenidos), página **Saldo** (filtros conservados del estado actual), **Resumen** e **Inversiones** (selecciones de años/período), y las medidas de **Valor Adquisición** (Medidas Transacciones / Medidas IRPF).

## 📋 Criterios de Aceptación (Nivel Máster)
- [ ] **CA-M-1:** El informe abre y refresca sin errores desde `C:\SW\Finanzas\financeBI` con el Python de `C:\SW\Finanzas\pyportfolio\.venv`.
- [ ] **CA-M-2:** Página Transacciones: la columna ALERTA con su formato condicional en rojo Y las columnas de Impuestos Retenidos Extranjero/Local conviven en la tabla.
- [ ] **CA-M-3:** Las medidas de Valor de Adquisición devuelven valores coherentes en los visuales que las usan.
- [ ] **CA-M-4:** Repaso página a página (Saldo, Movimientos, Inversiones, Resumen, Gastos No Computados, Impuestos): sin visuales rotos, campos huérfanos ni filtros perdidos relevantes.

## 🛠 Tareas de Componente
- _(pendiente de descomposición técnica)_
