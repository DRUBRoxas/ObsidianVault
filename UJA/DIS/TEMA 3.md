#Servidores

# Servidores de altas prestaciones

 El objetivo es montar un servidor de altas prestaciones. Se deben tener en cuenta los siguientes *requerimientos* :
* Servicios externos que el sistema debe proporcionar
* Numero de Clientes
* Disponibilidad
* Seguridad
* Etc.

Los requerimientos anteriores determinarán el diseño y características del servidor:
* Capacidad de procesamiento
* Arquitectura de servidores y servicios
* Sistema de almacenamietno
* Red de interconexión
* Disponibilidad
* Balanceo de Carga
* Escalabilidad
* Resto de Software Instalado

Algunos Ejemplos de alternativas:
![[Alternativa1T3DIS.png]]![[Alternativa3T3Dis.png]]![[Alternativa2T3Dis.png]]![[Alternativa4T3DIS.png]]

## Categorías Básicas

* **Front-end y Back-end** donde F.E. (presentation layer) es la máquina relacionada con lo que ve el cliente y B.E. (Data access layer) son equipos que ejecutan software de procesamiento y acceso a datos
* **Producción o desarrollo**.
* **Respaldo**: Por si cayese el principal
> [!tip]- Información adicional
> Puedes buscar en Google `warm/hot spare server` para saber más, aunque no debería ser necesario para el examen

* **Equipos de Seguridad**.
* **Equipos de gestión del sistema**: Provisionamiento, despliegue, etc.

![[ServidoresEntornoDesarrollo.png]]

## Alta disponibilidad
* Salvo casos especiales, deben estar activos 24/7
* Das mala imagen a los usuarios si tus servicios se caen mucho (meta???????)

### Definiciones
* **Disponibilidad**: Capacidad para que un servidor acepte peticiones (siempre)
* **Tiempo de inactividad (DOWNTIME)**: Cantidad de tiempo en el que el sistema no está disponible. Hay dos tipos:
	* *Tiempo de inactividad Planificado*: Para actualizar hardware, SO, Software, etc. Solo debe existir este tipo de tiempos
	* *Tiempo de actividad no planificado*: Surgen de algún evento físico tales como fallos en el hardware, anomalías ambientales o fallos software
			<!--El ultimo es un error 100% humano, esto es inaceptable --> 
* **Disaster Recovery Plan**: Protocolo para recuperar el sistema ante diferentes eventualidades


### Disaster Recovery Plan
Según el último GDRI de Acronis el ==origen en las interrupciones== de servicio se debieron:
* Desastres naturales -> 4%
* Incidentes en las instalaciones de los servidores (problemas eléctricos, fuegos y explosiones) -> 38%.
* Errores humanos, actualizaciones problemáticas y virus -> 52%.

Para estos casos se suele diseñan un **plan de recuperación ante desastres que debe ser personalizado** según las necesidades de las organizaciones teniendo en cuenta factores como:
* Tipo de negocio o actividad
* Nivel de seguridad necesario para datos y aplicaciones
* Ubicación
Se puede desarrollar internamente o adquirir de un proveedor como SaaS o RaaS

![[DSRDIS.png]]

###  Índice de disponibilidad
#FormulasServidores Índice de disponibilidad
* Escala "punto nueve":
		$100-(tiempoCaido/tiempoTotal*100 )$
* Ejemplos:
	* Caida de 1 hora al día: $100-(1/24)*100=95.83$%
	* Caída de 1 hora a la semana: 99.404%
	* Caída de 1 hora al mes: 99.86 %
	* Caída de 1 hora al año: 99.9885%
* Lo ideal sería un 100% pero a partir de un 99.9% ya se considera aceptable.
* Objetivo genérico: ==conseguir 5 nueves==

### Como conseguir la alta disponibilidad

* **Duplicando** (o x3, o x4, etc.) los componentes o lo que es lo mismo, planificando sistemas redundantes o de respaldo
* **Monitorizando** el funcionamiento de los componentes, para que cuando se detecte un fallo se ponga en marcha el sistema de respaldo correspondiente

Se debe comprobar también que el sistema esté bien dimensionado. ¿Tenemos suficiente *capacidad* para atender las peticiones?

![[Redundacia en servidores.png]]
> [!info] puede que caiga algo de aquí como tipo test pero poco probable, aun así, leerlo está bien
### Disponibilidad del servidor (Fault-Tolerant Servers)

Son Equipos que tienen duplicados de cualquier elemento que lo componen, para cambiar a este en caso de necesitarlo. Suelen usarse en entornos de virtualización
Ejemplos:
* NEC Express Server Series
* Stratus
* Fujitsu, etc.

### Infraestructuras con equipos redundantes

