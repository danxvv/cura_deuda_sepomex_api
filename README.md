# Backend para prueba de conocimiento de CURA DEUDA

## Preparacion del entorno

Antes de ejecutar algun comando o script se necesitan instalar ciertos paquetes para que todo pueda funcionar.
Instalar mediante:

`pip install -r requirements.txt`

Asi mismo es recomendable declarar de una vez las variables para que flask funcione:

* Linux : `export FLASK_APP=main.py`
* Windows-CMD : `set FLASK_APP=main.py`
* Windows-PowerShell : `$env:FLASK_APP = main.py`

## Uso del SeedScript

El script `extract_data.py` esta listo para funcionar sin configurar nada, pues hace uso de **sqlite3**, si no existe la base de datos el script la creara, procedera a borrar tablas que se requieran si existen para evitar conflictos y creara las siguientes para nosotros:
* estados
* municipios
* colonias
El script se encarga de filtrar la informacion en bruto del archivo `CPdescarga.xls` y nos ordena la informacion en las tablas ya mencionadas.

## Correr la API

La API se desarrollo en Flask, si ya se ha declarado la variable `FLASK_APP` basta con ejecutar el siguiente comando `flask run` lo que ejecutara el API en nuestra PC.

### Endpoints

* `http://127.0.0.1:5000/api/cp` - Nos devuelve todos los codigos postales del pais (tarda un poco en cargar todos)
* `http://127.0.0.1:5000/api/cp/{numerocp}` - Al poner un codigo postal valido, nos devolvera **Codigo Postal - Nombre Colonia - Nombre Estado - Tipo Colonia - Tipo Zona**
* `http://127.0.0.1:5000/api/estados` - Devuelve los estados con su numero de estado y su capital
* `http://127.0.0.1:5000/api/estado/{estado}` - Busca en los estados si hay alguno que coincida con el endpoint
* `http://127.0.0.1:5000/api/municipios` - Devuelve los municipios del pais y el estado al que pertencen
* `http://127.0.0.1:5000/api/municipio/{municipio}` Busca en los municipios si hay alguno que coincida con el endpoint
* `http://127.0.0.1:5000/api/colonias/` Devuelve todas las colonias del pais
* `http://127.0.0.1:5000/api/colonia/{colonia}` Busca en las colonias si hay alguno que coincida con el endpoint


## Docker

Tambien se creo una imagen del proyecto en Docker, el archivo `Dockerfile` muestra los comandos usados para crear dicha imagen.  
La imagen actualmente se encuentra en DockerHub en la siguiente liga: [DockerHub](https://hub.docker.com/r/danxvv/dockerhub/tags?page=1&ordering=last_updated)  
Para poder correr la imagen en un contenedor local se debe tener instalado Docker y ejecutar el siguiente comando:  
`docker run -p 5000:5000 danxvv/dockerhub:myfirstpush`