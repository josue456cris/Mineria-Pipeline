# Challenge 1 — Pipeline de Machine Learning | Minería

**Curso:** Machine Learning · **Caso:** asignación de un camión de acarreo a frentes de un tajo abierto de cobre. Este repositorio desarrolla **las cuatro asignaciones** del Challenge 1 (individual): presentación del problema, espacio de estados, pipeline de búsqueda y pipeline de predicción con regresión.

**Estudiante:** Josue Cristhian Mateo Mogollon Flores (nombre tomado del notebook proporcionado; modificar si corresponde). **Docente:** Yannick Patrick Carrasco Merma.

## 1. Caso y problema (5 puntos)
Un camión disponible debe asignarse a uno de cuatro frentes de explotación. Se consideran reservas, distancia, ley de cobre y acceso. Los datos y la formulación se explican en [`docs/01_caso_y_problema.md`](docs/01_caso_y_problema.md). Se justifica el uso de IA para decisión y de ML para estimación de tiempos.

## 2. Espacio de estados (5 puntos)
Estado inicial: camión disponible. Operadores: asignar A, B, C o D. Restricciones: reservas positivas, acceso habilitado y carga admisible. La descripción formal y el diagrama están en [`docs/02_espacio_estados.md`](docs/02_espacio_estados.md). El primer notebook dibuja el grafo.

## 3. Pipeline de razonamiento, búsqueda y resultados (5 puntos)
[`notebooks/01_busqueda_optimizacion.ipynb`](notebooks/01_busqueda_optimizacion.ipynb): Problema → Estados → Exploración → Búsqueda (exhaustiva, voraz e informada por puntuación) → Resultado. La estrategia por reservas elige B y el score ponderado elige D.

## 4. Pipeline de modelo predictivo y visualización (5 puntos)
[`notebooks/02_regresion_prediccion.ipynb`](notebooks/02_regresion_prediccion.ipynb): datos sintéticos → inspección → división entrenamiento/prueba → regresión lineal múltiple → métricas MAE, RMSE, R² → gráficos predicción vs. valor y residuos. Variable objetivo: **tiempo de viaje (minutos)**.

## Cómo ejecutar en Google Colab
1. Sube **toda** esta carpeta a un nuevo repositorio público de GitHub llamado `mineria-ml-pipeline` (la URL puede diferir si lo nombras de otra manera).
2. En GitHub, abre `notebooks/01_busqueda_optimizacion.ipynb` y pulsa **Open in Colab** si aparece, o entra a Colab → Archivo → Abrir cuaderno → GitHub y pega la URL del repositorio. Repite para el segundo notebook.
3. En Colab: Entorno de ejecución → Ejecutar todas. Si los enlaces a archivos aún contienen `USUARIO`, los notebooks incluyen datos de respaldo para permitir ejecución; **es preferible sustituir `USUARIO` por tu usuario real de GitHub**.
4. Si trabajas localmente: `pip install -r requirements.txt` y abre ambos notebooks desde la carpeta `notebooks/` usando Jupyter/VS Code.
5. Guarda los cambios de notebooks en GitHub (Colab: Archivo → Guardar una copia en GitHub).

## Advertencias metodológicas
- El notebook original denomina “A*” a un cálculo de score. Aquí se identifica correctamente como **heurística multicriterio**; no es A* sobre caminos.
- Las reservas de los frentes no son cargas por viaje. Camión 150 t y carga planificada 120 t son supuestos complementarios didácticos.
- El score es una regla comparativa ilustrativa, no una medida física validada ni una función empresarial calibrada.
- Los 240 registros del modelo predictivo son **simulados** y no deben interpretarse como mediciones mineras.

## Estructura
```text
mineria-ml-pipeline/
├── README.md
├── requirements.txt
├── .gitignore
├── docs/
│   ├── 01_caso_y_problema.md
│   └── 02_espacio_estados.md
├── data/
│   ├── README.md
│   ├── yacimientos.csv
│   └── operaciones_sinteticas.csv
├── notebooks/
│   ├── 01_busqueda_optimizacion.ipynb
│   └── 02_regresion_prediccion.ipynb
├── src/                 # opcional: futuras funciones reutilizables
└── images/              # opcional: exportaciones de gráficos
```
