# AI ENGINEERING KIT
## Especificación integral para ingeniería de automatizaciones con Google Apps Script

**Estado:** Especificación inicial consolidada  
**Idioma:** Español  
**Plataforma:** Google Apps Script y Google Workspace  
**Versionado:** GitHub + historial de versiones de Apps Script  
**Uso:** Contexto de IA, ingeniería, auditoría, implementación y mantenimiento

---

## 0. Cómo utilizar este documento

Este archivo concentra la visión, decisiones, estándares, requisitos, estructura y plan de construcción del AI Engineering Kit. Sirve como contexto reutilizable para una IA o desarrollador sin depender del historial de conversación.

Es una **especificación de referencia**. No significa que todas las capacidades descritas estén implementadas. Cada proyecto debe evaluar qué controles necesita, su viabilidad y cuáles están efectivamente configurados.

### Jerarquía documental

1. `AGENTS.md`: reglas globales para IA y desarrolladores.
2. `.ai/safety.md`: seguridad, límites de autonomía y aprobaciones.
3. `.ai/workflow.md`: metodología de trabajo.
4. `.ai/modes.md`: modos de actuación.
5. `.ai/config.md`: configuración del agente y proyecto.
6. `docs/`: especificaciones técnicas y operativas.
7. `ai-tasks/`: procedimientos reutilizables.

Ningún documento subordinado puede contradecir las reglas globales de seguridad, autorización, integridad y aprobación.

### Etiquetas de decisiones

- **CONFIRMADO:** decisión acordada.
- **PROPUESTA:** recomendación que debe validarse.
- **CONFIGURABLE:** valor que cada proyecto debe definir.
- **PENDIENTE:** decisión que requiere información.
- **CONDICIONAL:** solo se implementa si escala, riesgo o viabilidad lo justifican.

---

## 1. Visión y objetivo

Construir un estándar reutilizable de ingeniería para automatizaciones de Google Apps Script que permita analizar, diseñar, implementar, probar, auditar, optimizar, desplegar y mantener proyectos de diferentes tamaños y criticidad.

El kit será:
- Metodología de ingeniería.
- Estándar técnico para desarrolladores.
- Sistema de instrucciones para agentes de IA.
- Guía de auditoría y diagnóstico.
- Marco de seguridad y control de cambios.
- Marco de calidad, rendimiento y observabilidad.
- Base documental para proyectos nuevos y existentes.

### Alcance de servicios

- Google Sheets, Docs, Forms, Drive, Gmail y Calendar.
- Google Workspace APIs y Advanced Google Services.
- APIs REST externas y webhooks.
- Librerías de Apps Script.
- Integraciones con Node.js u otros servicios cuando se justifique.
- GitHub y `clasp` para control de código y sincronización cuando aplique.

### Tipos de proyectos

Scripts vinculados e independientes, web apps (`doGet`/`doPost`), automatizaciones de Forms, activadores, complementos, proyectos con múltiples archivos `.gs`/`.html`, procesamiento masivo, integraciones externas, sistemas multiusuario y sistemas críticos.

### Principios fundamentales

1. Comprender antes de modificar.
2. Seguridad desde el diseño.
3. Mínimo privilegio.
4. Integridad de datos prioritaria.
5. Medir antes de optimizar.
6. Complejidad proporcional.
7. Trazabilidad de operaciones importantes.
8. Recuperación ante fallos.
9. Documentación clara.
10. Separar hechos, inferencias y supuestos.
11. No afirmar pruebas, despliegues o verificaciones que no se realizaron.
12. Preservar funcionalidad y analizar dependencias antes de refactorizar.

### Complejidad proporcional

Utilizar la solución más sencilla que satisfaga los requisitos de forma segura. No crear arquitectura empresarial para un script pequeño, agregar servicios externos sin justificación, abstraer en exceso, implementar colas o dashboards innecesarios ni optimizar prematuramente.

La simplicidad no puede eliminar controles necesarios de seguridad, autorización, trazabilidad o integridad.

---

## 2. Perfil de actuación de la IA

### Autonomía

**CONFIRMADO:** la IA puede analizar, diseñar, implementar, refactorizar, probar, documentar y desplegar autónomamente cuando se cumplan los controles.

Puede inspeccionar proyectos, inventariar dependencias, detectar riesgos, desarrollar, ejecutar validaciones, generar informes, actualizar documentación y preparar despliegues.

### Acciones que requieren autorización expresa

Detenerse antes de aplicar cambios de producción que impliquen:
- Agregar, quitar o ampliar scopes OAuth.
- Cambiar identidad o permisos de ejecución en operaciones sensibles.
- Cambiar propietario o supuestos de ejecución de activadores.
- Eliminar o transformar datos de forma irreversible.
- Cambiar esquemas críticos.
- Debilitar seguridad o autorización.
- Riesgo alto/crítico.
- Acciones cuyo impacto no pueda delimitarse o revertirse.

Antes de solicitar aprobación, explicar cambio, motivo, impacto, riesgo, reversibilidad, pruebas, respaldo y autorización requerida. Las pruebas no sustituyen la autorización.

### Transparencia

Distinguir claramente entre comprobado, inferido, estimado, no verificado y bloqueado por permisos o información. No declarar seguro, probado, desplegado o monitoreado un sistema sin evidencia.

---

## 3. Clasificación de proyectos

