#Práctica 6
Práctica 6 de Servidores Webs de Altas Prestaciones

###Configuración del RAID por sofware

Partiremos de una máquina virtual ya instalada y configurada. Estando apagada le añadiremos dos disco del mismo tipo y la misma capacidad. Para ello nos vamos a la configuración de la máquina virtual.

![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica6/capturas/Captura1.PNG)

Una vez hemos hecho clic en los ajustes de la máquina se nos abrirá una ventana en la que aremos clic en el botón **add** que vemos en la siguiente imagen.

![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica6/capturas/Captura2.PNG)

Una vez hayamos hecho clic en el botón **add** nos aparecerá un asistente para la creación del nuevo hardware, en la primera ventana que nos aparece seleccionaremos crear una unidad **Hard Disk**.

![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica6/capturas/Captura3.PNG)

Una vez hayamos seleccionado la unidad, haremos clic en siguiente y nos aparecerá una ventana en la que elegiremos el tipo de disco, en nuestro caso elegiremos **SCSI**.

![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica6/capturas/Captura4.PNG)

Una vez hecho le damos a siguiente y en la nueva ventana que nos aparece nos preguntará si queremos crear una unidad virtual nueva, usar una existente o usar una unidad fisica, en este caso elegiremos Crear una unidad **virtual nueva**.

![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica6/capturas/Captura5.PNG)

Le daremos a siguiente y tendremos que elegir el tamaño que va a tener el disco, en este caso le daremos el mismo que el disco virtual de la máquina.

![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica6/capturas/Captura6.PNG)

Una vez hecho esto ya solo tenemos que ponerle un nombre a disco. Para el otros disco que hay que crear el proceso será el mismo que acabamos de realizar.

Una vez añadido los dos nuevos discos, arrancamos la máquina e instalamos el software necesario para configurar el RAID, para ello ejecutaremos el siguiente comando:
```sh
sudo apt-get install mdadm
```
si durante el proceso de instalación si queremos configurar *postfix* seleccionaremos *sin configuración*.

Una vez instalado buscamos la información de los dos disco con el comando:
```sh
sudo fdisk -l 
```
![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica6/capturas/Captura7.PNG)

Como vemos en la anterior imagen nos destecta 3 discos, el primero de ellos es en el que está instalado el sistema y como podemos ver nos muestra su tabla de particiones. Los otros 2 discos que detecta son los que hemos creado y como podemos ver están vacios.

Ahora ya podemos crear el RAID 1, usaremos el dispositivo **/dev/md0**, en el que le indicaremos que usaremo los dispositivos que hemos creado **/dev/sdb** **/dev/sdc**. Para ello ejecutaremos el siguiente comando:
```sh
sudo mdadm -C /dev/md0 --level=raid1 --raid-devices=2 /dev/sdb /dev/sdc
```
![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica6/capturas/Captura8.PNG)

Una vez llegado aquí, el dispositivo se habrá creado con el nombre ** /dev/md0** pero en cuanto reiniciamos la máquina  Linux lo renombrará y pasará a llamarlo **/dev/md127**.

Una vez creado el RAID, antes de reiniciar la máquina usaremos **/dev/md0** para darle formato, para ello ejecutaremos el siguiente comando:
```sh
sudo mkfs /dev/md0
```
![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica6/capturas/Captura9.PNG)

Por defecto, mkfs inicializa un dispositivo de almacenamiento con formato ext2.
Una vez hecho esto ya podemos crear el directorio en el que se montará la unidad del RAID, para ello ejecutaremos los siguientes comandos:
```sh
sudo mkdir /dat
sudo mount /dev/md0 /dat
```
Para comprobar que el proceso se ha realizado correctamente, y también los parámetros con los que Linux ha conseguido montarlo usando la orden:
```sh
sudo mount
```
![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica6/capturas/Captura10.PNG)

Para comprobar el estado del RAID ejecutaremos el siguiente comando:
```sh
sudo mdadm --detail /dev/md0
```
![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica6/capturas/Captura11.PNG)

Una vez hecho todo esto conviene configurar el sistema para que monte el dispositivo RAID creado al arrancar el sistema. Para ello deberemo de editar el archivo **/etc/fstab** y añadir la línea correspondiente para montar automáticamente el dispositivo. Es conveniente utilizar el identificador único de cada dispositivo de almacenamiento en lugar de simplemente el nombre del dispositivo.

Para obtener los UUID de todos los dispositivos de almacenamiento que tenemos, ejecutaremos la siguiente orden:
```sh
ls -l /dev/disk/by-uuid/
```
![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica6/capturas/Captura12.PNG)

Con la información obtenida ya podemos editar el archivo **/etc/fstab**, añadiendo al final de este la siguiente linea para que monte automáticamente el dispositivo RAID:
```sh
UUID=ccbbbbcc-dddd-eeee-ffff-aaabbbcccddd /dat ext2 defaults 0 0
```
![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica6/capturas/Captura13.PNG)

Una vez esté todo configurado y el dispositivo RAID funcionando podemos simular un fallo en uno de los discos, para ello utilizamos el siguiente comando:
```sh
sudo mdadm --manage --set-faulty /dev/md127 /dev/sdb
```
![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica6/capturas/Captura14.PNG)

También podremo retirar “en caliente” un disco, para ello ejecutaremos el comando:
```sh
sudo mdadm --manage --remove /dev/md127 /dev/sdb
```
![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica6/capturas/Captura15.PNG)

Y por último, podemos añadir, también “en caliente”, un nuevo disco que vendría a reemplazar al disco que hemos retirado, para ello utilizaremos el comando:
```sh
sudo mdadm --manage --add /dev/md0 /dev/sdb
```
![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica6/capturas/Captura16.PNG)



