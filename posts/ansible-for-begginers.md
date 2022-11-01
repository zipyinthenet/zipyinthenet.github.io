---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------

# ANSIBLE FOR BEGGINERS (ROOKIES)

## Ansible Documentation

[link-documentation-ansible](https://docs.ansible.com/ansible/latest/index.html)

-----------------------------------------------------------------------------

## Setting up Ansible

Ansible needs:

- ansible-controller host

- target hosts

Install ansible:

[link-install-ansible](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-fedora-or-centos)

```bash
ansible --version
```

-----------------------------------------------------------------------------

## Inventory Files

Ansible usa predeterminada mente , su fichero de inventario en /etc/ansible/hosts

Un inventario se define en formato ini:

```bash
server1.company.com
server2.company.com
```

Se pueden listar servidores , agruparlos por grupos:

```bash
[grupo1]
server1.company.com
server2.company.com
```

También se pueden añadir alias:

```bash
[grupo1]
web  server1.company.com
db   server2.company.com
mail server3.company.com
web2 server4.company.com
```

Parametros de inventario:

ansible_connection – ssh/winrm/localhost
ansible_port – 22/5986
ansible_user – root/administrator
ansible_ssh_pass – password

Como usar los parametros de inventario:

```bash
web  server1.company.com ansible_conection=ssh ansible_user=root ansible_ssh_pass=p@$$w0rd!!
db   server2.company.com ansible_conection=winrm ansible_user=admin ansible_ssh_pass=p@$$w0rd!!
mail server3.company.com ansible_conection=ssh ansible_port=56826 ansible_user=root ansible_ssh_pass=p@$$w0rd!!
web2 server4.company.com ansible_conection=winrm ansible_user=admin ansible_ssh_pass=p@$$w0rd!!
localhost ansible_conection=localhost
```

```bash
[grupo1]
web  server1.company.com ansible_conection=ssh ansible_user=root ansible_ssh_pass=p@$$w0rd!!
db   server2.company.com ansible_conection=winrm ansible_user=admin ansible_ssh_pass=p@$$w0rd!!
[grupo2]
mail server3.company.com ansible_conection=ssh ansible_port=56826 ansible_user=root ansible_ssh_pass=p@$$w0rd!!
web2 server4.company.com ansible_conection=winrm ansible_user=admin ansible_ssh_pass=p@$$w0rd!!
[grupo3]
localhost ansible_conection=localhost
```

DEMO

- Creamos inventario

```bash
cat inventory.txt
target1 ansible_host=192.168.0.122 ansible_ssh_pass=p@$$w0rd!!
```

Comprobar con modulo ping:

```bash
ansible target1 -m ping -i inventory.txt
```

- Añadimos el host2 al inventario

```bash
cat inventory.txt
target1 ansible_host=192.168.0.122 ansible_ssh_pass=p@$$w0rd!!
target2 ansible_host=192.168.0.123 ansible_ssh_pass=p@$$w0rd!!
```

Comprobar con modulo ping:

```bash
ansible target2 -m ping -i inventory.txt
```

FALLA , NO TENEMOS fingerprint de KEY HOST remoto

- Solución1:

Iniciar sesion manualmente para aceptar , la key , es lo mejor y mas habitual.

- Solución2:

NO es lo mas habitual.

```bash
vim /etc/ansible/ansible.cfg
```

Editar y descomentar --> host_key_checking

- Mejor usar SSH-KEYS (Solución1) , para no tener errores de sesión y por motivos de seguridad también es mas seguro.

-----------------------------------------------------------------------------

## Introduction to YAML

YAML , se usa para representar datos.

- Los espacios y organización de los datos , es importante en YAML con espacios necesarios.

- Dictionary vs list vs list of dictionaries

Dictionary

```bash
Banana:
  Calories: 105
  Fat: 0.3g
  Carbs: 27g
Grapes:
  Calories: 200
  Fat: 0.83g
  Carbs: 16g
```

list

```bash
Fruits:
-  Oranges
-  Apples
-  Bananas
Vegetables:
-  carrot
-  cauliflower
-  tomatoes
```

list of dictionaries

```bash
- Color: red
  model: 
    name: corvette
    model: 1995
  Price: 20.000$
- Color: grey
  model: 
    name: corvette
    model: 2000
  Price: 80.000$
```

-----------------------------------------------------------------------------

## PLAYBOOKS

Los playbooks se escriben en YAML , definicion playbook:
    - playbook is a single YAML file
        - Play , define set of activities (tasks) to be run on hosts
            - task is an action to be performed on the host
                - execute command
                - run script
                - install package
                - shutdown/restart

- ejemplo:

```bash
---
- name: Play 1
  hosts: localhost
  tasks:
    - name: Execute command ‘date’
    command: date

    - name: Execute script on server
    script: test_script.sh

    - name: Install httpd service
    yum:
     name: httpd
     state: present

    - name: Start web server
    service:
     name: httpd
     state: started
```

- ejemplo2:

```bash
---
- name: Play 1
  hosts: localhost
  tasks:
    - name: Execute command ‘date’
    command: date

    - name: Execute script on server
    script: test_script.sh

- name: Play 2
  hosts: localhost
  tasks:
    - name: Install httpd service
    yum:
     name: httpd
     state: present

    - name: Start web server
    service:
     name: httpd
     state: started
```

DEMO1 - ANSIBLE COMMANDS vs ANSIBLE-PLAYBOOK COMMANDS

ANSIBLE COMMANDS
ansible <hosts> -a <command>
ansible all -a “/sbin/reboot”
ansible <hosts> -m <module>
ansible target1 -m ping

ANSIBLE-PLAYBOOK COMMANDS
ansible-playbook <playbook name>
ansible-playbook playbook-webserver.yaml

Para comprobar que la sintaxis del playbook esta bien escrita:
[link-comprobar-sintaxis](http://www.yamllint.com/)

En caso de no tener git , podemos usar ‘remote-sync’ de gitea , en visual studio code se utiliza ‘Remote Development’

Desde el explorador remoto , podremos conectar a otras maquinas virtuales y editar los ficheros con visual studio code , remotamente.

DEMO2 - List of all modules
[list-of-all-modules](https://docs.ansible.com/ansible/2.9/modules/list_of_all_modules.html)
[Module-Copy](https://docs.ansible.com/ansible/2.9/modules/copy_module.html#copy-module)

- Creamos un fichero temporal para copiar

```bash
touch /tmp/test-file.txt
```

- creamos el playbook:

```bash
---
- name: Copy files to target servers
  hosts: all
  tasks:
    - name: Copy file
      copy:
        src: /tmp/test-file.txt
        dest: /tmp/test-file.txt
```

- Ejecución del playbook con inventario:

```bash
ansible-playbook playbook-copyfile.yaml -i inventory.txt
```

-----------------------------------------------------------------------------

## Modules

Los módulos son acciones a realizarse y pueden clasificarse en:

- System , se encuentran módulos para gestionar cosas del sistema , como usuarios , grupos , instalar paquetes..

- Commands , se encuentran módulos para ejecutar comandos simples , o scripts.

- Files, se encuentran módulos por ejemplo para buscar lineas en ficheros , copiar ..etc.

- Database , se encuentran módulos para interactuar con bases de datos como mongodb , mysql..etc.

- Cloud, se encuentran módulos para muchos clouds providers , para realizar tareas diversas.

- Windows, se encuentran módulos para gestionar windows hosts , por ejemplo copiar , command para ejecutar comandos..etc.

- Otros...

### Ejemplo command Module(command modules)

```bash
---
- name: Play 1
  hosts: localhost
  tasks:
   - name: Execute command ‘date’
     command: date

   - name: Display resolv.conf contents
     command: cat /etc/ resolv.conf

   - name: Display resolv.conf contents
     command: cat resolv.confchdir =/etc

   - name: Display resolv.conf contents
     command: mkdir/folder creates=/folder

   - name: Copy file from source to destination
     copy: src=/source_file dest=/destination
```

### Ejemplo script Module(command modules)

```bash
---
- name: Play 1
  hosts: localhost
  tasks:
   - name: Run a script on remote server
     script: /some/local/script.sh -arg1 -arg2
```

### Ejemplo service Module(system modules)

```bash
---
- name: Start Services in order
  hosts: localhost
  tasks:
   - name: Start the database service
     service: name= postgresql state=started

   - name: Start the httpd service
     service: name=httpd state=started

   - name: Start the nginx service
     service:
       name: nginx
       state: started
```

```bash
---
- name: Start Services in order
  hosts: localhost
  tasks:
   - name: Start the database service
     service:
      name: postgresql
      state: started
```

### Ejemplo lineinfile Module(files modules)

- script.sh:

```bash
#Sample script
echo “nameserver 10.1.250.10” >> /etc/resolv.conf
```

- playbook:

```bash
---
- name: Add DNS server to resolv.conf
  hosts: localhost
  tasks:
   - lineinfile:
        path: /etc/resolv.conf
        line: 'nameserver 10.1.250.10'
```

-----------------------------------------------------------------------------

## Variables

Las variables sirven para guardar datos y usarlos.
Para usar variables , podemos declara variables en playbooks y usarlas en alguna tasks , las variables para usarlas , se declaran con ‘{{}}’ , ejemplo:

```bash
---
- name: Add DNS server to resolv.conf
  hosts: localhost
  vars:
    dns_server : 10.1.250.10
  tasks:
      - lineinfile:
          path: /etc/resolv.conf
          line: 'nameserver {{ dns_server }}'
```

También , podemos usar ficheros que solo contengan variables:

```bash
#Sample variable File
variable1: value1
variable2: value2
```

Ejemplo ficheros variables:

```bash
---
- name: Set Firewall Configurations
  hosts: web
  tasks:
  - firewalld :
      service: https
      permanent: true
      state: enabled

  - firewalld :
      port: '{{ http_port }}'/tcp
      permanent: true
      state: disabled

  - firewalld :
      port: '{{ snmp_port }}'/udp
      permanent: true
      state: disabled

  - firewalld :
      source: '{{ inter_ip_range }}'/24
      Zone: internal
      state: enabled
```

```bash
#Sample Inventory File
Web http_port= snmp_port= inter_ip_range=
```

```bash
#Sample variable File - web.yml
http_port: 8081
snmp_port: 161-162
inter_ip_range: 192.0.2.0
```

-----------------------------------------------------------------------------

## Conditionals

Ejemplo uso condiciones en playbook.
Tenemos 2 playbooks , los cuales usan 2 modulos distintos para instalar paquetes, en este caso nginx , en una maquina debian y otra redhat.

```bash
---
- name: Install NGINX
  hosts: debian_hosts
  tasks:
  - name: Install NGINX on Debian
    apt:
      name: nginx
      state: present
```

```bash
---
- name: Install NGINX
  hosts: redhat_hosts
  tasks:
  - name: Install NGINX on Redhat
    yum:
      name: nginx
      state: present
```

### Condicional when

Podemos usar el condicional ‘when’ para que solo se ejecute en maquinas cuando sea cierto , cuando el sistema operativo sea debian o redhat en todas las maquinas.
Ansible_os_family , es una variable interna de ansible que obtiene la familia de os.

```bash
---
- name: Install NGINX
  hosts:
  tasks:
  - name: Install NGINX on Debian
    apt:
      name: nginx
      state: present
    when: ansible_os_family == 'Debian'

  - name: Install NGINX on Redhat
    yum:
      name: nginx
      state: present
    when: ansible_os_family == 'RedHat'
```

### Operador or

Podemos usar tambien , la condición ‘or’.
En este caso se instalar el paquete cuando sea redhat o suse:

```bash
---
- name: Install NGINX
  hosts:
  tasks:
  - name: Install NGINX on Debian
    apt:
      name: nginx
      state: present
    when: ansible_os_family == 'Debian'

  - name: Install NGINX on Redhat
    yum:
      name: nginx
      state: present
    when: ansible_os_family == 'RedHat' or
          ansible_os_family == 'SUSE'
```

### Operador and

Otro operador es ‘and’ , podemos usar ‘and’ , cuando queremos que se cumplan 2 condiciones para ejecutar lo deseado. Por ejemplo , solo cuando sea debian y tambien sea 16.04 , solo se ejecutara en ese caso:

```bash
---
- name: Install NGINX
  hosts:
  tasks:
  - name: Install NGINX on Debian
    apt:
      name: nginx
      state: present
    when: ansible_os_family == 'Debian'  and
          ansible_distribution_version == '16.04'

  - name: Install NGINX on Redhat
    yum:
      name: nginx
      state: present
    when: ansible_os_family == 'RedHat' or
          ansible_os_family == 'SUSE'
```

### Condicionales con loops

Es posible usar condicionales con loops , por ejemplo , solo se instalaran aquellos que esten en ‘true’:

Tambien podemos añadir un condicional when a la tarea tasks , para que solo se ejecute cuando sea true, en loop.

```bash
---
- name: Install Softwares
  hosts:
  vars:
     packages:
        - name: nginx
          required: True
        - name: mysql
          required: True
        - name: apache
          required: False
  tasks:
  - name: Install "{{ item.name }}" on Debian
    apt:
      name: "{{ item.name }}"
      state: present

    when: item.required == True

    loop: "{{ packages }}"
```

### Condicionales y registros

Revisa el estado del servicio , guarda en ‘register’ una variable llamada ‘result’ con el estado de la tarea(salida del comando se guarda en result) , y enviá email si esta caído(si hace un find de down y NO obtiene -1 , es por que esta caido y down si que lo ha encontrado , de otra forma , si encuentra down , entonces notifica , en caso de no encontrar down , entonces el resultado es -1).

```bash
---
- name: Check status of a service and email if its down
  hosts: localhost
  tasks:
    - command: service httpd status
      register: result

    - mail:
       to: admin@company.com
       subject: Service Alert
       body: Httpd Service is down

       when: result.stdout.find('down') != -1
```

-----------------------------------------------------------------------------

## Loops

Los loops sirven para repetir tareas.
Por ejemplo si tenemos que crear usuarios con el modulo user , podemos correr muchas veces el mismo modulo:

```bash
---
- name: Create users
  hosts: localhost
  tasks:
   - user: name= " { { item } } " state=present
   - user: name=george state=present
   - user: name=ravi state=present
   - user: name=mani state=present
   - user: name=kiran state=present
   - user: name=jazlan state=present
   - user: name=emaan state=present
   - user: name=mazin state=present
   - user: name=izaan state=present
   - user: name=mike state=present
   - user: name=menaal state=present
   - user: name=shoeb state=present
   - user: name=rani state=present
```

También , podemos organizar de otra manera , repitiendo la tarea con un ‘loop’(la ejecución se podria visualizar tarea derecha):

```bash
---
- name: Create users
  hosts: localhost
  tasks:
   - user: name= " { { item } } " state=present
     loop:
       - joe
       - george
       - ravi
       - mani
       - kiran
       - jazlan
       - emaan
       - mazin
       - izaan
       - mike
       - menaal
       - shoeb
       - rani
```

```bash
---
- name: Create users
  hosts: localhost
  tasks:

  - var: item=joe
    user: name= “{{ item }}” state=present
  - var: item=george
    user: name= “{{ item }}” state=present
  - var: item=ravi
    user: name= “{{ item }}” state=present
  - var: item=mani
    user: name= “{{ item }}” state=present
  - var: item=kiran
    user: name= “{{ item }}” state=present
  - var: item=jazlan
    user: name= “{{ item }}” state=present
  - var: item=emaan
    user: name= “{{ item }}” state=present
  - var: item=mazin
    user: name= “{{ item }}” state=present
  - var: item=izaan
    user: name= “{{ item }}” state=present
```

En caso de querer pasar 2 valores , se podrían pasar de la siguiente forma(derecha forma visual):

```bash
---
- name: Create users
  hosts: localhost
  tasks:
   - user: name=‘{{ item.name }}’ state=present uid='{{item.uid}}'
     loop:
       - name: joe    - { name: joe, uid: 1010 }
         uid: 1010
       - name: george - { name: george, uid: 1011 }
         uid: 1011
       - name: ravi   - { name: ravi, uid: 1012 }
         uid: 1012
       - name: mani   - { name: mani, uid: 1013 }
         uid: 1013
       - name: kiran  - { name: kiran, uid: 1014 }
         uid: 1014
       - name: jazlan - { name: jazlan, uid: 1015 }
         uid: 1015
       - name: emaan  - { name: emaan, uid: 1016 }
         uid: 1016
       - name: mazin  - { name: mazin, uid: 1017 }
         uid: 1017
       - name: izaan  - { name: izaan, uid: 1018 }
         uid: 1018
       - name: mike   - { name: mike, uid: 1019 }
         uid: 1019
```

Antes de existir ‘loops’ , se usaba ‘with_*’.
Ejemplo:

```bash
---
- name: Create users
  hosts: localhost
  tasks:
   - user: name='{{ item }}' state=present
     with_items:
       - joe
       - george
       - ravi
       - mani
```

```bash
---
- name: Create users
  hosts: localhost
  tasks:
   - user: name='{{ item }}' state=present
     loop:
       - joe
       - george
       - ravi
       - mani
```

Ejemplos:

```bash
---
- name: Create users
  hosts: localhost
  tasks:
   - user: name='{{ item }}' state=present
     with_items:
       - joe
       - george
       - ravi
       - mani
```

```bash
---
- name: View Config FIles
  hosts: localhost
  tasks:
   - debug: var=item
     with_file:
       - "/etc/hosts"
       - "/etc/resolv.conf"
       - "/etc/ntp.conf"
```

```bash
---
- name: Get from multiple URLs
  hosts: localhost
  tasks:
   - debug: var=item
     with_url:
       - "https://site1.com/get-servers"
       - "https://site2.com/get-servers"
       - "https://site3.com/get-servers""
```

```bash
---
- name: Check multiple mongodbs
  hosts: localhost
  tasks:
   - debug: msg="DB={{ item.database }} PID={{ item.pid }}"
     with_mongodb:
       - database: dev
         connection_string: "mongodb://dev.mongo/"
       - database: prod
         connection_string: "mongodb://prod.mongo/"
```

Otros plugins para usar con ‘with_*’:

```bash
with_items
with_file
with_url
with_mongodb

with_dict
with_etcd
with_env
with_filetree
With_ini
With_inventory_hostnames
With_k8s
With_manifold
With_nested
With_nios
With_openshift
With_password
With_pipe
With_rabbitmq

With_redis
With_sequence
With_skydive
With_subelements
With_template
With_together
With_varnames
```



-----------------------------------------------------------------------------

## Roles

Roles en ansible.
En automatización , un rol significa hacer todo lo que es necesario para cumplir las tareas de ese rol.
Por ejemplo , cumplir un rol de base de datos , seria instalar y configurar toda una base de datos.
Tareas muy comunes , se puede crear un playbook:

bash```
---
- name: Install and Configure MySQL
  hosts: db-server
  tasks:
     - name: Install Pre-Requisites
       yum: name=pre-req-packages state=present

     - name: Install MySQL Packages
       yum: name=mysql state=present

     - name: Start MySQL Service
       service: name=mysql state=started

     - name: Configure Database
       mysql_db: name=db1 state=present
```

El playbook que hemos creado , se puede usar para instalar tareas de ese mismo playbook.

De forma que , un playbook , lo usamos como rol , en otro playbook para hacer esas tareas:

bash```
---
- name: Install and Configure MySQL
  hosts: db-server1...db-servretr100
  roles:
      - mysql
```

-----------------------------------------------------------------------------

## Advanced topics

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

ZipyintheNet¡
