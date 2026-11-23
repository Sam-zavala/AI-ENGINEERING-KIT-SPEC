# AI Engineering Kit

> Kit de ingeniería asistida por IA para crear, mantener, auditar y operar automatizaciones confiables, principalmente con Google Apps Script.

## ¿Qué es?

AI Engineering Kit es un conjunto de instrucciones, procesos, plantillas y herramientas para que una IA trabaje en proyectos de automatización de manera ordenada y consistente.

Su objetivo no es solo generar código. También debe ayudar a entender proyectos existentes, detectar riesgos, diseñar soluciones, probarlas, documentarlas, mantenerlas y preparar despliegues.

La prioridad es que las soluciones sean **seguras, sencillas de entender, mantenibles y verificables**.

## Objetivos

- Construir y mantener automatizaciones de Google Apps Script.
- Integrar Google Sheets, Docs, Forms, Drive, Gmail y Calendar.
- Entender proyectos existentes antes de modificar su comportamiento.
- Separar configuración, lógica, datos, integraciones, validaciones y seguridad.
- Detectar problemas de rendimiento, cuotas, permisos, triggers y confiabilidad.
- Crear y ejecutar pruebas de forma segura.
- Mantener documentación y un historial claro de cambios.
- Automatizar tareas de ingeniería sin perder control de las acciones sensibles.
- Explicar resultados técnicos en lenguaje sencillo.

## Plataformas principales

| Plataforma | Uso previsto |
|---|---|
| Google Apps Script | Motor principal de automatizaciones |
| Google Sheets | Datos, configuración, reportes y, si se aprueba, registros iniciales |
| Google Docs | Documentos y generación de reportes |
| Google Forms | Captura de información |
| Google Drive | Archivos y almacenamiento |
| Gmail | Envío y procesamiento de correo |
| Google Calendar | Eventos, agenda y recordatorios |
| Git / GitHub | Código, revisión, colaboración e historial |

Se pueden recomendar APIs, bases de datos o servicios externos cuando Apps Script no sea suficiente. La IA debe explicar por qué, junto con sus costos, riesgos, requisitos y alternativas.

## Cómo trabaja la IA

El flujo de trabajo recomendado:

1. **Entender:** leer instrucciones, archivos, código, configuración y documentación.
2. **Evaluar:** identificar factibilidad, dependencias, riesgos, permisos, cuotas y alcance.
3. **Planear:** explicar la solución y los archivos que podrían cambiar.
4. **Implementar:** hacer cambios pequeños, coherentes y mantenibles.
5. **Validar:** ejecutar las pruebas y comprobaciones disponibles.
6. **Reportar:** resumir cambios, resultados, limitaciones y próximos pasos.

Para tareas pequeñas, el flujo puede ser más breve. Para cambios importantes, debe existir un plan antes de editar.

## Autonomía con límites

La IA puede trabajar autónomamente en tareas de bajo riesgo y reversibles, como:

- Inspeccionar el repositorio.
- Proponer arquitectura y planes.
- Escribir código y documentación.
- Crear y actualizar pruebas.
- Ejecutar comprobaciones locales no destructivas.
- Refactorizar dentro de un alcance definido.
- Preparar instrucciones de despliegue.

Debe solicitar aprobación antes de:

- Modificar, borrar, migrar o sobrescribir datos reales.
- Enviar correos, mensajes, invitaciones o notificaciones reales.
- Cambiar permisos, accesos, OAuth scopes o configuración de cuentas.
- Crear, eliminar o modificar triggers de producción.
- Desplegar o publicar en producción.
- Realizar acciones irreversibles, de alto impacto o que generen costos.

Siempre que sea posible, primero debe mostrar una vista previa, ejecutar un dry-run, crear respaldo o proponer un plan de reversión.

## Principios

- **Seguridad primero:** privilegios mínimos y datos confidenciales protegidos.
- **Simplicidad:** preferir soluciones fáciles de entender.
- **Modularidad:** separar responsabilidades cuando aporte valor.
- **No asumir:** identificar dudas, supuestos y decisiones pendientes.
- **Verificar:** no declarar algo probado si no se ejecutó.
- **No romper lo existente:** evaluar impactos antes de modificar.
- **Trazabilidad:** mantener cambios, decisiones y resultados documentados.
- **Privacidad:** evitar exponer información sensible en logs o repositorios.
- **Transparencia:** explicar qué se hizo y qué no se pudo comprobar.

