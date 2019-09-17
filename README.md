# Curso de mongo db
Código del curso db.py

# Postman
1. Descargar e instalar [Postman](https://www.getpostman.com/downloads/)
2. La URI de las colecciones de Postman usada para el proyecto está en [Postman-platzi-mongo](https://www.getpostman.com/collections/ffcbfb5c8d5cd2dc52d2)
3. Importar colección dentro de Postman [Instrucciones](https://learning.getpostman.com/docs/postman/collections/data_formats/#exporting-and-importing-postman-data)

## Instalar Anaconda 
La forma más simple de ejecutar el proyecto es instalando [Anaconda](https://www.anaconda.com/distribution/).
```
# navegar hasta el directorio del proyecto
cd platzi-mongo
# crear un nuevo ambiente
conda create --name platzi-mongo
# activar el ambiente 
conda activate platzi-mongo
# para desactivar el ambiente
conda deactivate
```
Si usas Python frecuentemente y tienes una versión 3.3+ no es necesario que 
instales Anaconda, crea un ambiente virtual con venv o virtualenv y sigue con 
el paso de instalar las dependencias.
## Instalar dependenias del proyecto
Con el ambiente activado, instalar las dependencias:
```
pip install -r requirements.txt
```
## Variables de entorno necesarias para ejecutar el proyecto
Asegurate de reemplazar el valor de PLATZI_DB_URI por la URI de tu cluster en MongoDB Atlas
```
Windows es con set
export FLASK_APP=platzi-api
export FLASK_ENV=development 
export PLATZI_DB_URI="MONGO-URI"
```

## Iniciar el servidor de platzi-mongo
```
flask run
```

# Comandos utiles y primeros pasos
1. Servidor online: [Mongo Atlas](https://www.mongodb.com/es/cloud/atlas)
2. Descargar mongo: [Mongo Download Center](https://www.mongodb.com/download-center/community)
3. Agregar la variable de entorno
4. Conectar con la variable de conexión desde https://cloud.mongodb.com

### Mostrar bases de datos
```
show dbs
```

### Crear seleccionar una base de datos
```
use nombredb
```