## Superficies de forma libre
Son modelos con una simetria, como por ejemplo un cono. Tenemos un eje de rotación y una generatriz, y al girar esa generatriz 360 grados alrededor del eje, nos sale un cono.

Al final siempre vamos a tener una malla de poligonos o una malla de triangulos, ya que las gpus estan preparadas para ello, a más poligonos, mas detalle.

Estas mallas tienen que cumplir unas condiciones ya que si no no sirven para representar un objeto del mundo real.
Estas son: 
* No puede haber aristas compartidas por menos de 2 triangulos
* No puede haber vertices compartidos por menos de dos aristas
* todas las aristas tienen que formar partes de un triangulo
* Cada arista conecta dos vértices y cada triángulo es una secuencia cerrada de tres aristas.

*Ejemplo de malla no valida*
![[Malla no válida.png]]
No hay una estructura de datos "buena" para las mallas, hay muchas especificas pero no hay ninguna optima para todos los casos.

La estructura de datos que vamos a usar contiene los datos necesarios para saber que triángulos debo eliminar en caso de borrar alguna arista

![[Estructura de datos mallas triangulos.png]]
*TODO: Pedirle a Fran info al respecto*


## Superficies de revolución
* Representación implícita de la topología
* muy fácil de diseñar manualmente
* permitir representar objetos complejos