## Arquitectura de referencia

No es obligatorio usar todos los módulos en cada proyecto. La estructura debe adaptarse al tamaño y complejidad.

- `config` — configuración y constantes.
- `orchestration` — entradas, workflows y coordinación.
- `business logic` — reglas y decisiones.
- `data access` — lectura, escritura y persistencia.
- `services` — Google Services y APIs externas.
- `validation` — validación de entradas, esquemas y reglas.
- `security` — identidad, autorización y protección de datos.
- `execution` — locks, retries, idempotencia y recuperación.
- `observability` — logs, métricas, alertas y health checks.
- `tests` — pruebas unitarias, integración y regresión.

Evitar estructuras grandes o complejas innecesarias para automatizaciones pequeñas.

## Seguridad y Google Apps Script

La IA debe considerar, según corresponda:

- OAuth scopes y principio de mínimo privilegio.
- Autenticación frente a autorización.
- Identidad del usuario y contexto de ejecución.
- Triggers simples e instalables; propietario/creador y cuenta ejecutora.
- Cuotas, límites de tiempo y límites de servicio.
- Ejecuciones concurrentes y `LockService`.
- Reintentos, duplicados e idempotencia.
- Validación de datos y recuperación ante fallos.
- Secretos y configuración fuera del código.
- Separación de ambientes de desarrollo, pruebas y producción.

No recrear triggers sin analizar primero su identidad, permisos y efectos.

## Alertas y monitoreo

Las alertas deben ser configurables por destinatario, umbral, frecuencia, severidad y deduplicación.

Categorías propuestas:

- **ERROR:** fallos inesperados.
- **WARNING:** condiciones que requieren atención.
- **PERFORMANCE:** degradación o ejecución lenta.
- **QUOTA:** cuotas o límites próximos a agotarse.
- **MISSED EXECUTION:** ejecución esperada que no ocurrió.
- **HEALTH REPORT:** resumen periódico de salud.

El destino inicial de alertas y logs debe acordarse. Se puede comenzar con Google Sheets si es suficiente, y evaluar Cloud Logging u otras alternativas cuando el proyecto lo requiera. No enviar alertas reales de prueba sin autorización.

## Pruebas y calidad

Cada cambio debe validarse en función de su impacto. Considerar:

- Sintaxis y checks estáticos.
- Pruebas unitarias.
- Pruebas de integración.
- Regresión.
- Datos vacíos, inválidos y límites.
- Fallos de servicios y permisos.
- Reintentos y ejecuciones duplicadas.
- Concurrencia.
- Rendimiento y cuotas.
- Seguridad y manejo de datos.

El kit contempla archivos de prueba `.gs` cuando sean adecuados para el proyecto. Las pruebas deben evitar efectos reales no autorizados.

## Historial y versionado

El proyecto puede combinar:

- Git y GitHub para cambios, revisión, ramas y versionado del código.
- Historial de versiones de Apps Script para respaldar y rastrear cambios en el entorno de Google.

No se deben subir credenciales, tokens, datos confidenciales, exportaciones sensibles ni secretos al repositorio.

## Estructura sugerida

La estructura exacta se ajustará al proyecto. Para el kit, se propone:

```text
AI-ENGINEERING-KIT/
├── AGENTS.md
├── README.md
├── PROJECT_STATUS.md
├── CHANGELOG.md
├── .gitignore
├── .ai/
│   ├── config.md
│   ├── modes.md
│   ├── safety.md
│   └── workflow.md
├── docs/
│   ├── 00-project/
│   ├── 01-architecture/
│   ├── 02-design/
│   ├── 03-data/
│   ├── 04-api/
│   ├── 05-quality/
│   ├── 06-security/
│   ├── 07-operations/
│   ├── 08-maintenance/
│   └── 09-session/
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
└── .github/
    └── workflows/
```

