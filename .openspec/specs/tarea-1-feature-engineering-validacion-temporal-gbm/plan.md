# Plan: Tarea 1 - Feature Engineering y Validacion Temporal con GBM

## Enfoque

Trabajar desde el notebook base de `Tareas/` y generar una version final en `Entregas/Entrega_1/`. La solucion debe priorizar claridad academica, reproducibilidad, compatibilidad con Google Colab y cuidado con leakage temporal.

## Archivos a revisar

- `Tareas/Tarea_1,_Feature_Engineering_y_Validación_Temporal_con_GBM.ipynb`

## Material de clase a consultar

- `Clase 1/Codigo/Clase_1,_Leakage_Temporal_y_Validacion_Temporal.ipynb`
- `Clase 1/Codigo/Clase_1,_Conversión_a_Problema_Supervisado.ipynb`
- `Clase 2/Codigo/Clase_2,_Feature_Engineering.ipynb`
- `Clase 2/Codigo/Clase_2,_Baselines_Modernos_para_Series_de_Tiempo.ipynb`
- `Clase 1/Slides/`
- `Clase 2/Slides/`

## Archivos a crear o modificar

- `Entregas/Entrega_1/Tarea_1_Feature_Engineering_y_Validacion_Temporal_con_GBM.ipynb`
- `Entregas/Entrega_1/README.md`
- `.openspec/specs/tarea-1-feature-engineering-validacion-temporal-gbm/notes.md`

## Riesgos

- Introducir leakage temporal al crear lags, rolling windows o splits.
- Modificar accidentalmente el notebook original de `Tareas/`.
- Obtener resultados no reproducibles por dependencias, semillas o datos externos.
- Usar rutas locales que no funcionen en Google Colab.
- Enfocarse demasiado en tuning y poco en explicar la metodologia.

## Validacion

- Revisar que la entrega se pueda ejecutar de arriba hacia abajo si el entorno esta disponible.
- Revisar que el notebook no dependa de rutas absolutas locales.
- Confirmar que las divisiones temporales respetan el orden cronologico.
- Confirmar que las features usan solamente informacion disponible al momento de prediccion.
- Revisar que las conclusiones esten conectadas con las metricas.
- Revisar que el README documente objetivo, metodologia, resultados, ejecucion en Colab y conclusiones.
- Revisar que el README indique que materiales de clase se usaron como base.
