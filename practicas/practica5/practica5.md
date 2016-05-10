#Práctica 5
Práctica 5 de Servidores Webs de Altas Prestaciones

###Crear una BD e insertar datos
Para crear una base de datos deberemos tener instalado previamente MySQL, en caso de que no lo tengamos instalados podemos hacerlo con el comando:
```sh
$sudo apt-get install mysql-server mysql-client
```
Una vez tenemos instalado MySQL pasamos a crear una base de datos e insertamos datos todo ello desde la interfaz de línea de comandos de mySQL, para acceder a ella escribiremos el comando:
```sh
mysql -uroot -p
```
Una vez ejecutado el comando anterior, escribiremos la clave que nos pide y ya habremos accedido. En la siguiente imagen podemos ver como se ha llevado a cabo el acceso.
![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica5/capturas/Captura1.PNG)

Una vez hemos accedido a la interfaz de línea de comando de MySQL procedemos a crear la base de datos y a insertar datos.

Para crear la base de datos escribiremos la siguiente orden:
```sh
create database contactos;
```
Una vez creada la base de datos le indicaremos sobre que vamos a trabajar con la base de datos recien creada:
```sd
use contactos;
```
Una vez ya tenemos la base de datos seleccionada crearemos una tabla en la que los datos que se le introduzcan serán un nombre y un teléfono:
```sh
create table datos(nombre varchar(100),tlf int);
```
Una vez creada la tabla le insertamos datos con la siguiente orden:
```sh
 insert into datos(nombre,tlf) values ("Manuel",95820154);
 ```
 Una vez llegados hasta aquí ya tendremos insertados uno o varios registros que podremos consultarlos mediante la siguiente orden:
```sh
select * from datos;
```
La ejecución de dicha orden nos dará un resultado como el de la siguiente imagen:

![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica5/capturas/Captura2.PNG)

###Realizar la copia de seguridad de la BD completa usando mysqldump

En este apartado vamos a realizar una copia de una base de datos, lo haremos con la herramienta **mysqldump** que es proporcionada por MySQL.

Para la realización de la clonación de la BD que hemos creado anteriormente con nombre *contactos* ejecutaremos la siguiente orden:
```sh
mysqldump ejemplodb -u root -p > /root/ejemplodb.sql
```
Cuando vayamos a clonar una BD debemos de tener en cuneta que esta no se esté por lo tanto antes de realizar la orden anterior debemos de bloquear la base de datos, para ello accederemos a MySQL y utilizaremos la siguiente sintaxis:
```sh
mysql> FLUSH TABLES WITH READ LOCK;
```
Una vez ejecutado el comando de la clonación de la BD siendo root, nos pedirá que confirmemos nuestra clave para realizar la operación.

![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica5/capturas/Captura3.PNG)

Una vez hecho todo esto en la máquina 1, copiaremos la base de datos a la máquina 2, para ello utilizaremos **spc** con la siguiente sintaxisis.
```sh
sudo scp /root/contactos.sql manuel@192.168.244.132:/home/manuel/
```
![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica5/capturas/Captura4.PNG)  

Una vez hecho lo anterior tendremos la base de datos copiada en la carpeta *home* de la máquina 2, ahora solo tendremos que moverla con el comando **mv** de la siguiente formas:
```sh
sudo mv contactos.sql /root/
```
He tenido que realizar la copia de esta manera porque tenia problemas si hacia el scp directo a la carpeta **root**.

Una vez ya tenemos realizada la copia teneos que tener en cuenta que el archivo .SQL de copia de seguridad tiene formato de texto plano, por lo que primero tendremos que crear la base de datos y luego restaurarla.
Creamos la base de datos como ya hemos visto anteriormente:
```sh
CREATE DATABASE contactos;
```
![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica5/capturas/Captura5.PNG) 

Y una vez creada restauramos los datos contenidos en la BD de la siguiente forma siendo root:
```sh
mysql -u root -p contactos < /root/contactos.sql
```
![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica5/capturas/Captura6.PNG) 

###Replicación de BD mediante una configuración maestro-esclavo

MySQL tiene la opción de configurar el demonio para la clonación de las BD sobre un esclavo con los datos que almacena el maestro. Es un proceso automático pero antes deberemos de hacer algunas configuraciones en el servidor principal y en el esclavo.          

Primero configuraremos el maestro, para ello tendremo que editar el archivo de configuración **/etc/mysql/my.cnf**.

Los cambios que tendremos que realizar son:
<ul>
 <li>Cometaremos el parámetro bin-address **#bind-address 127.0.0.1**</li>
 <li>Le indicamos el archivo donde almacenar el log de errores: **log_error = /var/log/mysql/error.log**</li>
 <li>Establecemos el identificador del servidor, en el archivo de configuración aparecerá comentado, lo descomentaremos: **server-id = 1**</li>
 <li>Estableceremos el registro binario: **log_bin = /var/log/mysql/bin.log**</li>
</ul>

Una vez hecho todo esto reiniciaremos el servicio con el siguiente comando:
```sh
/etc/init.d/mysql restart
```



