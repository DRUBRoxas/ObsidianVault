#Servidores 
# Infraestructuras Virtuales

## Introducción

![[EvolucionDesarrolloyDeploy.png]]

## Virtualización
Conjunto de tecnologías encargadas de simular recursos hardware, puede virtualizarse prácticamente cualquier recurso (CPU, Memoria, Disco, ETC.)

### Historia

La virtualización data de la **década de los 60** aunque empiezan a utilizarse mayoritariamente a **partir de los 2000**

Estas técnicas, que consistían en aislar a los usuarios dentro de los SSOO, permitían que varios usuarios accediesen a la vez a computadoras que realizaban procesamiento por lotes.
Durante la década de los 90 ya se empiezan a utilizar soluciones no propietarias que abaratan costes, pero se desperdiciaba muchos recursos hardware![[whyvirtualizacion.png]]

### Cómo Funciona
Se define una capa software de virtualización denominada *hipervisor* o VMM(Virtual Machine Monitor).
La maquina que ejecuta el supervisor se denomina *host* y las virtuales *guest*

El hipervisor:
* Accede y gestiona los recursos físicos de un servidor
* Asigna esos recursos a las máquinas virtuales
![[Virtualización.png]]

### Tipos de Hipervisores
* Tipo 1 o Nativo:
	* Se ejecutan sobre el hardware físico del sistema
	* Aísla más los posibles problemas que se produzcan en el host o los guests
	* Ventajas:
		* Más rápidos
		* Más seguro
	* Ejemplos:
		* Hyper-V
		* VMware ESX/ESXi
		* KVM
		* Critix XenServer
![[hypervisorNativo.png]]
* Tipo 2 o Alojado:
	* Se ejecutan en el sistema operativo host
	* Si el SO host tiene un problema lo tendrán todas las máquinas
	* Como ventaja es más facil de configurar
	* Ejemplos
	* VMware Workstation
	* Microsoft Virtual PC
	* Oracle Virtual Box
![[HypervisorAlojado.png]]
### Características de la virtualización
![[EsquemaVirtualizacion.png]]
* Compartición de recursos (Sharing)
	* Permite la creación de entornos de computación independientes en un host pero que comparten recursos. Esto permite *Reducir el número de servidores físicos, la administración y consumo de estos*
* Agregación (Aggregation)
	* En dirección opuesta al anterior, un grupo de hosts separados se puede vincular y presentarse como un único host
* Aislamiento (Isolation)
	* El entorno de computación proporcionado es completamente separado e independiente. Así el guest realiza la actividad *interactuando con una capa de abstracción*
	* Esta capa puede *filtrar la actividad del invitado y evitar operaciones dañinas contra el host.*
	* Implica un *aumento en la seguridad*
* Emulación (Emulation)
	* Se puede emular un entorno completamente diferente respecto al host, lo que permite la ejecución de programas invitados que requieren características específicas que no están presentes en el host físico
	* Portabilidad: El guest se empaqueta en una imagen virtual que, en la mayoría de casos, se puede mover entre hosts
* Portabilidad
	* El guest se empaqueta en una imagen virtual que,  en la mayoría de casos, se puede mover y ejecutar de forma segura sobre diferentes hosts
### Ventajas y beneficios
![[VentajasyBeneficiosVirtualizacion.png]]

### Tipos de virtualización
![[Tipos de virtualizacion.png]]

* Virtualización de servidores
	* Permite alojar más de un servidor virtual en un servidor físico.
	* Simplifica la gestión de recursos y supone un gran ahorro (ya que compras menos físicos)
	* ![[virtualizacionServidor.png]]
* Virtualización de Escritorio
	* Permite a los usuarios ejecutar múltiples sistemas operativos de escritorio desde una sola computadora
	* ![[VirtualizacionEscritorio.png]]
* Virtualización de Almacenamiento
	* combinan un grupo de dispositivos de almacenamiento físico como si fueran un solo dispositivo
	* Las aplicaciones y servidores acceden a la información sin saber en que dispositivo físico se almacenan los datos.
	* Facilita:
		* Acceso a datos
		* Copias de Seguridad
		* Transporte de datos entre ubicaciones
	* Ejemplo: Redes SAN
	* ![[NASEsquema.png]]
* Virtualización de Software
	* El objetivo es separar el software del hardware y SO de la máquina host
	* Las aplicaciones virtualizadas pueden llegar a ser accedidas desde equipos remotos.
	* Ej: Java, aplicaciones web, PCs remotos ...
	* ![[VirtualizacionSoftware.png]]
