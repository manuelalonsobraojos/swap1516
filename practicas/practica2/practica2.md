#Prática 2
Práctica 2 de Servidores Web de Altas Prestaciones

###Clonado de una carpeta entre dos máquinas
Empezaremos creando un directorio al que llamaremos "*prueba*" dentro del directorio **/var/www** de la máquina1 . Una vez hemos creado dicho directorio clonaremos la carpeta en la máquina2, para ello desde la máquina2 utilizaremos el comando: 

**rsync -avz -e ssh root@<dir_IP_maquina1>:/var/ww /var/www/**

Una vez ejecutado el comando anterior comprobamos con el comando **ls -la /var/www** que el diretorio con el nombre de prueba nos aparece en nuestra máquina2.

 ![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica2/Captura1.PNG)
 
 En la imagen podemos como nos queda el directorio **/var/www/** antes y despues de la clonación.
 
 
###Configuración de ssh para acceder sin que solicite contraseña

Para poder acceder a la consola sin tener que introducir la contraseña, debemos generar una clave DSA que contendrá los datos de conexión del usuario que realizará las conexiones ssh y cada vez que realice una conexión ssh remota con ese usuario el servidor remoto leerá la clave pública DSA y cargará la información de conexión del usuario.

Para crear la clave DSA utilizaremos el comando: **ssh-keygen -t dsa**, acto seguido tendremos que indicar el directorio donde queremos que se cree el archivo de la clave y nos pedirá la contraseña que la dejaremos en blanco para poder acceder sin contraseña.

 ![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica2/Captura3.PNG) 
 
 Una vez hecho esto copiamos la clave pública creada al equipo remoto con el que queremos tener una relación de confianza, para ello ejecutaremos el comando: **ssh-copy-id usuario_remoto@dirección_ip**.
 
 ![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica2/Captura4.PNG)
 
 Como vemos en la anterior imagen, una vez ejecutado el comando nos dice que comprobemos si podemos acceder sin contraseña.
 Nos conectamos con el comando **ssh usuario_remoto@direccion_ip** y como podemos comprobar en la siguiente imagen no nos pide ninguna contraseña.
 
![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica2/Captura5.PNG)

###establecer una tarea en cron que se ejecute cada hora para mantener actualizado el contenido del directorio /var/www entre las dos máquinas

Cremoa un script para actualizar el directorio /var/www con el comando: **rsync -avz -e ssh root@<dir_IP_maquina1>:/var/ww /var/www/**.
Una vez hemos creado el script le damos permisos de ejecución con el comando **chmod a+x script.sh** y añadimos una nueva tarea al archivo */etc/crontab* en el que el script se ejecutará por el usuario root en el minuto 0 de cada hora, de cada mes, de cada día de la semana, realizando pocia del contenio del directorio */var/www*

![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica2/Captura6.PNG)
