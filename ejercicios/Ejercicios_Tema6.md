#Ejercicios Tema 6

###Ejercicio 6.1
**Aplicar con iptables una política de denegar todo el tráfico en una de las máquinas de prácticas. Comprobar el funcionamiento.**
**Aplicar con iptables una política de permitir todo el tráfico en una de las máquinas de prácticas. Comprobar el funcionamiento.**

Para la realización de este ejercicio debemos de tener en cuenta lo siguiente:
<ul>
<li>input: Todo lo que entra.</li>
<li>Output: Todo lo que sale.</li>
<li>Forward: Todo lo que pasa, pero tiene como direccion otro destino.</li>
</ul>

Para bloquear todo el trafico en una de lás máquinas aplicaremos los siguientes iptables:
```sh
iptable -F
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP
```
En la siguiente imagen vemos como los iptables han sido realizados en la máquina. 

![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/ejercicios/imagenes/Captura6.1.1.PNG)

Ahora en la siguiente imagen vemos como desde otra máquina antes de realizar los iptables hemos podido realizar un **ping**, pero una vez hecho el iptables no ha sido posible realizar el **ping**.

![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/ejercicios/imagenes/Captura6.1.2.PNG)

Para permitir todo el tráfico los siguiente iptables:
```sh
iptable -F
iptables -I INPUT -j ACCEPT
```
una vez hecho lo anterior comprobamos que efectivamente podemos volver a realizar un ping a la dirección de la máquina.

![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/ejercicios/imagenes/Captura6.1.3.PNG)


###Ejercicio 6.2
**Comprobar qué puertos tienen abiertos nuestras máquinas, su estado, y qué programa o demonio lo ocupa.**

Para comprobar todo lo especificado en el enunciado utilizaremos la herramienta **nmap**, si no la tenemos instalada podemos hacer con el siguiente comando:
```sh
apt-get install nmap
```
Una vez lo tenemos instalado ejecutamos el siguiente comando:
```sh
nmap -sT localhost
```
Una vez ejecutado nos mostrará el siguiente resultado:
![IMG](https://github.com/manuelalonsobraojos/swap1516/blob/master/ejercicios/imagenes/Captura6.2.1.PNG)

Como podemos ver en la anterior imagen, los puertos que están abiertos son el 22, el 80 y el 3306, que están ocupados por ssh, http y MySQL respectivamente.

###Ejercicio 6.3
**Buscar información acerca de los tipos de ataques más comunes en servidores web, en qué consisten, y cómo se pueden evitar.**

Los ataques más comunes son:

**Ataque por Injection**: es una técnica para modificar una cadena de consulta de base de datos mediante la inyección de código en la consulta. Para evitarlos podemos tomar las siguientes medidas:

<ul>
<li>Escapar los caracteres especiales utilizados en las consultas SQL como puden ser las comillas dobles o las simples</li>
<li>Delimitar los valores de las consultas</li>
<li>Asignar mínimos privilegios al usuario que conectará con la base de datos</li>
<li>Verificar siempre los datos que introduce el usuario</li>
</ul>

**DDoS**: Denegación de Servicio consiste en inundar un sitio con solicitudes externas, por lo que ese sitio no podría estar disponible para los usuarios reales. Para evitar este tipo de ataques podemos utilzar alguna herramienta como **DDoS Kona Site Defender** que mitiga los ataques DDoS por medio de la absorción del tráfico DDoS dirigido al nivel de aplicación, el desvío de todo el tráfico DDoS dirigido al nivel de red, como inundaciones SYN o inundaciones UDP, y la autenticación del tráfico válido en el extremo de la red. 

**Fuerza bruta**: este tipo de ataque intenta "romper" todas las combinaciones posibles de nombre de usuario + contraseña en una página web. Un ejemplo reciente de este tipo de ataques a sido el de hackeo de las cuentas de los famosos en ICloud. Para evitar este tipo de ataques es recomendable tener contraseñas seguras, es decir una contraseña  que contenga letras mayúsculas y minúsculas, números y símbolos.