| Nivel | Nombre | Características | Controles mínimos |
|---|---|---|---|
| 1 | Simple | Una tarea, pocos datos, bajo impacto | Funciones claras, validación, errores, logs y prueba básica |
| 2 | Intermedio | Varias etapas, servicios o activadores | Modularidad, logs estructurados, pruebas, inventario de activadores y medición |
| 3 | Complejo | Flujos múltiples, integraciones, usuarios o concurrencia | Arquitectura, permisos, idempotencia, recuperación, regresión, métricas y alertas |
| 4 | Crítico/empresarial | Datos sensibles, alto impacto o continuidad exigente | Riesgo formal, ambientes separados, auditoría, recuperación probada y releases controlados |

La IA debe justificar la clasificación y elevarla ante incertidumbre o impacto.

---

## 4. Evaluación de riesgo y viabilidad

Analizar pérdida, corrupción o exposición de datos; operaciones incorrectas; duplicados; acceso no autorizado; fallos de activadores; agotamiento de cuotas; APIs externas; recuperación; consecuencias legales, contractuales, reputacionales y operativas.

### Niveles de riesgo

| Nivel | Significado | Respuesta |
|---|---|---|
| Bajo | Impacto limitado, recuperación sencilla | Controles normales |
| Medio | Impacto perceptible, recuperación acotada | Pruebas y monitoreo específico |
| Alto | Impacto importante en datos, operación o seguridad | Análisis de impacto, pruebas reforzadas, respaldo y aprobación para cambios críticos |
| Crítico | Impacto severo, irreversible o no controlado | Bloquear hasta reducir riesgo y obtener autorización |

Evaluar viabilidad de Apps Script considerando volumen, frecuencia, duración, cuotas, concurrencia, latencia, disponibilidad, seguridad, integraciones, costos, mantenimiento, propiedad y recuperación. Si no es adecuado, proponer alternativa o arquitectura híbrida explicando límites y costos.

---

## 5. Arquitectura técnica

Separar responsabilidades, adaptando archivos a la escala real del proyecto.

### Capas

1. **Configuration:** constantes, ambientes, parámetros, IDs, umbrales y feature flags.
2. **Orchestration:** coordinación de procesos y flujos.
3. **Business Logic:** reglas, cálculos y transformaciones.
4. **Validation:** entradas, esquemas, formatos y consistencia.
5. **Security:** identidad, autorización y operaciones sensibles.
6. **Data Access:** lectura y escritura de datos.
7. **Integration Services:** Workspace, APIs y webhooks.
8. **Execution Management:** activadores, locks, colas, checkpoints y estado.
9. **Observability:** logs, métricas, auditoría, alertas e informes.
10. **Testing & Quality:** pruebas, fixtures, aserciones y criterios de aceptación.

### Capacidades complementarias (condicionales)

Dependency Management, State Management, Idempotency Engine, Recovery Engine, Queue Management, Schema Validation, Change Detection, Configuration Management, Notification Engine, Cost & Quota Control, Documentation Engine y Deployment Control.

### Reglas de separación

- La lógica de negocio no debe depender innecesariamente de menús o activadores.
- Centralizar acceso a datos cuando existan patrones repetidos.
- Evitar configuración dispersa.
- Aplicar autorización en operaciones sensibles, no solo en UI.
- Evitar logs con datos confidenciales.
- Aislar pruebas de producción.

---

## 6. Estructura de código sugerida

```text
src/
├── Config.gs
├── Main.gs
├── Orchestrator.gs
├── BusinessLogic.gs
├── Repositories.gs
├── Validators.gs
├── Security.gs
├── Logger.gs
├── Metrics.gs
├── Triggers.gs
├── Recovery.gs
└── Notifications.gs

tests/
├── Tests.gs
├── TestFixtures.gs
├── TestHelpers.gs
└── TestResults.gs
```

Es una referencia, no una obligación. Crear módulos solo cuando aporten claridad.

### Reglas de código

- Runtime V8.
- Funciones pequeñas y responsables.
- Configuración separada de lógica.
- Constantes centralizadas.
- Validación de entradas y salidas.
- Errores explícitos.
- Evitar duplicación.
- JSDoc en funciones importantes.
- No incrustar secretos.
- Nombres claros y consistentes.
- Documentar efectos secundarios.

---

## 7. Apps Script y servicios

### `appsscript.json`

Revisar runtime, zona horaria, scopes, logging, librerías, servicios avanzados y configuración de web app/add-on cuando aplique.

No asumir que una API está habilitada solo porque exista.

### Workspace

Para Sheets, Docs, Forms, Drive, Gmail y Calendar:
- Confirmar IDs y permisos.
- Validar antes de escribir o enviar.
- Evitar llamadas repetidas.
- Utilizar operaciones por lote.
- Manejar recursos movidos, eliminados o inaccesibles.
- Respetar cuotas.
- Documentar efectos secundarios.

### APIs y webhooks

Validar URL, método, payload y respuesta; limitar reintentos; usar backoff para errores transitorios; no repetir operaciones no idempotentes a ciegas; proteger tokens; validar autenticidad de webhooks si el proveedor lo permite; registrar resultados sin exponer payloads sensibles.

---

## 8. OAuth, scopes, identidad y permisos

Obligatorio para servicios protegidos.

### Scopes OAuth

1. Identificar servicios y métodos usados.
2. Determinar scopes mínimos.
3. Comparar scopes declarados con uso real.
4. Explicar scopes amplios o sensibles.
5. Registrar cambios en changelog y documentación.
6. Evaluar impacto en autorización y despliegue.
7. Verificar permisos de la cuenta ejecutora.

No agregar scopes amplios para ocultar errores. Cambios de scopes requieren autorización expresa.

### Identidades

Distinguir:
- Usuario que inicia la acción.
- Usuario activo, si es identificable.
- Usuario efectivo bajo cuya autorización corre.
- Propietario del proyecto.
- Propietario de archivos y recursos.
- Cuenta que creó activadores instalables.

