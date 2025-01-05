Texturas Semitransparentes
Texturas necesarias: 1 (para cruzarlas)
Caracteristicas de la textura: Canal Alpha (PNG)
Unidades de textura: 1 / Samplers: 1
¿Que cambia en OPenGL?
GL_Enable(GL_BLEND)
GlBlendFunc(GL_SRC_ALPHA,GL_ONE_MINUS_SRC_ALPHA);

Las texturas semitransparentes pueden usarse para añadir detalles (superponiendo texturas) 
(El ejemplo es un spray en una pared, utiliza 2 texturas, la pared y la pintura) la pintura necesitará tener el canal alpha