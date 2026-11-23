# PROJECT_STATUS.md

> Estado vivo del proyecto. Actualizar al cerrar cada sesión de trabajo, cambio importante, decisión o release.

## Estado actual

- **Proyecto:** Universal AI Engineering Kit para automatizaciones y aplicaciones en Google Apps Script.
- **Estado del kit:** documentación y plantillas prácticas consolidadas; siguiente etapa recomendada: convertir las reglas en herramientas ejecutables y validadores automáticos.
- **Última actualización:** 2026-11-23
- **Versión objetivo:** v3 — Kit ejecutable (propuesta; aún no implementada).

## Objetivo

Crear un kit reutilizable que permita a una IA y a un desarrollador diseñar, implementar, probar, auditar y operar proyectos de Apps Script de forma consistente, segura y mantenible.

## Componentes existentes

- `AGENTS.md`: reglas operativas para la IA y el desarrollo.
- `README.md`: guía de entrada y uso del kit.
- Especificación maestra: arquitectura, seguridad, calidad, operación y criterios de decisión.
- Documentación práctica sobre estructura, workflow, patrones, anti-patrones, configuración, concurrencia, límites de ejecución, integración, frontend/backend, pruebas, seguridad HTML y despliegue.
- Plantillas de tareas iniciales y documentos operativos.

## Cobertura de ingeniería

- Arquitectura modular y separación de responsabilidades.
- Configuración por entorno y manifiestos.
- Evaluación de impacto y riesgos antes de cambios.
- OAuth scopes y privilegio mínimo.
- Identidad, autenticación y autorización.
- Seguridad HTML y prevención de XSS.
- Estado, caché, propiedades y locks.
- Cuotas, runtime, límites de ejecución y concurrencia.
- Triggers: inventario, ownership, idempotencia y recuperación.
- Logs estructurados, trazabilidad y alertas.
- Tests, mocks, fixtures y limpieza.
- Git, `clasp`, entornos DEV/TEST/PROD y despliegue controlado.
- Health Score y checklist pre-deploy.
- Documentación proporcional al tamaño del proyecto.

## Pendientes prioritarios

### P0 — Kit ejecutable

- [ ] Crear un runner de pruebas real para archivos `.gs`.
- [ ] Añadir asserts, mocks, fixtures y reporte PASS/FAIL.
- [ ] Crear validadores automáticos para estructura, manifiesto, scopes, secretos y patrones peligrosos.
- [ ] Añadir comandos de auditoría reproducibles.
- [ ] Definir salida de CI que pueda bloquear un deploy por fallos críticos.

### P1 — Flujo de desarrollo

- [ ] Plantillas funcionales de `clasp` y configuración por entorno.
- [ ] Workflow de GitHub Actions ajustado a secretos y despliegue seguro.
- [ ] Ejemplo mínimo DEV → TEST → PROD con aprobación de producción.
- [ ] Script de backup/export y comprobación previa al despliegue.

### P2 — Observabilidad y operación

- [ ] Implementar formato de logs común y correlación de ejecuciones.
- [ ] Automatizar Health Report / Health Score.
- [ ] Implementar alertas configurables con deduplicación y control de ruido.
- [ ] Revisar recuperación de triggers y ejecuciones fallidas.

## Decisiones y criterios

- Mantener el kit agnóstico y reusable; evitar reglas duplicadas o documentación inflada.
- Preferir controles automatizados a reglas que solo se recuerdan manualmente.
- Los cambios sensibles y el despliegue a producción requieren revisión/aprobación explícita.
- No asumir que la IA puede ejecutar acciones externas o acceder a secretos sin permisos.
- Priorizar simplicidad proporcional al proyecto; no imponer arquitectura pesada a scripts pequeños.

## Riesgos / notas

- Las guías son recomendaciones; cada proyecto debe validar su contexto, cuotas, scopes y requisitos.
- No presentar todavía los validadores o el runner como implementados: están en la lista de pendientes.
- Mantener este documento actualizado con cambios verificables, no con planes aspiracionales.

## Registro de sesión

| Fecha | Cambio / resultado | Estado |
|---|---|---|
| 2026-11-23 | Consolidación de documentación práctica, arquitectura, seguridad, pruebas, despliegue y operación; se propone la siguiente fase ejecutable. | Documentación consolidada |