No asumir que `Session.getActiveUser().getEmail()` siempre devuelve un correo; depende del contexto y políticas.

En operaciones sensibles, verificar identidad mediante método apropiado, separar autenticación de autorización, aplicar mínimo privilegio y denegar por defecto si no se puede verificar. Un control visual no es seguridad.

### Verificación de usuarios

Definir roles, acciones permitidas, recursos, condiciones de autorización, tratamiento de identidad desconocida, revocación y auditoría.

Roles sugeridos (configurables): Administrador, Operador, Usuario autorizado, Consulta. No asumir que están definidos.

---

## 9. Activadores y propiedad de ejecución

Inventariar activadores simples e instalables. Registrar, cuando sea posible:
- ID y función manejadora.
- Tipo de evento/horario.
- Proyecto y ambiente.
- Creador, propietario o identidad efectiva verificable.
- Scopes y permisos.
- Fecha de creación y última verificación.
- Comportamiento esperado y manejo de fallos.

Reglas:
- No asumir que transferir propiedad transfiere activadores.
- Activadores instalables se ejecutan con autorización de la cuenta que los creó.
- Detectar duplicados antes de crear.
- Instalación y reparación idempotentes.
- Verificar inventario tras cambios.
- Documentar salida, suspensión o pérdida de acceso de cuenta creadora.
- No borrar/recrear activadores de producción a ciegas.

Capacidades deseadas: inventario automático, detección de duplicados, identificación de propietario/ejecutor cuando sea posible, validación de permisos, monitoreo de última ejecución, detección de fallos, reconstrucción controlada y alertas de activadores inactivos.

---

## 10. Rendimiento, cuotas y tiempo de ejecución

Todo proceso material o recurrente debe tener presupuesto de ejecución.

### Medir

Duración total y por etapa; llamadas a servicios cuando sean medibles; registros leídos, procesados, modificados, omitidos y fallidos; tamaño de lotes; reintentos; espera por locks; duración de APIs externas; consumo estimado de cuotas si es confiable.

### Optimizar

1. Medir línea base.
2. Leer rangos a arrays y procesar en memoria cuando convenga.
3. Escribir por lotes.
4. Evitar lecturas repetidas.
5. Usar caché solo con estrategia de frescura/invalidez.
6. Limitar loops y lotes.
7. Evitar `SpreadsheetApp.flush()` innecesario.
8. Evitar logs excesivos en loops grandes.
9. Paginación y procesamiento por bloques.
10. Checkpoints y continuación.
11. `LockService` cuando exista riesgo de concurrencia.
12. Idempotencia para prevenir duplicados.
13. Reintentos limitados con backoff y jitter cuando aplique.
14. Medir tiempo transcurrido y detenerse con presupuesto conservador; no asumir un indicador universal fiable de tiempo restante.
15. Verificar límites y cuotas actuales, no depender de cifras antiguas como universales.

Informes de optimización deben comparar antes/después y describir condiciones de prueba.

---

## 11. Concurrencia, idempotencia y resiliencia

Implementar según necesidad:
- Estado explícito.
- Operaciones idempotentes.
- Locks.
- Checkpoints.
- Procesamiento por bloques.
- Reintentos limitados.
- Backoff exponencial.
- Registro de elementos fallidos.
- Continuación segura.
- Conciliación.
- Compensación o reversión viable.

### Recuperación

1. Identificar ejecución fallida y último checkpoint confirmado.
2. Determinar efectos secundarios ya realizados.
3. Revisar escrituras parciales y duplicados.
4. Reanudar solo si es seguro.
5. Conciliar o solicitar intervención si no lo es.
6. Verificar integridad tras recuperación.
7. Registrar intento y resultado.
8. Notificar según severidad.

No prometer rollback transaccional si el servicio no lo soporta.

---

## 12. Integridad de datos

Controlar:
- Encabezados faltantes, renombrados o reordenados.
- Columnas inesperadas.
- Tipos y formatos.
- Valores permitidos y rangos.
- Duplicados según clave de negocio.
- Referencias entre registros.
- Cambios estructurales.
- Comparación antes/después.
- Sobrescrituras accidentales.
- Versionado de esquemas y migraciones.
- Conciliación de operaciones parciales.
- Reversión/compensación viable.

En Sheets, distinguir valores mostrados, valores sin formato y fórmulas. Prevenir inyección de fórmulas al escribir entradas no confiables.

---

## 13. Seguridad y confidencialidad

**CONFIRMADO:** información confidencial por defecto.

Nunca exponer en código, repositorios o logs: contraseñas, tokens OAuth, API keys, credenciales privadas, sesiones, encabezados de autenticación, datos personales innecesarios, contenido confidencial completo o payloads sensibles.

Usar mecanismos de secretos apropiados. Script Properties no sustituye a un gestor de secretos dedicado cuando se requieren controles más fuertes. Restringir acceso a propiedades y configuración.

Evaluar autenticación, autorización, scopes, mínimo privilegio, validación, acceso a archivos, identidad de web apps, APIs/webhooks, inyección de fórmulas, logs, errores, almacenamiento y rotación de secretos, dependencias, retención y uso indebido.

Aplicar minimización: recolectar y conservar únicamente lo necesario.

---

## 14. Trazabilidad, logs y auditoría

### Registro por ejecución

Registrar según aplique:
- ID único de ejecución/correlación.
- Proyecto y ambiente.
- Flujo o función.
- Inicio, fin y duración.
- Usuario iniciador e identidad efectiva (si se conocen y es apropiado).
- Origen: trigger, usuario, menú, API, etc.
- Estado.
- Conteos procesados, omitidos, modificados y fallidos.
- Reintentos y recuperación.
- Categoría de error y diagnóstico seguro.
- Versión o commit.

