#Prática 2
Práctica 2 de Servidores Web de Altas Prestaciones

###Clonado de una carpeta entre dos máquinas
Empezaremos creando un directorio al que llamaremos "*prueba*" dentro del directorio **/var/www** de la máquina1 . Una vez hemos creado dicho directorio clonaremos la carpeta en la máquina2, para ello desde la máquina2 utilizaremos el comando: **rsync -avz -e ssh root@<dir_IP_maquina1>:/var/ww /var/www/**.
Una vez ejecutado el comando anterior comprobamos con el comando **ls -la /var/www** que el diretorio con el nombre de prueba nos aparece en nuestra máquina2.
 ![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica2/Captura1.PNG)

