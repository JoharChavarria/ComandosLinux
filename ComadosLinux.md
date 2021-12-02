# ComandosLinux
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

`cat /proc/sys/vm/swappiness` Configura el uso de la memoria Swap

`free -h` Ver memoria libre

`swapon` Ver prioridad

`df -h` ver todos los discos y particiones
Creación de RAID Linux 
Se crean los discos duros

## RAID 5
En una terminal de Linux se instala mdadm para crear el RAID
`sudo apt install mdadm`
```
sudo apt install mdadm 
```
`Sudo fdisk -l` muestra la lista de discos conectados a la máquina

`sudo mdadm --create /dev/md/RAIDdisk: raid5 --level=raid5 --raid-device=4 /dev/sde /dev/sdd /dev/sdc /dev/sdb` crea el RAID 
```
sudo mdadm --create /dev/md/RAIDdisk: raid5 --level=raid5 --raid-device=4 /dev/sde /dev/sdd /dev/sdc /dev/sdb` crea el RAID 
```

`sudo mdadm -D /dev/md/RAIDdisk\:raid5` Para examinar y ver el proceso de creación del RAID
```
sudo mdadm -D /dev/md/RAIDdisk\:raid5
```

`sudo mkfs.ext4 /dev/md/RAIDdisk\:raid5` Cambia el formato del RAID a uno nativo de Linux 

````
sudo mkfs.ext4 /dev/md/RAIDdisk\:raid5
````

## Archivos
`Cp <nombre del archivo a copiar> <nombre de la copia>` Copia un archivo 
```
Cp texto.txt texto3. txt 
```

`MV <archivo a mover> <ruta>` Mueve un archivo a una ruta especificada
```
MV texto3. txt \tmp
```

`Nano file.sh` Crea un archivo para editar`

`dpkg`  es para instalar paquetes mediante de la terminal
```
dpkg -i google-chrome-stable_current_amd64.deb
```
`grep <string>`  muestra un string del comando anterior o de un ruta especificada 
```

























