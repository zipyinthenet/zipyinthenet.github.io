---
layout: default
---
-------[Inicio/Home](./../index.html)-------[Posts-Guias-Por-Fecha-Publicación](./../posts.html)-------[Posts-Guias-Por-Categorias](./../categorias.html)-------[Links](./../links.html)-------

# ANSIBLE

-----------------------------------------------------------

# SERVIDOR ANSIBLE

## INSTALL ANSIBLE

```console
yum install ansible -y
```

-----------------------------------------------------------

# SERVIDOR ANSIBLE

## CREAR USUARIO ANSIBLE

```console
USUARIO=useransible
```

```console
useradd useransible
```

## CREAR SSH-KEY con PASSPHRASE

ssh-keygen(passphrase)

```console
ssh-keygen -b 2048 -f /home/user/.ssh/rsa_useransible -t rsa -N "newpassphrase" -C "clave for ansible"
```

## AGREGAR ALIAS BASHRC de useransible

```console
echo "alias clave_ssh_useransible='eval $(ssh-agent);ssh-add /home/useransible/.ssh/rsa_useransible'" >> /home/useransible/.bashrc
```

## COPY SSH-KEY FROM SERVIDOR ANSIBLE useransible TO HOSTS

FROM ROOT

```console
su - useransible
clave_ssh_useransible
<mete el password>
ssh-copy-id -i /home/useransible/.ssh/rsa_useransible.pub useransible@iphost
```

## FIRST SESSION AUTH

```console
ssh useransible@iphost
```

-----------------------------------------------------------

HOSTS

USUARIO=useransible

-----------------------------------------------------------

## PRIMERA PRUEBA

```console
echo "x.x.x.x nombrehost1" >> /etc/hosts
```

```console
su - useransible
mkdir -p /home/useransible/ansible
touch /home/useransible/ansible/inventory
echo "[servidores-X]" >> /home/useransible/ansible/inventory
echo "x.x.x.x" >> /home/useransible/ansible/inventory
```

```console
su - useransible
clave_ssh_useransible
<mete el password>
ansible -vvv --become-user useransible -u useransible -i inventory servidores-X -m ping
```

-----------------------------------------------------------------------------

ZipyintheNet¡
