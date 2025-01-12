# Relación 2: Problemas de Sistemas Operativos

## Preguntas y Respuestas

### 1. ¿Qué transiciones de estado puede iniciar un proceso por sí mismo?

**Respuesta:** La única transición que puede iniciar (lo hace indirectamente) un proceso es la de "en ejecución" a "bloqueado". Para ello debe realizar una llamada al sistema que provoque el bloqueo del proceso.

### 2. Interprete el siguiente párrafo en el contexto de los ordenadores y los sistemas operativos. Relacione las actuaciones y los protagonistas de esta historia con distintas tareas y entes de un sistema informático.

**Respuesta:** En esta historia podemos equiparar a Juan con un procesador que ejecuta tareas (procesos). El manual de instrucciones que interpreta equivale a un programa que se ejecuta. La operación de pegar la cabina la podemos ver como la realización de una operación con un periférico que se puede simultanear con otras acciones como construir las alas. El timbre del teléfono se puede equiparar a la ocurrencia de una interrupción, que implica salvar el contexto de ejecución (señalar por dónde va) y darle servicio (ejecutar la rutina de servicio a la interrupción, en la parábola, el manual del vídeo).

### 3. Cuando se produce una interrupción, ¿se produce necesariamente un cambio de proceso?

**Respuesta:** No, cualquier interrupción no tiene por qué provocar un cambio de proceso. Por ejemplo, una interrupción del reloj que no coincide con el agotamiento del cuanto del proceso en ejecución no tiene por qué implicar un cambio de proceso.

### 4. Cuando se produce una llamada al sistema, ¿se produce necesariamente un cambio de proceso?

**Respuesta:** No, existen muchas llamadas al sistema que no provocan un cambio de proceso. Las llamadas al sistema que implican algún tipo de E/S suelen conllevar un cambio de proceso para que se utilice mejor el procesador. Sin embargo, hay llamadas al sistema, como la de liberación de memoria dinámica, que no implican ningún cambio de proceso.

### 5. Cuando un proceso desea bloquearse, ¿deberá encargarse él directamente de cambiar el valor de su estado en su descriptor de proceso?

**Respuesta:** No. El descriptor de proceso es una estructura de datos que gestiona el sistema operativo y a la que no tienen acceso los procesos gracias a los mecanismos de protección de la memoria.

### 6. ¿Tiene el dispatcher un descriptor de proceso y lucha por la CPU como el resto de procesos?

**Respuesta:** El dispatcher no lucha por la CPU como el resto de procesos de usuario. Por ejemplo, no tiene sentido que se sitúe en la cola de procesos en estado listo. Al dispatcher lo llama el sistema operativo cuando es preciso asignar la CPU, y se ejecuta sin entremezclarse con la ejecución de otros procesos de usuario. No compite por la CPU por tanto como éstos. Por otro lado, no tiene descriptor de proceso. Esto es debido a que no tiene estado de ejecución y no es preciso guardar su contexto, pues siempre se ejecuta en su totalidad. La zona de memoria que ocupa siempre es la misma, y se decide al inicializarse el sistema.

### 7. Dado un proceso que cambia su estado de en ejecución a bloqueado, ¿puede esto provocar un cambio de estado en otro proceso?, ¿entre qué estados?

**Respuesta:** Sí, cuando un proceso pasa de "en ejecución" a "bloqueado", la CPU queda ociosa. Un nuevo proceso de los que están en estado "listo" debe ocupar en este instante la CPU y pasar por tanto a "en ejecución".

### 8. Idem para cambio entre bloqueado y listo.

**Respuesta:** Dependerá de la política de planificación del sistema operativo. Por ejemplo, si la planificación es por turno rotatorio no puede provocar cambio. Si la planificación es la de colas de niveles múltiples con retroalimentación y el proceso que ocupa la CPU pertenece a una cola de menor prioridad que el proceso que pasa a estado "listo", entonces el proceso en ejecución se verá obligado a dejar la CPU, y pasará por tanto de "en ejecución" a "listo".

### 9. Idem para cambio entre listo y bloqueado.

**Respuesta:** Esta transición de estado nunca se da.

### 10. Sin reloj en la computadora, ¿qué algoritmos de planificación podríamos implementar?

**Respuesta:** FIFO y prioridad al más corto (SJF). Este último si la estimación de lo que dura una ráfaga no se calcula como el tiempo que duró la última ráfaga del proceso.

### 11. ¿Es posible que en algún momento la CPU esté ejecutando código que no pertenece a ningún proceso de usuario?

**Respuesta:** Sí, cuando realiza cualquier tarea del sistema como: conmutar entre procesos, planificación de procesos, gestión de interrupciones, etc.

### 12. Puesto que un controlador es un procesador dedicado a controlar el o los dispositivos asignados, ¿existirá un descriptor de proceso para cada uno de dichos controladores?

**Respuesta:** No, no tiene sentido.

### 13. Respecto a un proceso, ¿dónde se podría almacenar la información sobre el proceso que lo creó (su proceso padre), o sobre la de sus hijos?

**Respuesta:** En el PCB, que es la estructura de datos que utiliza el sistema operativo para guardar toda la información relativa a un proceso y así poder gestionarlo.