* Virtualización de Red
	* Es cuando varios recursos hardware de red se virtualizan en software.
	* Estos recursos se pueden gestionar virtualmente para asignarlos a usuarios o dispositivos de red. Ejemplo: VLANS
### Modos de Red
* Se pueden definir varios interfaces para una MV
* Para cada interfaz se puede establecer un modo de red o una topología de conexión

![[NAT.png]]
![[NATNETWORK.png]]
![[BridgetNetworking.png]]
![[adaptadorbridged.png]]
![[InternalNetwork.png]]
![[Host-Only-Adapter.png]]
#### Resumen
![[ResumenNetworks.png]]

## Contenedores

### Docker
#Definiciones 
Docker es una **plataforma de software para crear aplicaciones basadas en contenedores**

Los contenedores son **entornos de ejecución ligeros,** que disponen de las bibliotecas y dependencias del SO necesarias para ejecutar un código determinado, en cualquier entorno.

Docker es esencialmente un **conjunto de herramientas que permite a los desarrolladores crear, implementar, ejecutar, actualizar y detener contenedores**

#### Cómo funciona Docker

Los contenedores son posibles gracias a las capacidades de virtualización integradas en el kernel Linux, mas específicamente:
* Los grupos de control (Cgroups) para asignar recursos entre procesos
* Los espacios de nombres: para restringir el acceso o la visibilidad de un proceso a otros recursos o áreas del sistema.
 ![[EsquemaDocker.png]]

![[DockersvsMaquinas.png]]

#### Ventajas
* Peso más ligero
	* No llevan toda la carga de un SSOO Completo, únicamente lo que va a necesitar
* Mayor eficiencia de los recursos
	* Se pueden ejecutar varias veces mas copias de una aplicación en el mismo hardware que con maquinas virtuales completas
* Facilitan la orquestación y el escalado
	* Debido a lo ligeros que son ,se pueden lanzar muchos para una mejor escalabilidad de los servicios
* Productividad mejorada del desarrollador
	* Los contenedores son más rápidos y fáciles de mantener que las maquinas virtuales
#### Inconvenientes
* No proporcionan el mismo nivel de *aislamiento* que una máquina virtual
* Puede incurrir en una mayor *sobrecarga de rendimiento*
* Cuando un contenedor se elimina, pierde el estado de su ejecución, si se quiere que se mantenga la persistencia, se debe diseñar.

#### Componentes y Herramientas Docker
* Imágenes
	* Contienen el código fuente de la aplicación, asi como todas las herramientas, bibliotecas y dependencias que la aplicación necesita
* Contenedores
	* Un contenedor es una **instancia activa y en ejecución de una imagen.** Los *Cambios realizados en el contenedor,* como la adición o eliminación de archivos, se guardan solo en la capa del contenedor y **existen solo mientras el contenedor se está ejecutando**
* DockerFile
	* Archivo de texto que proporciona un conjunto de instrucciones para crear una imagen de Docker. Incluye el S.O, variables de entorno, etc. Promueve la automatización
	* Ejemplo:
``` DockerFile
FROM ubuntu:18.04
COPY . /app
RUN make /app
CMD python /app/app.py
```
* Utilidades Build y Run
	* ![[BuildyRunDocker.png]]
* Docker Hub
	* Repositorio público de imágenes de Docker
	* Contiene más de 100 000 imágenes de contenedores
	* Cualquier usuario de DockerHub puede descargar y compartir imágenes a voluntad
		* Esto se hace con `push` y `pull`
	* Estas imágenes pueden utilizarse como están o modificarse con DockerFiles
* Docker Engine
	* Núcleo de Docker con la tecnología necesaria para crear y ejecutar contenedores
* Docker Registry
	* Sistema escalable de almacenamiento y distribución de código abierto para imágenes de Docker
	* Permite realizar seguimiento de las versiones de imágenes de los repositorios
	* Basado en git. Puede ser propietario o estar disponible en diferentes servicios cloud de Google, AWS, Azure, etc
* Docker Compose
	* Este man es tan tocho que tiene su propio punto
##### DOCKER COMPOSE
* Herramienta para definir y ejecutar aplicaciones multicontenedor.
* Es un primer paso a la automatización de flujos de trabajo multicontenedor.
* Permite realizar acciones con los contenedores como: crear, iniciar, detener, ver el estado, ver salida del registro...
* En un archivo **docker-compose.yml**  se define de forma declarativa los contenedores que se van a desplegar, recursos que vas a utilizar, así como las dependencias, etc
> [!tip] 
> Esto fue una pregunta tipo test en la que cayó gente. el archivo debe llamarse SIEMPRE docker-compose.yml es la única opción válida, siempre y cuando esto no cambie a futuro.

