# Ejercicios Temas3

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
