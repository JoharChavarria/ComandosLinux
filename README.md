# ComandosLinux
[Comandos del Proyecto](https://github.com/JoharChavarria/ComandosLinux/blob/main/ComadosProyecto.md)

[Comandos Docker](https://github.com/JoharChavarria/ComandosLinux/blob/main/comandosDocker.md)

## Usuario Root
`sudo su –` Habilita los permisos de usuario root.
```
sudo su - 
```


## Crear Usuarios
`sudo sueradd -m usuarionuevo` Crea un nuevo usuario y al utilizar el parámetro `-m` permite que se creen las carpetas de usuario de manera automática. 
```
subo useradd -m marcec639
```

`sudo passwd usuarionuevo` Establece una contraseña para el usuario
```
subo passwd marcec639 
````



## Actualizar todos los paquetes 
`subo apt update` Actualiza todos los paquetes 
```
subo apt update 
```



## Memoria y Almacenamiento 
`for file in /proc/*/status ; do awk '/VmSwap|Name/{printf $2 " " $3}END{ print ""}' $file; done | sort -k 2 -n -r | lesser` Ver la memoria swap en uso

`sudo mount -t tmpfs -o size=1024m new_ram_disk /mnt/ram_disk` Crea un espacio de almacenamiento en la memoria RAM

`cat <ruta>` Configura el uso de la memoria Swap
```
cat /proc/sys/vm/swappiness
```

`free -h` Ver memoria libre

`swapon` Ver prioridad

`df -h` ver todos los discos y particiones

`sudo mount`sirve para montar datos
```sudo mount /dev/sdb1 /mnt/media```

`ps -aux` sirve para ver todos los Ids de los programas o los procesos

`Kill -9 PID` Mata o termina un proceso 
```kill -9 3139```



## RAID 5
En una terminal de Linux se instala mdadm para crear el RAID
```
sudo apt install mdadm 
```

`Sudo fdisk -l` muestra la lista de discos conectados a la máquina

`sudo mdadm --create <ruta donde se creará el RAID>: raid5 --level=<nivel del RAID> --raid-device=<Cantidad de dispositivos> <rutas de los dispositivos>` crea el RAID 
```
sudo mdadm --create /dev/md/RAIDdisk: raid5 --level=raid5 --raid-device=4 /dev/sde /dev/sdd /dev/sdc /dev/sdb` crea el RAID 
```

`sudo mdadm -D <ruta del RAID>` Para examinar y ver el proceso de creación del RAID
```
sudo mdadm -D /dev/md/RAIDdisk\:raid5
```

`sudo <Formato> <Ruta del RAID>` Cambia el formato del RAID a uno nativo de Linux 
````
sudo mkfs.ext4 /dev/md/RAIDdisk\:raid5
````



## Archivos
`Cp <nombre del archivo a copiar> <nombre de la copia>` Copia un archivo 
```
Cp texto.txt texto3. txt 
```
`pwd` muestra el directorio actual

`cd <ruta>` cambia de directorio 
```cd \home\jchavarriac400\repo```

`ls` muestra el contenido del directorio actual 

`MV <archivo a mover> <ruta>` Mueve un archivo a una ruta especificada
```
MV texto3. txt \tmp
```

`Nano <Nombre del archivo y extension` Crea un archivo para editar`
```
Nano text.txt
```

`dpkg`  es para instalar paquetes mediante de la terminal
```
dpkg -i google-chrome-stable_current_amd64.deb
```

`grep <string>`  muestra un string del comando anterior o de un ruta especificada 
```
is \tmp | grep texto3. txt 
```

`rm <ruta del archivo a borrar>` borra un archivo
```
rm \tmp\ texto3.txt
```
- `-R` Borra un elemento sin importar su origen y de manera recursiva con su contenido ```rm prueba -R```

- `-RF`  El parámetro F fuerza el borrado de todos los elementos ```rm ./text.txt -RF```


`wc <ruta>` hace conteo de palabras
cantidad de líneas, palabras y caracteres 
```
wc\var\log\syslog1583 \var\log\syslog 
```
- `-l` sólo líneas ¨`wc \var\log\syslog-l 199614 \var\log\syslog`
- `-w` sólo palabras ¨`wc \var\log\syslog-w 199614 \var\log\syslog`
- `-m` sólo caracteres `wc \var\log\syslog-m 199614 \var\log\syslog`


`Head <ruta>` muestra la primera parte o líneas de un texto 
```
 head \var\log\syslong
```
- `-n #` Solo muestra las primeras lineas del archivo según el número especificado `head \var\logsyslog` 


`more <ruta>` Muestra un archivo linea a linea 
```
more \var\log\syslog
```

`cat  <ruta>` Muestra todo el contenido de un archivo
```
cat \var\log\syslog
```

` find <ruta> -name <lo que se va a buscar>` busca un un ruta un archivo con el nombre especificado 
```
find\home\jchavarriac400\-name index.html 
```
`file <ruta del archivo>` muestra el formato de un archivo
```file /home/jchavarriac400/text``` 

`touch <ruta del archivo>` actualiza la fecha de modificacion del archivo especificado
```touch /home/jchavarriac400/text```

`du -h <ruta del archivo>` uestra el tamaño del archivo
```du -h /home/jchavarriac400/text```

`stat <ruta del archivo>`muestra la fecha de creación de un archivo 
```stat /home/jchavarriac400/text```

## Archivos en red 
`SCP <ruta del archivo a copiar> <usuario remoto>@<direccion ip/DNS del equipo donde está el archivo>:<Dirección donde se quiere copiar el archivo>`  copia un archivo hacia una localidad remota 
```
scp texto.txt mortasoft@192.168.1.184:\home\mortasoft\semana09\texto.txt
```

`wget <ruta web del archivo>` Extrae archivos desde una página web 
```
wger https:\\mirrors.ucr.ac.cr\ubuntu-cd\20.04.3\ubuntu-20.04.3-des 
```

`git clone <url a clonar>` Copia y descarga un repositorio de github
```
git clone https:\\github.com\mortasoft\linux-scripts
```

`Curl -x Get -L <URL>` Hace un API GET en la URL especificada 
```
Curl -x Get -L https\\script.google.com\macros\s\AKfycbyó1tcPuNY3dw_31YqNGFnR6Ei55MrLFPe_PHup_VMnGP07HeoRyIy5W8xLrheMB7vJ\exec?data=$nombre 
```

## System
`reboot` reinicia el equipo a la fuerza

`shutdown` apaga el equipo a la fuerza 

`sudo apt update` Instala todas las actualizaciones pendientes

`sudo apt upgrade` Actualiza el contenido de los repositorios configurados

`man` muestra el manual de un programa 
``` man printf```

`history` muestra el historial de los comandos ingresados en el terminal 

## PDF
`pdfunite <pdf> <pdf> <pdf> <nombre del pfd final>` Une varios PDFs en uno
```
pdfunite 1.pdf 2.pdf result.pdf 
```

`pdfseparate -f <rango de páginas> <archivo a separar> <nombre del pdf de resultado>` separar un PDF en un rango de páginas especificado.
```
pdfseparate -f 1 -L 5 salida.pdf resultado_%d.pdf
```







































