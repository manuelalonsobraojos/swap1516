# Ejercicios Tema3

### Ejercicio 3.1
**Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el enrutamiento del tráfico de un servidor para pasar el tráfico desde una subred a otra.**

**En windows**:
Para configurar el enrutamiento del tráfico de un servidor lo haremos con el comando:
```sh
C:\> route
```
Dependiendo lo que deseemos hacer usaremos diferentes opciones:
<ul>
<li>PRINT: imprime una ruta</li>
<li>ADD: agrega una ruta</li>
<li>DELETE: elimina una ruta</li>
<li>CHANGE: modifica una ruta existente</li>
</ul>

**En Linux**:
Para configurar el enrutamiento del tráfico de un servidor lo haremos con el comando:
```sh
$ route[opciones]
```
Dependiendo lo que deseemos hacer usaremos diferentes opciones:
<ul>
<li>-n: Muestra la tabla de enrutamiento en formato numérico [dirección IP]>
<li>-e: Muestra la tabla de enrutamiento en formato hostname</li>
<li>add: Añade una nueva ruta a la tabla de enrutamiento</li>
<li>del: Elimina una ruta de la tabla de enrutamiento</li>
</ul>

**Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el filtrado y bloqueo de paquetes.** 

 **Windows**

Para agregar un filtro de paquetes en Windows, seguiremos los siguientes pasos:
```sh
1.  Abrir Enrutamiento y acceso remoto.
2.  En el árbol de consola, hacemos clic en General Enrutamiento y acceso remoto/nombre de servidor/[IPv4 o IPv6]/General
3.  En el panel de detalles, hacemos clic con el boton secundadrio en la interfaz donde deseamos un filtro y a continuación, hacemos clic en Propiedades.
4.  En la ficha General, haga clic en Filtros entrantes o Filtros salientes.
5.  En el cuadro de diálogo Filtros entrantes o Filtros salientes, haga clic en Nuevo.
6.  En el cuadro de diálogo Agregar filtro IP, escriba la configuración del filtro y, a continuación, haga clic en Aceptar.
7.  En Acción de filtrado, seleccione la acción de filtrado apropiada y, a continuación, haga clic en Aceptar.
```

**Linux**

Para agregar un filtro de paquetes en Linux lo haremos mediante la herramineta *iptables*. Esta herramineta nos permite insertar y eliminar reglas de la tabla de filtrado de paquetes del núcleo. 
*IPtables* suele venir instalada por defecto en todas las distribuciones oficiales de linux, en caso de no ternerla instalada lo podemos hacer ejecutando el siguiente comando:
```sh
apt-get install -test iptables
```
Para obtener más información sobre esta herramienta podemos ejercutar la orden:
```sh
man iptables
```
O acceder a la dirección: http://www.ubuntu-es.org/node/422#.V1AGB5GLTIU
