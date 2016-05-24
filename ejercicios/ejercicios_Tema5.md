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
Una vez guardado los cambios y reiniciado el servicio nos iremos al navegador web y accederemos con la siguiente url **http://ip.address.here/nginx_status**
