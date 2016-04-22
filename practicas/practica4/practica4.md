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


En la siguiente gráfica podremos observar como el **servidor solo** atiende más peticiones por segundo que las otras dos configuraciones y además tiene menos peticiones fallidas que las otras dos configuraciones. La granja web con nginx atiende menos peticiones por segundo respecto a la granja web con haproxy, pero tiene menos peticiones fallidas.
![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica4/capturas/grafica1.PNG)

En la siguiente gráfica podemos ver una comparación del tiempo que se tarda en realizar los test en cada configuración y como podemos ver la que menos tarda es el **servidor solo**. La granja web con haproxy tarda menos en realizar los test que la granja web con nginx.
![img](https://github.com/manuelalonsobraojos/swap1516/blob/master/practicas/practica4/capturas/grafica2.PNG)



###Comprobar el rendimiento con Siege

En este apartado monitorizaremos el rendimiento de la granja web con **Siege** que es una herramienta de generación de carga HTTP para benchmarking. Para instalarlo utilizaremos el comando:
```sh
apt-get install siege
```
Una vez lo tenemos instalado pasaremos a ejecutar la herramienta con el siguiente comando:
```sh
siege -b -t60S -v http://ip/
```
Respecto al comando anterior el parámetro **-b** hace que los tests se ejecuten sin pausa, el parámetro **-t60S** el tiempo exacto que siege se estará ejecutando. Pondremos la **ip** de la máquina contra la que realizaremos el test.

En la siguiente tabla mostraremos los resultados de ejecutar el comando contra la ip del **servidor único**.


<table style="width:100%">
  <tr>
    <th>siege  
    Servidor único</th>
    <th>Availability</th>
    <th>Elapsed time</th>
    <th>Response time</th>
    <th>Transaction rate</th>
    <th>Failed transactions</th>
    <th>Longest transaction</th>
  </tr>
  <tr>
    <td>Medición 1</td>
    <td>100.00 %</td>		
    <td>59.29</td>
    <td>0.01 s</td>
    <td>1107.71 trans/s</td>		
    <td>0.42</td>
    <td>0.00</td>
  </tr>
    <td>Medición 2</td>
      <td>100.00 %</td>
      <td>59.55 s</td>
      <td>0.01 s</td>
      <td>112.12 trans/s</td>		
      <td>0</td>
      <td>0.34</td>
  </tr>
    <td>Medición 3</td>
    <td>100.00 %</td>	
    <td>59.57 s</td>
    <td>0.01 s</td>
    <td>1126.39 trans/s</td>		
    <td>0</td>
    <td>0.36</td>
  </tr>
  </tr>
    <td>Medición 4</td>
    <td>100.00 %</td>
    <td>59.26 s</td>
    <td>0.01 s</td>
    <td>1134.15 trans/s</td>		
    <td>0</td>
    <td>0.41</td>
  </tr>
  </tr>
    <td>Medición 5</td>
    <td>100.00 %</td>
    <td>59.58 s</td>
    <td>0.01 s</td>
    <td>1129.12 trans/s</td>		
    <td>0</td>
    <td>0.33</td>
  </tr>
  </tr>
    <th>Media</th>
    <th>100.00 %</th>	
    <th>59.45 s</th>
    <th>0.01 s</th>
    <td>921.898 trans/s</td>		
    <td>0.084</td>
    <td>0.288</td>
  </tr>
  </tr>
    <th>Desviación</th>
    <th>0</th>
    <th>0 </th>
    <th>0</th>
    <th>452.79</th>		
    <th>0.1878</th>
    <th>0.16392</th>
  </tr>
</table>

Ahora en la siguiente tabla mostraremos los resultados de ejecutar el comando contra la dircción de la granja web con **nginx**:

<table style="width:100%">
  <tr>
    <th>siege  
    Granja web nginx</th>
    <th>Availability</th>
    <th>Elapsed time</th>
    <th>Response time</th>
    <th>Transaction rate</th>
    <th>Failed transactions</th>
    <th>Longest transaction</th>
  </tr>
  <tr>
    <td>Medición 1</td>
    <td>100.00 %</td>		
    <td>59.19 s</td>
    <td>0.01 s</td>
    <td>1107.18 trans/s</td>		
    <td>0</td>
    <td>0.29</td>
  </tr>
    <td>Medición 2</td>
      <td>100.00 %</td>
      <td>59.67 s</td>
      <td>0.01 s</td>
      <td>1097.65 trans/s</td>		
      <td>0</td>
      <td>0.34</td>
  </tr>
    <td>Medición 3</td>
    <td>100.00 %</td>	
    <td>59.55 s</td>
    <td>0.02 s</td>
    <td>936.36 trans/s</td>		
    <td>0</td>
    <td>0.79</td>
  </tr>
  </tr>
    <td>Medición 4</td>
    <td>100.00 %</td>
    <td>59.32 s</td>
    <td>0.01 s</td>
    <td>1089.41 trans/s</td>		
    <td>0</td>
    <td>0.37</td>
  </tr>
  </tr>
    <td>Medición 5</td>
    <td>100.00 %</td>
    <td>59.20 s</td>
    <td>0.01 s</td>
    <td>1114.61 trans/s</td>		
    <td>0</td>
    <td>0.40</td>
  </tr>
  </tr>
    <th>Media</th>
    <th>100.00 %</th>	
    <th>59.386 s</th>
    <th>0.012 s</th>
    <th>1069.042 trans/s</th>		
    <th>0.0</th>
    <th>0.438</th>
  </tr>
  </tr>
    <th>Desviación</th>
    <th>0</th>
    <th>0.21501 </th>
    <th>0.004</th>
    <th>74.7809</th>		
    <th>0</th>
    <th>0.2009</th>
  </tr>
</table>

Ahora en la siguiente tabla mostraremos los resultados de ejecutar el comando contra la dircción de la granja web con **haproxy**:

<table style="width:100%">
  <tr>
    <th>siege  
    Granja web haproxy</th>
    <th>Availability</th>
    <th>Elapsed time</th>
    <th>Response time</th>
    <th>Transaction rate</th>
    <th>Failed transactions</th>
    <th>Longest transaction</th>
  </tr>
  <tr>
    <td>Medición 1</td>
    <td>100.00 %</td>		
    <td>59.41 s</td>
    <td>0.01 s</td>
    <td>1142.70 trans/s</td>		
    <td>0</td>
    <td>0.45</td>
  </tr>
    <td>Medición 2</td>
      <td>100.00 %</td>
      <td>59.25 s</td>
      <td>0.01 s</td>
      <td>1139.14 trans/s</td>		
      <td>0</td>
      <td>0.31</td>
  </tr>
    <td>Medición 3</td>
    <td>100.00 %</td>	
    <td>59.19 s</td>
    <td>0.01 s</td>
    <td>1137.062 trans/s</td>		
    <td>0</td>
    <td>0.38</td>
  </tr>
  </tr>
    <td>Medición 4</td>
    <td>100.00 %</td>
    <td>59.46 s</td>
    <td>0.01 s</td>
    <td>1156.71 trans/s</td>		
    <td>0</td>
    <td>0.40</td>
  </tr>
  </tr>
    <td>Medición 5</td>
    <td>100.00 %</td>
    <td>59.20 s</td>
    <td>0.01 s</td>
    <td>1136.01 trans/s</td>		
    <td>0</td>
    <td>0.44</td>
  </tr>
  </tr>
    <th>Media</th>
    <th>100.00 %</th>	
    <th>59.302 s</th>
    <th>0.01 s</th>
    <th>1142.32 trans/s</th>		
    <th>0.0</th>
    <th>0.396</th>
  </tr>
  </tr>
    <th>Desviación</th>
    <th>0</th>
    <th>0.12478 </th>
    <th>0</th>
    <th>8.43788</th>		
    <th>0</th>
    <th>0.05595</th>
  </tr>
</table>

Una vez hecho los test con las tres configuraciones y obtenido las medias, realizamos la siguiente tabla y la siguiente gráfica donde podremos comparar los resultados de las diferentes configuraciones:

<table style="width:100%">
  <tr>
    <th>siege</th>
    <th>Availability</th>
    <th>Elapsed time</th>
    <th>Response time</th>
    <th>Transaction rate</th>
    <th>Failed transactions</th>
    <th>Longest transaction</th>
  </tr>
  <tr>
    <td>Servidor solo</td>
    <td>100.00 %</td>		
    <td>59.45 s</td>
    <td>0.01 s</td>
    <td>921.898 trans/s</td>		
    <td>0.084</td>
    <td>0.288</td>
  </tr>
    <td>Granja web nginx</td>
      <td>100.00 %</td>
      <td>59.386 s</td>
      <td>0.012 s</td>
      <td>1069.042 trans/s</td>		
      <td>0.0</td>
      <td>0.438</td>
  </tr>
    <td>Granja web haproxy</td>
    <td>100.00 %</td>	
    <td>59.302 s</td>
    <td>0.01 s</td>
    <td>1142.32 trans/s</td>		
    <td>0</td>
    <td>0.396</td>
  </tr>
</table>


