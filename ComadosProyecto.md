# Comandos del proyecto
## Servidor pricipal
### Instalar un entorno gráfico ligero (XFCE)
`apt-get install lightdm xfce4 xfce4-goodies` Para instalar XFCE y demás paquetes

`sudo nano /etc/lightdm/lightdm.conf` Para crear un folder llamado lightdm.conf en /etc/lightdm

`systemctl reboot` reinicia el sistema.

Para dejar de usar la interfaz:
```
systemctl set-default multi-user.target
systemctl reboot
```

`systemctl isolate graphical.target` Para cambiar de interfaz a consola

### Instalar VNC

`$ sudo apt-get install --no-install-recommends ubuntu-desktop gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal gnome-core` Instala todo los paquetes de Gnome debido a que ayuda VNC a funcionar adecuadamente. 

```
sudo apt-get install --no-install-recommends ubuntu- desktop gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal gnome-core 
```
`sudo apt install tightvncserver` Instala los paquetes de VNC.

`$vncserver` Para configurar la contraseña de acceso y ver configuración
```
vncserver
```

Parámetros de escritorio: 
:1 - usa el puerto 5091
:2 - usa el puerto 5092
:3 - usa el puerto 5093

`vncpasswd` cambia contraseña de acceso

### Configurar el VNC

`vncserver -kill` detiene el servicio actual
```
- vncserver -Kill :2 Killing Xtightvnc process ID 8423
```

`nano ~/.vnc/xstartup`Crea un documento en la ruta establecida.

Se deberán añadir las siguientes líneas:
`#!/bin/bash`
`xrdb $HOME/.Xresources`
`startxfce4 & Ctrl + x `
para cerrar el documento y Y para guardarlo.

`VNCserver -localhost` reinicia el servidor

` ssh -L 59000:localhost:5901 -C -N -l user your_server_ip` Para conectarse al servidor

Se debe cambiar la siguiente información para el comando anterior.
`59000` es el puerto de salido de la máquina
`5901` el puerto a utilizar.
`user` el usuario con el que se iniciará session
`your_server_ip`  la ip del servidor VNC. 
`sudo apt-get install xtightvncviewer` Instalar cliente VCN para hacer la conexión
`vcnserver` para iniciar una nueva sesión en el servidor
`vncviewer [clear-linux-host-ip-address]:[fully-qualified VNC port  number]` para establecer la conexión.

### Probando el servidor VCN
```
Vcnviewer 192.168.8.34
```
### Instalar Firewall

`sudo apt install ufw` Instala los paquetes del firewall

Configurar políticas default:
`sudo ufw default deny incoming`
`sudo ufw default allow outgoing`
`sudo ufw allow port number` permite la el trafica del protocolo especificado(sudo ufw allow 22). También se pueden hacer en rangos como se muestra a continuación.

```
sudo ufw allow 5900: 5903\udp rules updated 
```
`sudo ufw deny` Deshabilita el puerto 
`sudo ufw enable` Habilita el funcionamiento del firewall 

### Instalación de Webmin

`sudo apt install wget apt-transport-https software-properties-common`  Instala los paquetes necesarios para la instalación
```
sudo apt install software-properties-common apt-transpot-https
```
`sudo wget -q http://www.webmin.com/jcameron-key.asc -O- | sudo apt-key add -`  añade el repositorio para la descarga de los paquetes de Webmin
```
sudo wget -q http:\\ www. wedmin.com \jcameron- key. asc -o- | sudo apt-key add- OK
```
`sudo apt install webmin`  Instalar webmin

```
sudo apt install webmin
```

`sudo systemctl status webmin` Verifica el estado del servidor

```
sudo systemctl statis webmin 
```

### Servidor FTP

`sudo apt-get install vsftpd` Instala los paquetes necesarios
```
sudo apt-get install vsftpd 
```

`sudo nano /etc/vsftpd.conf` Se edita el siguiente archivo y de se comentan las siguientes líneas
```
processing triggers for system (245.4-4ubuntu3.11)...
```
Líneas a descomentar

`write_enable=YES`
`local_umask=022`
`chroot_local_user=YES`

