#Práctica 3
Práctica 3 de Servidores Webs de Altas Prestaciones

###configurar una máquina e instalarle el nginx como balanceador de carga

Primero creamos una tercera máquina virtual sin el servicio apache, pero si con el servicio ssh.  
Una vez hecho pasamos ha instalar el balanceador de carga **nginx**.  
Primero importaremos la clave del repositorio de software, para ello utilizaremos las siguientes lineas de comandos:
```sh
cd /tmp/
wget http://nginx.org/keys/nginx_signing.key
apt-key add /tmp/nginx_signing.key
rm -f /tmp/nginx_signing.key
```
En la siguiente captura podemos ver la ejecución de los comandos realizada con éxito.
![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica3/capturas/Captura1.PNG)

Una vez hecho esto añadiremos el repositorio al fichero /etc/apt/sources.list, para ello ejecutaremos siendo previamente *Root* las órdenes que vemos a continucacion en nuestra terminal:
```sh
echo "deb http://nginx.org/packages/ubuntu/ lucid nginx" >> /etc/apt/sources.list
echo "deb-src http://nginx.org/packages/ubuntu/ lucid nginx" >> /etc/apt/sources.list
```
![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica3/capturas/Captura2.PNG)

Una vez hecho esto instalamos nginx utilizando el comando:
```sh
apt-get install nginx
```
![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica3/capturas/Captura3.PNG)


