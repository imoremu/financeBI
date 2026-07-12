---
id: T-FBI-0002
title: "Reducir el logging de los scripts Python.Execute (DEBUG → WARNING, rotación)"
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

# T-FBI-0002: Reducir el logging de los scripts Python.Execute (DEBUG → WARNING, rotación)

## 🎯 Objetivo de Negocio
El log de los scripts de `Python.Execute` creció hasta **386 MB** (`C:\Users\Public\Log\logfile.log`), degradando seriamente el rendimiento del refresco (el atasco se manifestó como "Power BI colgado"). El nivel y el destino del log se configuran en el propio código M del informe, por lo que la corrección pertenece a este repo (complementa a T-PYP-0003 en pyportfolio).

## 📍 Contexto Técnico
- `reports/Estado Financiero.SemanticModel/definition/tables/Transacciones.tmdl` (partición `Transacciones`) e `IRPF.tmdl`: el string de `Python.Execute` hace `logging.basicConfig(filename='C:\\Users\\Public\\Log\\logfile.log', level=logging.DEBUG/INFO/WARNING ...)` según la tabla.
- Agravante: el mecanismo de research/reintentos de `pydatastudio` re-loguea el mismo traceback decenas de veces (parte pyportfolio, ver T-PYP-0003).

## 📋 Criterios de Aceptación (Nivel Máster)
- [ ] **CA-M-1:** Todos los `Python.Execute` del modelo configuran `level=logging.WARNING` (o superior) de forma consistente.
- [ ] **CA-M-2:** El log usa rotación (p.ej. `RotatingFileHandler` vía `pyportfolio.logging_setup`) o, como mínimo, se documenta el truncado periódico en `Update.readme`.
- [ ] **CA-M-3:** Un refresco completo con datos reales no hace crecer el log más de unos pocos MB.

## 🛠 Tareas de Componente
- _(pendiente de descomposición técnica)_