### 14. Comente si es totalmente cierta la siguiente afirmación: En un sistema de tiempo compartido en el que los procesos se planifican mediante el algoritmo de turno rotatorio con cuanto de tiempo n unidades, cada proceso se ejecuta sin interrupción durante n unidades de tiempo. Justifique su respuesta.

**Respuesta:** No, porque durante el intervalo que dura un cuanto es muy posible que la CPU ejecute rutinas de servicio a interrupción originadas por eventos como la pulsación de una tecla en un terminal, el fin de una operación de E/S o la interrupción del reloj.

### 15. Jacinto acaba de terminar la carrera y su proyecto consiste en construir un sistema operativo que permita niveles altos de multiprogramación. Para ello deduce que es necesario disponer de mayor cantidad de memoria principal disponible y plantea como solución el mantener los descriptores de proceso en disco. ¿Es razonable?, ¿por qué?

**Respuesta:** No. Los descriptores de proceso son las estructuras de datos que mantienen toda la información relativa a los procesos, esta información es consultada y modificada con gran frecuencia por distintas unidades funcionales del sistema operativo. Por lo tanto, es imprescindible que estén en memoria principal para un acceso eficiente.

### 16. Supongamos un algoritmo de planificación que favorece a aquellos programas cuya última ráfaga ha sido corta. ¿Por qué favorecerá este algoritmo a los programas intensivos en E/S sin provocar inanición en los programas intensivos en el uso de la CPU?

**Respuesta:** Este tipo de algoritmo prioriza los programas que realizan operaciones de E/S frecuentes, ya que estas ráfagas suelen ser más cortas. Al asignarles la CPU rápidamente, estos programas pueden liberar los dispositivos de E/S más pronto, aumentando la eficiencia general del sistema. Además, los programas intensivos en CPU no quedan desatendidos, ya que eventualmente tendrán su turno, evitando la inanición.

### 17. Se aplica el término "tiempo compartido" a los sistemas operativos que permiten que varios usuarios interactivos trabajen simultáneamente, para lo cual será necesario asegurar que cada proceso disfrute de cierto tiempo de CPU a intervalos más o menos regulares. ¿Qué algoritmos de planificación quedan descartados para ser usados en este tipo de entornos?

**Respuesta:** Todos aquellos que no son apropiativos. Por ejemplo, FIFO, primero el más corto (SJF) o prioridad a la tasa de respuesta más alta (HRN), ya que estos algoritmos no garantizan que cada proceso reciba tiempo de CPU de manera regular.

### 18. ¿En qué grado discriminan a los procesos cortos los siguientes algoritmos de asignación de la CPU: FIFO, turno rotatorio, colas de niveles múltiples con retroalimentación?

**Respuesta:**

- **FIFO:** Discrimina significativamente a los procesos cortos, ya que deben esperar a que terminen los procesos largos que les preceden en la cola.
- **Turno rotatorio:** Discrimina menos, ya que los procesos cortos pueden completarse en su totalidad en uno o pocos cuántums.
- **Colas de niveles múltiples con retroalimentación:** Favorece a los procesos cortos, ya que estos suelen comenzar en las colas de mayor prioridad y terminan rápidamente sin bajar a colas inferiores.

### 19. ¿Es cierta la siguiente afirmación: La política de planificación turno rotatorio es equivalente a la política de planificación FIFO si el cuantum de tiempo es infinitamente largo?

**Respuesta:** Sí, porque con un cuantum infinitamente largo, el turno rotatorio se comporta como FIFO, ya que el proceso en ejecución no será interrumpido hasta que termine.

### 20. Muchos algoritmos de planificación son parametrizados. Por ejemplo, el algoritmo de turno rotatorio requiere un parámetro: el cuantum. Esto implica que estos algoritmos son en realidad grupos de algoritmos (por ejemplo, el conjunto de todos los algoritmos round robin para cada valor posible del cuantum). Puede ocurrir que un grupo de algoritmos incluya a otro, ¿qué relación de este tipo existe entre las siguientes parejas de algoritmos?

**Respuesta:**

- **Prioridad / El más corto primero:** El más corto primero es un caso particular de prioridad donde la prioridad se basa en la duración de la ráfaga.
- **Colas de niveles múltiples con retroalimentación / FIFO:** Son equivalentes si hay una sola cola y el cuantum es infinito.
- **Prioridad / FIFO:** FIFO puede considerarse un caso particular de prioridad donde la prioridad se asigna según el tiempo de llegada.
- **Turno rotatorio / El más corto primero:** No hay relación directa entre estos algoritmos, ya que tienen objetivos diferentes.

### 21. Estamos escribiendo el código de un programa de usuario. ¿Qué operaciones podemos realizar para provocar la activación del dispatcher?

**Respuesta:** Para activar el dispatcher, el proceso en ejecución debe bloquearse o terminar. Esto se puede lograr mediante operaciones como realizar una E/S (por ejemplo, una llamada a `scanf` en C), ejecutar una operación `wait` sobre un semáforo a cero o invocar una instrucción `exit` en C.

### 22. Un sistema tiene los siguientes recursos: una CPU, dos discos y una impresora. En el sistema se van a ejecutar dos procesos con las siguientes características:
Estos están a mano