# Contenedores Docker
(Docker is licensed under the open source Apache 2.0 license)

## Introducción

Docker es una plataforma para desarrolladores y administradores de sistemas para 
implementar y ejecutar aplicaciones en contenedores, denominadas 
aplicaciones contenerizadas. Las ventajas de la contenerización son:

Flexible: las aplicaciones más complejas pueden contenerizarse.
Ligera: los contenedores aprovechan y comparten el kernel de host.
Intercambiable: se pueden realizar actualizaciones y mejoras sobre la marcha.
Portátil: se pueden construir localmente o en la nube y ejecutarse en cualquier lugar.
Escalable: se puede aumentar o disminuir automáticamente réplicas de un contenedor.
Apilable: Se pueden apilar servicios verticalmente y sobre la marcha.

Un contenedor se ejecuta nativamente en Linux y comparte el kernel de la máquina host con otros contenedores. 
Por el contrario, una máquina virtual ejecuta un sistema operativo completo cuyo acceso a los recursos de host 
se realiza mediante un hipervisor. En general, las máquinas virtuales proporcionan un entorno 
con más recursos de los que la mayoría de las aplicaciones necesitan. En la siguiente imagen se muestran
las diferencias entre ambas tecnologías:

<img src="https://www.docker.com/sites/default/files/d8/2018-11/docker-containerized-appliction-blue-border_2.png" alt="Contenedores" width="45%" height="45%"/> <img src="https://www.docker.com/sites/default/files/d8/2018-11/container-vm-whatcontainer_2.png" alt="Máquinas Virtuales" width="45%" height="45%"/>

(Imágenes obtenidas desde https://www.docker.com)

En la actualidad, existen dos ediciones de Docker: Community Edition (CE) and Enterprise Edition (EE).
Docker CE es ideal para iniciarse en el mundo de los contenedores y experimentar con aplicaciones basadas en contenedores.
Docker EE está pensada para el despliegue en producción de aplicaciones empresariales.
Puede obtener más información, así como los detalles de instalación para diferentes plataformas, 
de ambas ediciones, en [la documentación de Docker](https://docs.docker.com/install).

## Conceptos Básicos

Docker permite empaquetar y ejecutar aplicaciones en un entorno aislado llamado contenedor.
Los contenedores son más ligeros que las máquinas virtuales porque no necesitan la carga adicional de un hipervisor.

Docker proporciona herramientas, mediante una arquitectura cliente/servidor, 
para administrar el ciclo de vida de los contenedores.

### Docker Engine

El motor de Docker (Docker Engine) es una aplicación con tres componentes principales:

- Un servidor (demonio) (dockerd).
- Una API REST para comunicación con el demonio.
- Un cliente de línea de comandos (CLI) (docker) que usa el API para comunicarse con el demonio.

### Imágenes

Una imagen es una plantilla, de solo lectura (estática), para crear contenedores.
A menudo, una imagen se basa en otra imagen, con alguna personalización adicional, 
que se añade como una nueva capa. Para ello, se utiliza el sistema de ficheros
UnionFS, donde cada elemento añadido es creado como una nueva capa.
Por ejemplo, puede crear una nueva imagen a partir de un ubuntu, pero con un servidor web Apache, 
la aplicación web correspondiente, así como los detalles de configuración necesarios.

Puede crear sus propias imágenes o solo puede usar aquellas creadas por otros y publicadas 
en un registro. Puede crear sus propias imágenes a partir de otros contenedores, o mediante un 
archivo Dockerfile con las instrucciones para crear la imagen. Cada instrucción crea una capa en la imagen.
Si cambia el archivo Dockerfile y se reconstruye la imagen, solo cambian las capas que han sido modificadas.

Puede gestionar las imágenes utilizando la API Docker o el docker CLI.

### Contenedores

Un contenedor es una instancia ejecutable de una imagen. Puede crear, iniciar, detener, mover o eliminar
un contenedor utilizando la API Docker o el docker CLI. Puede conectar un contenedor a una o más redes, adjuntarle 
almacenamiento o incluso crear una nueva imagen en función de su estado actual.

Cuando se elimina un contenedor, la imagen no se ve alterada y sólo perduran los datos
guardado en un almacenamiento persistente.

Por defecto, un contenedor está aislado de otros contenedores y de la máquina host.
Los contenedores pueden conectarse (link) mediante redes y utilizar volúmenes del host para almacenamiento persistente.


### Servicios

Un servicio permite publicar en Internet una aplicación contenerizada; así como su escalado, estableciendo
el número de réplicas deseadas, y proporcionando balaceo de carga. Esto es adecuado cuando 
los contenedores se ejecutan en varias máquinas formando un cluster (swarm).

Cuando un servicio es ofrecido por más de un contenedor; por ejemplo, una aplicación web con una base de datos,
es más adecuado crear grupos de contenedores. Para ello, Docker incluye la herramienta docker-compose que,
utilizando archivos de configuración declarativos, permite crear un ecosistema docker (redes, 
volúmenes de almacenamiento, contenedores, etc.)

### Orquestación de contenedores

La orquestación de contenedores hace referencia a la posibilidad de planificar y administrar contenedores
de forma automática. Este concepto se hace fundamental cuando una aplicación está organizada en varios 
contenedores; por ejemplo, si ha sido desarrollada bajo una arquitectura de microservicios o, 
en aplicaciones más monolíticas, donde es necesario un servidor web, un sistema gestor de base 
de datos e, incluso, algunos otros servicios.

El sistema de orquestación velará tanto por los contenedores como por el número de réplicas de éstos
y para que el resto de elementos estén en el estado deseado en cada momento, actuando en consecuencia si fuese necesario.

Los sistemas de orquestación más utilizados son: Kubernetes, Swarm, Apache Mesos. 



### Registros 

Un registro en Docker almacena imágenes públicas o privadas. 
Por ejemplo, Docker Hub y Docker Cloud son registros públicos, 
y el cliente Docker está configurado para buscar imágenes en Docker Hub de manera predeterminada. 


### Arquitectura Docker

![Arquitectura Docker](https://docs.docker.com/engine/images/architecture.svg)
(Imagen obtenida de https://docs.docker.com/engine/images/architecture.svg)