Otra opción es implantar una infra que duplique el equipo físico.
¿Cómo funciona esto?
* Montas dos servidores exactamente iguales
* Uno es el principal y el otro el de respaldo
* Monitorizas el principal, si este falla, entonces el de respaldo "sustituye" al principal
* No pierdes el servicio si el principal cae

Algunos conceptos:
* Recurso = servicio
	* Compuesto por varios servicios o subservicios
	* Ejemplo: Recurso WEB
		* Servicio: IP pública donde se pide el servicio/recurso. No pertenece a un equipo en particular
		* Servicio: httpd
		* Servicio: NFS
	* Suele ser necesaria al menos una doble conexión a un switch
* Dominio de Servicio (Failover Domain)
	* Conjunto de ordenadores de redundancia para un servicio
* Barreras o Vallas (Fences)
	* Mediante Software o Hardware se pueden definir dispositivos que se desactiven si se detectan problemas
		* Resource level: se impide el acceso a un recurso
		* Node level: se impide que el nodo acceda a recursos

### Disponibilidad de Aplicaciones
* Es más complicado monitorizar aplicaciones
* Esta monitorización depende también del Sistema Operativo 
* Dependencia entre módulos de una aplicación 
* Intentar que si falla un módulo no falle la aplicación completa, siempre que sea posible -> Desarrollar aplicaciones robustas

## Escalabilidad

Es la capacidad de aumentar los recursos del sistema con el objetivo de conseguir una mejora.
Idealmente, el aumento de recursos debería ser un aumento lineal de la mejora de los servicios.

> [!info] A tener en cuenta
Ante el incremento de peticiones, se puede disminuir la calidad del servicio ofrecido por el sistema. Para que esto NO ocurra, hay que escalar el sistema.

Es importante tener *previsto un aumento de la demanda de servicios* que ofrecemos para poder responder a esta.

Para que el sistema sea escalable hay que tener en cuenta esta característica *desde la etapa de diseño*

Algunos consejos son:
* Diseñar arquitecturas paralelas escalables
* Que estas arquitecturas trabajen asíncronamente
### Consideraciones de diseño

En principio siempre se puede pensar en ampliar el hardware
* Por ejemplo si detectamos que la CPU suele estar constantemente al 90%

Problema:
* Puede que la actualización de un recurso sobrecargue otro
* Actualizar la CPU puede saturar la memoria, sistema de almacenamiento, etc.

Existen dos formas de escalar el sistema:
* Escalar en *vertical* (scale up)
	* Incrementar CPU, memoria, discos, etc. -> Servidor mas potente
* Escalar en *horizontal* (scale out)
	* Añadir más máquinas a algún subsistema -> Aumento de concurrencia

Algunas veces puede que solo baste un escalado vertical, sin embargo, para ciertos sistemas solo el escalado horizontal será eficiente.

![[EscaladoVertical.png]]
![[MejoraHorizontal.png]]

### Detectando la sobrecarga de un sistema

La respuesta está en la monitorización, generalmente, se detectarán síntomas de lentitud en las respuestas a los servicios

Más concretamente podemos monitorizar diferentes elementos:
* Si la CPU está por encima del 80-85% podemos plantear una mejora
* Una ocupación de RAM importante y una alta cantidad de swaping nos pueden sugerir incrementar la memoria
* % de uso de las conexiones de red

### Diseñando un sistema escalable

* Sistema de Red 
	* Debe poder soportar tráfico creciente
* Sistema de almacenamiento 
	* Compartido 
	* Redundante
* Balanceador de carga 
	* Hardware 
	* Software
* Aplicaciones y servicios
	* Independientes de la máquina en que se ejecutan 
	* Que puedan trabajar en paralelo
### Capacity Planning

Proceso por el que se determina la capacidad de un sistema para afrontar un incremento en la demanda del servicio

infraestructura IT: Hardware + Software

¿Cuándo se realiza?
* Mientras se desarrolla un proyecto
* Periódicamente cuando el sistema esté en producción para identificar cuellos de botella y posibles riesgos
* Cuando se tomen decisiones sobre el negocio
#### Fases
* Definición de los niveles de servicio
	* Establecimiento de un nivel mínimo
* Análisis de la capacidad
	* Modelos matemáticos, minería de datos,...
	Ejemplo básico:
		Capacidad_predicha: $UtilizacionActual*FactorEscala*MargenError$
		- Heurística o la experiencia como base
- Planificación de acciones
	- En el caso de que sean necesarias para ofrecer el servicio
	- Entra en juego la escalabilidad del sistema

## Balanceo de carga
Reparte el trabajo entre varias máquinas

Balanceador de carga: se encarga de repartir tareas
- Software
- Hardware
Clave para:
* Eficiencia
* Disponibilidad
* Escalabilidad
Inicialmente, se pensaba que lo adecuado para realizar una gran tarea era adquirir un gran equipo único

Esta opción supone importantes problemas:
* Caro de adquirir
* Caro de mantener
* Software propietario
* Complicado de escalar...
Alternativa a mainframe: Varias máquinas menos potentes trabajando en paralelo