Líneas a añadir
`allow_writeable_chroot=YES`
`pasv_enable=Yes`
`pasv_min_port=40000`
`pasv_max_port=40100`

`sudo service vsftpd restart` Seguido a esto, se reinicia el servidor con el siguiente comando

Mediante la edición del archivo `sudo nano /etc/shells` se indica que el usuario tiene permitido conectarse.  

Para se escribe `/usr/sbin/nologin`  en el archivo.

```
\bin\sh
\bin\bash
\usr\bin\bash
\bin\rbash
\usr\bin\rbash
\bin\dash
\usr\bin\dash 
\usr\bin\tmux
\usr\bin\screen
\usr\sbin\nolongin 
```

Para habilitar que el servicio se inicie con la máquina se usan los siguientes comandos.
`systemctl start vsftpd`

`systemctl enable vsftpd`

`adduser vsftp` Crea usuario para el servidor
`mkdir /home/vsftp/ftp` Para hacer el directorio
 ```
 
 sudo mkdir \home\ vsftp\ftp\marcec639\
 ```
 
 `chown [propietario/grupo propietario] [nombre del archivo]` Para cambiar el propietario 
```
sudo chown -R 755 \home\vsftp\ftp\jchavarriac400\
```

`chown -R 755 /etc/misarchivos` cambia los permisos del directorio y subdirectorios. Solo el propietario puede leer y escribir en este directorio.
```
sudo chown -R 755 \home\vsftp\ftp\jchavarriac400\
```

`sudo addgroup groupname` crea un nuevo grupo de usuarios
`sudo adduser username groupname` añade un usuario al grupo. 
```
sudo addgroup invitados adding group invitados (GID 1007)...
```
Conectarse al servidor


### Servidor LAMP
`sudo apt install apache2` Instala los paquete necesarios
```
sudo apt install apache2
```

Buscar la dirección IP del servidor en buscador para verificar instalación.
Instala los paquetes de MySQL y se corre el código para terminar de configurar parámetros de seguridad de la instalación.
`sudo apt install mysql-server`
`sudo mysql_secure_installation`

### Probando MySQL:
`Sudo mysql`
```
sudo mysql
```
`sudo systemctl start mysql`  Hace que MySQL se ejecute al iniciar la maquina.
```
sudo systemctl start mysql 
```
### Instalando PHP 
`sudo apt install php libapache2-mod-php php-mysql`  Instalalos paquetes necesrios de PHP.
```
php -v 
```
### Instalando MariaDB
`sudo apt install mariadb-server` instala los paquetes necesarios.

### Wordpress
`wget -c http://wordpress.org/latest.tar.gz` Descarga los paquetes necesarios para utilizar wordpress.

`tar -xzvf latest.tar.gz` extrae los paquetes necesarios.

`sudo mv wordpress/* /var/www/html/` Mueve los paquetes extraidos a la carpeta del servidor de apache. 

Cambia lo permisos de la caprte del servidor de apache.
`sudo chown -R www-data:www-data /var/www/html/`
`sudo chmod -R 755 /var/www/html/`
`sudo mysql -u root -p` Entra en el portal de configuacion de MySQL.

Se escribe los sigueinte para crear la base de datos.
`mysql> CREATE DATABASE wp_myblog;`
`mysql> CREATE USER 'username'@'%' IDENTIFIED WITH`
`mysql_native_password BY 'password';`
`mysql> GRANT ALL ON wp_myblog.* TO 'username'@'%';`
`mysql> FLUSH PRIVILEGES;`
`mysql> EXIT;`

Se cambia el nombre de algunos de los archivos para hacer en cambio de los parametrso de las configuracion del servidor de apache. 
`cd /var/www/html/`
`sudo mv wp-config-sample.php wp-config.php`
`sudo rm -rf index.html`

Se reinicia los servios para aplicar los cambios
`$ sudo systemctl restart apache2.service`
`$ sudo systemctl restart mysql.service`


### Conectado el servidor principal a VPN
`sudo apt install openvpn openvpn-systemd-resolved` Instalar el VPN
```
sudo apt install openvpn openvpn-systemd-resolved 
```

### Servicio Proxy
`sudo apt-get install squid3` Instalar paquetes del servicio de proxy. 
```
sufo apt-get install squid3
```






















































