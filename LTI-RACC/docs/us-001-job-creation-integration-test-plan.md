# Plan de prueba de integración US-001

## Objetivo
Validar el flujo completo feliz de creación de vacantes asistida por IA, desde la generación de la descripción hasta el guardado del borrador y la notificación al hiring manager.

## Archivo de prueba objetivo
`src/tests/integration/us-001-job-creation.spec.ts`

## Alcance
### Flujo 1: Creación completa asistida por IA
1. `POST /api/v1/jobs/ai/generate-description` con `title` y `level`
2. `POST /api/v1/jobs` con `title`, `description_html`, `hiring_manager_id` y campos relacionados
3. Verificar la creación del registro de notificación para el hiring manager
4. Verificar que la tarea de correo queda encolada en BullMQ mediante el spy del mailer

### Flujo 2: Guardado manual con detección de sesgo
1. `POST /api/v1/jobs` con `description_html` que contenga lenguaje sesgado
2. Verificar que la API devuelva `bias_flags` para la frase detectada

### Flujo 3: Servicio de IA no disponible
1. Simular que el servicio de IA responde `503`
2. `POST /api/v1/jobs/ai/generate-description`
3. Verificar que no se cree ningún registro de job y que no se encole ninguna notificación

## Preparación del test
- Usar la base de datos de pruebas con transacciones aisladas por test
- Simular el servicio de IA con `nock` o `msw`
- Reemplazar el envío real de SendGrid/correo por un spy en memoria
- Usar fixtures deterministas para usuarios, organizaciones y hiring managers

## Aserciones
- `draft_html` incluye las cuatro secciones requeridas
- `bias_flags` se devuelve y se persiste cuando aplica
- Los jobs guardados quedan por defecto en estado `draft`
- La notificación se crea para el hiring manager correcto
- La tarea de correo se encola exactamente una vez
- Los fallos de IA devuelven una respuesta `503` controlada

## Criterios de aceptación
- Los tres flujos pasan de forma consistente en CI
- No hay fuga de datos entre tests
- La suite completa en menos de 10 segundos

## Riesgos
- Las tareas de cola pueden volverse inestables si no se simulan los workers asíncronos
- Las fixtures compartidas pueden filtrar estado sin rollback transaccional
- Las dependencias externas de IA/correo no deben invocarse directamente en el test