No guardar contenido confidencial para aumentar detalle.

### Destino de logs

**CONFIRMADO:** preguntar dónde almacenar. Google Sheets será la primera opción presentada.

Alternativas:
- Google Sheets: consulta sencilla y volumen modesto.
- Google Cloud Logging: monitoreo y registros técnicos.
- BigQuery: análisis histórico o grandes volúmenes.
- Combinación justificada.

Explicar costos, accesos, retención, volumen y operación. No asumir que está configurado.

### Retención

Definir tipo de registro, período, responsable, accesos, eliminación y excepciones legales/operativas. No imponer retención universal.

---

## 15. Métricas y seis categorías de alertas

### Métricas

Seleccionar:
- Número de ejecuciones.
- Tasa de éxito/fallo.
- Duración promedio, mediana y máxima si aporta.
- Registros procesados por unidad de tiempo.
- Reintentos y recuperaciones.
- Salud de activadores y ejecuciones omitidas.
- Contención de locks.
- Uso o estimación de cuotas.
- Tendencia de rendimiento.
- Fallos de validación.
- Alertas emitidas.

Definir nombres, unidades, ventanas y umbrales.

### Seis categorías de alertas

Estas capacidades deben existir en el kit y ser configurables por proyecto:

1. **ERROR:** ejecución o proceso fallido.
2. **WARNING:** anomalía que no detiene el proceso.
3. **PERFORMANCE:** duración o rendimiento fuera de presupuesto o degradación.
4. **QUOTA:** cuota/límite próximo a agotarse o alcanzado.
5. **MISSED EXECUTION:** ejecución programada ausente dentro de tolerancia.
6. **HEALTH REPORT:** resumen periódico de métricas, ejecuciones, activadores, errores y cambios.

Cada alerta debe configurar correo destinatario, habilitación, severidad, umbral, frecuencia, periodo de silencio, deduplicación, contenido seguro y manejo de fallo de entrega.

**Pendiente por proyecto:** confirmar correo destino. Nunca inventarlo.

---

## 16. Respaldos y recuperación

Antes de cambios importantes/destructivos:
- Identificar datos a proteger.
- Elegir respaldo apropiado.
- Verificar existencia y acceso.
- Registrar fecha, alcance, versión e instrucciones.
- Restringir acceso.
- Definir retención.
- Probar restauración en procesos críticos.

Un respaldo no verificado no es recuperación confirmada. Revertir código no deshace automáticamente correos, invitaciones, llamadas externas o cambios de datos. Documentar limitaciones.

---

## 17. Pruebas y calidad

**CONFIRMADO:** cada proyecto debe incluir un archivo `.gs` de pruebas o equivalente documentado.

Categorías:
- Unitarias.
- Validación.
- Integración.
- Regresión.
- Identidad y autorización.
- Instalación y duplicidad de activadores.
- Idempotencia y concurrencia.
- Recuperación y fallos parciales.
- Rendimiento para volúmenes relevantes.
- Integridad de datos.

No modificar producción en pruebas normales. Usar fixtures, mocks o recursos aislados. Pruebas con efectos reales (envío de correo, creación de archivos, cambios de Calendar, etc.) deben identificarse y requerir configuración explícita.

Estados: `PASS`, `FAIL`, `NOT RUN`, `BLOCKED`.

No declarar aprobada una prueba solo porque su código existe. Funciones materiales deben tener criterios de aceptación observables: entradas, resultado, errores y verificación.

---

## 18. Análisis de impacto

Antes de modificar un sistema, identificar:
- Archivos y funciones afectadas.
- Llamadores directos e indirectos.
- Activadores.
- Menús, endpoints y entradas.
- Esquemas y consumidores.
- Scopes y servicios.
- Integraciones.
- Notificaciones y efectos secundarios.
- Pruebas y documentos que actualizar.

Ejemplo:

```text
CHANGE IMPACT ANALYSIS

Modified:
  - processContracts()

Affected:
  - updateContractStatus()
  - sendNotifications()
  - dailyTrigger()

Risk:
  HIGH

Potential impact:
  - Contract status synchronization
  - Email notifications
  - Scheduled executions

Required:
  - Regression tests
  - Integration tests
  - Performance comparison
  - Trigger validation
```

Explicar el motivo de cada riesgo en lenguaje sencillo.

---

## 19. GitHub, versiones y despliegues

**CONFIRMADO:** GitHub e historial de Apps Script serán historiales complementarios.

Cuando aplique, utilizar `clasp` para sincronización local. No asumir que Actions está configurado.

Cada release registra versión, fecha, responsable/agente, resumen, riesgo/impacto, commit, pruebas, ambiente, resultado y rollback.

### Ambientes

**CONFIRMADO:** DEV, TEST y PROD.

- **DEV:** desarrollo.
- **TEST:** validación controlada.
- **PROD:** operación real.

Separar IDs, parámetros, destinatarios y secretos. Evitar que pruebas apunten a producción. Si no se pueden separar proyectos/recursos, documentar aislamiento alternativo y riesgo.

### Despliegue autónomo

**CONFIRMADO:** la IA puede desplegar autónomamente si el destino está identificado, impacto completo, pruebas y seguridad aprobadas, permisos/configuración verificados, respaldo/rollback disponible cuando corresponda, no existen aprobaciones pendientes y el resultado puede verificarse.

Si falta una condición, detenerse y explicar el bloqueo.

### Rollback

Documentar objetivo, versión/commit, cambios de datos que requieren restauración o compensación, recuperación de activadores y despliegues, y verificación posterior.

---

## 20. Documentación técnica sencilla

