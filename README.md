# Contenedores Docker
(Docker is licensed under the open source Apache 2.0 license)

## Introducción

Docker es una plataforma para la gestión y ejecución de aplicaciones (imágenes) 
en contenedores software. Los contenedores surgen como una alternativa, más ligera,
a las máquinas virtuales.

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

Una imagen es una plantilla, de solo lectura (estática), para crear contenedores Docker.
A menudo, una imagen se basa en otra imagen, con alguna personalización adicional, 
que se añade como una nueva capa. Para ello, se utiliza el sistema de ficheros
UnionFS, donde cada elemento añadido es creado como una nueva capa.
Por ejemplo, puede crear una nueva imagen a partir de un ubuntu, pero con un servidor web Apache, 
la aplicación web correspondiente, así como los detalles de configuración necesarios.

Puede crear sus propias imágenes o solo puede usar aquellas creadas por otros y publicadas 
en un registro. Puede crear sus propias imágenes a partir de otros contenedores, o mediante un 
archivo Dockerfile con las instrucciones para crear la imagen. Cada instrucción crea una capa en la imagen.
Si cambia el archivo Dockerfile y se reconstruye la imagen, solo cambian las capas que han sido modificadas.


### Contenedores

Un contenedor es una instancia ejecutable de una imagen. Puede crear, iniciar, detener, mover o eliminar
un contenedor utilizando la API Docker o la CLI. Puede conectar un contenedor a una o más redes, adjuntarle 
almacenamiento o incluso crear una nueva imagen en función de su estado actual.

Por defecto, un contenedor está aislado de otros contenedores y de la máquina host.
Cuando se elimina un contenedor, la imagen no se ve alterada, y sólo perduran los datos
guardado en un almacenamiento persistente.


### Servicios

Un servicio permite hacer público un contenedor; así como escalado, estableciendo
el número de réplicas deseadas, y proporciona balaceo de carga. Esto es adecuado cuando 
los contenedores se ejecutan en varias máquinas formando un cluster (swarm).


### Registros

Un registro en Docker almacena imágenes públicas o privadas. 
Por ejemplo, Docker Hub y Docker Cloud son registros públicos, 
y el cliente Docker está configurado para buscar imágenes en Docker Hub de manera predeterminada. 


### Arquitectura Docker

![Arquitectura Docker](https://docs.docker.com/engine/images/architecture.svg)

