# Desarrollo e integracion de Scripts en Python

  

## :wrench:Iniciar MongoDB con Docker

  

![alttext](https://cdn-icons-png.flaticon.com/256/919/919853.png)

  

Si no tienes Docker, [descárgalo e instálalo.](https://www.docker.com/products/docker-desktop/)

  

A continuación abre una terminal (o consola de comandos) y ejecuta el siguiente comando para levantar un contenedor de MongoDB:

  

    docker run -d --name mongo -p 27017:27017 mongo:latest

  

Si quieres verificar que el contenedor está corriendo:

    docker ps

  
  

## :rocket:Ejecución de scripts de Python

  

Para la ejecución de los scripts es necesario tener instalado Python, y algún gestor de paquetes como por ejemplo conda.

Puedes descargar conda [aquí](https://docs.anaconda.com/miniconda/install/#quick-command-line-install).

  

Ya habiendo instalado conda, podremos crear un entorno a partir del exportado presente en el repositorio a través de este comando ejecutado en la terminal.

  

    conda env create -f requirements.yaml

  

Se creará un entorno ya con librerías necesarias para ejecutar los scripts del repositorio.

  
  


### Primer script

  

El primer script presente en el repositorio se encarga de conectarse a una [api]("http://api.citybik.es/v2/networks/bicicorunha") y almacenar los datos extraídos en una base de datos mongo.

Para ejecutar el script en la terminal:

    python script1.py
Para verificar que los datos están insertados correctamente en la terminal escribe. 

    docker exec -it nombre_tu_contenedor mongosh
    use city
    db.bikes.find()

### Segundo script
 El segundo script presente en el repositorio se encargará de pasar los datos de nuestra base de datos mongo a un Dataframe de la librería [pandas](https://pandas.pydata.org/), que podrá ser visto en la consola. Después de esto nuestro Dataframe será exportado a csv y a Parquet. 

  Podremos ejecutar este script con: 

	python script2.py

### :soccer:Tercer script (Parte adicional)
El tercer script presente en el repositorio es una copia del primero, pero utilizando una [api diferente.](https://www.thesportsdb.com/api/v1/json/3/eventslast.php?id=133602). Esta api devolverá los últimos partidos de un equipo, por lo que el script en un supuesto caso de que esté continuamente funcionando, se actualizará cada 3 días (media de días que pasa para que un equipo juegue un partido). El funcionamiento es exactamente igual al primer script, pero creará una base de datos diferente. 
Para ejecutar el script: 

    python script3.py

Para comprobar que los datos están insertados: 

    docker exec -it nombre_tu_contenedor mongosh
    use football
    db.matches.find()

