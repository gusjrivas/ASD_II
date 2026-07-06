# OpenSpec para ASD_II

Esta carpeta organiza el trabajo asistido con Codex para la materia Analisis de Series de Tiempo 2.

La idea es que cada cambio, tarea o entrega tenga una especificacion breve antes de modificar notebooks, informes o codigo. Codex debe leer primero el contexto general y luego la spec puntual.

## Estructura

```text
.openspec/
  project.md
  conventions.md
  workflow.md
  specs/
    _template/
      spec.md
      plan.md
      tasks.md
      notes.md
    tarea-1-feature-engineering-validacion-temporal-gbm/
      spec.md
      plan.md
      tasks.md
      notes.md
```

## Uso rapido con Codex

Para iniciar un trabajo:

```text
Lee .openspec/project.md, .openspec/conventions.md, .openspec/workflow.md y la spec de la tarea.
Primero completa o ajusta plan.md y tasks.md. Despues implementa las tareas.
```

Para continuar una tarea:

```text
Continua con .openspec/specs/<nombre>/tasks.md. Actualiza notes.md con decisiones, dudas y resultados.
```

