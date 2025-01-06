## Ejercicio 1
Un modelo de simulación meteorológica se ejecuta en ==135 segundos.== Si las operaciones de división con números reales consumen el ==82 % de este tiempo==, ¿en cuánto se tendría que mejorar la velocidad de estas operaciones si queremos conseguir que dicho programa se ejecute ==seis veces más rápidamente==? ¿Cuál es la ==aceleración máxima== que podríamos conseguir si pudiésemos acelerar dichas operaciones tanto como quisiéramos?

### Comprensión del ejercicio
Para este tipo de ejercicios en los que se buscan la aceleración y hacerlo más rápido, se usa la **Ley de Amdahl**
![[Ley de Ahmdal#Formula]]

### Resolución
Separamos en A) y B) siendo:
* A)  ¿en cuánto se tendría que mejorar la velocidad de estas operaciones si queremos conseguir que dicho programa se ejecute ==seis veces más rápidamente==?
* B) ¿Cuál es la ==aceleración máxima== que podríamos conseguir si pudiésemos acelerar dichas operaciones tanto como quisiéramos?

#### A)
Datos a tener en cuenta:
A=6
f=0.82
k=????
Debemos despejar K
$$
6=\frac{1}{(1-0.82)+(\frac{0.82}{k})}
=>6*\left(0.18+(\frac{0.82}{k})\right)=1
=>0.18+(\frac{0.82}{k})=\frac{1}{6}
$$
$$
=>\frac{0.82}{k}=0.16-0.1
=>0.82=-0.02*k
=>\frac{0.82}{-0.02}=k
=> k = -41
$$
==Resultado: No hay mejora posible porque no puede ser un mejora negativa==

#### B)

![[Ley de Ahmdal#Formula con n mejoras]]



## Ejercicio 2
2.- Un computador tarda 100 segundos en ejecutar un programa de simulación de una red de interconexión para multicomputadores. El programa dedica el 30 % en hacer operaciones de aritmética entera, el 60 % en hacer operaciones de aritmética en coma flotante, mientras que el resto se emplea en operaciones de entrada/salida. Calcule el tiempo de ejecución si las operaciones aritméticas enteras y reales se aceleran de manera simultánea 2 y 3 veces, respectivamente.