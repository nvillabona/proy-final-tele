# Proyecto de balanceo de carga de base de datos con MySQL y Nginx

Este proyecto tiene como objetivo implementar un sistema de balanceo de carga para una base de datos MySQL utilizando Nginx como servidor proxy.
Esto permitirá distribuir el tráfico de consultas entre una instancia principal (master) y una instancia secundaria (slave), proporcionando mayor disponibilidad y rendimiento.

## Configuración del entorno
El proyecto utiliza Docker Compose para definir y desplegar los servicios necesarios.

El archivo **docker-compose.yml** define los siguientes servicios:
- **load_balancer:** El servicio de Nginx que actúa como balanceador de carga. Se utiliza la imagen de Nginx y se mapea el puerto 3306 para permitir conexiones a la base de datos.
- **master_db:** El servicio de la instancia principal de MySQL. Se utiliza la imagen de MySQL y se configura la contraseña de root y la base de datos.
- **slave_db:** El servicio de la instancia secundaria de MySQL. Se utiliza la imagen de MySQL y se configura la contraseña de root, la base de datos y los parámetros de replicación para conectarla con la instancia principal.
- **debian1:** Un servicio adicional que utiliza la imagen de Debian para ejecutar comandos en el contenedor. En este caso, se utiliza para instalar el servidor MySQL de pruebas y Sysbench en el contenedor.

## Configuración de la base de datos
Las bases de datos se almacenan en volúmenes de Docker para preservar los datos incluso si los contenedores se reinician o eliminan. Se definen dos volúmenes, uno para la instancia principal (master_db) y otro para la instancia secundaria (slave_db), en las rutas ./mysql/master y ./mysql/slave respectivamente.

Además, se comparten los archivos de configuración de MySQL (my.cnf) y los certificados TLS (certs) entre los contenedores.

## Configuración del balanceador de carga
La configuración del balanceador de carga se realiza mediante el archivo nginx.conf, que se encuentra en la carpeta conf.

## Ejecución del proyecto
Para ejecutar el proyecto, asegúrate de tener Docker y Docker Compose instalados en tu sistema. A continuación, sigue los siguientes pasos:
1. Clona el repositorio en la carpeta deseada.
2. Normalmente las credenciales no se encuentran en el repositorio pero por el contexto se incluyen en el repositorio.
3. Abre una terminal o línea de comandos y navega hasta la ubicación donde se encuentra el archivo docker-compose.yml.
4. Ejecuta el siguiente comando para iniciar los servicios:
``docker-compose up -d
``
