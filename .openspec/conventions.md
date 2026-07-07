# Convenciones

## Idioma

Usar espanol para explicaciones, conclusiones, nombres de secciones y notas academicas.

Usar ingles solo cuando corresponda por nombres de librerias, funciones, variables tecnicas establecidas o APIs.

## Notebooks

Para notebooks de tareas y entregas:

- mantener una narrativa clara en celdas Markdown;
- separar carga de datos, exploracion, feature engineering, modelado, validacion y conclusiones;
- evitar celdas sueltas sin contexto;
- conservar la consigna original cuando sea util para rastrear el objetivo;
- no borrar material de clase o enunciado salvo que se cree una copia de trabajo;
- priorizar reproducibilidad sobre experimentos aislados.
- cuando la consigna este dividida en partes, conservar el titulo de cada parte y resolverla inmediatamente debajo;
- en cada parte, comenzar con una breve seccion `Resolucion` y luego incluir el codigo que implementa esa parte;
- evitar que una parte dependa visualmente de codigo "hecho antes" sin mostrar donde se resuelve;
- si una variable, grupo de features, particion o modelo es pedido explicitamente por la consigna, dejar su definicion visible en codigo debajo de la parte correspondiente;
- redactar las explicaciones academicas en voz impersonal;
- incluir al inicio de la resolucion los datos del alumno cuando el usuario los indique;
- dejar conclusiones desarrolladas, conectando metodologia, resultados, interpretacion y limitaciones, no solo una lista de afirmaciones generales.

## Material de clase

Las carpetas `Clase N/` contienen material teorico y practico que debe usarse como base para resolver las entregas.

Antes de resolver una tarea, revisar el material de clase relacionado:

- slides teoricas en `Clase N/Slides/`;
- notebooks explicativos en `Clase N/Codigo/`;
- ejercicios practicos vistos en clase;
- resumentes o notebooks de apoyo.

La solucion debe estar alineada con los conceptos, metodologia y ejemplos de clase. Si se usa una tecnica distinta o adicional, explicarla y justificar por que aporta valor a la entrega.

El README de cada entrega debe mencionar que material de clase fue utilizado como referencia.

## Google Colab

Los notebooks deben estar pensados para ejecutarse en Google Colab:

- incluir una celda inicial de instalacion de dependencias solo si es necesaria;
- evitar rutas absolutas locales de Windows;
- usar rutas relativas o una configuracion clara para Google Drive cuando haga falta;
- dejar imports concentrados al inicio del notebook;
- definir semillas aleatorias cuando aplique;
- evitar dependencias innecesarias o muy pesadas;
- documentar si se requiere GPU, CPU o acceso a Drive;
- mantener salidas importantes, pero limpiar salidas excesivamente grandes.

Cuando se use Google Drive, preferir una celda explicita y facil de activar:

```python
from google.colab import drive
drive.mount("/content/drive")
```

No asumir que el notebook tiene acceso automatico a archivos locales del repo si se ejecuta en Colab.

## Python

Para codigo Python:

- usar `pandas`, `numpy`, `matplotlib`, `scikit-learn` y librerias de boosting cuando correspondan a la consigna;
- escribir funciones auxiliares cuando reduzcan duplicacion o aclaren el flujo;
- mantener nombres de variables descriptivos;
- evitar logica oculta en celdas desordenadas;
- mostrar metricas y graficos relevantes para justificar decisiones.

## Series de tiempo

Para todo analisis de series temporales:

- respetar el orden temporal;
- evitar leakage temporal;
- explicitar la estrategia de validacion;
- diferenciar entrenamiento, validacion y test;
- justificar ventanas temporales, lags, rolling features y horizonte de prediccion;
- comparar contra baselines simples cuando corresponda.

## Entregas

Los archivos finales deben ir en `Entregas/`, organizados en una carpeta por entrega.

Cuando se trabaje desde una consigna en `Tareas/`, preferir crear una carpeta de entrega antes de modificar o resolver el trabajo, salvo que el usuario pida trabajar directamente sobre el archivo base.

Las entregas deben ser notebooks `.ipynb` compatibles con Google Colab, salvo que la consigna pida otro formato.

Por cada tarea resuelta se debe generar una carpeta especifica dentro de `Entregas/`. Esa carpeta debe hacer referencia a la tarea resuelta y contener la resolucion completa.

Formato recomendado:

```text
Entregas/
  Entrega_1/
    Tarea_1_Feature_Engineering_y_Validacion_Temporal_con_GBM.ipynb
    README.md
```

Dentro de cada carpeta de entrega debe existir:

- notebook `.ipynb` compatible con Google Colab;
- `README.md` con la explicacion detallada de como se resolvio;
- archivos auxiliares necesarios, si la consigna lo requiere.

El `README.md` de la entrega debe incluir:

- objetivo de la tarea;
- archivos utilizados;
- material de clase consultado;
- resumen de la consigna;
- metodologia aplicada;
- preparacion de datos;
- estrategia de validacion temporal;
- features creadas;
- modelos entrenados;
- metricas obtenidas;
- interpretacion de resultados;
- decisiones tomadas;
- problemas encontrados;
- instrucciones para ejecutar el notebook en Google Colab;
- conclusiones finales.

## Nombres

Usar nombres descriptivos y estables:

```text
Entregas/Entrega_1/Tarea_1_Feature_Engineering_y_Validacion_Temporal_con_GBM.ipynb
Entregas/Entrega_1/README.md
```

Evitar nombres ambiguos como `final.ipynb`, `prueba.ipynb` o `nuevo.ipynb`.

## Verificacion

Antes de dar por terminada una tarea:

- revisar que el notebook ejecute de arriba hacia abajo si el entorno lo permite;
- revisar que el notebook pueda abrirse en Google Colab;
- revisar que exista un README de entrega claro y completo;
- documentar errores si no se puede ejecutar;
- revisar que las metricas y conclusiones esten conectadas;
- actualizar `notes.md` con resultados y pendientes.