**CONFIRMADO:** documentar funciones importantes con JSDoc y lenguaje sencillo.

Explicar qué hace, recibe, devuelve/modifica, dependencias, permisos, fallos, efectos secundarios y rendimiento cuando sea relevante.

Ejemplo:

```javascript
/**
 * Processes contracts waiting for review.
 *
 * In simple terms:
 * Finds pending contracts, checks their data, and updates their status.
 *
 * @param {Object} options - Execution options.
 * @returns {Object} Summary of processed, skipped, and failed records.
 * @throws {Error} If required data cannot be validated.
 *
 * Side effects:
 * - Reads and updates Google Sheets records.
 * - May create or update files in Google Drive.
 *
 * Security:
 * - Requires an authorized execution context.
 *
 * Performance:
 * - Reads and writes records in batches.
 */
function processPendingContracts(options) {
  // Implementation
}
```

Evitar comentarios vagos.

### Sincronización documental

Ante cambios de código, revisar según impacto: `MODULE_MAP.md`, `DATA_FLOW.md`, `API_CONTRACTS.md`, `AUTHENTICATION.md`, `AUTHORIZATION.md`, `DATABASE_SCHEMA.md`, `DATA_DICTIONARY.md`, `MONITORING.md`, `SECURITY_AUDIT.md`, `CHANGELOG.md`, `PROJECT_STATUS.md`, `TECHNICAL_DEBT.md`.

Actualizar solo lo afectado, pero corregir inexactitudes conocidas.

---

## 21. Diagnóstico de salud y puntaje

Generar informe durante discovery, antes de releases importantes y cuando se solicite.

Ejemplo:

```text
PROJECT HEALTH REPORT

Architecture:          PASS
OAuth Scopes:        REVIEW
Trigger Ownership:    WARNING
Security:             PASS
Performance:          WARNING
Execution Limits:     REVIEW
Data Integrity:       PASS
Test Coverage:        INSUFFICIENT
Documentation:        INCOMPLETE

Quality Score:        78/100
Overall Status:       NEEDS IMPROVEMENT
```

### Puntaje inicial (0–100)

| Dimensión | Peso |
|---|---:|
| Corrección y aceptación | 20% |
| Seguridad y autorización | 20% |
| Integridad y recuperación | 15% |
| Pruebas y regresión | 15% |
| Confiabilidad y ejecución | 10% |
| Rendimiento y cuotas | 10% |
| Observabilidad y trazabilidad | 5% |
| Documentación y mantenimiento | 5% |

Los pesos pueden ajustarse justificadamente. No otorgar puntos por afirmaciones no verificadas. Un puntaje alto nunca compensa un fallo crítico.

### Estados

- **PRODUCTION READY:** controles obligatorios aprobados y sin riesgos bloqueantes.
- **CONDITIONAL:** uso permitido con limitaciones documentadas y aceptadas.
- **NEEDS IMPROVEMENT:** deficiencias importantes.
- **BLOCKED:** problema crítico de seguridad, integridad, autorización o funcionamiento.

---

## 22. Workflow obligatorio

### Fase 1 — Discovery
Inspeccionar archivos, tipo de proyecto, funciones, servicios, activadores, dependencias, datos, IDs, esquemas, comportamiento, identidad y propiedad cuando sea posible. Registrar incertidumbres.

### Fase 2 — Requisitos y viabilidad
Documentar objetivo, usuarios, roles, entradas/salidas, volumen, frecuencia, concurrencia, duración, disponibilidad, confidencialidad, retención, integraciones, cuotas y recuperación.

### Fase 3 — Riesgo y arquitectura
Clasificar complejidad/riesgo. Definir arquitectura proporcional, flujo de datos, permisos, scopes, activadores, despliegue, métricas, respaldo y pruebas.

### Fase 4 — Implementación
Cambios pequeños, validación, lotes, concurrencia, idempotencia, errores, métricas, pruebas y documentación.

### Fase 5 — Verificación
Validaciones estáticas, unitarias, integración, regresión, seguridad, permisos, integridad, activadores y rendimiento según aplique.

### Fase 6 — Despliegue
Confirmar ambiente, autorización, respaldo, versión, pruebas y rollback. Desplegar, verificar y monitorear primeras ejecuciones.

### Fase 7 — Cierre
Actualizar estado, changelog, documentos, registro de sesión y próxima sesión. Reportar pendientes, bloqueos, riesgos y pruebas.

---

## 23. Discovery por proyecto

La IA preguntará solo lo que no pueda descubrir y que afecte al diseño.

1. ¿Qué problema se automatiza?
2. ¿Qué servicios Workspace y sistemas externos intervienen?
3. ¿Qué usuarios/roles?
4. ¿Quién es propietario del proyecto y recursos?
5. ¿Qué cuenta crea y ejecuta activadores?
6. ¿Qué datos se procesan y su sensibilidad?
7. ¿Volumen y frecuencia aproximados?
8. ¿Qué ocurre si falla o se ejecuta dos veces?
9. ¿Presupuesto de ejecución?
10. ¿Retención?
11. ¿Correo para alertas?
12. ¿Destino de logs? Presentar Sheets primero y explicar cuándo conviene Cloud Logging, BigQuery o combinación.
13. ¿Ambientes y controles de despliegue?
14. ¿Respaldos y recuperación esperados?

Si no puede descubrirse un dato, marcarlo desconocido y preguntar lo mínimo.

---

## 24. Estructura completa del repositorio

