# Como librarse de ecw usando gdal y geotiffs comprimidos
## Hot to get rid of ECW using gdal and compressed geotiffs

Para ello necesitamos solo 2 herramientas
- Docker/Podman
- GDAL

## Introducción

Reconocimientos:
* Paul Ramsey - [GeoTiff Compression for Dummies](http://blog.cleverelephant.ca/2015/02/geotiff-compression-for-dummies.html)
* Luigi Pirelli - [Docker-gdalecw](https://github.com/luipir/docker-gdalecw)
* Keith Jenkins - [TIFF compression options](https://gist.github.com/kgjenkins/877ff0bf7aef20f87895a6e93d61fb43)
* koko Alberti - [Guide to GeoTIFF compression and optimization with GDAL](https://kokoalberti.com/articles/geotiff-compression-optimization-guide/)

### ¿Por qué no debemos usar ecw?
- No es formato abierto.
- Necesita de un SDK privativo para funcionar en sistemas GNU/Linux, Windows o Mac.
- Las versiones de GDAL incluidos en las distribuciones de GNU/Linux no tienen soporte para ecw (u otros formatos privativos) porque no se puede distribuir el SDK bajo licencias de software libre.
- Desde hace muchos años tenemos alternativas con la compresión JPEG en el formato GeoTIFF en el caso de la fotografía aérea y otros tipos de compresión (con y sin perdida) que pueden utilizarse con imágenes GeoTIFF.

## Proceso de compresión con GDAL




