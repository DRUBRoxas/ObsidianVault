# Parte 1
## Consideraciones Iniciales
Para empezar, todo esto viene del archivo Shell-Primeros-Pasos de platea
Link al PDF en la web de platea: [P07-shell-primeros-pasos](https://platea.ujaen.es/pluginfile.php/453787/mod_resource/content/7/P07-shell-primeros-pasos.pdf)
Link al PDF en mi carpeta (Esto es solo para mi) [[P07-shell-primeros-pasos.pdf]]
Inicio de cualquier **script de bash**
``` Bash
#! /bin/bash

# Autor: Manuel Sánchez Salazar
# Descripción: Hace tal tal

echo codigo
```
Todos los shell scripts deberían tener las siguientes partes:

* **Cabecera (hash-bang)**: La primera línea de un shell script es un tipo especial de comentario.
	* Comienza por los caracteres \#! y va seguido del nombre de un intérprete de órdenes o shell. 
	* IMPORTANTE: ==Los caracteres \#! deben aparecer justo al comienzo del archivo==, es decir, deben ser los dos primeros bytes del archivo de texto para que el sistema los pueda reconocer. 
	* Puedes encontrar tu path de la shell de bash (el cual podría variar del de arriba) usando el comando: `which bash`
* **Comentarios** Se indican con el carácter \# al comienzo de una línea o palabra. 
	* Todos los shell scripts ==deberían incluir como mínimo quién es su autor y una breve descripción== de para qué sirve el script.
	* El intérprete ignora el comentario desde el signo \# hasta el final de la línea. 
	* **IMPORTANTE**: Un carácter \#, sólo se interpreta como comentario, si va ==justo al principio de una línea o de una palabra de un shell script==. Si va en medio o al final de una palabra de un shell script, no se interpreta como comentario. 
* **Órdenes**: Las órdenes que componen el shell script.
	* ==Se escriben de la misma forma que se escriben en la consola== cuando se ejecutan a mano
* No es necesario, pero los ==scripts deberían tener una extensión==, como por ejemplo ==.sh== , que ayudan a reconocer que archivos son scripts.
* Para ejecutarlos ==SIEMPRE HA DE DARSE EL PERMISO DE EJECUCIÓN==


## Escribiendo nuestro primer script

Script del típico "Hello World", vamos a hacer **los pasos a seguir de CUALQUIER SCRIPT,** esto son los pasos indispensables para cualquier script que hagamos.

### Elegir el directorio y abrir el script
Vamos al directorio en el que queramos guardar el script. En este caso imaginamos que la carpeta Scripts está ya hecha en nuestro directorio de usuario
``` Bash
cd ~/Scripts
```
abrimos el editor de textos usando el nombre del script que queramos y usando el editor de texto que queramos (recomiendo gedit para no tener que escribir en la misma consola)
``` Bash
gedit helloworld.sh &
```
==el símbolo & al final del comando hace que se ejecute de fondo==, por asi decirlo, lo que hace que no te secuestre la terminal 👍

Se pueden usar otros en el examen, el mismo Manuel Carlos me ha dicho que se puede usar VSCode PERO no lo recomienda porque si alguien de un examen anterior se ha dejado instalada alguna extensión rara, puede suspenderte el examen (tipo integración con ChatGPT o ayudas a bash) así que la mas recomendable es gedit.
### Escribiendo y guardando el codigo
Una vez abierto el explorador veremos algo de este estilo (OBVIAMENTE EL ARCHIVO ESTARA VACIO)
![[gedit guia.png]]
dejo el código debajo (adaptado para mi porque me sale de los huevos)
``` Bash
#! /bin/bash

#:Autor: Manuel sánchez Salazar
#:Descripción: Imprime por pantalla el mensajito

echo ¡Vivan los toros!
```

### Ejecutando el código
Después le daremos al botón guardar (se que eres capaz de hacerlo solo/a)
y le daremos los ==permisos de ejecución al script==
``` Bash
chmod +x holamundo.sh
```

Después ==ejecutaremos el script de la siguiente manera== (a estas alturas no deberías ni necesitarlo)
```
./holamundo.sh
```

### Ejecutando código sin el ./ (OPCIONAL NO NECESARIO PARA EXAMEN)
En Ubuntu Linux (desde la versión Ubuntu 20.04 LTS), la ruta ~/bin o $HOME/bin se añade automáticamente a la variable de entorno PATH (para ver su valor ejecute `echo $PATH`), con lo que los programas que se coloquen en esa carpeta se pueden ejecutar directamente aunque no estemos situados en ese directorio. 

Para crear la carpeta ~/bin escribimos: `mkdir ~/bin` o `mkdir ${HOME}/bin` 

Cerramos la sesión y volvemos a entrar, a partir de ese momento, para ejecutar los programas que hayamos copiado en la carpeta bin sólo hay que escribir su nombre (sin ./), y el intérprete los encontrará, da igual el directorio en donde estemos.

También se puede poner el comando `bash holamundo.sh`

## Script para imprimir el contenido de una carpeta proporcionada por el usuario

``` Bash
#!/bin/bash 
# Autora: Lina García Cabrera 
# Descripción: Imprime la fecha y el contenido de una # carpeta que lee de la entrada 

echo "Hoy es " `date`
echo-e "\nEscribe la ruta al directorio" read la_ruta
echo-e "\n tu ruta tiene los siguientes archivos y carpetas: " 
ls $la_ruta
```

(Este script en los apuntes esta mal hecho xd)

* Línea \#1: El shebang (\#!/bin/bash) apunta hacia la ruta de la shell de bash.
* Línea \#2: Autor
* Línea \#3: Descripción
* Línea \#5: El comando echo muestra la fecha actual y el tiempo en la shell. Nota que date está con las comillas invertidas
* Línea \#6: el comando read lee la entrada y lo almacena en la variable la_ruta
* Línea \#8: ls toma la variable de la ruta y muestra los archivos y carpetas del directorio almacenado en la variable.
	* El símbolo $ hace que utilice la variable

## Parámetros

* Parámetros posicionales: argumentos presentes en la línea que invoca a la orden
	* Por ejemplo, en la orden `ls /bin`, hay un parámetro posicional, /bin, que ocupa la posición 1.
* Parámetros especiales: Su contenido lo rellena el intérprete de órdenes para guardar información sobre su estado actual, como por ejemplo el número de parámetros posicionales de la orden que se está ejecutando. Se referencian mediante caracteres no alfanuméricos, como por ejemplo * o \#.
* Variables: Las usa el programador del shell script para almacenar cualquier información que necesite.
	* Se referencian mediante un nombre.
	* El nombre de una variable puede ser cualquier combinación de letras, números o el guión bajo (\_) y siempre comienza por una letra o el guión bajo
	* Por ejemplo, nombres válidos de variables son: resultado, res_1, o res, pero no 1res
### ¿Por qué NO debo usar mayúsculas en los nombres de las variables? 
Porque los nombres de variables en mayúsculas están reservados para las variables internas del shell, y se corre el riesgo de sobrescribirlas. Los scripts pueden dejar de funcionar o tener un mal comportamiento. Por tanto, ==NUNCA uses MAYÚSCULAS en los nombres de tus variables.==

### Parámetros posicionales
#### Accediendo al valor de los parámetros
Para acceder al valor de un parámetro se usa $

Por ejemplo, para acceder al contenido del parámetro posicional que ocupa la segunda posición se escribe ==$2==.
Para acceder al contenido del parámetro especial \#, se escribe ==$\#==
Para acceder al contenido de la variable resultado, se escribe ==$resultado==

También se puede encerrar entre llaves el identificador del parámetro. Esto permite delimitar bien cual es ese identificador y es el método preferible3 aunque sea más difícil de escribir. Así, los ejemplos anteriores también se pueden escribir de la siguiente forma: 
``` bash
${2}
${#}
${resultado}
```

#### Estableciendo el valor de una variable
Igual que en casi todos los lenguajes de programación, se hace con un igual:
```
nombre=lafosforito
```

Para eliminar una variable se utiliza unset
``` Bash
unset nombre
```
##### espacios en variables NO
no debe haber espacios en esa asignación o el sistema dará un error.
``` bash
nombre = lafosforito
```
Esto dará error.

#### Ejemplo de uso de Parámetros posicionales

Vamos a usar de ejemplo el holamundo de antes

``` Bash
#! /bin/bash

#:Autor: Manuel sánchez Salazar
#:Descripción: Imprime por pantalla el mensajito

echo ${1}
```
En este caso, si nosotros invocamos al script usando el siguiente comando:
``` bash
./holamundo mamahuevo chupapinga
```
lo que imprimirá en pantalla el script será mamahuevo ya que es el primero en las posiciones.

Esto de aquí son los argumentos, si quieres asociarlo a algo.

### Parámetros especiales 

![[parametrosespeciales.png]]
Lo pongo como foto porque no me deja copiarlo y me da pereza

#### Diferencia entre comillas dobles y comillas simples
##### Comillas Dobles (" ") 
Permiten la expansión de variables y la interpretación de algunos caracteres especiales
* Expansión de variables: Si usas comillas dobles, el shell expande las variables (como $var), los caracteres de escape ( \\ ), y los comandos entre comillas inversas ( \` ).
* Carácter de Escape ( \\ ): puedes usar el carácter de escape (\\) para evitar que algunos caracteres especiales se expandan.
* "$\*": todos los argumentos se tratan como una sola cadena, unidos por el primer carácter del IFS (Internal Field Separator, que por defecto es el espacio).
* "$@"cada argumento se trata como un elemento individual, respetando las comillas originales de los argumentos
##### Ejemplos

``` bash
var="Mundo" 
echo "Hola $var" 

Resultado:
Hola Mundo
```

Aquí, el contenido de la variable $var se expandió dentro de las comillas dobles. 
⬆️ Eso lo dicen en los apuntes, en cristiano significa que ==como el $ está dentro de las comillas dobles, se coge la variable==. esto puede resolverse poniendo delante la barra \ , por ejemplo:

``` Bash
echo "Me debes $10"
```
Esto intentara imprimir algo que este en la variable 1, la forma correcta sería
``` Bash
echo "Me debes \$10"
```
Esto devolverá la cadena tal y como se ve, pero la barra invertida NO se mostrará. Por si acaso preguntasen (no lo creo) a esto se le llama que un valor "escape"

##### Comillas Simples ( \` \` )
Las comillas simples deshabilitan toda expansión de variables y la interpretación de caracteres especiales. Todo lo que se coloque entre comillas simples se interpreta literalmente.

No tiene mucho mas. No hay casos como los anteriores, lo que se meta entre comillas es cadena, y todo es todo, incluido la barra invertida
``` Bash
echo 'Me debes \$10'
```
Devolverá: Me debes \\$10

#### Ejemplos de uso de Parámetros Especiales

Vamos a escribir un shell script que haciendo uso de los parámetros especiales, nos muestre información relevante sobre la ejecución de ese shell script. Llamaremos a ese shell script muestrainfo.sh.

``` Bash
#! /bin/bash

#Autor: Manuel Sánchez Salazar
#Descripción: Muestra información relevante sobre la ejecución de este shell
#             script

echo la ruta del script es: ${0}
echo El número de parámetros posicionales: ${#}
echo Los parámetros son: ${*}
echo el PID del proceso actual: ${$}
```
![[muestrainfolinux.png]]
*LO SIENTO* si se ve borroso, ajo  y agua
Podemos ver que se usan los siguientes parámetros:
* 0 -> Se sustituye por la ruta hacia el script 
* \# -> Se sustituye por el número de parámetros (se puede ver en la foto)
* \* ->Se sustituye por el valor de todos los parámetros (una cadena de texto normalmente)
* \$ -> Se sustituye por el identificador del proceso actual

#### Ejemplos de uso de variables
![[usavariableslinux.png]]
Si os tengo que explicar esto salíos de la carrera (Es broma pero se entiende fácil, preguntadme si lo necesitáis)


==IMPORTANTE==
Al final del documento de primeros pasos de shell ([este de aquí maquina](https://platea.ujaen.es/pluginfile.php/453787/mod_resource/content/7/P07-shell-primeros-pasos.pdf)) al final de la pagina 15 y en adelante son ejercicios propuestos y ejercicios que ponen los profes para probar. hacedlos TODOS, no solo leerlos, los hacéis y veis que cambian, os dejo como deberes que me resolváis los ejercicios y me los enseñéis hechos (si tenéis dudas preguntadme, es literalmente la gracia) y intentad tenerlos para el domingo 10 de noviembre como muy tarde para que podamos corregirlos o ese mismo domingo o el lunes, porfi. Este examen lo sacamos entre todos.


![Alt Text](https://i.pinimg.com/originals/ec/da/d3/ecdad30106f0b7224486da4b7ea93de9.gif)

# Parte 2

## Introducción
### La estructura condicional if - then - else

==If NO es una orden== sino una palabra clave que indica al bash que lo siguiente a if es un condicional.
La síntesis correcta de un if en shell script es:
``` Bash
if [ condicion ]
then
	lo que quieras que haga en caso de que la condicion se cumpla
else
	Lo que quieras que haga en caso de que la condicion no se cumpla
```

==Los corchetes y los espacios que hay entre ellos son OBLIGATORIOS.== Es un fallo común no poner el espacio, si no lo pones, fallo seguro y suspenso al canto.
Ejemplo:
``` Bash
if [-d ${HOME}/bin]
```
Esto dará un error en el que no encontrará la orden \[-d.

==Es importante poner el espacio por AMBOS LADOS==

## CONDICIONALES Y OPERADORES

Para construir las condiciones, se usan valores, sustituciones de parámetros y operadores.
Por ejemplo:
```Bash
[ -r ${1} ]
```
es una condición sintácticamente bien construida que comprueba si el valor del parámetro posicional 1, es el nombre de un archivo que existe y es legible (readable)

En cristiano: -r dice si se puede leer y el parámetro posicional 1 es el que se le pasa al llamar al script ([[#Parámetros posicionales]])

### Operadores para aplicar a archivos:

Esto hay que aprendérselo si o si, son preguntas de examen y os hace falta para los scripts, os dejo aquí una tablita. Los ocho primeros son unarios, es decir que solo necesitan un archivo (El ejemplo del -r de antes) mientras que los dos últimos comparan 2 archivos 
(Ejemplo: `[ archivo1 -nt archivo2 ]`)

| Operador | Lo que hace                                                                                                                         |
| :------: | :---------------------------------------------------------------------------------------------------------------------------------- |
|    -r    | Comprueba si lo que va a continuación es el nombre de un archivo que existe y es legible.                                           |
|    -x    | Comprueba si el archivo existe y es ejecutable.                                                                                     |
|    -h    | Comprueba si el archivo existe y es un enlace simbólico.                                                                            |
|    -f    | Comprueba si el archivo existe y es un fichero regular u ordinario (no es un directorio, ni otro tipo de archivo especial)          |
|    -d    | Comprueba si el archivo existe y es un directorio.                                                                                  |
|    -s    | Comprueba si el archivo existe y no está vacío (su tamaño es mayor que cero).                                                       |
|    -e    | Comprueba si el archivo existe.                                                                                                     |
|    -O    | Comprueba si el archivo es propiedad de quien ejecuta el shell script. O es una o mayúscula.                                        |
|    -G    | Comprueba si el archivo pertenece al grupo de quien ejecuta el shell script.                                                        |
|   -nt    | Se coloca entre dos nombres de archivos y devuelve verdadero si el primero tiene fecha de modificación más reciente que el segundo. |
|   -ot    | Comprueba si el primer archivo tiene fecha de modificación más antigua que el segundo.                                              |
### Operadores para aplicar a números
Lo mismo pero con números, todos estos son binarios, es decir, necesitas dos numeros, te dejo la tabla:

| Operador | Lo que hace                                                            | Como recordarlo |
| :------: | ---------------------------------------------------------------------- | --------------- |
|   -eq    | Comprueba si los dos números que se pasan como argumentos son iguales. | Equal           |
|   -ne    | Comprueba si los dos números son distintos.                            | Not Equal       |
|   -ge    | Comprueba si el primer número es mayor o igual que el segundo.         | Greater Equal   |
|   -gt    | Comprueba si el primer número es mayor estricto que el segundo.        | Greater than    |
|   -le    | Comprueba si el primer número es menor o igual que el segundo.         | Less Equal      |
|   -lt    | Comprueba si el primer número es menor estricto que el segundo.        | Less Than       |

Como puedes ver, se basan en las comparaciones típicas en ingles, quizá eso te ayude a recordarlo
### Operadores para aplicar a cadenas de caracteres
Venga, que lo adivinas solo, otra tabla.

| -z  | Indica si la longitud de la cadena que se pasa como argumento es cero (cadena vacía).                                                                                                                     |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| -n  | Indica si la longitud de la cadena es mayor que cero.                                                                                                                                                     |
| =   | Comprueba si las dos cadenas de caracteres son iguales.                                                                                                                                                   |
| !=  | Comprueba si las dos cadenas de caracteres son distintas.                                                                                                                                                 |
| <   | Indica si la primera cadena es menor que la segunda. Hace una comparación lexicográfica (es decir, comparando carácter a carácter). Por ejemplo, la cadena “adiós” es menor que la cadena “hola”. ??????? |
| >   | Indica si la primera cadena es mayor que la segunda.                                                                                                                                                      |

Hemos terminado con las tablas (por ahora). Toma, un gatito feliz de que te hayas ==APRENDIDO LAS TABLAS DE MEMORIA QUE CAEN SIEMPRE==
![Alt Text](https://media.tenor.com/bWUeVRqW9-IAAAAi/fast-cat-cat-excited.gif)



### Condiciones compuestas

Se pueden usar condiciones compuestas, por ejemplo comprobar a la vez si un archivo es legible y ejecutable. Para ello se usan los operadores lógicos && (and) y || (or) para separar dos condiciones simples.

```Bash
[ -r ${file} ] && [ -x ${file} ]
```

Si te has aprendido las tablas (que deberías) ya sabrás qué hace ese código.

También puedes  usar el operador unario(Condicional que solo requiere 1) ! para negar cositas

### Comparaciones Avanzadas

También se pueden utilizar dobles corchetes \[\[ para realizar las comparaciones. Las diferencias son las siguientes:

* No tienes que utilizar las comillas con las variables, los dobles corchetes trabajan perfectamente con los espacios:
```Bash
Así [-f "$file" ]es equivalente a [[-f $file ]]
```

* Con \[\[ puedes utilizar los operadores || y &&, así como < y > para las comparaciones de cadena

* Puedes utilizar el operador =~ para expresiones regulares(voy a asumir que sabéis que es esto)
```Bash
[[ $respuesta =~ ^s(i)?$ ]]
```

* También puedes utilizar comodines como por ejemplo en la expresión
```Bash
[[ abc == a* ]]
```
Recordatorio de que los comodines se refiere a todo lo que va después (en este caso)

Es posible que te preguntes por la razón para seguir utilizando \[ simple corchete en lugar de doble. La cuestión es por compatibilidad. Si utilizas Bash en diferentes equipos es posible que te encuentres alguna incompatibilidad. Así que depende de ti y de dónde lo vayas a utilizar

	⬆️ Esto sale directamente del pdf, puede ser pregunta de examen asi que lo dejo aquí

## Ejemplos del uso de condicionales en Shell Script

### Comprobar si se han pasado todos los argumentos

Ejemplo:
Escribir un shell script que reciba dos argumentos y comprobar si se han pasado justamente dos argumentos.

```Bash
#!/bin/bash
# Autor: Manuel Sánchez
# Descripción: Comprueba si al script se le han pasado 
# justamente dos argumentos.
if [ ! ${#}-eq 2 ] 
then 
	echo "Error, se han pasado ${#} argumento(s)"
fi
```
1) el parámetro especial # contiene el número de parámetros posicionales que se han pasado al shell script cuando se ejecutó. Por tanto si comprobamos si es distinto de 2, habremos comprobado si a nuestro script se le han pasado, o no, justamente dos argumentos.
2) La palabra reservada then tiene que ir escrita en la línea siguiente a la línea donde está la palabra reservada if. Si se escribe en la misma línea se produce un error al interpretar la línea. 
3)  El sangrado es opcional, pero si se incluye, el código es mucho más legible.

Este código es importante porque probablemente pidan algo del estilo:
> Haz un Shell Script que una 2 archivos de texto en uno solo, comprueba errores

Probablemente sea mucho mas fácil que esto, pero esa comprobación (o la de ver si dos archivos son legibles) probablemente la pidan, es muy sencilla de hacer. En los ejercicios finales del tema lo usarán seguro

### Comprobar si existe o no un archivo

Ejemplo:
Escribir un shell script que reciba un argumento (el nombre de un archivo ejecutable) y compruebe si ese archivo está en el directorio `bin` del usuario que ejecuta el shell script y realmente es ejecutable. Si no está debe escribir por pantalla que no existe ese archivo, y si no es ejecutable debe escribir por pantalla que no es ejecutable.
```Bash
#!/bin/bash 
# Autor: Manuel Sánchez Salazar
# Descripción: Comprueba si un nombre que se pasa como 
# argumento corresponde a un programa 
# ejecutable situado en el directorio ~/bin 
if [ ${#}-ne 1 ] 
then 
	echo "Error. Se debe pasar un argumento"
	exit
fi
if [ !-e ${HOME}/bin/${1} ]
then
	echo No existe el script: ${1}
else
	if [ ! -x ${HOME}/bin/${1} ]
	then
		echo ${1} no es un ejecutable
	fi
fi
```

* La variable HOME contiene la ruta completa del directorio base del usuario que ejecuta el script. Fíjate la importancia de siempre usar las llaves {} en la sustitución de parámetros. Si no se usara, la sustitución `${HOME}/bin/${1}` sería imposible.

Esto podría haberse hecho realmente en un solo condicional usando || pero se hacen por separado para saber que esta fallando exactamente.

### Comparar cadenas de caracteres
Ejemplo:
Escribir un shell script que reciba exactamente dos argumentos y que compruebe que son distintos. Si no se escriben dos argumentos, o si éstos son iguales debe escribir un error en la pantalla.

```Bash
#!/bin/bash
# Autor: Manuel Sánchez Salazar
# Descripción: Comprueba si los dos argumentos que se dan
# son iguales.
if [ ${#}-ne 2 ]
then
	echo "Error. No se han dado dos argumentos"
else
	if [ ${1} = ${2} ]
	then
	echo "Error. Los argumentos son iguales"
	fi
fi
```

### Comparar expresiones y números

Ejemplo:
Script triangulo.sh al que se le pasan 3 argumentos y devuelve el tipo de triangulo utilizando las siguientes condiciones
Escaleno: Un triángulo en el que cada lado tiene una longitud diferente. 
Isósceles: Un triángulo en el que 2 de sus lados tienen la misma longitud. 
Equilátero: Un triángulo en el que todos los lados tienen la misma longitud.

Para saber si una variable es numérica en Shell Script podemos comprobar con una expresión regular si todos sus caracteres son numéricos.
`[[ "$variable" =~ ^[0-9]+$ ]]`
```Bash
 #!/bin/bash
 # Autor/a: Lina García Cabrera
 # Descripción: Tipo de triángulo:
 # EQUILÁTERO, ISÓSCELES o ESCALENO.
 # Se le pasan 3 números, los lados del triángulo y
 # dice el tipo de triángulo
 # Comprobar el número de argumentos
 if [ $# != 3 ]
 then
	 echo "No has pasado 3 argumentos."
	 echo "Sintaxis: ${0} lado1 lado2 lado3"
 else
	 # Comprobar que los argumentos son números
	 if [[ "$1" =~ ^[0-9]+$ ]] && [[ "$2" =~ ^[0-9]+$ ]] && [[
	 "$3" =~ ^[0-9]+$ ]]
	 then
		 # Todos los lados son iguales
		 if [ $1-eq $2 ] && [ $2-eq $3 ] && [ $1-eq $3 ]
		 then
			 echo "El triángulo es EQUILÁTERO"
		 # 2 lados son iguales
		 elif [ $1-eq $2 ] || [ $2-eq $3 ] || [ $1-eq $3 ]
		 then
			 echo "El triángulo es ISÓSCELES"
		 else
			 echo "El triángulo es ESCALENO"
		 fi
	 else
		 echo "Alguno de los argumentos no es un número"
		 echo "Sintaxis: ${0} lado1 lado2 lado3"
	 fi
 fi
```

==IMPORTANTE==
haced los putos ejercicios macho

