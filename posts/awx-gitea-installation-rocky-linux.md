---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------

## Instalacion AWX + Gitea en RockyLinux

[link-getting-started](https://github.com/ansible/awx/blob/17.1.0/INSTALL.md#getting-started)

[link-docker-compose](https://github.com/ansible/awx/blob/17.1.0/INSTALL.md#docker-compose)

Instalacion realizada en Rocky Linux 8

```bash

   01  yum install -y epel-release
   02  yum install -y git gcc gcc-c++ nodejs gettext device-mapper-persistent-data lvm2 bzip2 python-pip yum-utils ansible python3 libselinux-python3 python36-docker
   03  yum install python2-pip python3-pip python38-pip python39-pip -y
   04  yum install python3-docker -y
   05  yum install -y yum-utils
   06  yum-config-manager     --add-repo     https://download.docker.com/linux/centos/docker-ce.repo
   07  yum install -y docker-ce
   08  systemctl enable --now docker.service
   09  pip2 install docker-compose==1.23.2
   10  cd /tmp
   11  yum install wget -y
   12  wget https://github.com/ansible/awx/archive/refs/tags/17.0.1.zip
   13  unzip 17.0.1.zip 
   14  cd /tmp/awx-17.0.1/installer
   15  ls -ls

   -rw-r--r--. 1 root root  172 ene 26  2021 build.yml
   -rw-r--r--. 1 root root  437 ene 26  2021 install.yml
   -rw-r--r--. 1 root root 7031 ago 10 09:41 inventory
   drwxr-xr-x. 7 root root   99 ene 26  2021 roles 

   16  vim inventory 
   # descomenta la linea de admin_pasword y pon contraseña 
   admin_user=admin
   admin_password=password
   
   # faltan por instalar estos requisitos
   17  yum install ansible -y
   18  yum install make -y
   19  yum install git -y
   
   # lanzamos la instalación
   20  ansible-playbook -i inventory install.yml
   
   # una acabe el playbook de ansible , si salen errores y no levantan todos los containers
   # primer revisar si se ha generado el docker-compose que crea este playbook de ansible 
   21  ls -lsa /root/.awx/awxcompose/
   
   # en mi caso el unico contenedor que no pudo levantar con el playbook fue contenedor llamado tasks
   # podemos revisar los contenedores levantados en docker
   22  docker ps -a

   # levantamos el package de docker-compose que levanta todos los contenedores , los que ya estaban
   # levantados no los levanta , pero los que no esten levantados , si los levantara
   # el contenedor tasks empieza a correr
   23  docker-compose -f docker-compose.yml up -d
   
   # revisamos de nuevo
   24  docker ps -a

   CONTAINER ID   IMAGE                COMMAND                  CREATED          STATUS          PORTS                                   NAMES
   380e1b94d06e   ansible/awx:17.0.1   "/usr/bin/tini -- /u…"   30 minutes ago   Up 30 minutes   8052/tcp                                awx_task
   5642cf8dfcf6   ansible/awx:17.0.1   "/usr/bin/tini -- /b…"   34 minutes ago   Up 34 minutes   0.0.0.0:80->8052/tcp, :::80->8052/tcp   awx_web
   e1aa45833271   postgres:12          "docker-entrypoint.s…"   34 minutes ago   Up 34 minutes   5432/tcp                                awx_postgres
   8242e1a17037   redis                "docker-entrypoint.s…"   34 minutes ago   Up 34 minutes   6379/tcp                                awx_redis

   # revisamos nuestra ip
   25  ip a

   # comprobar login en navegador puerto 80

   # si no te acuerdas del password de admin
   26  cd /tmp/awx-17.0.1/installer/
   28  grep inventory admin

```

Una vez que este levantado todo el stack , se recomienda cambiar PASSWORD admin desde el portal web.

Se puede realizar cambios en el docker-compose , para guardar los volumenes bindeados a directorios de nuestro host. Realizando cambios fichero docker-compose y levantando de nuevo contenedores.

-----------------------------------------------------------------------------

ZipyintheNet¡
