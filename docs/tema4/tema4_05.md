El sublenguaje de SQL que permite la definición de datos es el DDL (Data Definitión Language). Las funciones de este lenguaje son:

- Crear tablas, índices y otros objetos de la base de datos como vistas.

- Definir las estructuras físicas donde se almacenarán los objetos de la base de datos (tablespace, ficheros de datos, etc).

En la sintaxis del lenguaje la palabras reservadas aparecen en mayúsculas y los nombres de los objetos aparecen en minúsculas, también hay que entender la diferente simbología, común a otros lenguajes, que nos indican modificadores opcionales, alternativos, obligatorios etc.

**Veamos un ejemplo**

```sql
SELECT [ALL | DISTINCT] columna1 [columna2, columna3,.......] | *
FROM tabla1 [tabla2, tabla3, ….]
[WHERE condición ]
[ORDER BY expr1 [DESC | ASC] [, expr2 [DESC | ASC] ....]
```

| Símbolo | Descripción |
|---|---|
| MAYÚSCULAS | Palabra reservada de SQL. |
| minúsculas | Variable que hay que sustituir por un dato concreto. |
| `[ ]` | Indica que un elemento es opcional. |
| `|` | Separa opciones alternativas. |
| `[ | ]` | Permite elegir uno de los valores indicados; la elección es opcional. |
| `{ }` | Obliga a elegir uno de los valores indicados. |
| `…` | Indica un número variable de datos. |

DDL tiene 3 instrucciones básicas:

- **CREATE tipo_objeto Nombre Definición**. Crea un objeto de una determinado tipo (DATABASE, TABLE, INDEX, etc) con un nombre y una definición.

- **DROP tipo_objeto Nombre**. Elimina un tipo de objeto especificado mediante un nombre. Por ejemplo la sentencia DROP TABLE actores borraría de la base de datos la tabla actores y todos sus datos.

- **ALTER tipo_objeto Nombre Modificación**. Modifica la definición de un objeto. Por ejemplo, la sentencia ALTER TABLE actores DROP COLUMN  fecha, eliminaría la columna fecha de la tabla Actores.
