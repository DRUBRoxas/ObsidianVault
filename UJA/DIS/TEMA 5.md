## Introducción

>[!info]
>En este tema se busca dar por culo, y utilizar absolutas putísimas mierdas que nadie a día de hoy hace a mano, pero a su vez es el mas importante de la asignatura. Vivan los toros y Mucha suerte

El objetivo de este tema es diseñar y configurar nuestro sistema para conseguir el mayor rendimiento, es decir, necesitamos evaluar el actual o futuro sistema

Posibilidades:
* Monitorización (medir)
	* Herramientas de medida sobre el sistema real
* Referenciación (Benchmarking)
	* Comparación del rendimiento de sistemas modelados o reales
* Modelado (predecir)
	* Reproducción de comportamientos del sistema
	* Métodos analíticos (Redes de colas, cadenas de Markov, redes de Petri, ...)
	* Simulación discreta (CSIM, SMPL, Simula,  ...)

## Rendimiento

### Índices clásicos de medición de rendimiento
Intuitivamente un índice básico para medir rendimiento puede ser el tiempo que se tarda en realizar una tarea

Después aparecen otros:
* Frecuencia de reloj
* Ciclos por instrucción
* MIPS
* MFLOPS
* etc.

### Frecuencia de reloj (f) y  Tiempo de Ciclo (T)

