#Servidores 
# Introducción


Antiguamente, los servidores se usaban únicamente para que descargases cosas, después se crearon las aplicaciones cliente-servidor y con ellas se fue avanzando a lo que se tiene hoy con las aplicaciones Cloud

**Contenedor**: El contenedor tiene los elementos mínimos necesarios para que una aplicación (como Maria DB o el mismo Jellyfinn) funcionen. Con esto te ahorras no tener que virtualizar un servidor completo para tener solo 1 aplicación
# Virtualización

### Definición y ventajas
==Tecnología para la creación de recursos simulados== (no reales), hoy en día prácticamente se puede virtualizar cualquier recurso.

Cuando se habla de virtualización de máquinas: 
* **Host**: Maquina que hospeda
* **Guest**: Máquina hospedada o virtual
* **Hipervisor**: Software que pone a disposición recursos hardware para crear máquinas virtuales

 Ventajas:
* Mejoras en la administración: eficiencia, seguridad, tiempo...
* Reducción de costos (es mas barato virtualizar 3 ordenadores cliente desde el servidor que tener 3 ordenadores cliente físicamente)

## Dockers

Docker es una plataforma de software para crear aplicaciones basadas en contenedores

**Contenedores**: Entornos de ejecución ligeros, que disponen de las bibliotecas y dependencias del SO necesarias para ejecutar un código determinado

(Información extra añadida por mi)
> Docker es utilizado en gran parte, como una manera de ahorrarte el virtualizar un SSOO completo para una sola aplicación, te permite mejorar mucho el rendimiento al tener una menor carga de trabajo y permite que levantar una aplicación en un servidor distinto (en este caso el servidor puede ser prácticamente cualquier máquina con Docker instalado en el SSOO) sea mucho más sencillo.
## Kubernetes

Plataforma de orquestación para el despliegue de apps en contenedores. Algunos lo consideran como un S.O en la nube
![[Kubernetes.png]]

## Cloud Computing
### Definición
Modelo de computación que habilita el acceso a distintos recursos de forma ubicua.

Tanto los recursos como el marco de acceso son altamente configurables permitiendo una rapida provisión de nuevas capacidades y recursos

### Tipos de cloud:
- IaaS
    - Infraestructure as a Service
    - Ej: Maquina Virtual en la nube
- PaaS
    - Platform as a Service
    - Ej: Azure
- SaaS
    - Software as a Service
    - Aplicación para usuarios finales Ej: Drive
[Cloud Computing - IaaS PaaS SaaS Explained](https://www.youtube.com/watch?v=36zducUX16w)

#### Ejemplos
![[Ejemplos Cloud.png]]
### Implementaciones Cloud:
> 	¿¿¿Esto supongo que se desarrollará mas adelante???
- Pública
- Híbrida
- Privada
# Definición y tipos de Servidores

## Definición

Un **servidor** es un equipo de altas prestaciones conectado a internet y que ofrece un servicio a unos determinados clientes.
Este servicio lo suele dar una aplicación software, el servidor suele encargarse de llevar varias aplicaciones software a la vez.

>Esta definición de servidor debe ser cogida con pinzas y aplica únicamente a la asignatura, ya que prácticamente, incluso un móvil de gama baja o un pc de usuario de hace 20 años puede ejercer de servidor. Lo realmente importante es el software y para lo que se use el mismo.

* Genéricamente un servidor va a ser un equipo que ofrece uno o varios servicios utilizando los siguientes recursos:
	* **Hardware**: conjunto de componentes físicos que forman el sistema informático: procesadores, memoria, almacenamiento externo, cables, etc.
	* **Software**: conjunto de componentes lógicos que forman el sistema informático: sistema operativo y aplicaciones.
	* **Humanware**: conjunto de recursos humanos. En nuestro caso, personal técnico que crea y mantiene el sistema (administradores, analistas, programadores, operarios, etc.) y los usuarios que lo utilizan.

## Tipos de Servidores

Tipos de clasificaciones
* Según su Hardware
* Según el servicio
* Arquitectura del servicio

 ### Según su hardware
 * Dispositivos empotrados
 * Mini-PCs
 * PCs
 * Equipos específicos
 * Clústers, granjas,etc

Clúster de computadores: En un clúster de computadores todos los equipos suelen tener la misma función y están mas orientados a ejecutar tareas de alto coste computacional

Granja de Servidores: Una granja de servidores se entiende que da un servicio al exterior y los equipos se suelen dividir en subgrupos que se dedican a diferentes tareas (p.ej: Servidor Web, de BBDD, de correo, etc)

### HPC Y HTC

- HPC (High-Performance Computing)
    - Computación efectiva de gran cantidad de tareas que se solicitan desde diferentes sitios, sin planificación de llegadas y sin que sean muy costosas
    - Es un termino mas genérico
    - Suele ser en granja
- HTC (High-Throughput Computing)
    - Computación eficiente de tareas muy costosas computacionalmente
    - Termino específico ligado a investigación
    - Soluciones más específicas (SGE,Torque,HTCondor)
    - Suele ser en clúster

### GRID COMPUTING Y CLOUD COMPUTING

Son dos ejemplos de servicios de computación distribuida que disminuyen costes de adquisición y mantenimiento

![[gridcloudcomputing.png]]

Grid Computing → HTC

Cloud Computing → HPC
## Ingeniería de Servidores

### Requerimientos

#### Rendimiento
Cantidad de trabajo realizado por unidad de tiempo
Magnitudes medibles:
* Consumo de tiempo
* Numero de accesos a un componente
* Utilización de dispositivos o recursos

Elementos que afectan al rendimiento:
* Hardware
* Sistema Operativo
* Aplicaciones
* Balanceador de Carga

##### Evaluación
Saber como el software está usando el hardware de una máquina

¿Para que sirve?
* Optimizar el diseño del servidor
* Ajustar el servidor
* Predecir la carga máxima aceptable
* Seleccionar un Servidor
###### Índices de rendimiento
* Tiempo de respuesta
	* Tiempo total desde el principio hasta el final de una tarea
* Productividad
	* Cantidad de trabajo realizada por el servidor por unidad de tiempo

###### ¿Cómo evaluar?
* Monitorización (medir)
* Referenciación(benchmarking)(comparar)
* Modelado(predecir)
#### Disponibilidad
Es cuanto tiempo está funcionando el servidor
#### Fiabilidad
Cuantas probabilidades de fallar tiene el servidor y que sea a prueba de ataques
#### Escalabilidad
Capacidad de Escalar el servidor (ya sea de potencia o de servicios)
#### Eficiencia energética
El nombre lo deja clarito
#### Mantenimiento
Se debe hacer un sistema fácil de mantener
#### Coste
POS LO QUE TE CUESTA

> [!info] Recordatorio
> Todo esto se explica en los siguientes temas, por eso no entramos demasiado en ello.

