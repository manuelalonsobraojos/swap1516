#Práctica 4
Práctica 4 de Servidores Webs de Altas Prestaciones

###Comprobar el rendimiento de servidores web con Apache Benchmark

Primero creamos una cuarta máquina virtual que será independiente a las máquinas que forman la granja web.
En este apartado monitorizaremos el rendimiento de la granja web con Apache Benchmark que es una utilizad que viene instalada con el servidor Apache, en caso de que no estuviera instalada la podemos instalar con el comando:
```sh
apt-get install apache2-utils
```
Para comprobar el rendimiento de la granja web utilizaremos el siguiente comando:
```sh
ab -n 1000 -c 10 http://ip/
```
El parámetro **-c 10** indica que se van a ejecutar 10 solicitudes concurrentemente y el parámetro **-n 1000** indica el número de solicitudes que se le van hacer al servidor, en este caso **1000**.
La dirección ip que pondremos será la de la máquina contra la que vamos hacer el comando "**ab**".

En la siguiente tabla veremos los resultados de ejecutar el comando "**ab**" contra el servidor solo:


<table style="width:100%">
  <tr>
    <th>ab  
    Servidor solo</th>
    <th>Time taken for tests</th>
    <th>Failed requests</th>
    <th>Requests per second</th>
  </tr>
  <tr>
    <td>Medición 1</td>
    <td>0.451 s</td>		
    <td>0</td>
    <td>2219.03 r/s</td>
  </tr>
    <td>Medición 2</td>
      <td>0.351 s</td>
      <td>0</td>
      <td>2847.97 r/s</td>
  </tr>
    <td>Medición 3</td>
    <td>0.355 s</td>	
    <td>0</td>
    <td>2820.29 r/s</td>
  </tr>
  </tr>
    <td>Medición 4</td>
    <td>0.355 s</td>
    <td>0</td>
    <td>2815.68 r/s</td>
  </tr>
  </tr>
    <td>Medición 5</td>
    <td>0.507 s</td>
    <td>0</td>
    <td>1973.87 r/s</td>
  </tr>
  </tr>
    <th>Media</th>
    <th>0.4035 s</th>	
    <th>0</th>
    <th>2535.368 r/s</th>
  </tr>
  </tr>
    <th>Desviación</th>
    <th>0.07146</th>
    <th>0</th>
    <th>410.12959 r/s</th>
  </tr>
</table>  

En la siguiente tabla veremos los resultados de ejecutar el comando "**ab**" contra la la granja web con **nginx**:


<table style="width:100%">
  <tr>
    <th>ab  
    nginx</th>
    <th>Time taken for tests</th>
    <th>Failed requests</th>
    <th>Requests per second</th>
  </tr>
  <tr>
    <td>Medición 1</td>
    <td>0.961 s</td>		
    <td>333</td>
    <td>1040.26 r/s</td>
  </tr>
    <td>Medición 2</td>
      <td>0.865 s</td>
      <td>334</td>
      <td>1156.54 r/s</td>
  </tr>
    <td>Medición 3</td>
    <td>0.736 s</td>	
    <td>333</td>
    <td>1359 r/s</td>
  </tr>
  </tr>
    <td>Medición 4</td>
    <td>0.764 s</td>
    <td>333</td>
    <td>1309.39 r/s</td>
  </tr>
  </tr>
    <td>Medición 5</td>
    <td>0.731 s</td>
    <td>666</td>
    <td>1367.85 r/s</td>
  </tr>
  </tr>
    <th>Media</th>
    <th>0.8114 s</th>	
    <th>399.8</th>
    <th>1246.608 r/s</th>
  </tr>
  </tr>
    <th>Desviación</th>
    <th>0.09956</th>
    <th>148.81</th>
    <th>143.14757 r/s</th>
  </tr>
</table>

En la siguiente tabla veremos los resultados de ejecutar el comando "**ab**" contra la la granja web con **haproxy**:


<table style="width:100%">
  <tr>
    <th>ab  
    haproxy</th>
    <th>Time taken for tests</th>
    <th>Failed requests</th>
    <th>Requests per second</th>
  </tr>
  <tr>
    <td>Medición 1</td>
    <td>0.594 s</td>		
    <td>500</td>
    <td>1683.80 r/s</td>
  </tr>
    <td>Medición 2</td>
      <td>0.602 s</td>
      <td>500</td>
      <td>1660.64 r/s</td>
  </tr>
    <td>Medición 3</td>
    <td>0.583 s</td>	
    <td>500</td>
    <td>1714.89 r/s</td>
  </tr>
  </tr>
    <td>Medición 4</td>
    <td>0.593 s</td>
    <td>500</td>
    <td>1687.67 r/s</td>
  </tr>
  </tr>
    <td>Medición 5</td>
    <td>0.607 s</td>
    <td>500</td>
    <td>1648.51 r/s</td>
  </tr>
  </tr>
    <th>Media</th>
    <th>0.5958 s</th>	
    <th>500</th>
    <th>1679.102 r/s</th>
  </tr>
  </tr>
    <th>Desviación</th>
    <th>0.0092</th>
    <th>0</th>
    <th>25.75354 r/s</th>
  </tr>
</table>


Una vez hechas las mediciones con las tres configuraciones realizaremos una tabla y un gráfico con las medias obtenidas, para así poder comparar los resultados.  
<table style="width:100%">
  <tr>
    <th>ab</th>
    <th>Time taken for tests</th>
    <th>Failed requests</th>
    <th>Requests per second</th>
  </tr>
  <tr>
    <td>Servidor solo</td>
    <td>0.4035 s</td>		
    <td>0</td>
    <td>2535.368 r/s</td>
  </tr>
    <td>granja web con nginx</td>
      <td>0.8114 s</td>
      <td>399.8</td>
      <td>1246.608 r/s</td>
  </tr>
    <td> granja web con haproxy</td>
    <td>0.5958 s</td>	
    <td>500</td>
    <td>1679.102 r/s</td>
</table>



En la siguiente gráfica podremos observar como el **servidor solo** atiende más peticiones por segundo que las otras dos configuraciones y además tiene menos peticiones fallidas que las otras dos configuraciones.
![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica4/capturas/grafica1.PNG)

En la siguiente gráfica podemos ver una comparación del tiempo que se tarda en realizar los test en ada configuración y como podemos ver la que menos tarda es el **servidor solo**.
![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica4/capturas/grafica2.PNG)



###Comprobar el rendimiento con Siege
