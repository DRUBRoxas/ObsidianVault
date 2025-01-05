# PAG-mss00048  
  
# Autor:  
- [Manuel Sánchez Salazar](mailto:mss00048@red.ujaen.es)  
- [Perfil GitHub](https://github.com/DRUBRoxas/PAG-mss00048)  
  
# Descripción:  
Este repositorio contiene la práctica de la asignatura Programacion de Aplicaciones Gráficas.  
  
# Practica 1:  
## Ejercicio 1  
Se ha realizado una función que permite que, al mover la rueda del ratón se genere un color aleatorio y se cambie el color de fonde del programa  
## Ejercicio 2  
Utilizar un Singleton puede ser una buena solución para este caso, ya que garantiza que haya una única instancia  
de la clase PAG::Renderer en toda la aplicación y facilita el acceso global a esa instancia desde cualquier parte,   
incluyendo funciones de C registradas como callbacks.  
Para implementar un singleton, necesitas:  
* La clase tenga un único punto de acceso.  
* El constructor sea privado, para que no se puedan crear más instancias.  
* Se proporcione un método estático para obtener la instancia única.  
  
  
![UMLSingleton.png](Assets/UMLSingleton.png)  
  
Esto puede presentar las siguientes ventajas:  
* Simplicidad en el código.  
* Acceso global controlado.  
* Encapsulamiento.  
  
  
# Practica 2:  
## Ejercicio 1  
La clase PAG::Renderer ha sido completada, se han añadido los siguientes cambios:  
  
![UMLRenderer.png](Assets%2FUMLRenderer.png)  
  
## Ejercicio 2  
Se han sustituido todas las llamadas a openGL en el main por llamadas a PAG::Renderer  
## Ejercicio 3  
Todos los mensajes han sido añadidos a la consola de Dear imgui y para el selector de color  
se ha elegido un ColorPicker4, había varias opciones a elegir, y otras versiones de este mismo,  
he usado esta porque me parece la mas sencilla y la que mejor se adapta a lo que necesitamos.  
Para usarla se ha utilizado la flag:  
```cpp  
ImGuiColorEditFlags_PickerHueWheel  
```  
Hay muchas mas flags que permiten la modificación al gusto del selector del color, pero he decidido  
usar solo esta por ahora.  
  
# Practica 3:  
## Ejercicio 5  
Este comportamiento se debe a que la proyección y las coordenadas de la ventana no se están  
ajustando correctamente cuando se redimensiona la ventana. Al cambiar el tamaño de la ventana,  
la relación de aspecto de la ventana cambia, lo que significa que la proyección debee ajustarse a la nueva relación  
de aspecto.  
  
# Practica 4:  
## Ejercicio 4  
He creado la funcion auxiliar leerArchivo, que se encarga de leer los archivos, manejar los errores y leer el contenido  
Se ha añadido y modificado el metodo cargaArchivos, para cargar las dos versiones del archivo glsl de golpe.  
Se ha añadido manejo de excepciones en el metodo cargaArchivos, para asegurarse de que cuando se lance la excepcio, el mensaje se mande a la consola  
y siga funcionando el programa. A parte de esto, se ha encapsulado en su propia clase el Shader Program, para que el renderer haga unicamente su trabajo.  
Despues, desde la clase TextBox, se llama (con el nombre del archivo) al program shader, que se encarga de hacer todo lo demás.  
![UMLPractica4.png](Assets%2FUMLPractica4.png)  
  
  
# Practica 5  

Se ha añadido la Camara y los tipos de movimiento enseñados en clase, siendo estos:  
* Zoom  
* Pan  
* Orbit  
* Crane  
* Dolly  
* Truck  
  
Se han hecho cambios al shader para poder manejar la camara.  
Además, se han añadido los controles de la camara en una interfaz de imgui, parecida a la usada en clase.  
  
Instrucciones:  
Al ejecutar la aplicacion, primero debes cargar un shader (El shader de ejemplo es "Pag03")  
Desde la ventana para cargar los shaders. con poner Pag03 es suficiente.   
  
Una vez cargado, puedes empezar a usar la camara.  
Esto puedes hacerlo desde la ventana de imgui donde se encuentran los movimientos.  
  
  
Cada opción de las anteriores tiene sus propios controles adaptados y pueden usarse de manera intuitiva. por lo general son simplemente  
botones que debes pulsar para activar el movimiento.  
  
Ademas de esto, se ha añadido un boton para resetear la camara a su posicion inicial.  
  
Aquí dejo el UML de la practica 5:  
![PAG.jpg](Assets%2FPAG.jpg)  
  
# Practica 6  

Se ha añadido a los modelos la posibilidad de transformarlos, rotarlos y escalarlos.  
Actualmente usamos para ello las teclas siguientes en el teclado (No se si me dara tiempo a implementarlo en el gui)  
Traslación:  
Flecha Arriba: Mover hacia arriba  
Flecha Abajo: Mover hacia abajo  
Flecha Izquierda: Mover hacia la izquierda  
Flecha Derecha: Mover hacia la derecha  
  
Rotación:  
W: Rotar hacia arriba  
S: Rotar hacia abajo  
A: Rotar hacia la izquierda  
D: Rotar hacia la derecha  
  
Escalado:  
Z: Escalar hacia arriba  
X: Escalar hacia abajo  
  
Se ha utilizado la biblioteca Assimp para cargar modelos, así como imfilebrowser para cargar los modelos desde el explorador de archivos.  
En el renderer ahora se pueden tener varios modelos cargados a la vez,eliminarlos, y se pueden transformar de manera independiente.  
![P6-UML.png](Assets%2FP6-UML.png)  
  
# Practica 7  
  
1. **Añadido tipo de visualización al modelo**  
    - La clase `Modelo` ahora incluye un atributo que representa el tipo de visualización utilizado. Esto permite cambiar dinámicamente el modo en que se renderiza cada modelo.  
  
2. **Nuevo enumerador `Visualización`**  
    - Se ha creado un `enum` llamado `Visualización` que define los posibles modos de visualización. Este enumerador facilita la gestión y la selección de los distintos modos de renderizado.  
  
3. **Cambios en los shaders**  
    - Se han modificado los shaders para incluir la lógica necesaria para implementar los diferentes modos de visualización.  
  
4. **Corrección de problemas de dependencias (`#include`)**  
    - Se han solucionado conflictos y redundancias en las dependencias. Esto mejora el tiempo de compilación y reduce posibles errores derivados de duplicaciones o referencias circulares.  
  
5. **Cambio en la gestión de shaders para modelos**  
    - La lógica de renderizado ha sido modificada.  
      - Ahora, cada modelo gestiona su propio Shader asociado en lugar de utilizar un único Shader compartido para todos los modelos de la escena.  
      - Esto permite que cada modelo tenga su propio modo de visualización, sin afectar a los demás modelos.  
6. **Incorporación de subrutinas y lógica de cambio de visualización**  
    - Se han añadido las subrutinas necesarias en los shaders para implementar los modos de visualización definidos en el enumerador.  
   - Además, se ha desarrollado la lógica para gestionar el cambio dinámico de modos de visualización desde la aplicación,   
     
7. **Botón para cambiar el modo de visualización en el selector de modelos**  
    - Se ha añadido un botón al componente de interfaz gráfica `SelectorModelo`, que permite alternar entre los diferentes modos de visualización de un modelo seleccionado.  
   - Para gestionar los cambios de manera eficiente, se ha implementado un sistema inspirado en el patrón Observador, asegurando que cualquier cambio en el modo de visualización se propague automáticamente a los elementos relevantes de la aplicación.  
  
El UML ha sido modificado para dejar solo lo relevante a esta práctica, ya que se quedaba un UML demasiado grande.  
![P7-UML.png](Assets/UML%20P7.png)

# Practica 8

Cambios realizados:
1. **Cambios en la interfaz**
	* Se han modificado las ventanas dependientes de modelos y luces en ImGui para que solo aparezcan si hay luces o modelos en la escena.
	* Corregido mal funcionamiento de botones en los controles de la cámara y transformación del modelo
	* Añadido un selector de luces. Este Selector es muy similar al de modelos.
		* Para el desacople, el main está siempre comprobando esta clase y, cuando hay un cambio, el main es el encargado de notificarlo al Renderer.
2. **Clases nuevas**
	* Añadida la clase Luz, con la siguiente estructura:![[LuzUML.png]]
	* Añadida la clase SelectorLuces, con la siguiente estructura:![[SelectorLuces.png]]
3. **Cambios implementados para añadir las luces**
	1. Modelos
		*  He cambiado todos los vec4 de ColorDifuso, ColorAmbiental, ColorEspecular por un vec3. 
		* He cambiado todos los float por GLfloat
		* Ordenado el código de la clase modelo para que sea un poco más legible
	2. Renderer
		* Añadido inicialización de luces en el constructor del Renderer (falta añadir luces desde ImGui pero falta de tiempo)
		* Modificado las subrutinas
		* Añadido bucle de luces teniendo en cuenta las propiedades vistas en clase, activando en la primera luz la función ``glBlendFunc(GL_SRC_ALPHA, GL_ONE_MINUS_SRC_ALPHA);`` y en la segunda ``glBlendFunc(GL_SRC_ALPHA, GL_ONE);``
		* Añadido el manejo de las subrutinas necesarias para todos los tipos de luces y el modo alambre o relleno.
		* Activado GL_BLEND y la función GL_LEQUAL en la inicialización del Renderer.
		* Añadido el vector de luces
		* Añadidos los métodos:
			* BorraLuz
			* ObtenerNombresLuces
			* EnciendeLuz
	3. Shaders
		* Se han modificado los Shaders para poder manejar las subrutinas, para no tener que manejar distintas subrutinas en el mismo shader, he añadido la subrutina del modo alambre a las de las luces, llamándola "sinLuces".
		* Añadidas las subrutinas necesarias para los 4 tipos de luces.
	4. Main
		*  añadidos 2 métodos que controlan los cambios en el selector de modelos