> Esta es una estructura inicial. No crear todos los archivos y carpetas vacíos por adelantado; agregar lo que realmente se use y mantener el repositorio fácil de navegar.

## Modos de trabajo de la IA

La IA selecciona el modo según la solicitud, sin obligar al usuario a elegir:

| Modo | Propósito |
|---|---|
| `DISCOVERY` | Revisar y documentar un proyecto sin modificarlo |
| `PLAN` | Diseñar una solución, alcance, riesgos y validación |
| `IMPLEMENT` | Implementar un cambio aprobado y probarlo |
| `DEBUG` | Encontrar causa raíz, corregir y validar |
| `REFACTOR` | Mejorar estructura sin cambiar comportamiento |
| `TEST` | Crear, ejecutar o mejorar pruebas |
| `REVIEW` | Revisar código o arquitectura sin editar por defecto |
| `SECURITY AUDIT` | Evaluar seguridad, permisos, secretos y riesgos |
| `DEPLOY` | Preparar o ejecutar una publicación autorizada |
| `SESSION CLOSE` | Registrar estado, decisiones y siguientes pasos |

## Reporte de finalización

Al terminar una tarea, la IA debe reportar de forma breve:

1. Qué se hizo.
2. Qué archivos cambiaron.
3. Qué pruebas o comprobaciones se realizaron y su resultado.
4. Qué riesgos, limitaciones o elementos no se verificaron.
5. Qué acción, si alguna, necesita el usuario.

## Evaluación de salud del proyecto

Cuando se solicite una auditoría o health check, evaluar —si existe evidencia suficiente— de 0 a 100:

- Correctitud y confiabilidad.
- Arquitectura y mantenibilidad.
- Seguridad y privacidad.
- Pruebas.
- Rendimiento y cuotas.
- Monitoreo y alertas.
- Documentación.
- Despliegue y recuperación.
- Integridad de datos.

La puntuación no debe ocultar problemas críticos. Un riesgo crítico de seguridad, pérdida de datos o producción se reporta como crítico aunque el promedio sea alto.

## Documentación que puede mantener el kit

| Archivo | Contenido |
|---|---|
| `PROJECT_STATUS.md` | Estado actual, bloqueos y siguientes pasos |
| `CHANGELOG.md` | Cambios relevantes |
| `REQUIREMENTS.md` | Requisitos y decisiones pendientes |
| `ARCHITECTURE.md` | Arquitectura y módulos |
| `TEST_STRATEGY.md` | Estrategia de pruebas |
| `SECURITY_POLICY.md` | Reglas de seguridad |
| `DEPLOYMENT.md` | Despliegue |
| `BACKUP_RECOVERY.md` | Respaldos y recuperación |
| `ROADMAP.md` | Mejoras futuras |
| `SESSION_LOG.md` | Registro de sesiones |
| `NEXT_SESSION.md` | Continuación de trabajo |

Crear o actualizar estos documentos según necesidad; evitar documentación duplicada o desactualizada.

## Empezar a usar el kit

1. Copia `AGENTS.md` y `README.md` en la raíz del repositorio.
2. Inicializa el repositorio con Git.
3. Añade los archivos y documentación que correspondan al proyecto.
4. Entrega a la IA una tarea concreta, por ejemplo:

   > Revisa este repositorio en modo DISCOVERY. No modifiques nada. Identifica arquitectura, automatizaciones, triggers, permisos, riesgos, cuotas, problemas y documentación faltante. Entrega un resumen claro y un plan priorizado.

5. Antes de implementar cambios grandes, pide una propuesta de plan y revisa el impacto.
6. Mantén actualizado el estado del proyecto después de cambios importantes.

## Documentación principal

- [`AGENTS.md`](./AGENTS.md) — instrucciones y reglas operativas para la IA.
- `docs/` — documentación técnica y del proyecto.
- `ai-tasks/` — tareas reutilizables para flujos de trabajo de ingeniería.
- `PROJECT_STATUS.md` — estado actual.
- `CHANGELOG.md` — historial de cambios.

---

**Regla final:** que la automatización funcione no es suficiente. Debe ser segura, entendible, mantenible, comprobable y adecuada para el impacto que tendrá.
