---
id: T-FBI-0001
title: "Revisar el espejo M frente a traspasos registrados con dos filas (Fase C)"
type: infra
weight: 4
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

# T-FBI-0001: Revisar el espejo M frente a traspasos registrados con dos filas (Fase C)

## 🎯 Objetivo de Negocio
Con el soporte de traspasos fondo→fondo en pyportfolio se adoptó la convención de registrar **ambas filas** del traspaso en el Excel (salida en el fondo origen y entrada en el destino, enlazadas por `ID Transacción Espejo`). La query M `Transacciones Power Query` genera además "transacciones espejo" automáticas. Hay que verificar que ambas mecánicas no colisionan: un espejo espurio duplicaría participaciones o importes y falsearía FIFO/IRPF.

## 📍 Contexto Técnico
- Query compartida `Transacciones Power Query` en `reports/Estado Financiero.SemanticModel/definition/expressions.tmdl`: paso `#"[Limpiar] Transacción Espejo"` (invierte Compra↔Venta, anula participaciones) y dedup por `ID Transacción Espejo` / `#"[Row] Duplicados quitados - General"`.
- El pipeline Python ya ignora espejos con participaciones nulas (el emparejamiento del pre-pass solo considera filas con participaciones ≠ 0), pero la interacción con la dedup del M **no está verificada** con traspasos de dos filas reales.

## 📋 Criterios de Aceptación (Nivel Máster)
- [ ] **CA-M-1:** Con un traspaso fondo→fondo registrado con sus dos filas reales, la tabla `Transacciones` resultante no contiene filas espejo espurias ni duplicados de ninguna de las dos.
- [ ] **CA-M-2:** Los casos preexistentes (dividendos con espejo, movimientos con contraparte de efectivo) siguen generando exactamente las mismas filas que antes.
- [ ] **CA-M-3:** Existe al menos un caso en el dataset de test (`data/demo` o `Test Data`) que cubre un traspaso de dos filas atravesando el espejo + dedup.

## 🛠 Tareas de Componente
- _(pendiente de descomposición técnica)_
