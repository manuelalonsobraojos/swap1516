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
Una vez ejecutado el comando anterior, escribiremos la clave que nos pide y ya habremos accedido.
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

