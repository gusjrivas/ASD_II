# Workflow con Codex

## 1. Crear o elegir una spec

Cada tarea, entrega o cambio importante debe tener una carpeta en:

```text
.openspec/specs/<nombre-del-trabajo>/
```

La carpeta debe incluir:

- `spec.md`: que hay que lograr;
- `plan.md`: como se va a encarar;
- `tasks.md`: checklist ejecutable;
- `notes.md`: decisiones, resultados y pendientes.

## 2. Contexto minimo para Codex

Antes de implementar, Codex debe leer:

```text
.openspec/project.md
.openspec/conventions.md
.openspec/workflow.md
.openspec/specs/<nombre-del-trabajo>/spec.md
```

Si existen `plan.md`, `tasks.md` o `notes.md`, tambien debe revisarlos.

## 3. Modo de trabajo

Para cambios chicos:

1. revisar la spec;
2. ejecutar las tareas pendientes;
3. actualizar `notes.md`.

Para tareas o entregas completas:

1. revisar consigna y material relacionado;
2. revisar clases teoricas y practicas relacionadas;
3. completar o ajustar `plan.md`;
4. completar o ajustar `tasks.md`;
5. implementar por pasos;
6. verificar resultados;
7. actualizar `notes.md`;
8. indicar archivos modificados.

## 4. Uso de clases como base

Las carpetas `Clase N/` son la referencia teorica y practica de la materia. Para cada entrega, Codex debe identificar que clases estan relacionadas y revisar sus materiales antes de resolver.

Prioridad de consulta:

- notebooks en `Clase N/Codigo/`;
- ejercicios practicos de clase;
- slides en `Clase N/Slides/`;
- resumentes o notebooks auxiliares.

La resolucion debe apoyarse en esos materiales cuando sea posible. El README de entrega debe listar las clases o archivos consultados y explicar brevemente como influyeron en la solucion.

## 5. Trabajo con Google Colab

Cuando el resultado sea un notebook para Colab:

1. crear o actualizar una carpeta especifica en `Entregas/`, por ejemplo `Entregas/Entrega_1/`;
2. crear o actualizar el `.ipynb` dentro de esa carpeta;
3. asegurar que no dependa de rutas locales absolutas;
4. incluir instalacion de paquetes solo cuando sea necesaria;
5. dejar imports y configuracion al inicio;
6. documentar como cargar datos;
7. verificar que el flujo sea ejecutable de arriba hacia abajo;
8. generar `README.md` dentro de la carpeta de entrega con la explicacion detallada de la resolucion;
9. registrar en `notes.md` cualquier paso manual requerido en Colab.

## 6. README por entrega

Cada resolucion de tarea debe incluir un README propio. El README no reemplaza al notebook: funciona como explicacion externa de lo que se hizo y por que.

Nombre recomendado:

```text
Entregas/Entrega_<numero>/README.md
```

La carpeta de entrega debe contener tambien el notebook de resolucion:

```text
Entregas/Entrega_<numero>/<nombre-de-la-tarea>.ipynb
```

Contenido minimo:

- objetivo;
- consigna resumida;
- archivos fuente y archivos generados;
- material de clase utilizado como referencia;
- pasos realizados;
- metodologia;
- decisiones tecnicas;
- validacion utilizada;
- resultados principales;
- instrucciones para ejecutar en Google Colab;
- conclusiones;
- pendientes o limitaciones.

## 7. Prompt recomendado

```text
Lee el contexto OpenSpec de este repo y trabaja sobre .openspec/specs/<nombre-del-trabajo>.
Primero revisa spec.md, plan.md, tasks.md y notes.md.
Antes de resolver, revisa las carpetas de clases relacionadas porque contienen material teorico y practico base.
Despues implementa las tareas pendientes, respetando las convenciones del proyecto.
Al finalizar, genera la carpeta de entrega con el notebook y README.md, y actualiza notes.md con resultados y pendientes.
```