Ejemplo de un Docker Compose con comentarios:
``` docker-compose.yml
services:
	web: # servicio (contenedor) para despliegue de servidor web
		build: .      # se compila a partir de un DockerFile
		ports:
			- 8080:80
		depends_on:
			- database  # necesita del siguiente servicio para funcionar
		restart: always # política de reinicio si se cae el servicio
		volumes:
			- /usercode/:/code
	database:  # servicio que pone en marcha una BBDD (mysql)
		image: mysql:latest # Imagen de Docker Hub a poner en marcha
		environment: # variables de entorno necesarias para el servicio
			- MYSQL_ROOT_PASSWORD=root
			- MYSQL_USER=testuser
			- MYSQL_PASSWORD=admin123
			- MYSQL_DATABASE=backend
		restart: always
		volumes:
		- /usercode/db/init.sql:/docker-entrypoint-initdb.d/init.sql
```


## Kubernetes

#Definiciones 
Es una **plataforma de orquestación** para el despliegue de apps desarrolladas sobre contenedores

Permite a los desarrolladores crear **flujos de trabajo personalizados y automatización de nivel superior** para implementar y administrar aplicaciones compuestas de múltiples contenedores.

### Componentes
#Definiciones 
* **Clúster**: Conjunto de máquinas *worker (nodos)* que ejecutan aplicaciones en contenedores
* **Nodos (workers)**: Computadoras físicas o máquinas virtuales que alojan los *Pods* que ejecutan las cargas de trabajo
* **Pods**: Encargados de ejecutar las máquinas de trabajo/contenedores
* **Plano de Control**: Administra los nodos y los Pods y se ejecuta en diferentes máquinas de clúster

#### Agrupaciones de componentes

##### Componentes del plano de control
Toman decisiones globales, detectan y responden a los eventos del clúster y se pueden ejecutar en cualquier máquina del clúster.
Algunos componentes (Los que le importan a Rivera) son:
* **kube-apiserver**
	* Expone o sirve la API de kubernetes
* **etcd**
	* Almacenamiento de alta disponibilidad para todos los datos del clúster
* **kube-scheduller**
	* Asigna pods recién creados a nodos

Los controladores trabajan para conducir el estado real hacia el estado deseado. 
Hay varios tipos: Para controlar el *estado* de los nodos, la *replicación* (escalado automático), los *endpoints* (servicios y pods), y los *tokens* (espacios de nombres)
* Estos son:
	* **kube-controller-manager**
		* Encargado de ejecutar procesos controlador.
		* Ejemplos:
			* Controlador de nodos: Responsable de notar y responder cuando los nodos caen
			* Controlador de trabajos: Crea pods para ejecutar tareas hasta su finalización
	* **cloud-controller-manager**
		* Permite vincular un clúster a la API de su proveedor de nube y prepara los componentes que interactúan con esa plataforma de la nube.
 ![[planodecontrol.png]]
##### Componentes de nodo
Se ejecutan en cada Nodo. Mantienen los Pods en ejecución y proporcionan el entorno adecuado para ello.
* Son:
	* **kubelet**: El más importante, se ejecuta uno en cada Nodo y se asegura que cada contenedor esté ejecutándose en un Pod
	* **kube-proxy**: Se ejecuta en cada Nodo para posibilitar la comunicación entre Pods
	* **Container runtime**: Software responsable de ejecutar los contenedores

![[Esquema kubernetes.png]]

#### Pod
Es un **Host lógico** que puede contener uno o más contenedores (acoplados o menos relacionados)

Recursos en un Pod:
* Almacenamiento
* Redes
* Contexto 
![[esquemapod.png]]

Estos contenedores comparten una IP y un espacio de puertos, ejecutándose en un espacio compartido.

### Deployments y ReplicaSets
#Definiciones 
Un **Deployment** es una declaración donde se definen Pods y ReplicaSets. Se define un estado deseado y el controlador lo mantiene.

Un **ReplicaSet** mantiene estable y funcionando un conjunto de Pods

### Servicios
#Definiciones 
Un servicio es una abstracción que **describe cómo se accede a las aplicaciones, definidas por conjuntos de Pods,** y que puede describir puertos y balanceadores de carga

