Issuu Download
==============

Script bash para descargar archivos del sitio http://issuu.com

## Versión

1.0.0

## Instalación

Clonar el proyecto:

```
cd <path>
git clone git@github.com:mostofreddy/issuu_download.git
cd issuu_download
# permisos de ejecición
chmod +x issuu_download.sh
```

## Uso

```
cd <path>/isss_download
./issuu_download [-i="...."] [-o="..."] [-t="..."] [--pages=...]
```

Donde:

* __-o=[folder], --output=[folder]__: Directorio donde guardar el pdf
* __-p=[number], --pages=[number]__: Paginas totales del pdf
* __-i=[UID], --id=[UID]__: Identificador del pdf en issuu
* __-t=[string], --title=[string]__: Título del pdf exportado

Nota: Si alguno de los parametos no es pasado en el comando, el scritp luego los pide

### ID

El id del documento se visualiza en el código fuente, solo hay que buscar esta línea `<link rel="image_src" href="https://image.issuu.com/<ID>/jpg/page_<PAGE>.jpg">` 


## Changelog

__1.0.0__

* Creación del script de descarga