```text
AI-ENGINEERING-KIT/
│
├── AGENTS.md
├── README.md
├── PROJECT_STATUS.md
├── CHANGELOG.md
├── .gitignore
│
├── .ai/
│   ├── config.md
│   ├── modes.md
│   ├── safety.md
│   └── workflow.md
│
├── docs/
│   ├── 00-project/
│   │   ├── PROJECT_BRIEF.md
│   │   ├── REQUIREMENTS.md
│   │   ├── SCOPE.md
│   │   ├── CHANGELOG.md
│   │   └── GLOSSARY.md
│   │
│   ├── 01-architecture/
│   │   ├── SYSTEM_OVERVIEW.md
│   │   ├── ARCHITECTURE.md
│   │   ├── MODULE_MAP.md
│   │   ├── DATA_FLOW.md
│   │   ├── TECH_STACK.md
│   │   └── ADR/
│   │
│   ├── 02-design/
│   │   ├── DESIGN_SYSTEM.md
│   │   ├── UX_FLOWS.md
│   │   ├── SCREEN_INVENTORY.md
│   │   └── COMPONENTS.md
│   │
│   ├── 03-data/
│   │   ├── DATABASE_SCHEMA.md
│   │   ├── DATA_DICTIONARY.md
│   │   ├── MIGRATIONS.md
│   │   └── DATA_POLICIES.md
│   │
│   ├── 04-api/
│   │   ├── API_CONTRACTS.md
│   │   ├── AUTHENTICATION.md
│   │   └── AUTHORIZATION.md
│   │
│   ├── 05-quality/
│   │   ├── TEST_STRATEGY.md
│   │   ├── ACCEPTANCE_CRITERIA.md
│   │   ├── REGRESSION_CHECKLIST.md
│   │   └── BUGS.md
│   │
│   ├── 06-security/
│   │   ├── SECURITY_POLICY.md
│   │   ├── THREAT_MODEL.md
│   │   └── SECURITY_AUDIT.md
│   │
│   ├── 07-operations/
│   │   ├── ENVIRONMENTS.md
│   │   ├── DEPLOYMENT.md
│   │   ├── BACKUP_RECOVERY.md
│   │   └── MONITORING.md
│   │
│   ├── 08-maintenance/
│   │   ├── TECHNICAL_DEBT.md
│   │   ├── REFACTOR_PLAN.md
│   │   └── ROADMAP.md
│   │
│   └── 09-session/
│       ├── SESSION_LOG.md
│       └── NEXT_SESSION.md
│
├── ai-tasks/
│   ├── 00-initialize.md
│   ├── 01-discovery-audit.md
│   ├── 02-architecture.md
│   ├── 03-design-system.md
│   ├── 04-implementation.md
│   ├── 05-refactoring.md
│   ├── 06-testing.md
│   ├── 07-security-audit.md
│   ├── 08-code-review.md
│   ├── 09-deployment.md
│   └── 10-session-close.md
│
└── .github/
    └── workflows/
```

Notas:
- `.gitignore` está en la raíz.
- `.github/workflows/` contiene workflows de GitHub Actions.
- `CHANGELOG.md` raíz registra releases/cambios del kit. El changelog dentro de `docs/00-project/` solo se mantiene si tiene un propósito distinto y claro.
- `02-design/` es más relevante para interfaces, web apps o add-ons; puede no aplicar a scripts sin UI.
- Los documentos de cada automatización deben adaptarse a su alcance.

---

## 25. Propósito de cada archivo

| Archivo | Propósito |
|---|---|
| `AGENTS.md` | Reglas globales obligatorias |
| `README.md` | Presentación, instalación y uso |
| `PROJECT_STATUS.md` | Estado, riesgos, bloqueos y próximos pasos |
| `CHANGELOG.md` | Historial de cambios y releases |
| `.ai/config.md` | Parámetros del agente/proyecto |
| `.ai/modes.md` | Modos de análisis, implementación, revisión y despliegue |
| `.ai/safety.md` | Restricciones, permisos y aprobación |
| `.ai/workflow.md` | Proceso de trabajo |
| `PROJECT_BRIEF.md` | Objetivo y contexto |
| `REQUIREMENTS.md` | Requisitos funcionales y no funcionales |
| `SCOPE.md` | Alcance, exclusiones y límites |
| `GLOSSARY.md` | Definiciones compartidas |
| `SYSTEM_OVERVIEW.md` | Visión general |
| `ARCHITECTURE.md` | Diseño técnico y capas |
| `MODULE_MAP.md` | Módulos y dependencias |
| `DATA_FLOW.md` | Flujo de información |
| `TECH_STACK.md` | Tecnologías y servicios |
| `DATABASE_SCHEMA.md` | Estructuras de datos |
| `DATA_DICTIONARY.md` | Significado de campos |
| `MIGRATIONS.md` | Cambios de estructura |
| `DATA_POLICIES.md` | Integridad, retención y tratamiento |
| `API_CONTRACTS.md` | Entradas, salidas y contratos |
| `AUTHENTICATION.md` | Identidad y autenticación |
| `AUTHORIZATION.md` | Roles y permisos |
| `TEST_STRATEGY.md` | Estrategia de pruebas |
| `ACCEPTANCE_CRITERIA.md` | Condiciones de aceptación |
| `REGRESSION_CHECKLIST.md` | Verificación de regresión |
| `BUGS.md` | Registro de defectos |
| `SECURITY_POLICY.md` | Reglas de seguridad |
| `THREAT_MODEL.md` | Amenazas y mitigaciones |
| `SECURITY_AUDIT.md` | Resultados de auditoría |
| `ENVIRONMENTS.md` | DEV, TEST y PROD |
| `DEPLOYMENT.md` | Despliegue |
| `BACKUP_RECOVERY.md` | Respaldos y recuperación |
| `MONITORING.md` | Logs, métricas y alertas |
| `TECHNICAL_DEBT.md` | Deuda técnica |
| `REFACTOR_PLAN.md` | Plan de refactorización |
| `ROADMAP.md` | Evolución |
| `SESSION_LOG.md` | Trabajo por sesión |
| `NEXT_SESSION.md` | Continuidad |

