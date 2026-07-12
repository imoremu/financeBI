---
id: T-FBI-0004
title: "Documentar y verificar el contrato de columnas pyportfolio ↔ informe"
type: infra
weight: 2
version: ""
status: backlog
effort_unit: h
estimated_effort: 0
remaining_effort: 0
actual_effort: 0
created_at: 2026-07-12
updated_at: 2026-07-12
original_ref: ""
---

# T-FBI-0004: Documentar y verificar el contrato de columnas pyportfolio ↔ informe

## 🎯 Objetivo de Negocio
Las queries M del informe dependen de los nombres exactos de las columnas que devuelve `pyportfolio.scripts.powerquery.pq_get_fifo_irpf_data` / `pq_get_irpf_report`. Un renombrado en Python (caso real: `GPP` ↔ `GPP Allowable`) rompe el informe en silencio y solo se descubre al refrescar. Documentar el contrato (y verificarlo donde sea posible) acorta el diagnóstico y evita sorpresas al actualizar pyportfolio.

Nota de alcance: el fallo real que motivó esto fue de **sincronización de versiones entre equipos**, ya mitigado con git como fuente de verdad. Esta tarea es de prioridad baja; es un cinturón de seguridad complementario.

## 📍 Contexto Técnico
- Consumidores del contrato: pasos `Text.Replace` / `TransformColumnTypes` / `RenameColumns` en `tables/Transacciones.tmdl`, `tables/IRPF.tmdl` (y `Saldo` indirectamente).
- Productores: `pyportfolio/scripts/powerquery/*.py` (columnas definidas en `pyportfolio/columns.py`).

## 📋 Criterios de Aceptación (Nivel Máster)
- [ ] **CA-M-1:** Existe un documento (en este repo o en pyportfolio, enlazado desde ambos) con la lista de columnas que cada entry point devuelve y qué pasos M las consumen.
- [ ] **CA-M-2:** pyportfolio incluye un test que fija ese conjunto de columnas de salida (falla si un renombrado lo cambia sin actualizar el contrato).
- [ ] **CA-M-3:** El README de actualización (`Update.readme`) referencia el contrato como paso a revisar al actualizar pyportfolio.

## 🛠 Tareas de Componente
- _(pendiente de descomposición técnica)_
