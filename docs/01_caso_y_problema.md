# Actividad 1 — Presentación del caso y problema (5 puntos)

## Contexto
Operación minera a tajo abierto de cobre con una unidad de acarreo disponible y cuatro frentes activos o potenciales: A, B, C y D.

## Problema
¿Cómo asignar la próxima unidad de acarreo a un yacimiento con reservas, vía accesible y capacidad operacional compatible, buscando equilibrar distancia, disponibilidad de mineral y ley de cobre?

## Justificación de IA y ML
La búsqueda en IA permite evaluar alternativas y restricciones explícitas para elegir un destino. Como extensión **distinta de la búsqueda**, una regresión supervisada puede estimar el **tiempo de viaje de acarreo** según distancia, carga y ley del mineral, facilitando la planificación del turno. La regresión se entrena con datos simulados exclusivamente para este ejercicio.

## Objetivos
- Representar los estados y decidir un frente de destino factible.
- Comparar búsqueda exhaustiva, selección voraz por reservas y función de puntuación multicriterio.
- Predecir tiempo de viaje con regresión lineal y visualizar errores.

## Datos del caso
A: 5000 t, 12 km, 0.80 %; B: 12000 t, 25 km, 0.60 %; C: 0 t, 8 km, 0.00 %; D: 8000 t, 15 km, 0.90 %. En el material original las cuatro vías figuran habilitadas. Estos valores son ilustrativos, no observaciones de una mina real.

## Alcances y límites
Los tonelajes del caso son reservas del yacimiento, **no** carga efectiva de una unidad de acarreo. Los métodos de búsqueda aquí operan sobre cuatro destinos, no rutas por una red de vías. Por ello la puntuación multicriterio se rotula correctamente como heurística de decisión y **no como A* formal**. Para A* real sería necesario un grafo de rutas, costos acumulados g(n) y heurística admisible h(n).
