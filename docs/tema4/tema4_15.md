`ALTER TABLE` modifica el diseño de una tabla después de que haya sido creada con la instrucción CREATE TABLE.

## Sintaxis

```sql
ALTER TABLE nombre_tabla
ADD definición_columna [FIRST | AFTER nombre_columna] |
ADD [CONSTRAINT …] PRIMARY KEY (nombre_columna, …) |
ADD [CONSTRAINT …] UNIQUE (nombre_columna, …) |
ADD [CONSTRAINT …] FOREIGN KEY (nombre_columna, …) |
CHANGE [COLUMN] nombre_columna_anterior definición_columna [FIRST | AFTER nombre_columna)]|
RENAME COLUMN anterior_nombre_columna TO nuevo_nombre_columna |
MODIFY definición_columna [FIRST | AFTER nombre_columna]| DROP COLUMNS nombre_columna |
DROP PRIMARY KEY |
DROP FOREIGN KEY fk_nombre |
```

La opción `ADD` permite añadir una columna, se puede especificar el lugar donde se va a insertar mediante las cláusulas `AFTER` (después de una columna) y `FIRST` (laprimera columna). Oracle no admite AFTER ni FIRST.

Con la opción `MODIFY` se cambia el tipo de datos de una columna y se pueden añadir restricciones.

```sql
CREATE TABLE usuario (
id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
nombre VARCHAR(25)
);
ALTER TABLE usuario MODIFY nombre VARCHAR(50) NOT NULL;
```

Con la opción `DROP` se pueden eliminar las restricciones de claves primarias y foráneas, dejando el tipo de dato y su contenido intacto.

Con la opción `CHANGE` permite renombrar una columna, modificar el tipo de dato y sus atributos.

```sql
ALTER TABLE usuario CHANGE nombre usuario VARCHAR(30) DEFAULT ‘usuario’;
```

## Ejemplos:

```sql
CREATE TABLE clientes(
dni VARCHAR(9) PRIMARY KEY,
nombre VARCHAR(50),
direccion VARCHAR(60));

CREATE TABLE mascostas(
codigo INTEGER PRIMARY KEY,
nombre VARCHAR(50),
raza VARCHAR(50));

ALTER TABLE mascotas ADD especie VARCHAR(10) AFTER raza;
ALTER TABLE mascotas ADD cliente VARCHAR(9) AFTER nombre;
ALTER TABLE mascotas ADD CONSTRAINT fk_dueño FOREIGN KEY (cliente) REFERENCES clientes(dni);
ALTER TABLE mascotas MODIFY codigo INT(3) AUTO_INCREMENT;
ALTER TABLE clientes CHANGE nombre nommascosta VARCHAR(50);
```

Se puede agregar o eliminar más de un campo o restricción a la vez, siempre que sea sobre la misma tabla.
