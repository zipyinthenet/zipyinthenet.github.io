---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------

# ANSIBLE FOR BEGGINERS (ROOKIES)

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
-
  name: Copy files to target servers
  hosts: all
  tasks:
    - name: Copy file
      copy:
        src: /tmp/test-file.txt
        dest: /tmp/test-file.txt
```

```bash
ansible-playbook playbook-copyfile.yaml -i inventory.txt
```

-----------------------------------------------------------------------------

## Modules



-----------------------------------------------------------------------------

## Variables

-----------------------------------------------------------------------------

## Conditionals

-----------------------------------------------------------------------------

## Loops

-----------------------------------------------------------------------------

## Roles

-----------------------------------------------------------------------------

## Advanced topics

-----------------------------------------------------------------------------

-----------------------------------------------------------------------------

ZipyintheNet¡
