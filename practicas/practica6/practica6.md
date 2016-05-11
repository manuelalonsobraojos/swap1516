#Práctica 6
Práctica 6 de Servidores Webs de Altas Prestaciones

###Configuración del RAID por sofware

Partiremos de una máquina virtual ya instalada y configurada. Estando apagada le añadiremos dos disco del mismo tipo y la misma capacidad. Para ello nos vamos a la configuración de la máquina virtual.

![IMG](captura1)

Una vez hemos hecho clic en los ajustes de la máquina se nos abrirá una ventana en la que aremos clic en el botón **add** que vemos en la siguiente imagen.

![IMG](captura2)

Una vez hayamos hecho clic en el botón **add** nos aparecerá un asistente para la creación del nuevo hardware, en la primera ventana que nos aparece seleccionaremos crear una unidad **Hard Disk**.

![IMG](captura3)

Una vez hayamos seleccionado la unidad, haremos clic en siguiente y nos aparecerá una ventana en la que elegiremos el tipo de disco, en nuestro caso elegiremos **SCSI**.

![IMG](captura4)

Una vez hecho le damos a siguiente y en la nueva ventana que nos aparece nos preguntará si queremos crear una unidad virtual nueva, usar una existente o usar una unidad fisica, en este caso elegiremos Crear una unidad **virtual nueva**.

![IMG](captura5)

Le daremos a siguiente y tendremos que elegir el tamaño que va a tener el disco, en este caso le daremos el mismo que el disco virtual de la máquina.

![IMG](captura6)

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
![IMG](captura7)

Como vemos en la anterior imagen nos destecta 3 discos, el primero de ellos es en el que está instalado el sistema y como podemos ver nos muestra su tabla de particiones. Los otros 2 discos que detecta son los que hemos creado y como podemos ver están vacios.

Ahora ya podemos crear el RAID 1, usaremos el dispositivo **/dev/md0**, en el que le indicaremos que usaremo los dispositivos que hemos creado **/dev/sdb** **/dev/sdc**. Para ello ejecutaremos el siguiente comando:
```sh
sudo mdadm -C /dev/md0 --level=raid1 --raid-devices=2 /dev/sdb /dev/sdc
```
![IMG](captura8)

Una vez llegado aquí, el dispositivo se habrá creado con el nombre ** /dev/md0** pero en cuanto reiniciamos la máquina  Linux lo renombrará y pasará a llamarlo **/dev/md127**.

Una vez creado el RAID, antes de reiniciar la máquina usaremos **/dev/md0** para darle formato, para ello ejecutaremos el siguiente comando:
```sh
sudo mkfs /dev/md0
```
![IMG](captura9)

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
![IMG](captura10)

Para comprobar el estado del RAID ejecutaremos el siguiente comando:
```sh
sudo mdadm --detail /dev/md0
```
![IMG](captura11)

Una vez hecho todo esto conviene configurar el sistema para que monte el dispositivo RAID creado al arrancar el sistema. Para ello deberemo de editar el archivo **/etc/fstab** y añadir la línea correspondiente para montar automáticamente el dispositivo. Es conveniente utilizar el identificador único de cada dispositivo de almacenamiento en lugar de simplemente el nombre del dispositivo.

Para obtener los UUID de todos los dispositivos de almacenamiento que tenemos, ejecutaremos la siguiente orden:
```sh
ls -l /dev/disk/by-uuid/
```
![IMG](captura12)

Con la información obtenida ya podemos editar el archivo **/etc/fstab**, añadiendo al final de este la siguiente linea para que monte automáticamente el dispositivo RAID:
```sh
UUID=ccbbbbcc-dddd-eeee-ffff-aaabbbcccddd /dat ext2 defaults 0 0
```
![IMG](captura13)

Una vez esté todo configurado y el dispositivo RAID funcionando podemos simular un fallo en uno de los discos.