---

## 26. Procedimientos de IA (`ai-tasks/`)

| Archivo | Objetivo |
|---|---|
| `00-initialize.md` | Inicializar kit y revisar estructura |
| `01-discovery-audit.md` | Auditar proyecto existente |
| `02-architecture.md` | Definir arquitectura y viabilidad |
| `03-design-system.md` | Definir interfaz cuando aplique |
| `04-implementation.md` | Implementar |
| `05-refactoring.md` | Refactorizar con análisis de impacto |
| `06-testing.md` | Ejecutar y documentar pruebas |
| `07-security-audit.md` | Auditar permisos y seguridad |
| `08-code-review.md` | Revisar código y estándares |
| `09-deployment.md` | Desplegar y verificar |
| `10-session-close.md` | Actualizar documentación y continuidad |

Cada task debe contener objetivo, cuándo usarlo, información necesaria, pasos, archivos a revisar, validaciones, condiciones de detención, entregables y registro de resultados.

---

## 27. Formato de informe de IA

Al terminar tareas sustanciales:

### Resumen
Qué se descubrió o modificó.

### Verificación
Pruebas con PASS, FAIL, NOT RUN o BLOCKED.

### Seguridad y permisos
Impacto en scopes, identidad, activadores y autorización.

### Rendimiento
Mediciones, línea base y optimizaciones.

### Integridad y recuperación
Respaldos, checkpoints, efectos secundarios y recuperación.

### Documentación y versión
Archivos, commit, versión y despliegue.

### Riesgos pendientes
Problemas, supuestos, aprobaciones y próximos pasos.

No reportar completa una tarea si faltan pruebas, aprobación, verificación de despliegue o documentación obligatoria.

---

## 28. Decisiones confirmadas y configuración pendiente

### Confirmado para el kit

- Metodología, estándar técnico e instrucciones para IA.
- Documento maestro.
- Cobertura de Sheets, Docs, Forms, Drive, Gmail y Calendar.
- Scripts vinculados, independientes, web apps, add-ons, APIs y procesos masivos.
- Arquitectura modular por responsabilidades.
- Controles de OAuth y scopes.
- Propiedad y ejecución de activadores.
- Medición de tiempos y rendimiento.
- Trazabilidad, métricas y viabilidad.
- Verificación de identidad y autorización.
- Cuentas personales y Workspace.
- Reintentos, locks, idempotencia y checkpoints cuando apliquen.
- Información confidencial por defecto.
- Archivo `.gs` de pruebas o equivalente.
- GitHub e historial de Apps Script.
- Análisis de impacto antes de modificar.
- Autonomía de IA dentro de límites de aprobación.
- Seis categorías de alertas.
- Alertas a correo configurable.
- Preguntar destino de logs; Sheets como primera opción.
- DEV, TEST y PROD.
- Informe de salud.
- Documentación sincronizada con código.
- Puntaje de calidad de 0 a 100 sin compensar fallos críticos.
- Documentación sencilla.

### Configurable por automatización

Complejidad, riesgo, correo de alertas, destino de logs, retención, umbrales, frecuencia de reportes, usuarios, roles, identidades ejecutoras, ambientes, volumen, frecuencia, presupuestos, respaldo, despliegue e integraciones.

### Pendiente por proyecto

Correo de alertas, cuenta propietaria, cuenta creadora de activadores, destino de logs, retención exacta, umbrales, cuotas, política de datos, roles, servicios externos y disponibilidad.

La IA debe preguntar o descubrir estos datos antes de depender de ellos.

---

## 29. Plan de construcción del kit

### Etapa 1 — Núcleo
1. `AGENTS.md`
2. `README.md`
3. `.ai/safety.md`
4. `.ai/workflow.md`
5. `.ai/modes.md`
6. `.ai/config.md`

### Etapa 2 — Proyecto y arquitectura
1. `PROJECT_BRIEF.md`
2. `REQUIREMENTS.md`
3. `SCOPE.md`
4. `GLOSSARY.md`
5. `SYSTEM_OVERVIEW.md`
6. `ARCHITECTURE.md`
7. `MODULE_MAP.md`
8. `DATA_FLOW.md`
9. `TECH_STACK.md`

### Etapa 3 — Datos, APIs e identidad
1. `DATABASE_SCHEMA.md`
2. `DATA_DICTIONARY.md`
3. `MIGRATIONS.md`
4. `DATA_POLICIES.md`
5. `API_CONTRACTS.md`
6. `AUTHENTICATION.md`
7. `AUTHORIZATION.md`

### Etapa 4 — Calidad y seguridad
1. `TEST_STRATEGY.md`
2. `ACCEPTANCE_CRITERIA.md`
3. `REGRESSION_CHECKLIST.md`
4. `BUGS.md`
5. `SECURITY_POLICY.md`
6. `THREAT_MODEL.md`
7. `SECURITY_AUDIT.md`

### Etapa 5 — Operación y mantenimiento
1. `ENVIRONMENTS.md`
2. `DEPLOYMENT.md`
3. `BACKUP_RECOVERY.md`
4. `MONITORING.md`
5. `TECHNICAL_DEBT.md`
6. `REFACTOR_PLAN.md`
7. `ROADMAP.md`

### Etapa 6 — Procedimientos de IA
Construir y validar los once archivos de `ai-tasks/`.

