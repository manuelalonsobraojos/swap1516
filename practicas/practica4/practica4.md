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

En la siguiente tabla veremos los resultados de ejecutar el comando "**ab**" contra la máquina 1:
<table style="width:100%">
  <tr>
    <th>ab  
    Máquina 1</th>
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
    <th>2535.368cr/s</th>
  </tr>
  </tr>
    <th>Desviación</th>
    <th>0.07146</th>
    <th>0</th>
    <th>410.12959 r/s</th>
  </tr>
</table>
