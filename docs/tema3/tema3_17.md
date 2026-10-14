# DICCIONARIO DE DATOS

El objetivo de un Diccionario de Datos es dar precisión semántica sobre los datos que se manejan en la Base de Datos de un sistema de información, evitando así ambigüedades e interpretaciones.

EL Diccionario de Datos recogerá todo el esquema lógico que hemos obtenido del Esquema Entidad-Relación así como las perdidas semánticas que no hemos podido recoger.

El esquema que seguiremos será el siguiente:

| ENTIDADES | CAMPOS | TIPO DE DATOS | RESTRICCIONES | OBSERVACIONES |
|-----------|--------|---------------|---------------|---------------|
|           |        |               |               |               |

ENTIDADES: En esta columna pondremos las todas las entidades que hemos obtenido en el esquema lógico.

CAMPOS: Los campos de cada pertenecen a cada entidad.

TIPO DE DATOS: El dominio o tipo de datos que tiene cada campo.

RESTRICCIONES: Aquí pondremos las Restricciones de cada campo: PK, AK, FK, VNN, UNIQUE, DEFAULT, lista de valores, etc

OBSERVACIONES: Las perdidas semánticas como: CHECK >0 AND < 100 o cualquier información relevante.
