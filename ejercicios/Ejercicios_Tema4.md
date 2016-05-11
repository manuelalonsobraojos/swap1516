#Ejercicios Tema 4

###Ejercicio 4.1
**Buscar información sobre cuánto costaría en la actualidad un mainframe. Comparar precio y potencia entre esa máquina y una granja web de unas prestaciones similares.**  

Para ver cuanto costaría el precio de un mainframe en la actualidad me fijado en el último mainframe lanzado por la empresa IMB, el z13, su precio no ha sido confirmado por IBM, pero se estima que puede pasar facilmente los cien mil dolares. Si lo comparamos con un granja web en cuanto a precio sería más caro un mainframe, pero ocupa menos espacio y gasta menos electricidad.
Una de las contras del mainframe es que un fallo nos dejaria sin poder servir a los clientes.

###Ejercicio 4.2
**Buscar información sobre precio y características de balanceadores hardware específicos. Compara las prestaciones que ofrecen unos y otros.**  

LM-2600 Balanceador de carga de servidores - El LoadMaster 2600 está diseñado para cargas de trabajo en crecimiento con las siguientes características:
<ul>
<li>4 puertos GbE</li>
<li>1,7 Gbps L4 balanceador rendimiento</li>
<li>Transacciones SSL por / segundo (TPS): 2.000</li>
<li>Servidores soportados: 1.000 físico / virtual 500</li>
<li>Solicitudes por segundo (HTTP): 69.000</li>
<li>Precio:$6775.00</li>
</ul>

LM-5400 Server Load Balancer – Proporcionar un rendimiento con mejoras SSL, el LM-5400 está optimizado para entornos empresariales e infraestructuras de comercio electrónico de alta prestación, así como características:
<ul>
<li>8 X GbE and 2x10GbE (SFP+) ports</li>
<li>10.2 Gbps L4 balancer throughput</li>
<li>SSL TPS (2K Keys): 7,000</li>
<li>SSL TPS (1K Keys): 9,300</li>
<li>L4 Concurrent Connections: 25,600,000</li>
<li>Servers Supported: 1,000 Physical / 1,000 Virtual Servers</li>
<li>Precio:$17990</li>
</ul>

###Ejercicio 4.3
**Buscar información sobre los métodos de balanceo que implementan los dispositivos recogidos en el ejercicio 4.2**  

Los métodos de balanceo que implementan los balanceadores comentados en el anterior ejercicio son:
<ul>
<li>round Robin</li>
<li>Ponderada Round Robin</li>
<li>Conexión menos</li>
<li>Conexión menos ponderada</li>
<li>Adaptativo basado en agentes</li>
<li>Conmutación por error encadenado (Fijo Ponderación)</li>
<li>Fuente-IP Hash</li>
<li>Capa 7 Contenido de conmutación</li>
</ul>

###Ejercicio 4.4
**Instala y configura en una máquina virtual el balanceador ZenLoadBalancer.**  

Para su instalación y configuración debemos de realizar los siguientes pasos.
<ul>
<li>Podemos instalarlo, con una iso o con un paquete de Zen Load Balancer. En el caso de Debian basta con añadir los siguientes repositorios y ejecutar el comando  **apt-get update && apt-get install zenloadbalancer** para tenerlo andando (se puede gestionar a nivel de servicio).
deb http://zenloadbalancer.sourceforge.net/apt/x86 v2/</li>
<li>Para acceder a la interfaz de gestión lo haremos con la dirección: https://<ip>:444, donde <ip> es la dirección ip que le hemos asignado al host. Las credenciales de acceso por defecto son admin:admin.</li>
<li>Para la creación y configuración de una ip virtual lo haremos hciendo clic en (Settings > Interfaces > Add virtual network interface).</li>
<li>Para la creación y configuración de un farm (usando la recién creada ip virtual) lo haremos haciendo clic en: Manage > Farms > Add farm, especificando el profile (protocolo) a usar y otros settings.</li>
<li>Asignación de real servers. Dentro de la configuración del farm está la opción **Add real server**, que usaremos para añadir cada real server. En este punto debemos tener los hosts y el servicio a balancear instalados y debidamente configurados en cada backend.</li>
<li>Para comprobar su funcionamiento lo haremos comprobando que atacando a la ip definida en el farm esten sirviendo los distintos real servers.</li>
</ul>

###Ejercicio 4.5
**Probar las diferentes maneras de redirección HTTP. ¿Cuál es adecuada y cuál no lo es para hacer balanceo de carga global? ¿Por qué?**  

Hay varias maneras de hacer redirecciones: puedes usar meta refresh, JavaScript, o incluso redirecciones 302 (temporales). Sin embargo, las únicas que pasan la prueba de los buscadores son las 301.

La diferencia está en que una redirección 301 transmite todo el valor de enlace de la antigua URL a la nueva (se dice que al menos el 90% del valor). Y esto no sería importante sino fuera porque los buscadores calculan la popularidad de una página basándose en enlaces.

Cuando un buscador se encuentra con una redirección 301 reacciona de esta manera:
<ul>
  <li>Elimina la antigua página de su índice – De esta forma la página no volverá a aparecer en las páginas de resultados.</li>
  <li>Incluye la nueva página en su índice – Para en adelante tenerla en cuenta al confeccionar los resultados de búsqueda.</li>
  <li>Transfiere el valor de la antigua página a la nueva – Y con esto me refiero a la popularidad que dan los enlaces a las páginas, la cual afecta directamente a los rankings.</li>
</ul>

###Ejercicio 4.6
**Buscar información sobre los bloques de IP para los distintos países o continentes. Implementar en JavaScript o PHP la detección de la zona desde donde se conecta un usuario**  

Para este script hará falta tener en tu servidor el **archivo GeoIPLocation Library**.
```sh
<?php
error_reporting(E_ALL & ~E_NOTICE);
include("geoiploc.php"); 
  if (empty($_POST['checkip']))
  {
        $ip = $_SERVER["REMOTE_ADDR"]; 
  }
  else
  {
        $ip = $_POST['checkip']; 
  }
?> 
Tu dirección IP es: <?php echo($ip); ?> <br>
Tu País es : <?php echo(getCountryFromIP($ip, " NamE"));?>
 (<?php echo(getCountryFromIP($ip, "code"));?>)
 ```
 

