---
id: T-FBI-0005
title: "Eliminar medidas obsoletas del modelo Transacciones"
type: infra
weight: 1
version: ""
status: backlog
effort_unit: h
estimated_effort: 0
remaining_effort: 0
actual_effort: 0
created_at: 2026-07-13
updated_at: 2026-07-13
original_ref: ""
---

# T-FBI-0005: Eliminar medidas obsoletas del modelo Transacciones

## 🎯 Objetivo de Negocio
El modelo semántico arrastra cinco medidas de la tabla `Transacciones` que ya no reflejan la lógica vigente y no se usan en ningún informe. Mantenerlas confunde al mantenedor (aparecen como opciones válidas al construir visuales), infla el modelo y riesga que alguien las reutilice por error con cálculos caducados. Retirarlas deja el catálogo de medidas limpio y alineado con la lógica actual.

## 🗑 Medidas a retirar
- `Transacciones - Beneficio Antes Transacción`
- `Transacciones - Beneficio Bruto Venta Total`
- `Transacciones - Beneficio Tras Transacción`
- `Transacciones - Coste Participaciones Vendidas Total`
- `Transacciones - Coste Participaciones Vendidas Transaccion`

## 📍 Contexto Técnico
- Definición esperada en `reports/Estado Financiero.SemanticModel/definition/tables/Medidas Transacciones.tmdl` (archivo estaba bloqueado al crear la tarea; confirmar ubicación exacta al abordarla).
- Antes de borrar hay que verificar que **ninguna** medida sobreviviente ni ningún visual (`reports/Estado Financiero.Report/definition/pages/**/visuals/**/visual.json`) las referencia, para no romper informes en silencio.

## 📋 Criterios de Aceptación (Nivel Máster)
- [ ] **CA-M-1:** Las cinco medidas ya no existen en el modelo semántico (`.tmdl`).
- [ ] **CA-M-2:** No queda ninguna referencia a ellas en otras medidas ni en las definiciones de visuales del informe.
- [ ] **CA-M-3:** El informe abre y refresca sin errores tras la eliminación.

## 🛠 Tareas de Componente
- _(pendiente de descomposición técnica)_
