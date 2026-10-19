# Optimización de asignación de acarreo minero mediante Inteligencia Artificial y Machine Learning

## Descripción del proyecto

Este proyecto presenta una aplicación de **Inteligencia Artificial (IA)** y **Machine Learning (ML)** para apoyar la toma de decisiones en una operación minera a tajo abierto de cobre. El trabajo combina dos enfoques complementarios: un sistema de **búsqueda y evaluación de alternativas**, que selecciona un frente de explotación para asignar un camión de acarreo, y un **modelo predictivo de regresión**, que estima el tiempo de viaje durante las operaciones de transporte.

El propósito es mostrar cómo representar formalmente una decisión operativa, analizar restricciones, comparar estrategias de selección y utilizar datos para anticipar una variable relevante para la planificación minera.

## Problema abordado

Una operación minera dispone de un camión de acarreo que debe ser asignado a uno de cuatro frentes de explotación: **A, B, C o D**. Cada frente presenta características diferentes en cuanto a reservas disponibles, distancia de traslado, ley de cobre y accesibilidad.

La elección del destino no debería basarse en un solo criterio: seleccionar únicamente el frente más cercano, por ejemplo, podría conducir a un yacimiento sin reservas disponibles. Por ello, se plantea una evaluación que primero descarte opciones inviables y después compare las alternativas restantes.

Como complemento, se desarrolla un modelo que **predice el tiempo de viaje** a partir de variables operativas. Esta estimación puede contribuir a la planificación de desplazamientos, aunque los resultados de este ejercicio no sustituyen mediciones ni validaciones de campo.

## Objetivos

**Objetivo general:** desarrollar un flujo de razonamiento y predicción aplicado a la asignación de acarreo en minería mediante técnicas de IA y aprendizaje supervisado.

**Objetivos específicos:**

- Representar el problema como un espacio de estados, con operadores, restricciones y un estado objetivo.
- Identificar qué frentes de explotación son factibles para recibir el camión.
- Comparar distintas estrategias de selección de alternativas.
- Entrenar y evaluar un modelo de regresión para estimar tiempos de viaje.
- Visualizar los resultados de búsqueda y predicción para facilitar su interpretación.

## Datos del caso de estudio

Los frentes de explotación considerados tienen las siguientes características:

| Frente | Reservas (t) | Distancia (km) | Ley de cobre (%) | Acceso vial |
|:--|--:|--:|--:|:--|
| A | 5 000 | 12 | 0,80 | Habilitado |
| B | 12 000 | 25 | 0,60 | Habilitado |
| C | 0 | 8 | 0,00 | Habilitado |
| D | 8 000 | 15 | 0,90 | Habilitado |

Estos datos corresponden al **caso didáctico** desarrollado en el notebook inicial. Las reservas representan mineral disponible en cada frente, **no** la carga transportada en un único viaje. Para ilustrar las restricciones de capacidad, el pipeline incorpora como supuestos adicionales un camión de 150 t y una carga planificada de 120 t.

## Metodología

### 1. Representación y búsqueda de soluciones

El estado inicial corresponde a un camión disponible, aún sin destino. Las acciones posibles son asignarlo a los frentes A, B, C o D. Antes de considerar una asignación válida, se verifican las reservas, la accesibilidad y la compatibilidad entre la carga planificada y la capacidad del camión.

El notebook compara tres estrategias:

- **Búsqueda exhaustiva:** analiza todas las alternativas factibles.
- **Selección voraz por reservas:** prioriza el frente con mayor cantidad de mineral disponible.
- **Evaluación heurística multicriterio:** considera conjuntamente distancia, reservas y ley de cobre mediante una función de puntuación.

La función multicriterio utilizada en el caso es:

```text
puntuación = distancia_km - reservas_ton / 1000 - ley_cobre_pct * 10
```

Se prefiere la alternativa factible con la **menor puntuación**. Los coeficientes tienen carácter ilustrativo y no constituyen una función de costos operativos validada. Aunque el notebook original hacía referencia a A*, este ejercicio realiza una **evaluación heurística de destinos**, no una implementación formal del algoritmo A* para búsqueda de rutas.

### 2. Predicción del tiempo de viaje

La segunda parte utiliza un enfoque de **aprendizaje supervisado**, específicamente **regresión lineal múltiple**, para estimar el tiempo de viaje de acarreo en minutos.

- **Variables de entrada:** distancia recorrida (km), carga transportada (t) y ley de cobre (%).
- **Variable objetivo:** tiempo de viaje (min).
- **Datos:** 240 registros **sintéticos** creados para demostrar el procedimiento.
- **Evaluación:** error absoluto medio (MAE), raíz del error cuadrático medio (RMSE) y coeficiente de determinación (R²).

El flujo comprende la revisión de datos, la separación de conjuntos de entrenamiento y prueba, el ajuste del modelo, la generación de predicciones y la visualización de los errores.

## Resultados e interpretación

En el escenario analizado, el frente **C queda descartado** porque no tiene reservas. La selección por mayor disponibilidad de mineral prioriza el frente **B**, mientras que la puntuación multicriterio favorece el frente **D**. Esto muestra que una misma decisión puede producir resultados distintos según los criterios utilizados.

En el experimento de regresión con datos sintéticos se obtuvieron aproximadamente los siguientes indicadores:

| Indicador | Valor aproximado |
|:--|--:|
| MAE | 2,62 min |
| RMSE | 3,36 min |
| R² | 0,965 |

Estas métricas describen el desempeño del modelo **sobre datos generados artificialmente**. No permiten afirmar que tendría el mismo rendimiento en una mina real. Los notebooks incluyen gráficos de comparación entre tiempos reales simulados y tiempos predichos, así como análisis de residuos.

## Estructura del repositorio

```text
mineria-ml-pipeline/
├── README.md                         # Presentación y explicación del proyecto
├── requirements.txt                  # Dependencias de Python
├── .gitignore
├── docs/
│   ├── 01_caso_y_problema.md         # Contexto, planteamiento y objetivos
│   └── 02_espacio_estados.md         # Estados, operadores y restricciones
├── data/
│   ├── README.md
│   ├── yacimientos.csv               # Datos de los cuatro frentes
│   └── operaciones_sinteticas.csv    # Datos para el modelo predictivo
├── notebooks/
│   ├── 01_busqueda_optimizacion.ipynb # Razonamiento y selección de frentes
│   └── 02_regresion_prediccion.ipynb # Entrenamiento y evaluación de regresión
└── images/                           # Espacio para gráficos exportados/presentaciones
```

## Alcances y limitaciones

Este desarrollo es un **prototipo académico** orientado a representar decisiones y explicar una metodología reproducible. La selección multicriterio no incorpora costos reales de combustible, pendientes, tiempos de carga y descarga, tráfico interno o condiciones geomecánicas. Asimismo, el modelo predictivo fue entrenado con datos sintéticos. Una aplicación operativa requeriría información histórica real, revisión de variables relevantes, ajuste de los criterios de decisión y validación con especialistas de la mina.

## Conclusiones

La representación de estados y restricciones permite descartar destinos inviables antes de evaluar alternativas. La comparación entre estrategias evidencia que la definición de los criterios de decisión influye directamente en el frente seleccionado. Por su parte, la regresión lineal múltiple muestra cómo podría estructurarse un modelo predictivo para apoyar la estimación de tiempos de acarreo.

En conjunto, ambos pipelines ilustran dos aplicaciones complementarias de la IA en minería: **elegir entre opciones disponibles** y **estimar resultados operativos a partir de datos**.