Ventajas:
* Menos costes de adquisición. Varias maquinas mas baratas hacen mejor el trabajo que una muy potente.
* Menos costes de mantenimiento.
* Mejora de la disponibilidad
* Mejora la seguridad
![[EsquemaBasicoBalanceo.png]]
![[EsquemaBasicoClustering.png]]

### Tipos de dispositivos de balanceo
2 tipos:
* Por Software
	* En linux tenemos HAProxy
	* Local Director (cisco)
	* BIG-IP
	* NLB (microsoft)
* Por Hardware
#### Ventajas e inconvenientes
* Un software será mas versátil, más genérico y menos costoso que un dispositivo específico.
* un dispositivo específico ofrecerá más eficiencia que un ordenador
Así pues la elección de uno o otro vendrá marcada por la carga y por el coste.

#### Dispositivo de Balanceo específico
* Mas eficientes y con mas funciones
* Su configuración se suele realizar mediante línea de comandos o servicio web empotrado
* Ejemplos:
	* Cisco Systems
	* Foundry Networks
	* Nortel Networks
	* F5 Networks
	* Radware
#### Funcionalidades 
Garantizan disponibilidad:
- Los de tipo hardware suelen disponer de componentes redundantes (CPU, RAM, etc.)
- Monitorizan
- Se permite la implantación de dos balanceadores (activo y pasivo)
- Permiten persistencia aunque algo falle
- Permiten la inclusión de servidores en plan Plug and Play
- Realizan NAT
- Definición de cortafuegos
- Caching service: almacenan contenidos estáticos por los clientes, de forma que los sirven ellos mismos sin redirigir la petición
#### Monitorización
Los balanceadores deben monitorizar la disponibilidad de los equipos mediante:
* pings
* Consultas específicas de las que se esperan respuestas específicas
Indirectamente se aumenta la disponibilidad

#### Persistencia
#Definiciones
Persistencia: Consiste en mantener las conexiones de un usuario siempre al mismo equipo físico que empezó a atenderlo

> [!warning] Recordatorio
> Las conexiones HTTP *NO SON PERSISTENTES*

La persistencia puede ser imprescindible para ciertas aplicaciones web sobre todo si se mantienen cookies o un estado por usuario: administración electrónica. una tienda web, etc.

El balanceador elige el equipo físico al que se reenviará la primera petición, pero los subsiguientes peticiones deben reenviarse a ese mismo equipo
![[EjemploBalanceoCargaDNS.png]]


### Algoritmos de balanceo de carga
* Si las máquinas tienen todas las misma potencia puede utilizarse un algoritmo de asignación por turnos
* En caso contrario ya se suelen usar ponderaciones
* Ejemplos:
	* Balanceo según turnos (RR)
	* Balanceo según el menor número de conexiones
	* Balanceo según ponderación
	* Balanceo según prioridad
	* Balanceo según tiempo de respuesta
	* Combinación de los algoritmos de tiempo de respuesta y menor número de conexiones
	![[BalanceopPorTurnos.png]]
	![[BalanceoSegunelmenornúmerodepeticiones.png]]![[BalanceoSegunmenornumeropeticiones.png]]
	![[BalanceoSegunPonderación.png]]
	![[balanceoSegunPrioridad.png]]
	![[balanceoseguntiempo.png]]
>[!info] Aclaración
>Podria haber hecho esto mejor pero sinceramente que puta pereza para media puta pregunta tipo test te lees esto y la chupas

### Consideraciones Finales
* Algoritmos más simples funcionan peor pero menos coste computacional
* Se puede empezar analizando el tipo de tráfico que vamos a tener e ir probando desde los algoritmos más fáciles hasta los más complicados, buscando una solución óptima para ti, no necesitas siempre tener los algoritmos más complicados.
* También se puede hibridar estos algoritmos:
	* Establecer turnos en servidores con similares ponderación, prioridad, etc.
	* Monitorizar tiempo de respuesta y números de servicios realizados para decidir la siguiente asignación

### GSLB (Global Sever Load Balancing)
Balanceo de carga entre distintos CPDs situados en diferentes ubicaciones geográficas

#### Ventajas
* Se evita la no disponibilidad por una caída total de un CPD
* Aumenta la disponibilidad en general
* Disminuye los tiempos de respuesta por ubicación geográfica
* Evidentemente también se permite balancear carga.

#### Implementaciones
* Por DNS
* Redirección HTTP
* GSLB Basado en Balanceador/DNS
* GSLB usando protocolos de enrutamiento
![[Balanceo Global DNS.png]]![[Balanceo Global por HTTP.png]]
![[BGB-BalanceadorDNS.png]]
![[BalanceadorDNSGLobal.png]]
![[Balanceo GLobal Enrutamiento.png]]