### Etapa 7 — Validación del kit
- Revisar coherencia entre documentos.
- Detectar reglas duplicadas o contradictorias.
- Comprobar enlaces y rutas.
- Validar que las instrucciones sean ejecutables.
- Probar con Apps Script simple e intermedio.
- Registrar limitaciones y mejoras.
- Versionar el kit.

---

## 30. Regla final

> Construir la solución segura más sencilla que cumpla el requisito real. Comprender antes de cambiar, medir antes de optimizar, proteger antes de automatizar, probar antes de desplegar, documentar para que otros entiendan y declarar siempre qué está comprobado y qué no.

Este documento es el contexto integral de referencia del AI Engineering Kit. Los archivos individuales se desarrollarán progresivamente, manteniendo coherencia con esta especificación y con `AGENTS.md`.

---

# 31. Manual operativo y de ingeniería práctica (extensión universal)

Esta extensión convierte la especificación de gobernanza en guía operativa. No reemplaza las secciones anteriores: las complementa con procedimientos, ejemplos, plantillas y criterios concretos.

## 31.1 Testing práctico
Cada proyecto define cómo ejecutar pruebas, cómo aislar datos, cómo simular servicios y cómo presentar resultados. El kit incluye un harness mínimo custom, fixtures temporales, inyección de servicios, resultados PASS/FAIL, duración y errores sanitizados. No ejecutar pruebas contra producción por defecto.

## 31.2 Clasp y ambientes
Usar `clasp` cuando facilite sincronización y versionado. Mantener IDs de proyectos separados por ambiente, configuración no secreta documentada, secretos fuera del repo y promoción DEV→TEST→PROD con validación y aprobación. Nunca hacer `clasp push` a producción desde una PR sin revisión/aprobación.

## 31.3 Manifiestos
Proveer ejemplos de `appsscript.json` para scripts vinculados con UI, scripts sin UI, Web Apps, Add-ons y Advanced Services. Los scopes son ejemplos que deben verificarse y minimizarse para el proyecto concreto.

## 31.4 Patrones y anti-patrones
El manual contiene patrones prácticos: batch de Sheets, polling y cancelación cooperativa, índices en memoria, caché versionada, normalización, pre-filtros por trigramas, errores estructurados, escritura masiva formateada, mapeos persistentes y limpieza de temporales. Contiene anti-patrones como lectura/escritura por celda dentro de loops, `openById` repetido, `flush()` innecesario, locks sin timeout, HTML no escapado, asumir identidad de usuario y triggers recursivos.

## 31.5 Estado y concurrencia
Distinguir CacheService (temporal), PropertiesService (persistente de configuración/estado pequeño) y LockService (coordinación de ejecución). Documentar alcance, TTL, invalidación, límites y privacidad. Locks tienen timeout y liberación en `finally`; no son transacciones de datos.

## 31.6 HtmlService frontend/backend
Definir contratos de `google.script.run`, handlers de éxito/fallo, inclusión de templates, polling, cancelación, estados de UI, IDs de ejecución, escapado y limitaciones del entorno. Datos del cliente siempre se consideran no confiables.

## 31.7 Alertas y Health Score
Las alertas tienen plantilla consistente, categoría, ambiente, ejecución, acción, error sanitizado, duración y enlace de diagnóstico. El score de salud usa estado ponderado; BLOCKED por un hallazgo crítico puede forzar el estado general BLOCKED. Documentar evidencia, pesos y limitaciones; nunca esconder hallazgos críticos detrás de un promedio.

## 31.8 Estructura proporcional
Definir niveles de proyecto (mínimo, intermedio, complejo, crítico). No crear archivos vacíos. Omitir ADR, threat model, UX flows, data dictionary y checklist de regresión cuando el proyecto no los necesita; documentar la razón si la omisión es relevante.

## 31.9 Seguridad de HTML y configuración
Evitar XSS: escapar texto, no interpolar datos no confiables en HTML sin escape, evitar `innerHTML` cuando pueda usarse `textContent`, nunca colocar tokens en frontend. Centralizar keys de configuración, cachear lecturas durante una ejecución, separar ambientes y documentar rotación de secretos.

## 31.10 Rendimiento y ejecución
Definir presupuesto por etapa, medir tiempos y alertar por degradación. Para procesos largos, diseñar checkpoints y continuación en vez de asumir que una ejecución puede durar indefinidamente.

## 31.11 Despliegue
El checklist de despliegue es ejecutable e incluye ambiente, scopes, tests, prueba E2E, respaldo, aprobación, rollback, monitoreo, triggers y comunicación. La promoción de PROD requiere aprobación explícita.

## 31.12 Blast radius y estimación
Los planes de cambio cuantifican, cuando sea posible, usuarios, hojas, triggers, integraciones, riesgo de producción, downtime y migraciones. Las estimaciones por fase son orientativas, no promesas.

## 31.13 Declaración de limitaciones
Todo reporte final declara explícitamente qué no se verificó, qué accesos faltaron, qué pruebas no se ejecutaron, qué supuestos quedan y qué limitaciones conocidas existen.

## 31.14 Caso de referencia
El Generador de Reportes puede servir como ejemplo Nivel 3 solo si su código, permisos, datos y evidencias se revisan y se aprueba su inclusión. No copiar secretos, IDs, información de usuarios ni datos reales al ejemplo universal.

## 31.15 Prioridad de implementación de la extensión
P0: testing práctico; clasp/ambientes; manifests; patterns/anti-patterns; frontend/backend; state management.
P1: alertas; fórmula Health Score; estructuras por nivel; plantilla task; seguridad HTML; configuración; execution budget; concurrency; Sheets output.
P2: scopes; blast radius; estimación; ADR; pre-deploy; declaración de limitaciones.
P3: caso de referencia sanitizado.
