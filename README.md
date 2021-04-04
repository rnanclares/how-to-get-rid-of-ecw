# Como librarse de ecw usando gdal y geotiffs comprimidos
## Hot to get rid of ECW using gdal and compressed geotiffs

Para ello necesitamos solo 2 herramientas
- Docker/Podman
- GDAL

## Introducción

Reconocimientos:
* Paul Ramsey - [GeoTiff Compression for Dummies](http://blog.cleverelephant.ca/2015/02/geotiff-compression-for-dummies.html)
* Luigi Pirelli - [Docker-gdalecw](https://github.com/luipir/docker-gdalecw)[1]
* Keith Jenkins - [TIFF compression options](https://gist.github.com/kgjenkins/877ff0bf7aef20f87895a6e93d61fb43)
* koko Alberti - [Guide to GeoTIFF compression and optimization with GDAL](https://kokoalberti.com/articles/geotiff-compression-optimization-guide/)

### ¿Por qué no debemos usar ecw?
- No es formato abierto.
- Necesita de un SDK privativo para que GDAL lo soporte en sistemas GNU/Linux, Windows o Mac.
- Las versiones de GDAL incluidos en las distribuciones de GNU/Linux no tienen soporte para ecw (u otros formatos privativos) porque no se puede distribuir el SDK bajo licencias de software libre.
- Desde hace muchos años tenemos alternativas con la compresión JPEG en el formato GeoTIFF en el caso de la fotografía aérea y otros tipos de compresión (con y sin perdida) que pueden utilizarse con imágenes GeoTIFF.

## Proceso de compresión con GDAL

Para la compresión con gdal vamos a usar gdal_translate con compresión JPEG. Para los usuarios de distribuciones Linux tenemos dos opciones: compilar GDAL con soporte para ecw o usar la imagen de Docker de Luigi Pirelli (o la de [Klokan](https://gist.github.com/klokan/bfd4a07e8072ffae4bb6)).

Una vez instalado Docker (o Podman) podemos seguir las instrucciones de [1] para convertir de ecw a geotiff. En este caso Luigi Pirelli nos recomienda crear una variable de entorno para almacenar el parámetro que define el volumen que se va a usar con el contenedor.

`$ export DATAFOLDER="-v /directorio_con_nuestros_ecw/:/home/datafolder"`

A continuación podemos iniciar el contenedor (la primera vez tarda un poco porque tiene que descargar la imagen desde Docker Hub)

`$ docker run $DATAFOLDER --name gdalecw -it --rm ginetto/gdal:2.4.4_ECW /bin/bash`

En el caso de Podman podemos hacerlo de la siguiente manera

`$ podman run $DATAFOLDER --name gdalecw -it --privileged --rm ginetto/gdal:2.4.4_ECW /bin/bash`

Otra opción, sin necesidad de usar la variable de entorno, es movernos a la carpeta donde están nuestros ecw y usar el siguiente comando:

`$ docker run -v $pwd:/home/datafolder --name gdalecw -it --rm ginetto/gdal:2.4.4_ECW /bin/bash`

En este caso hacemos uso de la variable $pwd que es el "wordking directory" en desde donde hacemos docker run.

Con cualquier de estos comandos lo que hacemos es iniciar una terminal dentro del contenedor. Veremos algo así:

`root@7b666f83e385:/usr/local# `

Ahora basta con que nos cambiemos al directorio con nuestros datos y empecemos a trabajar.

`$ cd /home/datafolder/



