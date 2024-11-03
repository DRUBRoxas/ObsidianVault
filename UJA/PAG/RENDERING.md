### Pipeline de Rendering

Listado:
1. Transformación de modelado
	1. Rotación y traslación
	2. Matriz 4x4
	3. Cada objeto va a tener su propia matriz de traslación
	4. GLM::MAT4 (mickey-herramienta para las matrices 4x4)
	5. 
2. Transformación de visión
3. Transformación de Perspectiva
4. Clipping
5. División de perspectiva y viewport
6. Rasterización
	1. Fragmento (Definicion)
7. Sombreado
	1. Fragment Shaders que solo pinte alambre o que pinte con color liso aplicando el sombreado de Phong o meter textura
8. Test de profundidad
	1. Cada fragmento lleva asociada una profundidad y en esta etapa se comprueba la profundidad del fragmento y las que no se descartan
9. Blending
	1. El blending consiste en dar varias pasadas

## Definición
Llamamos *rendering* al proceso a través del cual combinamos en el ordenador dos tipos de información para generar imágenes, la forma y la apariencia visual de los objetos.

* Por un lado, la información sobre la *forma* de los objetos. Esto incluye tanto *geometría* como *topología*
* Por otro lado, la información sobre la *apariencia visual* de los objetos. Basicamente, su *color*, y cómo reaccionan a la *luz*.
![[rendering.png]]
### La forma de los objetos
En una escena 3D, los objetos están formados por **primitivas** de dibujo. Lo más habitual es que estas primitivas sean triángulos, ya que es la figura tridimensional más simple de procesar.

> **primitivas de dibujo** se refieren a las formas básicas que se utilizan para construir objetos más complejos.

La **geometría** de los objetos viene determinada por la posición de sus **vértices**, y la **topología** indica cómo se combinan esos vértices para formar **aristas** y **caras**.
En nuestro contexto, lo normal es que un vértice no sólo incluya información sobre su posición en el espacio, sino que también puede incluir información como la **normal**, las **coordenadas de textura** o el **color**, por ejemplo.

## Cuestiones matemáticas

### Sistema de referencia
![[sistemadereferencia.png]]
Necesitamos un **sistema de referencia** para expresar la geometría de los objetos. Las **coordenadas** siempre están expresadas en función del sistema de referencia que se esté utilizando, por lo que es imprescindible conocerlo.

En nuestro contexto el sistema de referencia es el *sistema ortonormal*
> Está formado por tres vectores de longitud uno y perpendiculares entre sí

De las dos posibles formas de organizar estos vectores denominadas _sistema de referencia levógiro_ y _sistema de referencia dextrógiro_, utilizaremos el sistema dextrógiro, también llamado **sistema de coordenadas de la mano derecha** (Ejemplo en la foto).
>Como recordatorio, mira tu mano derecha: tu dedo pulgar representa el eje X, el índice representa el eje Y, y el dedo corazón representa el eje Z.

Las **coordenadas** de un punto o de un vector en realidad representan los factores por los que se multiplica cada vector del sistema de referencia, para así identificar la posición del vértice o el extremo del vector

### Puntos
Un punto es una **localización** en el espacio, descrita mediante sus coordenadas (en nuestro caso, _x_, _y_ y _z_, en un sistema dextrógiro ortonormal). Además, y para facilitar el procesamiento matemático, se añade una cuarta coordenada, denominada **coordenada homogénea** (_w_), y cuyo valor canónico es 1 (el valor canónico para las coordenadas _x_, _y_ y _z_ es 0).

>El valor canónico es el valor que se asigna por defecto a una coordenada para simplificar y estandarizar los cálculos.

![[representacionpuntos.png]]