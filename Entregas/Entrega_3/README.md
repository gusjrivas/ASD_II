# Entrega 3 - Comparacion de Arquitecturas de Forecasting

## Objetivo

Resolver la Tarea 3 de Analisis de Series de Tiempo II mediante una comparacion controlada entre N-BEATS, N-HiTS y DeepAR sobre la demanda horaria del sistema Capital Bikeshare.

## Archivos

- Notebook de resolucion: `a1620_Tarea_3_Comparacion_de_Arquitecturas_de_Forecasting.ipynb`
- Explicacion de la entrega: `README.md`
- Notebook fuente: `../../Tareas/Tarea_3,_Comparacion_de_Arquitecturas_de_Forecasting.ipynb`

## Material de clase utilizado

Se utilizaron como referencia las diapositivas y practicas de la Clase 5, especialmente:

- `Clase 5/Codigo/Clase_5,_N_BEATS_vs_N_HiTS.ipynb`
- `Clase 5/Codigo/Clase_5,_Ejercicio_N_BEATS_vs_N_HiTS.ipynb`
- `Clase 5/Codigo/Clase_5,_Convoluciones_1D.ipynb`
- `Clase 5/Codigo/Clase_5,_TCN.ipynb`

De los ejemplos se conserva el formato long de NeuralForecast, la separacion temporal, el protocolo comun de entrenamiento, las metricas y la visualizacion comparativa. La resolucion agrega DeepAR y su intervalo probabilistico.

## Metodologia

La fecha y la hora se combinan en `ds`, `cnt` se renombra como `y` y se agrega un identificador constante. La serie se reindexa sobre una grilla horaria completa. Los huecos se completan sin mirar el futuro: primero con el valor de la misma hora de la semana anterior, luego con el de la misma hora del dia anterior y finalmente mediante propagacion del ultimo valor disponible.

Se usa un horizonte de 24 horas y una ventana de entrada de 168 horas. La semana de contexto permite representar simultaneamente la estacionalidad diaria, el ciclo semanal y la diferencia entre dias habiles y fines de semana. Las ultimas 24 horas, correspondientes al 31 de diciembre de 2012, se reservan como test. Las 24 horas anteriores del entrenamiento se usan como validacion interna para calcular la perdida de validacion; esta configuracion no activa detencion temprana.

Se fijan las semillas de Python, NumPy y PyTorch y se solicitan algoritmos deterministas para reducir la variabilidad entre ejecuciones. Esto mejora la reproducibilidad, aunque no garantiza resultados identicos entre distintas versiones de las librerias, plataformas o GPU.

## Modelos

N-BEATS y N-HiTS se entrenan con MAE. DeepAR se entrena con una DistributionLoss Student-t y genera una mediana y un intervalo predictivo del 90%. Los tres modelos comparten horizonte, ventana de entrada, pasos maximos de entrenamiento, escalado y semilla.

## Evaluacion

La tabla final informa MAE, RMSE y MAPE. MAPE excluye objetivos iguales a cero y el notebook informa cuantos casos fueron omitidos. La visualizacion superpone el historico reciente, el test, los tres pronosticos puntuales y la banda de DeepAR.

Los resultados guardados en el notebook son:

| Modelo | MAE | RMSE | MAPE |
| --- | ---: | ---: | ---: |
| N-BEATS | 27.015 | 40.934 | 83.39% |
| N-HiTS | 32.293 | 52.083 | 101.24% |
| DeepAR (mediana) | 66.425 | 87.877 | 112.41% |

N-BEATS obtiene el menor error puntual en esta ventana. El intervalo predictivo del 90% de DeepAR alcanza una cobertura empirica del 16.7% (4 de 24 horas).

## Como ejecutar en Google Colab

1. Abrir el notebook de resolucion en Google Colab.
2. Ejecutar las celdas de arriba hacia abajo.
3. Se requiere conexion para instalar NeuralForecast y descargar `hour.csv`.
4. Se recomienda GPU, aunque el notebook tambien puede ejecutarse en CPU.

## Limitaciones

El resultado principal corresponde a una unica ventana de 24 horas y una sola semilla. Ademas, el test es el 31 de diciembre de 2012, una fecha potencialmente atipica por ser vispera de Año Nuevo. Sirve para comparar los modelos en ese origen, pero no demuestra superioridad general ni permite concluir por si solo que DeepAR este descalibrado. El notebook propone robustecer la conclusion mediante rolling-origin, multiples semillas, metricas por horizonte y evaluacion de cobertura y ancho de los intervalos predictivos.
