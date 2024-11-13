(Voy por la mitad imagen de tonos de marron)
Primer detalle a tener en cuenta: las coordenadas de los pixeles se corresponden con el centro de cada pixel, es decir que la cuadricula cambia (ejemplo en la diapo)
como es el centro de cada píxel, el 131 está cerca del centro del pixel y el 76.8 esta casi. Se puede seleccionar el mas cercano (redondear) con GL_NEAREST

Otra opcion es una interpolación lineal, es decir en vez de coger el pixel directamente, cojo los 4 mas cercanos y hacemos una interpolacion. Se usa con GL_LINEAR. Esta interpolación de 4 (de normal la hacemos entre 2) se hace en 2 Dimensiones, tenemos el alpha y el 1-alpha pero con la parte decimal de esas coordenadas. Hoy en día esto lo tienen las GPUs aplicado en Hardware asi que van como un tiro (palabras de mi colegon angel luis)

Imagen que diferencia, a la derecha se ven los dientes de sierra (aliasing). En la linear de cerca se pierde nitidez, pero se ve mejor overall

![[Diferencias Aliasing.png]]

# Magnificacion y # Minificacion
Magnificación es tener menos píxeles que en la textura
Minificacioón es al reves.
Siempre ocurre uno de los dos

Para resolver situaciones que no podemos controlar de manera simple, usamos los mipmaps

TODO: Terminar esto por dios