## Diseño de Sistemas Informáticos
## Informe Práctica 1: Configuración de máquina virtual en el IaaS

En la realización de esta práctica se lleva a cabo la configuración de la máquina virtual disponible a través del **servicio IaaS de la ULL**, así como la instalación y configuración de todas las herramientas necesarias para comenzar a trabajar en la asignatura. Para ello, se recomienda el uso de material de apoyo como el guión disponible en el campus para el desarrollo de esta práctica:
* [Guión de la práctica](https://ull-esit-inf-dsi-2021.github.io/prct01-iaas)

Además, la realización de este informe a modo de GitHub Page mediante el empleo de **Markdown**. Con este fin, he consultado información en los siguientes enlaces que me han sido de interés para aprender a manejar estos conceptos:
* [Acerca de GitHub Pages](https://docs.github.com/en/github/working-with-github-pages)
* [Guía sobre Markdown](https://guides.github.com/features/mastering-markdown)


### --> Primeros pasos

Antes de nada, debemos ser capaces de conectarnos a la **red de la ULL** para poder trabajar de forma remota. Para lograrlo, debemos ir hasta la página del [Servicio de VPN de la ULL](https://www.ull.es/servicios/stic/2020/12/01/servicio-de-vpn-de-la-ull) donde encontraremos unos documentos en formato pdf que nos explicarán como establecer conexión desde los distintos sistemas operativos. En mi caso, trabajaré con Windows 10, por lo que precisaré de la instalación del GlobalProtect (véase páginas 4-6 de este [documento](https://drive.google.com/file/d/1yviLlpLFT5p0e8lXXzOQjdFYL74y5lyE/view)).

Una vez instalado, debe de poder iniciarse sesión empleando nuestro identificador y contraseña como se aprecia en la siguiente imagen:
* [Inicio de sesión](https://drive.google.com/file/d/1eFySvjDCwhkFPtZKLdo-WD8k9Ye5s7K-/view?usp=sharing)

Si todo ha salido correctamente, cuando vayamos a GlobalProtect nos debe indicar que estamos conectados:
* [Conectado](https://drive.google.com/file/d/10sw4DMZl2gRvbJaYVgMKHq7XIlDA--zU/view?usp=sharing)

Una vez tengamos acceso a la red, podremos entrar al [IaaS](https://iaas.ull.es) y una vez ahí introducir nuestras credenciales. A continuación, se nos despliega un menú con las distintas máquinas que tenemos asignadas, en nuestro caso, nos centraremos en la máquina identificada por **DSI**, si es la primera vez que la arrancamos, deberemos hacerlo, y se nos asignará una de entre todas las disponibles. Sabremos que estará operativa cuando apreciemos en su nombre un número fijo _DSI-XX_. En las siguientes líneas hasta terminar el informe, mi máquina tendrá el nombre de _DSI-30_.

### --> Configuración de la MV del IaaS

Tras haber terminado con los pasos anteriores, podemos coemnzar con la **configuración de nuestra máquina virtual** (en adelante MV). Tras lo realizado en el apartado anterior, ahora debemos pinchar sobre el nombre de la MV, y nos saldrá una descripción de ella. Uno de los apartados es `Dirección IP`, que nos indicará la IP asignada a nuestra máquina de la forma `10.6.XXX.XXX`, con esta información podremos acceder a ella de forma remota por ***ssh***. 
Yo tengo una terminal en WSL, y para conectarme a mi máquina debo escribir en la terminal **ssh usuario@IP_de_mi_MV** de la siguiente manera:
```
ssh usuario@10.6.129.123
```
Una vez hecho eso nos saldrá un texto como el siguiente:
```
The authenticity of host '10.6.129.123 (10.6.129.123)' can't be established.
ECDSA key fingerprint is SHA256:PtBmnNTY7PGFZ4JIColNvGzFCVZVgToYxL35aKx4HZs.
Are you sure you want to continue connecting (yes/no)?
```
Introducimos `yes` y pasamos a la siguiente pregunta, nos pedirá una contraseña, esta por defecto es `usuario`, al igual que el nombre de usuario. Una vez hecho esto, el sistema nos pedirá que establezcamos una nueva contraseña. Tendremos que poner primeramente la contraseña actual, y luego la nueva dos veces para confirmarla.

A continuación vamos a modificar el nombre de nuestra MV, pasará de llamarse **_ubuntu_** a **_DSI-30_**:
```
usuario@ubuntu:~$ cat /etc/hostname
ubuntu
usuario@ubuntu:~$ sudo vim /etc/hostname
usuario@ubuntu:~$ cat /etc/hostname
DSI-30
```
Ahora cambiaremos el nombre de nuestro host:
```
usuario@ubuntu:~$ cat /etc/hosts
127.0.0.1	localhost
127.0.1.1	ubuntu
... 
```
Pasará de llamarse **_ubuntu_** a **_DSI-30_** quedando de la siguiente forma:
```
usuario@ubuntu:~$ vim /etc/hosts
usuario@ubuntu:~$ cat /etc/hosts
127.0.0.1       localhost
127.0.1.1       DSI-30

# The following lines are desirable for IPv6 capable hosts
::1     localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```
Finalmente, antes de reiniciar nuestra MV para que se apliquen los cambio, tenemos que actualizar el software de nuestra máquina:
```
usuario@ubuntu:~$ sudo apt update
...
usuario@ubuntu:~$ sudo apt upgrade
...
```
En caso de tener algún problema al emplear estos comandos como en mi caso, puede probar a usar `sudo apt-get update` y `sudo apt-get upgrade`.
Para terminar reiniciaremos nuestra MV:
```
usuario@ubuntu:~$ sudo reboot
Connection to 10.6.129.123 closed by remote host.
Connection to 10.6.129.123 closed.
```

Para mayor comodidad, mientras nuestra máquina se reinicia, podemos  editar nuestro fichero de hosts de la máquina local para incluir información de conexión a la máquina virtual. De ese modo, no tendremos que recordar la IP de la máquina virtual:
```
saul@DESKTOP-F06QRH9:~$ cat /etc/hosts
# This file was automatically generated by WSL. To stop automatic generation of this file, add the following entry to /etc/wsl.conf:
# [network]
# generateHosts = false
127.0.0.1       localhost
127.0.1.1       DESKTOP-F06QRH9.localdomain     DESKTOP-F06QRH9

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters

saul@DESKTOP-F06QRH9:~$ vim /etc/hosts
saul@DESKTOP-F06QRH9:~$ cat /etc/hosts
# This file was automatically generated by WSL. To stop automatic generation of this file, add the following entry to /etc/wsl.conf:
# [network]
# generateHosts = false
127.0.0.1       localhost
127.0.1.1       DESKTOP-F06QRH9.localdomain     DESKTOP-F06QRH9
10.6.129.123    DSI-30

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```
Esto nos permitirá entrar usando `ssh usuario@DSI-30`.
Ahora toca configurar, en la máquina local, la infraestructura de clave pública-privada (si lo tiene hecho, puede pasar al siguiente párrafo), si es que no lo había hecho anteriormente, para ello debemos generar una clave pública con `ssh-keygen` y pulsaremos `enter` a todas las opciones que nos aparezcan, creando así la clave. Es importante es no introducir ninguna passphrase asociada al par de claves pública-privada.
Una vez hecho esto, podemos copiar esta clave haciéndola visible en nuestra terminal con el comando `cat` de la siguiente manera

```
saul@DESKTOP-F06QRH9:~$ cat .ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDo5iXL/ixeWnvoBfnmIjEgSFpSTTNHPzm9NxwvJK/UNnDkQ0vPe4P3v7BNiOnc2RlA8ZZHWCUwsizm5b9HUZoRPiX1B+HdN+FlYHCi2wEqNSfXEI5HJGyZloY6zVqLUqbrVoCimcUykHxdS5TcvXyr858fOHuSwM6oGlZCKB84uREQts7hnUPWJ2b98iH7GVPQy9YidpCd8gFtOfvNIYUYZBIJt+uHqJgqwd+OUaHSq+nfjj5HGnoPWeOdMbgomY1v+6pJtHpD1g3Vuk6g72bWKqZh4gEDzuc+fGlREluKvx2gNGVHGv970BTorYmNphSE4Mp4qvYMPE1h27RX190b saul@DESKTOP-F06QRH9
```
Una vez generadas las claves, ejecutaremos el siguiente comando, lo que nos permitirá copiar la clave pública desde la máquina local a la máquina virtual:
```
saul@DESKTOP-F06QRH9:~$ ssh-copy-id usuario@DSI-30
The authenticity of host 'DSI-30 (10.6.129.123)' can't be established.
ECDSA key fingerprint is SHA256:PtBmnNTY7PGFZ4JIColNvGzFCVZVgToYxL35aKx4HZs.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
usuario@dsi-30's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'usuario@dsi-30'"
and check to make sure that only the key(s) you wanted were added.
```
Si todo ha ido bien podremos iniciar sesión en nuestra MV de la siguiente manera:
```
saul@DESKTOP-F06QRH9:~$ ssh usuario@iaas-dsi2
Welcome to Ubuntu 18.04.5 LTS (GNU/Linux 4.15.0-135-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Thu Feb 18 17:18:28 WET 2021

  System load:  0.09              Processes:           96
  Usage of /:   35.7% of 8.17GB   Users logged in:     0
  Memory usage: 7%                IP address for ens3: 10.6.129.123
  Swap usage:   0%

 * Introducing self-healing high availability clusters in MicroK8s.
   Simple, hardened, Kubernetes for production, from RaspberryPi to DC.

     https://microk8s.io/high-availability

 * Canonical Livepatch is available for installation.
   - Reduce system reboots and improve kernel security. Activate at:
     https://ubuntu.com/livepatch

Pueden actualizarse 0 paquetes.
0 of these updates are security updates.


Last login: Tue Feb 16 16:46:53 2021 from 10.20.52.231
```

Hemos sido capaces de acceder a nuestra MV sin necesidad de contraseña, también podemos cambiar el prompt para no tener que usar `usuario` a la hora de iniciar sesión por la conexión ssh de la siguiente manera:
```
saul@DESKTOP-F06QRH9:~$ cat ~/.ssh/config
Host DSI-30
  HostName DSI-30
  User usuario
```
Ahora podemos establecer la conexión solo con el nombre de nuestra máquina `ssh DSI-30`.

Para terminar con la configuración, debemos generar las claves pública-privada en nuestra MV, siguiendo los pasos empleados anteriormente en la máquina local:
```
usuario@dsi-30:~$ ssh-keygen 
Generating public/private rsa key pair.
Enter file in which to save the key (/home/usuario/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/usuario/.ssh/id_rsa.
Your public key has been saved in /home/usuario/.ssh/id_rsa.pub.
The key fingerprint is:
...

usuario@dsi-30:~$ cat .ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDo5iXL/ixeWnvoBfnmIjEgSFpSTTNHPzm9NxwvJK/UNnDkQ0vPe4P3v7BNiOnc2RlA8ZZHWCUwsizm5b9HUZoRPiX1B+HdN+FlYHCi2wEqNSfXEI5HJGyZloY6zVqLUqbrVoCimcUykHxdS5TcvXyr858fOHuSwM6oGlZCKB84uREQts7hnUPWJ2b98iH7GVPQy9YidpCd8gFtOfvNIYUYZBIJt+uHqJgqwd+OUaHSq+nfjj5HGnoPWeOdMbgomY1v+6pJtHpD1g3Vuk6g72bWKqZh4gEDzuc+fGlREluKvx2gNGVHGv970BTorYmNphSE4Mp4qvYMPE1h27RX190b saul@DESKTOP-F06QRH9
```

### --> Instalación de git y Node.js en la Máquina Virtual del IaaS


### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-github-campus-experts-ostream07/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
