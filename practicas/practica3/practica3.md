#Práctica 3
Práctica 3 de Servidores Webs de Altas Prestaciones

###configurar una máquina e instalarle el nginx como balanceador de carga

Primero creamos una tercera máquina virtual sin el servicio apache, pero si con el servicio ssh.  
Una vez hecho, pasamos ha instalar el balanceador de carga **nginx**.  
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


Despues de instalar nginx tenemos que modificar su configuracion ya que la configuración básica que tiene no nos vale, por lo que modificamos el fichero de configuración **/etc/nginx/conf.d/default.conf** eliminando el contenido que tuviese. El fichero debe de quedarnos como en la siguiente imagen. 

![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica3/capturas/Captura4.PNG)

Como vemos en la definición de "upstream" las IPs son las de nuestras másquinas servidoras. 
Ahora reiniciaremos el servicio nginx con el comando:
```sh
service nginx restart
```
Si despues de ejecutar el comando no hemos obtenido ningun fallo es signo de que todo esta funcionando correctamente, por lo que podemos probar la configuración, para ello utilizaremos el comando **curl ip-balanceador** , el resultado que nos mostrara es la página de inicio de las máquina 1 y la máquina 2, alternamente, ya que se reparten el trabajo.  

Por defecto cada máquina tiene un peso de 1 pero podemos cambiarselo modificando la definicion del “upstream” del fichero de configuración **/etc/nginx/conf.d/default.conf** con el modificador **weight**.  

En la siguiente imagen muestro el archivo modificado, en este caso la máquina 1 atenderá a dos peticiones de cada tres que lleguen.

![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica3/capturas/Captura5.PNG)


###Configurar una máquina e instalarle el haproxy como balanceador de carga

En este apaartado vamos a instalar y a configurar el balanceador de carga Haproxy, para ello solo tenemos que ejecutar el comando:
```sh
apt-get install haproxy
```
En la siguiente imagen vemos la ejecución del comando.

![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica3/capturas/Captura6.PNG)

Una vez hayamos instalado haproxy tenemos que modificar el archivo de configuración **/etc/haproxy/haproxy.cfg** ya que la configuración que trae por defecto no nos vale. La configuración nos deberia de quedar de la siguiente forma:

![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica3/capturas/Captura7.PNG)

Una vez hayamos modificado la configuración, solo nos queda comprobar que el balanceador funciona. Primero lanzaremos haproxy utilizando el comando: 
```sh
/usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg
```

