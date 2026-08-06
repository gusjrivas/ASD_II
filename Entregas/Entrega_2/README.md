# Entrega 2 - Global Forecasting Multivariado

## Objetivo

Resolver la Tarea 2 de Analisis de Series de Tiempo II usando la serie horaria de contaminacion de Beijing. La entrega convierte la serie en un panel y compara un baseline, modelos recurrentes locales y globales, y modelos globales con embedding categorico.

## Archivos

- Notebook de resolucion: `a1620_Tarea_2_Global_Forecasting_Multivariado.ipynb`
- Explicacion de la entrega: `README.md`
- Notebook fuente: `../../Tareas/Tarea 2, Global Forecasting Multivariado.ipynb`

## Material de clase utilizado

Se uso como referencia el material teorico y practico de:

- `Clase 3/Codigo/Clase_3,_LSTM,_GRU_y_Benchmark_contra_el_Naive.ipynb`
- `Clase 3/Codigo/Clase_3,_Rollout_Recursivo.ipynb`
- `Clase 4/Codigo/Clase_4,_Exploracion_de_Series_Multivariadas.ipynb`
- `Clase 4/Codigo/Clase_4,_Global_Forecasting_Models.ipynb`
- `Clase 4/Codigo/Clase_4,_Embeddings_Categoricos.ipynb`

De esos materiales se tomaron especialmente estas ideas:

- construir ventanas respetando el orden temporal;
- comparar las redes contra un baseline estacional;
- estandarizar cada serie usando solamente el tramo de entrenamiento;
- diferenciar modelos locales, entrenados por serie, de un modelo global entrenado sobre un pool;
- incorporar la identidad de cada serie mediante un embedding repetido a lo largo de la secuencia.

## Resumen de la consigna

La tarea pide convertir una serie en un panel de entre 4 y 12 series, definir una ventana de entrada, un horizonte de 24 horas y un test temporal. Luego se deben comparar siete configuraciones: un baseline, dos arquitecturas recurrentes en versiones local y global, y las dos versiones globales con embedding.

La comparacion debe incluir MAE, cantidad total de parametros, numero de modelos entrenados y mejora porcentual frente al baseline. Tambien se deben responder dos preguntas conceptuales sobre modelos globales y estabilidad de la mejora producida por embeddings.

## Metodologia aplicada

La serie se divide en cinco series identificadas por año, desde 2010 hasta 2014. Esta segmentacion conserva la frecuencia horaria y la variable pollution original. Cada modelo recibe una ventana multivariada de 168 horas y predice directamente pollution 24 horas despues de la ultima observacion de entrada.

Las covariables son punto de rocio, temperatura, presion y velocidad acumulada del viento. Cada variable se estandariza por serie usando media y desvio del entrenamiento.

## Validacion temporal

Los ultimos 30 dias, equivalentes a 720 horas, se reservan como test en cada serie. Todas las configuraciones se evaluan sobre esas mismas observaciones. Para early stopping se usa el ultimo 15% del entrenamiento de cada serie como validacion.

El test mantiene el orden temporal. Sus ventanas pueden utilizar observaciones del final del entrenamiento, porque esa informacion estaria disponible al emitir el pronostico, pero ningun objetivo de test participa del ajuste ni del escalado.

## Modelos y metricas

El baseline es un naive estacional diario: usa como pronostico el valor observado 24 horas antes.

El Modelo A contiene una GRU y una capa de salida. El Modelo B combina una LSTM y una GRU. Se entrenan cinco copias de cada arquitectura para los enfoques locales y una sola copia para cada enfoque global. Las dos configuraciones globales se repiten incorporando un embedding de `series_id`.

La tabla final informa:

- MAE en la escala original de PM2.5;
- parametros totales que deben mantenerse;
- cantidad de modelos entrenados;
- mejora porcentual frente al baseline.

## Respuestas de analisis

El notebook explica por que el pooling puede permitir que un modelo global supere a modelos locales, en que condiciones puede aparecer transferencia negativa y que evidencia hace falta para evaluar una mejora de 3% producida por un embedding.

La propuesta de evaluacion incluye semillas emparejadas, intervalos de confianza sobre diferencias de MAE, resultados por serie y validacion rolling origin.

## Como ejecutar en Google Colab

1. Abrir `a1620_Tarea_2_Global_Forecasting_Multivariado.ipynb` en Google Colab.
2. Ejecutar las celdas de arriba hacia abajo.
3. Se requiere conexion para descargar `pollution.csv`.
4. No es obligatorio usar GPU, aunque puede reducir el tiempo de entrenamiento.
5. Si alguna dependencia no estuviera disponible, descomentar la celda inicial de instalacion.

## Limitaciones

La comparacion principal usa una semilla y un unico holdout temporal. Por eso permite describir el rendimiento en este periodo, pero no demostrar superioridad general. El notebook deja explicitado como ampliar la evaluacion mediante varias semillas y multiples origenes temporales.

## Conclusiones

La entrega compara las siete configuraciones pedidas bajo el mismo protocolo temporal. La solucion prioriza conservar la serie horaria original, definir sin ambiguedad el horizonte de 24 horas, evitar leakage y evaluar la precision junto con el costo de mantenimiento.
