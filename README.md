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

### Documentación
1. [PyMongo](https://api.mongodb.com/python/current/)
2. [Operadores mongo](https://docs.mongodb.com/manual/reference/operator/)
3. [Agregaciones](https://docs.mongodb.com/manual/aggregation/)

### Mostrar bases de datos
```
show dbs
```

### Crear seleccionar una base de datos
```
use nombredb
```

### Eliminar una base de datos seleccionada
```
db.dropDatabase()
```

### Mostrar todas las colecciones de la base de datos
```
show collections
db.getCollectionNames()
```

### Crear una colección (se crea vacia)
```
db.createCollection("nombre_coleccion")
db.coleccion.drop()
```

## CRUD: Insertar, Mostrar, Actualizar y Eliminar
### Inserts (Acepta los datos sin crear una estructura definida y se amolda con el tiempo)
Al hacer cada inserción, mongodb automáticamente generara un ID unico, similar al “auto_increment primary key”, pero este ID es del tipo ObjectId de mongodb y es alfanumérico, muy similar a sha1 o md5. Tambien podemos hacer inserciones mas complejas, todo lo que sea soportado por JSON y por BSON ( el formato de MongoDB, con algunos tipos agregados sobre el original JSON)
```
db.micoleccion.insert({"nombre":"Agustin","apellido":"Ramos","domicilio":"Tabasco"})
db.micoleccion.insert({"nombre":"Sebastian","apellido":"Ramos","domicilio":"Tabasco"})
db.micoleccion.insert({"nombre":"Leonardo","apellido":"Ramos","domicilio":"Tabasco"})
db.micoleccion.insert({"nombre":"Jennifer","apellido":"Jimenez","domicilio":"Tabasco"})
db.micoleccion.insert({"nombre":"Diana","apellido":"Jimenez","domicilio":"Tabasco"})
db.micoleccion.insert({"nombre":"Jeremias","apellido":"Escalante","domicilio":"Quintana Roo"})
```
Insertar muchos
```
db.inventory.insertMany(
[{ _id: 1, item: { name: "ab", code: "123" }, qty: 15, tags: [ "A", "B", "C" ] },
{ _id: 2, item: { name: "cd", code: "123" }, qty: 20, tags: [ "B" ] },
{ _id: 3, item: { name: "ij", code: "456" }, qty: 25, tags: [ "A", "B" ] },
{ _id: 4, item: { name: "xy", code: "456" }, qty: 30, tags: [ "B", "A" ] },
{ _id: 5, item: { name: "mn", code: "000" }, qty: 20, tags: [ [ "A", "B" ], "C" ] }]
)
```
### Selects (Muestra todo lo que hay en la colección)
```
db.micoleccion.find()
db.micoleccion.find({"apellido":"Ramos"})
db.micoleccion.find({"_id":ObjectId("56c9a1ffbb6e73925f958b1a")})
```
### Updates (Actualización de registros)
```
db.micoleccion.update({"_id":ObjectId("56c9a1ffbb6e73925f958b1a")},{$set:{"apellido":"Ramos Escalante"}})
```

### Delete (Eliminación de registros)
```
db.micoleccion.remove({"_id":ObjectId("56c9a1ffbb6e73925f958b1a")})
db.micoleccion.remove()
```
No es necesario finalizar las consultas con “;” (punto y coma)
No existe “describe mitabla”: Las colecciones en MongoDB no tienen una “estructura” fijada, por lo que en una colección incluso pueden haber registros que tengan ciertos “campos” y otros no, dicho esto, no se puede hacer una descripción de la colección.

### Otros códigos
```
// $or
db.inventory.find({$or: [{qty: {$gt: 25}}, {qty: {$lte: 15}}]})

// $gte
db.inventory.find({qty: {$gte: 25}})

// $size
db.inventory.find({tags: {$size: 2}})

db.survey.insertMany([
{ _id: 1, results: [ { product: "abc", score: 10 }, { product: "xyz", score: 5 } ] }
{ _id: 2, results: [ { product: "abc", score: 8 }, { product: "xyz", score: 7 } ] }
{ _id: 3, results: [ { product: "abc", score: 7 }, { product: "xyz", score: 8 } ] }
])

db.survey.find(
   { results: { $elemMatch: { product: "xyz", score: { $gte: 8 } } } }
)
db.survey.find(
   { results: { $elemMatch: { product: "xyz" } } }```
```

### Operadores comunes
```
$addToSet
```

## Índices en Mongo
Tipos de índices:
1. De un solo campo (Cuando nos interesa un campo)
2. Compuestos 
3. Multi-llave
4. Geoespaciales (Querys con Latitud y longitud, por geoposicionamiento)
5. De texto (Busque da de texto)
6. Hashed (Convertir valores en hash)
### Ver los índices
```
db.cursos.getIndexes()
```
### Crear índices
```
db.cursos.createIndex({"nombre": "text"})
```
### Hacer consultas
```
db.cursos.find({$text: {$search:"aws"}}, {nombre: 1})
db.cursos.find({$text: {$search:"aws"}})
db.cursos.find({$text: {$search:"aws"}}).pretty()
```

## Apuntes teoricos
1. One to one: Documentos embebidos
2. One to many: Documentos embebidos cuando la información no va a cambiar muy frecuentemente y referencias cuando si.