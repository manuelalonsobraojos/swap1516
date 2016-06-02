#Ejercicios Tema 7

###Ejercicio 7.1
**¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 0 a partir de dos discos de 100 GB y 100 GB?** 

El RAID 0 lo que hace es mejorar el rendimiento y aumentar la capacidad del disco final, por lo que la capacidad final de la unidad RAID con dos discos de 100GB será de 200GB.

**¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 0 a partir de tres discos de 200 GB cada uno?**

Como hemos visto en el anterior ejercicio al tratarse de un RAID se sumna las capacidades de cada disco por que la unidad RAID será de 600GB.

###Ejercicio 7.2
**¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 1 a partir de dos discos de 100 GB y 100 GB?**

El tamaño del RAID será de 100GB puesto que la principal caracteristica del RAID 1 es la réplica de los datos en ambos discos.

**¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 1 a partir de tres discos de 200 GB cada uno?**

El tamaño del RAID será de 200GB puesto que la información se replica en los tres discos.

###Ejercicio 7.3
**¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 5 a partir de tres discos de 120 GB cada uno?**

La unidad RAID sería de 240GB quedando un disco de 120GB como disco de paridad.

###Ejercicio 7.4
**Buscar información sobre los sistemas de ficheros en red más utilizados en la actualidad y comparar sus características. Hacer una lista de ventajas e inconvenientes de todos ellos, así como grandes sistemas en los que se utilicen.**

Los sistemas de ficheros en red más utilizados son NFS, el programa Samba y Server Message Block. Destacando ampliamente NFS.
NFS está dividido en dos partes, servidor y clientes. Los clientes acceden de manera remota a los sdatos almacenados en el servidor. De esta manera las estaciones de trabajo locales utilizan menos espacio de disco, pues los datos se encuentran centralizados, aunque pueden ser accedidos y modificados por varios usuarios. También se puede acceder a través de la red a dispositivos de almacenamiento como disqueteras o lectores CD-ROM.

Server Message Block (SMB) es un protocolo de red que permite compartir archivos e impresoras entre nodos de una red usado principalmente en ordenadores con Windows y DOS. Fue originalmente inventado por IBM aunque la versión más utilizada hoy en día es la modificada por Microsoft, llamada CIFS e incluye soporte para enlaces simbólicos, enlaces duros y mayores tamaños de archivo. Samba es una implementación libre del protocolo de archivos compartidos de Windows para sistemas Unix. Está basado en Server Message Block (De hecho su nombre surge al añadirle dos vocales a SMB). Funciona configurando directorios Unix como recursos para compartir a través de la red. Éstos aparecen como carpetas de red para los usuarios de Windows. Se permite dar distintos permisos según el usuario.

**Configurar en una máquina virtual un servidor NFS. Montar desde otra máquina virtual en la misma subred la carpeta exportada y comprobar que ambas pueden acceder a la misma para lectura y escritura.**

Lo primero que hacemos es descargar e instalar el servidor NFS. Lo realizamos mediante el siguiente comando:

    apt-get install nfs-kernel-server portmap
    
Una vez instalado el servidor NFS creamos un directorio ejecutando la siguiente orden:

    mkdir /var/nfs/
    
Una vez hemos creado el directorio le cambiaremos los permisos de acceso al directorio ejecutando la siguiente orden:

    chown nobody:nogroup /var/nfs
    
Exportaremos los directorios desde el fichero /etc/exports

    nano /etc/exports
    
una vez exportados editaremos dicho fichero añadiendole las siguientes sentencias:

    /var/nfs        192.168.64.128(rw,sync,no_subtree_check)
    
Una vez hemos editado el fichero le aplicamos la configuración con el comando:

    exportfs -a.
  
Una vez aquí pasaremos a la máquina que hará de cliente e instalamos el cliente NFS.

    apt-get install nfs-common portmap

Montamoremos el directorio ejecutando las siguientes ordenes:

    mkdir -p /mnt/nfs/var/nfs
    mount 192.168.64.128:/var/nfs /mnt/nfs/var/nfs
    
Para comprobar su funcionamiento tal simple como crear un fichero en el servidor y en el directorio montado en el NFS cliente debe aparecernos si realizamos un ls en el directorio.