*Señal de reloj:* señal cuadrada periódica para sincronizar el funcionamiento del procesador
Ejemplo:
- Procesador con reloj 500 MHz o 0.5GHz 
![[Frecuencia de Reloj#Formula]]
$$
T=Ciclo de Reloj=\frac{1}{500MHz}=\frac{1}{500x10^6Hz}=2x10^{-9}s=2ns
$$
### Ciclos por Instrucción
* Ciclos empleados por el procesador para ejecutar una instrucción
* Es un valor medio que depende de la instrucción ejecutada. Interesa minimizarlo
* Depende de la organización y la arquitectura
* Inconveniente: ignora el tiempo imprevisible que aparecen en la ejecución del programa habitual (riesgos)
#FormulasServidores 
$$
CPI=\frac{\text{Ciclos de reloj de CPU Usados}}{\text{Instrucciones Ejecutadas}}=\frac{\text{Tiempo De Ejecución * Frecuencia  de  reloj}}{\text{Instrucciones Ejecutadas}}
$$
### Estimación del CPI medio de un programa
Cada instrucción necesita de un determinado número de ciclos, y por tanto, el valor de CPI depende de las instrucciones ejecutadas por cada programa

| Instrucciones                     | Porcentaje | Ciclos |
| --------------------------------- | ---------- | ------ |
| Instrucciones de escritura(store) | 12%        | 2      |
| Instrucciones de Lectura(load)    | 21%        | 2      |
| Instrucciones de la ALU           | 43%        | 1      |
| Instrucciones de salto            | 24%        | 2      |
**CPI = 1.57**

$$
Tiempo de Ejecución=\frac{\text{Instrucciones Ejecutadas}*CPI}{Frecuencia de reloj}
$$

### MIPS (Millions of Instructions Per Second)

#### MIPS Nativos
+ Depende del juego de instrucciones y los MIPS medidos varían entre programas en el mismo computador
+ *Meaningless indicator of processor speed*
$$
MIPS=\frac{\text{Instrucciones Ejecutadas}}{Tiempo de Ejecución *10^6}=\frac{Frecuencia de  reloj de la CPU}{CPI*10^6}
$$
#### MIPS relativos
* Referidos a una máquina de referencia (proceso de normalización)
* Problema: Establecer la referencia
$$
MIPS_{relativos}=\left(\frac{\text{Tiempo de referencia}}{\text{Tiempo de ejecución}}\right)*MIPS_{referencia}
$$
#### Ejemplos
* El programa P contiene $200*10^6$ instrucciones
* Procesador 1 (175MHZ): ejecuta P en 10s
* Procesador 2 (400MHz) ejecuta P en 5s
$$
MIPS_1=\frac{\text{Instrucciones Ejecutadas}}{\text{Tiempo de Ejecución} *10^6}=\frac{200*10^6}{10*10^6}=20
$$
$$
MIPS_2=\frac{\text{Instrucciones Ejecutadas}}{\text{Tiempo de Ejecución} *10^6}=\frac{200*10^6}{5*10^6}=40
$$
$$
CPI_1=\frac{\text{Ciclos de reloj de CPU Usados}}{\text{Instrucciones Ejecutadas}}=\frac{10*175*10^6}{200*10^6}=8.75
$$
$$
CPI_2=\frac{\text{Ciclos de reloj de CPU Usados}}{\text{Instrucciones Ejecutadas}}=\frac{5*400*10^6}{200*10^6}=10
$$

### MFLOPS

Basado en operaciones y no en instrucciones

* El tiempo de ejecución de la forma es el del programa, incluyendo el tiempo consumido por las instrucciones de enteros

$$
MFLOPS=\frac{\text{Operaciones de coma flotante ejecutadas}}{\text{Tiempo de ejecución}*10^6}
$$
* Problema: El formato de los números en coma flotante puede variar de una arquitectura a otra, y por tanto, tener diferente precisión.

#### MFLOPS normalizados
* Consideran la complejidad de las operaciones en coma flotante
	* Suma, resta, multiplicación, comparación, negación: poco costosas
	* División, raíz cuadrada: costosas
	* Trigonométricas: muy costosas
* Ejemplo de normalización de operaciones en coma flotante 
	* ADD, SUB, COMPARE, MULT ⇒ 1 operación normalizada 
	* DIVIDE, SQRT ⇒ 4 operaciones normalizadas
	* EXP, SIN, ATAN ⇒ 8 operaciones normalizadas
#### Ejemplos
* Programa Spice: El computador DECStation 3100 tarda 94 segundos en ejecutarlo
	* Contiene 109.970.178 operaciones de coma flotante de las cuales:
	* 15.682.333 son divisiones (DIVD)
	* El resto tiene una complejidad similar a la suma
$$
MFLIPS_{nativos}=\frac{109.970.178}{94*10^6}=1,2
$$
$$
MFLIPS_{normalizados}=\frac{94.287.845+15.685.333*4}{94*10^6}=1,2
$$
> [!note]
> Por si eres corto como yo, el 94 millones sale de restar el total menos los 15 millones de divisiones xD


### Comparación de prestaciones
**Objetivo:** Comparar dos equipos con diferentes configuraciones hardware y/o software.

Para evaluar el rendimiento de un sistema, se ejecutan los programas reales (o los más parecidos a los mismos). Se compararán y para el más rápido se podrá medir la ganancia en prestaciones se conoce como aceleración.

#### Medidas de comparación
+ "El equipo X es A veces más rápido que Y"
$$
Aceleración=\frac{\text{Tiempo de ejecución}_Y}{\text{Tiempo de ejecución}_X}=\frac{Rendimiento_X}{Rendimiento_Y}
$$
* "El equipo X es un n% más rápido que Y"
$$
\frac{\text{Tiempo de ejecución}_Y}{\text{Tiempo de ejecución}_X}=\frac{Rendimiento_X}{Rendimiento_Y}=1.0+\frac{n}{100}
$$
* Puede causar confusión:
	* "El computador X es un n% MEJOR que Y"
	* "El computador Y es un n% más LENTO que X"
*Ejemplo*:
Un programa se ejecuta en 36 s en el computador VERDE y en 45 s en el computador ROJO


$$
A=\frac{\text{Tiempo }_{ROJO}}{\text{Tiempo }_{VERDE}}=\frac{45s}{36s}=1.25=1.0+\frac{25}{100}
$$
* El computador VERDE es 1.25 veces más rápido que el ROJO 
* El computador VERDE es un 25% más rápido
* El computador ROJO tarda un 25% más de tiempo que el verde en ejecutar el programa
* El computador VERDE cuesta 625€
* El computador ROJO cuesta 550€
$$
∆C=\frac{\text{Coste }_{VERDE}}{\text{Coste }_{ROJO}}=\frac{\text{625€}}{\text{625€}}=1.14=1.0+\frac{14}{100}
$$
* El computador VERDE es 1.14 veces **más caro** que el ROJO
* El computador VERDE es un 14% **más caro** que el ROJO

En comparaciones de sistemas, en ausencia de otra información, siempre interesará elegir aquellas opciones que maximicen el cociente prestaciones / coste
$$
\frac{\text{Rendimiento }_{ROJO}}{\text{Coste }_{ROJO}}=\frac{1}{\text{Tiempo }_{ROJO}*\text{Coste }_{ROJO}}=\frac{1}{45*550}=4.04*10^{-5}
$$
$$
\frac{\text{Rendimiento }_{VERDE}}{\text{Coste }_{VERDE}}=\frac{1}{\text{Tiempo }_{VERDE}*\text{Coste }_{VERDE}}=\frac{1}{36*625}=4.44*10^{-5}
$$
En este caso, el computador VERDE presenta una relación ligeramente más alta que el ROJO

### Límites en la mejora del tiempo de respuesta
* La mejora del tiempo de respuesta en la ejecución de un proceso no es ilimitada
* Hay que saber hacia donde dirigir los esfuerzos de optimización
* La mejora de cualquier sistema usando un componente más rápido depende del tiempo que éste se utilice
* Discusión preliminar
	* Un sistema tarda un tiempo $T_{original}$ en ejecutar un proceso/programa
	* Mejoramos el sistema acelerando k veces uno de sus componentes
	* Este componente se utiliza durante una fracción $f$ del tiempo $T_{original}$ 
	* ¿Cuál es la ganancia en prestaciones A (speedup) del sistema con respecto a ese programa?![[Pasted image 20250105175543.png]]
### Ley de Amdahl

#### Formula:
$$
A=\frac{1}{(1-f)+(\frac{f}{k})}
$$
* Casos particulares de la ley
	* Si f=0 → A=1: no hay ninguna mejora en el sistema
	* Si f=1 → A=k: el sistema mejora igual que el componente
#### Ejemplo
La utilización del disco duro es del 60% para un programa dado. ¿En cuánto aumentará el rendimiento del sistema si se duplica la velocidad del disco (k=2)?

$$
A=\frac{1}{(1-0.6)+(\frac{0.6}{2})}=1.43
$$
* El rendimiento aumenta 1.43 veces (Es decir, un 43%)
Aceleración máxima que se puede conseguir:
$$
\lim _{k \rightarrow \infty} A=\frac{1}{(1-f)}=\frac{1}{(1-0.6)}=2.5
$$
![[Pasted image 20250105181234.png]]
#### Generalización de la ley de Amdahl
* Caso con una mejora Solamente
$$
A=\frac{1}{(1-f)+\left(\frac{f}{k}\right)}
$$
* Caso con n mejoras
$$
A=\frac{1}{\left(1-\sum_{i=1}^n f_i\right)+\sum_{i=1}^n\left(\frac{f_i}{k_i}\right)}
$$
#### Reflexiones finales
* Una mejora es más efectiva cuanto más grande es la fracción de tiempo en que ésta se aplica.
* Para mejorar un sistema complejo hay que optimizar los elementos que se utilicen durante la mayor parte del tiempo (caso más común)
* Con la ley de Amdahl podemos estimar la aceleración A(speedup) de la ejecución de *un único programa* en un sistema después de acelerar *k* veces un componente, es decir, su tiempo de respuesta óptimo en ausencia de otros programas.
### Análisis operacional
* Me la suda quien lo presente
* Basado en magnitudes medibles del sistema informático
![[Pasted image 20250105182007.png]]
* Leyes operacionales: relaciones entre las magnitudes medibles.
* Límites asintóticos de las prestaciones por medio de cálculos muy sencillos.
* Se utiliza en el modelado de las redes de colas
### Estación de Servicio
Objeto abstracto compuesto por un dispositivo (recurso físico) que presta un servicio y una cola de espera para los trabajos (clientes) que demandan un servicio de él.
* Una estación de servicio puede ser:
	* Servidor completo
	* Recurso hardware: CPU, memoria, disco...
* Usado en modelado por redes colas
 ![[Pasted image 20250105182316.png]]
#### Variables temporales de una estación de servicio
* Tiempo de espera en cola - Latencia (W)
	* Tiempo transcurrido desde que un trabajo quiere hacer uso de un recurso hasta que empieza a utilizarlo
* Tiempo de Servicio (S)
	* Tiempo transcurrido desde que un trabajo hace uso de un recurso hasta que lo libera.
* Tiempo de respuesta de la estación de servicio (R)
	* Suma de los dos tiempos anteriores
	* También  puede conocerse como latencia
	* $R=W+S$
![[Pasted image 20250105182601.png]]

### Variables operacionales básicas
* Sus valores se obtienen a partir de medidas experimentales (monitorización, son). Variable global temporal:
	* **T:** Duración del periodo de medida para el que se extrae el modelo.
* Variables relacionadas con el dispositivo i:
	* $A_i$: Número de trabajos solicitados (llegadas, arrivals).
	* $C_i$: Número de trabajos completados (salidas, completions).
	* $B_i$: Tiempo que el dispositivo está ocupado (busy time)
![[Pasted image 20250105183135.png]]

### Variables operacionales deducidas
Ya conocidas:
* Trabajos/segundo:
	* $λ_i$: Tasa de llegada (Arrival rate)
	* $X_i$: Productividad (throughput)
* Segundos/trabajo:
	* $S_i$: Tiempo de servicio (service time)
	* $W_i$: Tiempo de espera en cola (waiting time)
	* $R_i$: Tiempo de respuesta (response time)
	* $τ_i$: Tiempo entre llegadas (inter-arrival time)
![[Pasted image 20250105183825.png]]
> [!note]
> Dejo pendiente pasar todas esas formulas a texto, pero que pereza

**Utilización** $U_i$: Es la proporción de tiempo que el dispositivo ha estado en uso con respecto al intervalo total de medida (T). Variable *Adimensional*. Coincide con el número medio de trabajos siendo servidos por el dispositivo (como máximo 1 si $B_i=T$).
$$
U_i=\frac{B_i}{T}$
$$
**Saturación** $Q_i$: Número medio de trabajos en cola de espera (jobs in queue)

$N_i$: Número medio de trabajos en la estación de servicio (cola más recurso). Se cumple que $N_i=Q_i+U_i$.
![[Pasted image 20250105203144.png]]
#### Ejemplos
>[!note]
>Igual que lo mencionado anteriormente, mas adelante haré los ejemplos mejores visualmente

![[Pasted image 20250105203303.png]]
![[Pasted image 20250105203316.png]]
![[Pasted image 20250105203331.png]]
### Las variables del sistema en su conjunto
#### Variables básicas
- $A_0$: Número de trabajos solicitados al sistema (arrivals).
- $C_0$: Número de trabajos completados por el sistema(completions)
#### Variables deducidas
* $λ_0$: Tasa de llegada al sistema (Arrival rate)
* $X_0$: Productividad del sistema (throughput)
* $R_0$: Tiempo de respuesta del sistema (response time, latency).
* $N_0$: Número medio de trabajos en el sistema (jobs).
![[Pasted image 20250105203855.png]]

### Leyes operacionales

* Todas las variables operacionales son valores medios para el intervalo de monitorización T. Por lo que el valor de las variables operacionales depende del intervalo de observación T.
* Existen, sin embargo, una serie de relaciones entre las variables operacionales que se mantienen válidas para cualquier intervalo de observación y que no dependen de suposiciones sobre la distribución de servicio o de la forma en la que llegan los trabajos. Las leyes operacionales
* Estas leyes son mas útiles cuando se cumple la **hipótesis del equilibrio de flujo** que establece que en un servidor no saturado, si se escoge un intervalo de observación suficientemente largo, se cumple que:
	* El número de trabajos que llegan al servidor coincide con el que sale $(A_i=C_i)$.
$$
\frac{\left|A_i-C_i\right|}{C_i} \approx 0 \Rightarrow \lambda_i \approx X_i
$$
#### Ley de Little 
>[!tip]- ¡Dato curioso!
>la ley del Little sale porque el creador de esta ley era muy fan de Stuart Little! es algo super gracioso verdad? al ser una Ley reciente, se usan referencias a peliculas

 > [!tip]- ¡Otro dato curioso! 
 >Es mentira

 * Relaciona el número medio de trabajos en el sistema ($N_0$) con el tiempo de respuesta ($R_0$) y su tasa de llegada ($λ_0$)
$$
N_0=λ_0*R_0
$$
* Bajo la hipótesis del equilibrio de flujo, esta ley relaciona las tres variables más importantes que reflejan el rendimiento de un servidor: N, X y R.![[Pasted image 20250105211414.png]]
* ==Esta ley puede ser aplicada no solo al sistema en su totalidad, sino a cada estación de servicio y a cada uno de los diferentes sub-niveles de una estación de servicio.==
#### Como aplicarla
![[Pasted image 20250105211546.png]]
####  Ley de la utilización
$$
U_i=\frac{B_i}{T}=\frac{C_i}{T} \frac{B_i}{C_i}=X_i \times S_i \Rightarrow U_i=X_i \times S_i
$$
* En realidad, se podía haber deducido también a partir de la ley de Little aplicada al servidor de una estación:
![[Pasted image 20250105214422.png]]

##### Ejemplo de aplicación I
![[Pasted image 20250105214504.png]]
![[Pasted image 20250105214516.png]]

### Límites asintóticos del rendimiento
* Se trata de encontrar una cota superior de la productividad ($X_0$) e inferior del tiempo de respuesta del sistema ($R_0$). Son *límites optimistas* del rendimiento.
	* ¿Cuál es la productividad máxima ($X_0^{max}$)?
	* ¿Cuál es el tiempo de respuesta mínimo?
* Campos de aplicación:
	* Estudios preliminares: consideración de un gran número de configuraciones candidatas
	* Estimación de la mejora potencial de prestaciones que pueden reportar acciones sobre el sistema
	* Planificación de la capacidad (capacity planning)
![[Pasted image 20250105231642.png]]

## Monitorización
un monitor es una herramienta para observar/medir las actividades ligadas al rendimiento de un sistema mientras es utilizado por los usuarios. Un monitor recoge datos, los analiza y los visualiza. Incluso pueden identificar problemas y solucionarlos.

### ¿Qué medir?

#### Carga de trabajo
Se puede definir como el **Conjunto de tareas que ha de realizar un sistema** (= todo aquello que demande recursos del sistema)

* Variables que reflejan la carga:
	* Número de programas simultáneos en ejecución.
	* Accesos por unidad de tiempo a un servidor de páginas web
	* Órdenes de los usuarios a través de los terminales
	* Peticiones por unidad de tiempo a una base de datos, etc.
* Carga de prueba (test workload)
	* Carga empleada en un estudio de evaluación
* Una carga de trabajo genera una determinada actividad en el sistema
#### Midiendo la actividad del sistema

El que medir lo decimos nosotros con nuestro objetivo

* Magnitudes medibles (tiempos de respuesta, utilizaciones, productividades...)
	* **Procesadores**: Utilización, número de procesos, interrupciones, cambios de contexto, etc.
	* **Memoria**: memoria física utilizada, fallos de caché, fallos de página, uso de memoria de intercambio, fallos de TLB, etc.
	* **Discos**: lecturas/escrituras por unidad de tiempo, longitud de las colas de espera, tiempo de espera medio por acceso, etc.
	* **Red**: paquetes recibidos/enviados, colisiones por segundo, paquetes perdidos, etc.
### Monitorización de aplicaciones
 * Módulos más ejecutados
 * Instrucciones más ejecutadas