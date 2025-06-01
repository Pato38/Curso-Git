# Git y herramientas para implementar el control de versiones en aplicaciones para desarrolladores/as
## IPAP 2025

curso: Git y herramientas para implementar el control de versiones en aplicaciones para desarrolladores/as que forma parte del programa de capacitación planificado por el IPAP para garantizar el derecho al desarrollo profesional, mediante una formación integral y de calidad sostenida en el compromiso de la gestión pública. 

Dentro del aula virtual contarán con una serie de herramientas teóricas para poder adquirir estos conocimientos. 


# georef-ar-api
[![Build Status](https://travis-ci.org/datosgobar/georef-ar-api.svg?branch=master)](https://travis-ci.org/datosgobar/georef-ar-api)
![Docs Status](https://readthedocs.org/projects/georef-ar-api/badge/?version=latest)
![](https://img.shields.io/github/license/datosgobar/georef-ar-api.svg)
![](https://img.shields.io/badge/python-3-blue.svg)

API del Servicio de Normalización de Datos Geográficos de Argentina.

## Documentación
Para consultar la documentación de la API, acceder a [https://apis.datos.gob.ar/georef](https://apis.datos.gob.ar/georef).

## Contenedores
Para correr los contenedores asegúrate de tener instalado docker-compose\
El archivo de configuración puede correr dos servicios creando los siguientes contenedores:
- georef-api_es01: Un contenedor con Elasticsearch procesar e indexar los datos. Estos datos son almacenados y persistidos en un volumen de docker.
- georef-api_app: Un contenedor con la aplicación. Al correrlo la primera vez es necesario correr una indexación.

Antes de levantar el servicio de la app deberás generar un archivo config/georef.cfg que puedes hacerlo copiando el que ya existe (docker/georef.example.cfg) y renombrando ciertas variables. 
Tener en cuenta que dentro de la red de docker por defecto el host para el servidor de Elasticsearch es "es01" y el puerto es 9200.\
Las carpetas config/; source/; backups/ y logs/ serán montadas dentro del contenedor de georef-api_app y se podrá acceder desde el host a los archivos generados por la app.

El archivo de configuración docker/georef.example.cfg está preparado para ser copiado al destino config/georef.cfg\
La fuente de datos está configurada para ser leida desde la carpeta source/; pero si se desea se puede cambiar el archivo georef.cfg para especificar otra ruta o una URL.
Si bien se puede copiar los archivos fuente dentro de /source, se recomienda crear un enlace duro; sobre todo si se están haciendo pruebas con el ETL en el mismo entorno de desarrollo.

```
cp -rl /home/georef-etl/files/latest /home/georef-api/source
```
Si se encuentra en otra partición se puede optar por un enlace simbólico:

```
ln /home/georef-etl/files/latest /home/georef-api/source
```

Para correr la aplicación:

Situarse dentro de la carpeta "docker" y correr el siguiente comando:

```
docker-compose up -d
```

Para indexar los archivos generados por el ETL correr el siguiente comando:

```
docker-compose exec app make index
```

Nota: Para más comandos referirse a la documentación (https://datosgobar.github.io/georef-ar-api/georef-api-development/#3-crear-los-indices)

El puerto utilizado por la aplicación es el 5000 y se mapea al mismo puerto del host. Ambos valores pueden ser modificados en el archivo docker-compose.yml

Para realizar consultas a la api se puede hacer una petición desde el host a dicho puerto.

Ejemplo:

```
curl localhost:5000/api/provincias
```

Nota: Para más endpoints referirse a la documentación (https://datosgobar.github.io/georef-ar-api/open-api/)

Si se modifica el código fuente reconstruir la imagen

`docker-compose build app`

## Soporte
En caso de que encuentres algún bug, tengas problemas con la instalación, o tengas comentarios de alguna parte de Georef API, podés mandarnos un mail a [datosargentina@jefatura.gob.ar](mailto:datosargentina@jefatura.gob.ar) o [crear un issue](https://github.com/datosgobar/georef-ar-api/issues/new?title=Encontre-un-bug-en-georef-ar-api).

# links y descripciones de herramientas web para aprender ramas en Git
https://www.w3schools.com/git/git_exercises.asp 
Los ejercicios de Git en W3Schools sirven para practicar y reforzar los comandos básicos de Git, ayudando a los usuarios a aprender a gestionar versiones de código, usar repositorios, hacer commits, branches y merges de forma interactiva.

https://git-school.github.io/visualizing-git/
Visualizing Git es una herramienta interactiva que permite visualizar cómo los comandos de Git afectan al grafo de commits. Al ingresar comandos como git commit, git branch, git merge o git rebase, la aplicación muestra en tiempo real cómo se modifican las ramas y los nodos del repositorio. Esto facilita la comprensión de las operaciones internas de Git, especialmente para quienes están aprendiendo o desean reforzar conceptos complejos

## Recursos
Git- Módulo 1- Git y herramientas libres
Git -Módulo 2- Repositorios y cambios
Git- Actividad intermedia- PARMISANO-1
Qué tan importante es aprender este tipo de herramientas y por qué
Qué tan importante es escribir comentarios en los commits y por qué
La principal diferencia entre Subversion y Git
Comparativa_GitLab_vs_GitHub
