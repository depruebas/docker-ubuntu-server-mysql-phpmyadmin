
<img width="514" height="256" alt="image" src="https://github.com/user-attachments/assets/f1eb36ff-4b6c-49a6-94b6-29555a0c58c5" />


### In English below


## ⚙️ Instrucciones de uso:
>
>
>Para utilizar este entorno, clonar el repo:
>
>`git clone https://github.com/depruebas/docker-ubuntu-server-mysql-phpmyadmin.git`
>
>Entar en el directorio y ejecutar
>
>`make all` (mas abajo las instruccion del makefile) pero este comando construira por primera vez el docker y lo activara.
>
>`make shell` para entrar en la shell de ubuntu server
>
>`localhost:8889` para acceder al phpMyAdmin y root / root para usuario y password del MySql
>
>Si ya teneis un puerto 8889 con algún servicio lo podeis cambiar en del docker-compose.yml
>




## Esquema de directorios y archivos
 
docker:  directorio donde estan los ficheros de configuración del entorno

   - user_data: directorio del usuario /home/ubuntu donde se guarda la configuración. Solo se crea cuando se crea la imagen del contenedor, después los ficheros de configuración son persistentes
     - apache-vhost.conf, virtuahost de apache para phpMyAdmin. Si quieres mas web puedes añadir aqui los ficheros virtualhosts que necesites
       
   - provision: directorio donde estan los ficheros de configuración del servidor.
     - entrypoint.sh, se ejecuta al realizar un build de la imagen, configura apache2, MySql y phpMyAdmin
   

temp: directorio temporal para traspasar cosas al contenedor, podria ser el directorio donde esta el proyeto web. Este directorio temp se crea dentro del directorio /data en el contenedo, lo he creado para ir enlazando todos los directorios de nuesto hosts que necesitemos, por ejemplo, los del código.

Makefile: fichero para ejecutar comandos docker.


El fichero Makefile es el que utilizaremos para enceder, parar y reconstruir el contenedor.



## Iniciar proyecto

Para iniciar el proyecto ejecutar `make all` desde el directorio raiz, todos los comandos make se lanzan desde el diretorio raiz donde esta el fichero Makefile.

`make all` lo que hara es crear y construir el contenedor.




## Comandos `make`

Construir el contenedor

`make build`

Iniciar el contenedor

`make all`

Parar el contenedor

`make stop`

Parar y eliminar el contenedor

`make down`

Entrar en el shell del contenedor

`make shell`



<br><br>

### English version

⚙️ ## Instructions for use:
>
>
>To use this environment, clone the repository:
>
>`git clone https://github.com/depruebas/docker-ubuntu-server-mysql-phpmyadmin.git`
>
>Navigate to the directory and run:
>
>`make all` (see below for the makefile instructions), but this command will build Docker for the first time and activate it.
>
>`make shell` to enter the Ubuntu Server shell.
>
>`localhost:8889` to access phpMyAdmin and root /root for the MySQL username and password.
>
>If you already have port 8889 configured for another service, you can change it in the docker-compose.yml file.
>


## Directory and file scheme

docker: directory where the environment configuration files are located

   - user_data: user's /home/ubuntu directory where the configuration is stored. It is only created when the container image is created; after that, the configuration files are persistent.
     - apache-vhost.conf: Apache virtual host for phpMyAdmin. If you want to add more websites, you can add the necessary virtual host files here.

  - provision: directory where the server configuration files are located.
  
    - entrypoint.sh: runs when building the image; it configures Apache2, MySQL, and phpMyAdmin.

temp: temporary directory for transferring files to the container.

Makefile: file for executing Docker commands. The Makefile is the file we will use to start, stop, and rebuild the container.



## Starting the Project

To start the project, run `make all` from the root directory. All `make` commands are launched from the root directory where the Makefile is located.

`make all` will create and build the container.


## `make` Commands


Build the container

`make build`

Start the container

`make all`

Stop the container

`make stop`

Stop and remove the container

`make down`

Enter the container shell

`make shell`

