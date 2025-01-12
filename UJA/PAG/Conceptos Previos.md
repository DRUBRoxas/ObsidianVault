## Rendering
Es el proceso para dibujar en pantalla que realiza la GPU en el cual se combina en el ordenador dos tipos de información:
### Forma de los objetos
Esto incluye:
#### Geometría
Es la posición en el espacio de los vertices
#### Topología
Forma en la que están unidos (Generalmente son las aristas y las caras)
### Apariencia Visual
Todas las características correspondientes a los objetos.

Forma -> Objeto formado por primitivas -> Objeto (Conjunto de puntos y como se conectan)

## Cuestiones matemáticas

### Sistema de referencia
Vacío por ahora, contenido que ya conozco

### Punto
Localización en el espacio, es un valor para cada eje. se añade al final 1 si es punto o 0 si es vector.

### Vector
Representan una dirección, no se pueden colocar en el espacio (no tienen posición)
Tienen 2 valores:
* Dirección - Lo que abarca
* Sentido - hacia donde va
### Diferencia entre puntos y vectores
![[Pasted image 20250108034111.png]]

### Operaciones con vectores

#### Modulo 
longitud (magnitud) de un vector
$$
\begin{gathered}
\mathbf{v}=(x, y, z) \\\\
|\mathbf{v}|=\sqrt{x^2+y^2+z^2}
\end{gathered}
$$
#### Normalizar
Igualar el vector a la unidad
$$
\hat{v}=(x,y,z)
$$
$$
\hat{\mathbf{v}}=\frac{\mathbf{v}}{|\mathbf{v}|}=\left[\begin{array}{llll}
\frac{x}{|\mathbf{v}|} & \frac{y}{|\mathbf{v}|} & \frac{z}{|\mathbf{v}|} & 0
\end{array}\right]^T
$$
#### Producto Escalar
Hay 2 formas:
##### Sumando productos
$$
a*b=a_x*b_x+a_y*b_y+a_z*b_z
$$
##### Multiplicando los módulos
$$
a*b=| a|*|b|*cos \alpha
$$
#### La proyección de un vector
vector $\frac{a*b}{|b|}$
