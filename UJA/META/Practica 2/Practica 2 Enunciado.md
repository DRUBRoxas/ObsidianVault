En esta práctica seguiremos trabajando con el problema del viajante de comercio (TSP) y en las secciones siguientes se describen el problema y los casos considerados, los aspectos relacionados con cada algoritmo a desarrollar y las tablas de resultados a obtener.

## **OBJETIVOS**

El objetivo de esta práctica es estudiar el funcionamiento de los algoritmos evolutivos en la resolución del problema del viajante de comercio (TSP). Para ello, se requerirá que se implementen los algoritmos:

●    Algoritmo evolutivo estacionario (EST)  
●    Algoritmo evolutivo generacional (GEN)

La fecha límite de entrega será el viernes **_22 de NOVIEMBRE de 2024 antes de las 23:00 horas_**. La entrega se realizará a través de la plataforma virtual.

## **CASOS DE ESTUDIO**

Dentro del material de las prácticas se encuentran disponibles distintos problemas con distinto tamaño.

El formato de los ficheros puede ser analizado en el documento del [Seminario 2](https://platea.ujaen.es/mod/resource/view.php?id=375711 "Seminario 2"). Para cada problema se cuenta con el fichero de datos de distancias euclídeas entre las distancias y un fichero con la mejor solución encontrada para cada problema.

La forma en que habitualmente se estima la calidad de un algoritmo es la siguiente: se ejecuta sobre un conjunto de ejemplos y se comparan los resultados obtenidos con las mejores soluciones conocidas para dichos problemas.

Además, los algoritmos pueden tener diversos parámetros o pueden emplear diversas estrategias. Para determinar qué valor es el más adecuado para un parámetro o saber la estrategia más efectiva los algoritmos también se comparan entre sí.

La comparación de los algoritmos se lleva a cabo fundamentalmente usando dos criterios, la calidad de las soluciones obtenidas y el tiempo de ejecución empleado para conseguirlas. Además, es posible que los algoritmos no se comporten de la misma forma si se ejecutan sobre un conjunto de instancias u otro.

Por otro lado, a diferencia de los algoritmos determinísticos, los algoritmos probabilísticos se caracterizan por la toma de decisiones aleatorias a lo largo de su ejecución. Este hecho implica que un mismo algoritmo probabilístico aplicado al mismo caso de un problema pueda comportarse de forma diferente y por tanto proporcionar resultados distintos en cada ejecución. Cuando se analiza el comportamiento de una metaheurística probabilística en un caso de un problema, se desearía que el resultado obtenido no estuviera sesgado por una secuencia aleatoria concreta que pueda influir positiva o negativamente en las decisiones tomadas durante su ejecución. 

Dada la influencia de la aleatoriedad en el proceso, es recomendable disponer de un generador de secuencia pseudoaleatoria de buena calidad con el que, dado un valor semilla de inicialización, se obtengan números en una secuencia lo suficientemente grande (es decir, que no se repitan los números en un margen razonable) como para considerarse aleatoria. 

Como norma general, el proceso a seguir consiste en realizar un número de ejecuciones diferentes de cada algoritmo probabilístico considerado para cada caso del problema. Es necesario asegurarse de que se realizan diferentes secuencias aleatorias en dichas ejecuciones. Así, el valor de la semilla que determina la inicialización de cada secuencia deberá ser distinto en cada ejecución y estas semillas deben mantenerse en los distintos algoritmos (es decir, la semilla para la primera ejecución de todos los algoritmos debe ser la misma, la de la segunda también debe ser la misma y distinta de la anterior, etc.). Para mostrar los resultados obtenidos con cada algoritmo en el que se hayan realizado varias ejecuciones, se deben construir tablas que recojan los valores correspondientes a estadísticos como el mejor y peor resultado para cada caso del problema, así como la media y la desviación típica de todas las ejecuciones. Alternativamente, se pueden emplear descripciones más representativas como los boxplots, que proporcionan información de todas las ejecuciones realizadas mostrando mínimo, máximo, mediana y primer y tercer cuartil de forma gráfica, Finalmente, se construirán unas tablas globales con los resultados agregados que mostrarán la calidad del algoritmo en la resolución del problema desde un punto de vista general.

**Este será el procedimiento que aplicaremos en las prácticas. Como norma general, _el alumno realizará 3 ejecuciones_ diferentes de cada algoritmo probabilístico considerado para cada caso del problema. Se considerará como semilla inicial el número del DNI del alumno al igual que hicimos en la [Práctica 1](https://platea.ujaen.es/mod/page/view.php?id=382711 "Práctica 1").**

## **ALGORITMOS**

### **1. ALGORITMO EVOLUTIVO GENERACIONAL**

Se implementará un algoritmo con los distintos componentes:

- **_Inicialización_** de una población de 100 individuos con un 80% de los individuos generados de forma aleatoria completamente, y el resto mediante un greedy aleatorizado con tamaño de lista de candidatos igual a 5. Lo tenemos implementado en la [práctica 1](https://platea.ujaen.es/mod/page/view.php?id=382711 "Práctica 1").
- **_Esquema de evolución_** generacional con élite E=1 y E=2.
- **_Operador de selección_** basada en un torneo binario con kBest=2 y kBest=3 aplicándose tantas veces como individuos tengamos en la población.
- **_Reemplazamiento_** que será realizado con el reemplazo de la población completa por la población descendiente. Para conservar el elitismo, si la mejor solución de la generación anterior no sobrevive, sustituye al peor de un torneo de perdedores de la nueva población con kWorst=3.
- **_Operador de cruce_** con una probabilidad del 70% se deberán implementar dos operadores el cruce de orden OX2 y el cruce MOC.
- **_Operador de mutación_** con una probabilidad del 10% por individuo será el operador de intercambio 2-opt que hemos empleado en la [práctica 1](https://platea.ujaen.es/mod/page/view.php?id=382711 "Práctica 1"), de forma, que si el individuo debe mutarse se seleccionan aleatoriamente dos posiciones distintas y se intercambian.
- **_Condición de parada_** de un máximo número de evaluaciones 50.000 ó 60 segundos.

### **2. ALGORITMO EVOLUTIVO ESTACIONARIO**

Se implementará un algoritmo con las distintas modificaciones del algoritmo anterior:

- **_Esquema de evolución_** estacionario con dos individuos.
- **_Operador de selección_** basada en un torneo binario con kBest=2 aplicándose solo para elegir dos individuos a evolucionar.
- **_Operador de cruce_** igual que el anterior, pero con una probabilidad del 100%.
- **_Reemplazamiento_** de los dos individuos en la población padre mediante un torneo de perdedores con kWorst=2.

### **COMPARACIONES DE ALGORITMOS**

En resumen, tenemos dos algoritmos con **TODAS ESTAS VERSIONES**:

- Gen: Cruce=OX2, M=100, E=1, kBest=2, kWorst=3.
- Gen: Cruce=OX2, M=100, E=1, kBest=3, kWorst=3.
- Gen: Cruce=OX2, M=100, E=2, kBest=2, kWorst=3.
- Gen: Cruce=OX2, M=100, E=2, kBest=3, kWorst=3.
- Gen: Cruce=MOC, M=100, E=1, kBest=2, kWorst=3.
- Gen: Cruce=MOC, M=100, E=1, kBest=3, kWorst=3.
- Gen: Cruce=MOC, M=100, E=2, kBest=2, kWorst=3.
- Gen: Cruce=MOC, M=100, E=2, kBest=3, kWorst=3.
- Est: Cruce=OX2, M=100, kBest=2, kWorst=2.
- Est: Cruces=MOC, M=100, kBest=2, kWorst=2.

Las comparaciones se hacen:

- 1) Generacionales con Cruce OX2
- 2) Generacionales con Cruce MOC
- 3) Mejor generacional OX2 vs. MOC, es decir, mejor de 1) vs. 2)
- 4) EstOX2 Vs. EstMOC
- Mejor generacional de la comparación anterior (3) Vs. Mejor estacionario de la comparación anterior (4) Vs. Mejor algoritmo de la [Práctica 1](https://platea.ujaen.es/mod/page/view.php?id=382711 "Práctica 1")

## **DOCUMENTACIÓN Y NORMATIVA**

Lee atentamente la normativa de entrega de prácticas:

- Solo se admitirá el formato ZIP. No se corregirán guiones en cualquier otro formato al indicado.
- La memoria que se acompañará en la entrega será exclusivamente en formato PDF y se incluirá una portada con:

- Identificación de los dos alumnos (Nombre, apellidos y DNI).
- Identificación del guion.
- Identificación del grupo de los alumnos.
- Algoritmos implementados en la práctica.

- El nombre de los ficheros tendrá el siguiente formato: “Ape11-Ape12-Ape21-Ape22-GuionX.zip”. Dentro se incluirá el fichero “Documentacion.pdf” junto con el código fuente, cuyo formato de entrega se detalla más adelante, donde:

- Ape11 es el primer apellido del primer alumno.
- Ape12 es el segundo apellido del primer alumno.
- Ape21 es el primer apellido del segundo alumno.
- Ape22 es el segundo apellido del segundo alumno.
- X es el número del guion.

Por ejemplo, para los alumnos cuyos apellidos sean García Vico y Carmona del Jesus, el fichero ZIP para el guion 1 tendrá como nombre: Garcia-Vico-Carmona-delJesus-Guion1.zip.

- Los ficheros con el código de los algoritmos deberán tener el siguiente formato (Nota: se pone como ejemplo un fichero Java) “AlgXX_ClaseXX_GrupoXX.java”
- La documentación a entregar en formato pdf debe incluir obligatoriamente los siguientes apartados:

- Una breve descripción de 2 páginas donde se detalle el problema y los algoritmos empleados, así como todas las restricciones y consideraciones empleadas por los alumnos para la implementación de las metaheurísticas solicitadas en el guion: esquema de representación de soluciones, descripción del código, función objetivo, operadores comunes, etc.
- Descripción en pseudocódigo de la estructura del método de búsqueda y de todas aquellas operaciones relevantes de cada algoritmo. Este contenido, específico a cada algoritmo se detallará en los correspondientes guiones de prácticas. El pseudocódigo deberá forzosamente reflejar la implementación y el desarrollo realizados y no ser una descripción genérica extraída de las transparencias de clase o de cualquier otra fuente. La descripción de cada algoritmo no deberá ocupar más de 6 páginas.
- Experimentos y análisis de resultados:

- Descripción de los valores de los parámetros considerados en las ejecuciones de cada algoritmo (incluyendo las semillas utilizadas).
- Resultados obtenidos según el formato especificado.
- Análisis de resultados. El análisis deberá estar orientado a justificar (según el comportamiento de cada algoritmo) los resultados obtenidos en lugar de realizar una mera “lectura” de las tablas. Se valorará la inclusión de otros elementos de comparación tales como gráficas de convergencia, boxplots, análisis comparativo de las soluciones obtenidas, uso de test estadísticos, representación gráfica de las soluciones, etc.
- Análisis de tiempos y desviaciones, e influencia del tamaño de la instancia en los resultados obtenidos, etc.
- Análisis de la mejor solución obtenida con una explicación de qué significa.
- Por último, es clave obtener un fichero de registro que vaya almacenando la información de la ejecución del algoritmo indicando las soluciones y costes que va obteniendo en las distintas iteraciones siempre que haya un cambio a mejor, o incluso a peor. Se deberá subir los ficheros “log” a Google Drive e indicar en el informe el directorio para consultarlos.

- Referencias bibliográficas u otro tipo de material distinto del proporcionado en la asignatura que se haya consultado para realizar la práctica (en caso de haberlo hecho).

_NOTA_: Aunque lo esencial es el contenido, también debe cuidarse la presentación y la redacción. La documentación nunca deberá incluir listado total o parcial del código fuente.