Se implementa de modo que **provee de un mecanismo de descubrimiento de servicios.** De esta manera *se otorga a sus Pods su propia IP y un nombre DNS* para un conjunto de Pods lo que *permite balancear la carga* entre ellos

### Addons

Usan recursos de Kubernetes para implementar funciones de clúster.

Ejemplos:
* DNS: Servidor DNS que sirve los registros DNS
* WEB UI (Dashboard): Interfaz de usuario basado en WEB para Kubernetes
* Container Resource Monitoring: Registra métricas sobre contenedores

## Computación en la nube

#Definiciones 
Consiste en proporcionar **acceso a recursos y servicios informáticos** de cualquier índole, desde aplicaciones a centros de datos, **a través de internet** y con un modelo de uso bajo demanda.

La computación en la nube depende de gran medida de tecnologías como la virtualización y la automatización.
* La virtualización facilita la abstracción y la gestión de recursos.
* La automatización permite a los usuarios un alto grado de autoservicio en la gestión de recursos.

>[!tip]- La historia no le interesa a nadie
>![[Pasted image 20241229024238.png]]

### Tipos de servicios en la nube


![[Pasted image 20241229024343.png]]

>[!note] Notas del editor:
>Este es el esquema más feo visualmente que me he cruzado en la carrera wtf

#### Infraestructure as a Service (IaaS)

* Proporciona instancias de servidores virtuales (VM) y almacenamiento, así como APIs de acceso a éstos.
* Las MVs son administradas libremente por los usuarios.
* Se ofrecen instancias con diferentes capacidades de cómputo y almacenamiento.
#### Platform as a Service (PaaS)

* Se ofrecen herramientas de desarrollo que se usan para el desarrollo de software en general.
* Se accede mediante APIs, portales web, etc.
* Ejemplos:
	* AWS Elastic Beanstalk
	* Google App Engine
#### Software as a Service (SaaS)
* Se ofrecen aplicaciones software por Internet
* Estas aplicaciones pueden ser accedidas desde un dispositivo que tenga conexión a Internet
* Ejemplos:
	* Microsoft 365.
	* Servicios de Correo Electronico.
	* Suit de Google (Docs, Slides, etc).

### Tipos de implementaciones en la nube
#### Privada

* La propia empresa crea y mantiene su propia infraestructura
* Este modelo ofrece la versatilidad y la comodidad de la nube, al tiempo que conserva:
	* La gestion
	* El control
	* La seguridad
* Tecnologías en la nube privada (Ejemplos):
	* VMWare
	* OpenStack
#### Pública

* Un proveedor de servicios en la nube (CSP) ofrece un servicio en la nube a través de internet
* Los servicios de nube pública se venden bajo demanda
	* Generalmente por Minutos o Horas
	* Puede haber compromisos a largo plazo disponibles para muchos servicios
* Los clientes pagan por ciclos de la unidad central de procesamiento, el almacenamiento o el ancho de banda que consumen
* Ejemplos:
	* AWS
	* Azure
	* IBM
	* GCP -> el de google, por si acaso.
#### Híbrida

* Combinación de servicios de nube pública y una nube privada local, con orquestación y automatización entre los dos.
* Las empresas pueden **ejecutar cargas de trabajo de misión crítica o aplicaciones confidenciales en la nube privada** y usar la nube pública para **manejar ráfagas de carga de trabajo o picos en la demanda.**
* El objetivo es crear un entorno **unificado, automatizado y escalable** que aproveche lo que puede proporcionar una pública, al mismo tiempo que mantiene el control sobre los datos de misión crítica
#### Nube múltiple

+ Se dispone de diferentes proveedores de IaaS
+ Ventajas:
	+ Minimizar el riesgo de una interrupción en el servicio
	+ Aprovechar los precios más competitivos de un proveedor en particular
+ Inconveniente:
	+ El desarrollo de aplicaciones puede ser un desafío debido a las diferencias entre los servicios de proveedores de nube y las API. Esto debería minimizarse con el tiempo.
	+ Ejemplo: Open Cloud Computing Interface

#### Ventajas de la computación en la nube
+ Aprovisionamiento en modo autoservicio 
+ Elasticidad
+ Pago por uso
+ Resiliencia de la carga de trabajo
+ Movilidad de datos y cargas de trabajo
+ Amplio acceso a la red
+ Gestión de usuarios y de recursos de recursos 
+ Manejo de costos
+ Continuidad del negocio y recuperación ante desastres (BCDR).

