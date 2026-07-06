# Entrega 1 - Feature Engineering y Validacion Temporal con GBM

## Objetivo

Resolver la Tarea 1 de Analisis de Series de Tiempo II usando la serie mensual AirPassengers. La entrega implementa feature engineering temporal, compara dos grupos de variables, evalua dos tipos de holdout y entrena modelos `GradientBoostingRegressor`.

## Archivos

- Notebook de resolucion: `Tarea_1_Feature_Engineering_y_Validacion_Temporal_con_GBM.ipynb`
- Explicacion de la entrega: `README.md`
- Notebook fuente: `../../Tareas/Tarea_1,_Feature_Engineering_y_Validación_Temporal_con_GBM.ipynb`

## Material de clase utilizado

Se uso como referencia el material teorico y practico de:

- `Clase 1/Codigo/Clase_1,_Leakage_Temporal_y_Validacion_Temporal.ipynb`
- `Clase 1/Codigo/Clase_1,_Conversión_a_Problema_Supervisado.ipynb`
- `Clase 2/Codigo/Clase_2,_Feature_Engineering.ipynb`
- `Clase 2/Codigo/Clase_2,_Baselines_Modernos_para_Series_de_Tiempo.ipynb`
- `Clase 2/Codigo/Clase_2,_Ejercicio_Feature_Engineering.ipynb`

De esos materiales se tomaron especialmente estas ideas:

- separar features de calendario, que representan el "cuando";
- usar lags, rolling y expanding para representar el "que venia pasando";
- aplicar `.shift(1)` en rolling y expanding para evitar leakage;
- usar holdout temporal como validacion valida para forecasting;
- calcular MASE contra un naive estacional.

## Resumen de la consigna

La tarea pide construir features sobre AirPassengers y entrenar cuatro modelos:

- `features_fecha` con holdout temporal;
- `features_all` con holdout temporal;
- `features_fecha` con holdout aleatorio usando shuffle;
- `features_all` con holdout aleatorio usando shuffle.

Luego se deben calcular MAE, RMSE, MAPE y MASE, analizar importancias del modelo valido y responder cuatro preguntas conceptuales.

## Metodologia aplicada

El notebook construye una base mensual con la serie AirPassengers desde enero de 1949 hasta diciembre de 1960. Para que la entrega sea reproducible en Google Colab sin depender de descargas externas, la serie queda embebida directamente en el notebook.

Se crean dos grupos de features:

- `features_fecha`: mes, trimestre, anio, dia del anio y codificaciones ciclicas `sin/cos` para mes y dia del anio.
- `features_all`: todas las features de calendario mas lags `[1, 2, 3, 12]`, rolling windows de tamanos 3 y 12, y expanding mean/std.

Las features rolling y expanding usan `.shift(1)` para que el valor de la fila `t` no use `y_t` ni informacion futura.

## Validacion temporal

Se implementan dos particiones:

- Holdout temporal: ultimos 24 meses como test y todo lo anterior como train.
- Holdout con shuffle: mismo tamano de test, pero mezclando filas con `train_test_split(shuffle=True)`.

El README y el notebook remarcan que el holdout temporal es el valido para el escenario real de forecasting. El shuffle se incluye porque lo pide la consigna, pero no representa una evaluacion realista de prediccion futura.

## Modelos y metricas

Para cada combinacion de features y holdout se entrena un `GradientBoostingRegressor`.

Las metricas calculadas son:

- MAE;
- RMSE;
- MAPE;
- MASE.

MASE se calcula usando como escala el error promedio del naive estacional de lag 12 sobre el entrenamiento temporal. Esto permite comparar el GBM contra un baseline fuerte para una serie mensual estacional.

## Interpretabilidad

Sobre el modelo valido, `features_all` con holdout temporal, se calculan:

- importancia nativa del modelo con `feature_importances_`;
- permutation importance sobre el conjunto de test con `scoring="neg_mean_absolute_error"` y `n_repeats=30`.

El notebook grafica el top 10 de ambos rankings y deja una interpretacion conceptual sobre por que variables como `lag_12` o las de ciclo anual suelen ser relevantes en AirPassengers.

## Respuestas de analisis

El notebook incluye respuestas para las cuatro preguntas:

- por que el holdout temporal refleja mejor el uso real del modelo;
- cuanto aportan lags, rolling y expanding frente a usar solo calendario;
- como interpretar MASE frente al naive estacional;
- que feature domina los rankings de importancia y por que tiene sentido.

Ademas, una celda genera un resumen cuantitativo automatico a partir de las metricas calculadas al ejecutar el notebook.

## Como ejecutar en Google Colab

1. Abrir `Tarea_1_Feature_Engineering_y_Validacion_Temporal_con_GBM.ipynb` en Google Colab.
2. Ejecutar las celdas de arriba hacia abajo.
3. No se requiere GPU.
4. No se requiere montar Google Drive.
5. Si Colab no tuviera alguna dependencia disponible, descomentar la celda inicial de instalacion.

## Limitaciones

El notebook fue preparado en el repositorio local, pero no fue ejecutado localmente porque el entorno actual no tiene Python disponible en PATH. La verificacion final de metricas y graficos debe realizarse al abrirlo en Google Colab.

## Conclusiones

La entrega queda estructurada para comparar correctamente el enfoque valido de forecasting contra un holdout con shuffle. La solucion prioriza evitar leakage temporal, construir features causales y evaluar contra un baseline estacional fuerte mediante MASE.

