# Notes: Tarea 1 - Feature Engineering y Validacion Temporal con GBM

## Estado

Entrega inicial implementada en `Entregas/Entrega_1/`.

## Decisiones

- El notebook original de `Tareas/` se trata como fuente.
- La entrega final debe generarse en `Entregas/Entrega_1/`.
- La entrega debe desarrollarse en Python como notebook compatible con Google Colab.
- Cada entrega debe incluir una carpeta propia dentro de `Entregas/`.
- Cada carpeta de entrega debe incluir el notebook de resolucion y un `README.md` explicativo detallado.
- Las carpetas `Clase N/` se consideran material teorico y practico base para resolver entregas.
- La prioridad metodologica es evitar leakage temporal y explicar la validacion.
- La serie AirPassengers se incluyo embebida en el notebook para evitar dependencia de descargas externas en Colab.
- La comparacion entre `features_fecha` y `features_all` usa una base comun sin valores faltantes para evaluar ambas familias sobre las mismas fechas.
- La escala de MASE se calcula con el naive estacional de lag 12 sobre el entrenamiento temporal y se reutiliza para comparar los cuatro modelos.

## Resultados

- Se creo `Entregas/Entrega_1/Tarea_1_Feature_Engineering_y_Validacion_Temporal_con_GBM.ipynb`.
- Se creo `Entregas/Entrega_1/README.md`.
- El notebook contiene carga de datos, feature engineering, holdout temporal, holdout con shuffle, entrenamiento de cuatro modelos GBM, metricas, interpretabilidad y respuestas de analisis.
- Se valido que el notebook sea JSON valido con `nbformat` 4.5.

## Pendientes

- Ejecutar el notebook completo en Google Colab para generar metricas, graficos y salidas renderizadas.
- Revisar visualmente las salidas despues de ejecutar en Colab.