#### Inconvenientes de la computación en la nube
+ Seguridad en la nube.
+ Imprevisibilidad de costes 
+ Falta de capacidad y experiencia
+ Gestión de múltiples nubes
+ Gobernanza de TI y cumplimiento de las leyes de la industria
+ Rendimiento (latencia) en la nube
+ Migración a la nube
+ Dependencia de un proveedor

## Aplicaciones nativas en la nube. Microservicios

#Definiciones 
Consiste en crear y ejecutar **aplicaciones para aprovechar la computación distribuida** que ofrece este modelo de ejecución en la nube.

Las aplicaciones nativas de la nube están **diseñadas y creadas para aprovechar la escala, la elasticidad, la resiliencia y la flexibilidad** que ofrece la nube.

Algunos elementos son:
+ Contenedores
+ Kubernetes
+ Mallas de servicio
+ microservicios
+ funciones sin servidor

Los proveedores de servicios en la nube (Google, AWS, Azure...) habilitan herramientas y servicios para que los desarrolladores reduzcan las tareas operativas y desarrollen más rápido.

### Arquitecturas tradicionales monolíticas

**Problemas cuando se desarrollan y prueban nuevas funciones**  ya que necesita mucho esfuerzo para implementar este cambio en producción:
* Múltiples equipos tienen que coordinar sus cambios de código
* La implementación de varias características a la vez requiere mucha integración inicial y pruebas funcionales.
* Los equipos de desarrollo estaban restringidos a usar uno o dos lenguajes de programación.

### Nuevas arquitecturas basadas en la nube
![[Pasted image 20241229030959.png]]


### Características de las aplicaciones nativas en la nube
Estas aplicaciones **se desarrollan en base a servicios independientes** (microservicios),**empaquetados en componentes** (contenedores por ejemplo) livianos autónomos que son portátiles y se pueden escalar fácilmente según la demanda.

Características:
* al encapsular todo en un contenedor, **aísla la aplicación y sus dependencias de la infraestructura subyacente**
* Esto le permite **implementar esa aplicación en contenedores en cualquier entorno** 
* El **ciclo de vida de los contenedores se administrará** promoviendo la automatización de Kubernetes
* Las **aplicaciones nativas de la nube a menudo se entregan a través de una canalización de DevOps** que incluye cadenas de herramientas de integración continua y entrega continua (CI/CD). Las canalizaciones de CI/CD son importantes para automatizar la creación, las pruebas y la implementación de aplicaciones nativas en la nube

### Arquitecturas de microservicios
#Definiciones 
Consiste en una colección de servicios independientes, ligeros y poco acoplados.
Cada servicio:
+ Tiene su propio código fuente
+ Es responsable de una sola parte de la funcionalidad
+ Puede elegir la mejor tecnología para sus casos de uso
+ Cada servicio tiene su propio plan DevOps (Ver abajo) . Cada servicio se despliega en un entorno autónomo.
+ Se comunican entre sí mediante APIs bien definidas y protocolos sencillos como REST sobre HTTP (Si no sabes lo que es REST [What is REST?: REST API Tutorial](https://restfulapi.net/), no es de este examen pero es algo que deberías saber a estas alturas)
+ Es responsable de la persistencia de sus propios datos
>[!nota]- Plan DevOps
> + Probar
> + Liberar
> + Desplegar
> + Escalar
> + Integrar
> + Mantener de forma independiente

#### Beneficios
* Escalado independiente
* Desarrollo independiente
* Despliegue (adivina qué) independiente
* Arquitectura robusta y tolerante a fallos
* Gobernanza descentralizada
	* Cada equipo de desarrollo puede elegir la tecnología y el lenguaje.

#### Aspectos Rotativos
>[!note] Es paja, no se hasta que punto puede caer

Para que esta arquitectura funcione hace falta solventar ciertos aspectos operativos:
+ **Replicación de servicios**: mecanismo mediante el cual los servicios pueden escalar fácilmente basándose en metadatos
+ **Búsqueda y descubrimiento de servicios**: un mecanismo que permite la búsqueda de servicios y encuentra el punto final para cada servicio.
+ **Monitoreo y registro de servicios**: mecanismo para agregar registros de diferentes microservicios y proporcionar un reporte consistente.
+ **Resiliencia**: un mecanismo para que los servicios tomen automáticamente acciones correctivas cuando hay fallos.
+ **DevOps**: mecanismo para manejar la integración y el despliegue continuo 
+ **API gateway**: un mecanismo para proporcionar un punto de entrada para los clientes

![[PatronDiseniooArquitecturanube.png]]
#### Ejemplo Netflix
![[ArquitecturaNetflix.png]]