#Ejercicios Tema 4

###Ejercicio 5.1
**Buscar información sobre cómo calcular el número de conexiones por segundo.**

Lo podemos hacer con nginx ya que tiene un módulo llamado **HttpStubStatusModule**, que muestra información sobre el estado de nginx, como:
<ul>
<li>El número de conexiones abiertas</li>
<li>Estadísticas sobre las conexiones aceptadas</li>
<li>Conexiones por segundo</li>
</ul>

Para ello editaremos el archivo de configuración de nginx **nginx.conf** añadiendole lo siguiente:
```sh
location /nginx_status {
        # Turn on stats
        stub_status on;
        access_log   off;
        # only allow access from 192.168.1.5 #
        allow 192.168.1.5;
        deny all;
   }
```
Una vez guardado los cambios y reiniciado el servicio nos iremos al navegador web y accederemos con la siguiente url **http://ip.address.here/nginx_status** y nos mostrará unos resultados como en la siguiente imagen:

![IMG](http://s0.cyberciti.org/uploads/faq/2013/02/nginx_status_output.png)


###Ejercicio5.3
**Buscar información sobre características, disponibilidad paradiversos SO, etc de herramientas para monitorizar las prestaciones de un servidor.**

**netstat**: es una herramienta de línea de comandos que muestra un listado de las conexiones activas de una computadora, tanto entrantes como salientes.La información que resulta del uso del comando incluye el protocolo en uso, las tablas de ruteo, las estadísticas de las interfaces y el estado de la conexión.  
Está disponible para varios sistemas como Unix, GNU/Linux, Mac OS X, Windows y BeOS.

**vmstat**: esta herramienta muestra información sobre el funcionamiento del sistema, la memoria, los procesos, las interrupciones, paginación y bloque E/S.  
Esta herramienta está disponible en la mayoria de sistemas operativos Unix tales como FreeBSD, Linux or Solaris.

**top**: esta herramineta usada por ventana de comando mediante el comando **top** muestra una lista de procesos que se va actualizando frecuentemente, estos procesos se van ordenando en funcion de uso de CPU y se muestran PID, usuario, %CPU, %MEM.


