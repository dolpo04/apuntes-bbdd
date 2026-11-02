
MySQL permite crear una tabla nueva utilizando como referencia los datos de otra tabla. Para ello, se utiliza la sentencia `CREATE TABLE ... AS SELECT`.

Esta sentencia permite crear una tabla y rellenarla automáticamente con los datos obtenidos de otra tabla.

**Sintaxis:**

```sql
CREATE TABLE nombreNuevaTabla AS
SELECT * FROM nombreTablaOriginal;
```

Aunque todavía no hemos estudiado la sentencia `SELECT`, podemos adelantar algunos de sus elementos:

- `CREATE TABLE nombreNuevaTabla`: indica el nombre de la tabla que queremos crear.
- `AS`: establece que la nueva tabla se creará a partir del resultado de una consulta.
- `SELECT *`: indica que se quieren obtener todas las columnas.
- `FROM nombreTablaOriginal`: indica de qué tabla se obtendrán los datos.

### Ejemplo

Supongamos que tenemos una tabla llamada `alumnos` con la siguiente información:

| id | nombre | apellidos |
|---|---|---|
| 1 | Ana | García López |
| 2 | Luis | Pérez Sánchez |
| 3 | Marta | Ruiz Martín |

Queremos crear una tabla nueva llamada `copia_alumnos` que contenga los mismos datos.

Ejecutamos:

```sql
CREATE TABLE copia_alumnos AS
SELECT * FROM alumnos;
```

Como resultado, MySQL creará la tabla `copia_alumnos` y copiará en ella los registros de `alumnos`.

Las dos tablas tendrán inicialmente la misma información:

**Tabla `alumnos`:**

| id | nombre | apellidos |
|---|---|---|
| 1 | Ana | García López |
| 2 | Luis | Pérez Sánchez |
| 3 | Marta | Ruiz Martín |

**Tabla `copia_alumnos`:**

| id | nombre | apellidos |
|---|---|---|
| 1 | Ana | García López |
| 2 | Luis | Pérez Sánchez |
| 3 | Marta | Ruiz Martín |

### Aspectos importantes

- La tabla de destino no debe existir previamente.
- La tabla original no se modifica.
- Los datos se copian en el momento de ejecutar la sentencia.
- Los cambios posteriores que se realicen en la tabla original no se reflejan automáticamente en la copia.
- Esta sentencia no copia necesariamente todas las restricciones de la tabla original, como las claves primarias, las claves ajenas o las restricciones `UNIQUE`.

**Recuerda:** `CREATE TABLE ... AS SELECT` permite crear una tabla nueva a partir de los datos de otra tabla. Más adelante, cuando estudiemos la sentencia `SELECT`, veremos cómo seleccionar únicamente determinadas columnas o registros para crear tablas con información más específica.