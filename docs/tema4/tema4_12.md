
La cláusula `CONSTRAINT` permite **asignar un nombre a una restricción** (*constraint*) de una tabla.

Las restricciones son reglas que se establecen sobre las columnas o tablas para garantizar que los datos almacenados cumplen determinadas condiciones.

Por ejemplo, podemos establecer que:

- Una columna no admita valores repetidos (`UNIQUE`).
- Una columna sea la clave primaria de la tabla (`PRIMARY KEY`).
- Una columna haga referencia a la clave primaria de otra tabla (`FOREIGN KEY`).
- Los valores de una columna cumplan una condición (`CHECK`).

### Sintaxis

```sql
CONSTRAINT nombreRestriccion tipoRestriccion
```

Donde:

- `CONSTRAINT`: indica que vamos a definir una restricción.
- `nombreRestriccion`: nombre que asignamos a la restricción.
- `tipoRestriccion`: indica qué tipo de restricción queremos establecer.

El nombre de la restricción debe ser único dentro de la base de datos para aquellas restricciones que requieren un nombre único, como las claves ajenas.

### Ejemplos

**1. Asignar un nombre a una clave primaria**

Creamos una tabla llamada `alumnos` cuya columna `id` será la clave primaria.

```sql
CREATE TABLE alumnos (
    id INT,
    nombre VARCHAR(50),
    apellidos VARCHAR(100),
    CONSTRAINT pk_alumnos PRIMARY KEY (id)
);
```

En este ejemplo:

- `pk_alumnos` es el nombre que hemos asignado a la restricción.
- `PRIMARY KEY (id)` indica que la columna `id` será la clave primaria.

**2. Asignar un nombre a una restricción UNIQUE**

Creamos una tabla llamada `usuarios` en la que el correo electrónico no podrá repetirse.

```sql
CREATE TABLE usuarios (
    id INT,
    nombre VARCHAR(50),
    email VARCHAR(100),
    CONSTRAINT uq_usuarios_email UNIQUE (email)
);
```

La restricción `uq_usuarios_email` impide que dos usuarios tengan el mismo correo electrónico.

**3. Asignar un nombre a una clave ajena (FOREIGN KEY)**

Supongamos que tenemos dos tablas: `autores` y `libros`.

Cada libro pertenece a un autor. Para establecer esta relación, utilizamos una clave ajena:

```sql
CREATE TABLE autores (
    id INT PRIMARY KEY,
    nombre VARCHAR(100)
);

CREATE TABLE libros (
    id INT PRIMARY KEY,
    titulo VARCHAR(150),
    autor_id INT,
    CONSTRAINT fk_libros_autores
        FOREIGN KEY (autor_id)
        REFERENCES autores(id)
);
```

En este ejemplo:

- `fk_libros_autores` es el nombre de la restricción.
- `FOREIGN KEY (autor_id)` indica que `autor_id` es una clave ajena.
- `REFERENCES autores(id)` establece que dicha columna hace referencia a la columna `id` de la tabla `autores`.

De esta forma, no se podrá introducir un libro cuyo `autor_id` haga referencia a un autor que no exista.

**4. Asignar un nombre a una restricción CHECK**

Podemos establecer que la edad de un alumno tenga que ser igual o superior a 18 años.

```sql
CREATE TABLE alumnos (
    id INT PRIMARY KEY,
    nombre VARCHAR(50),
    edad INT,
    CONSTRAINT chk_edad CHECK (edad >= 18)
);
```

La restricción `chk_edad` impide introducir alumnos cuya edad sea inferior a 18 años.

*Nota: MySQL aplica las restricciones `CHECK` a partir de la versión 8.0.16.*

### Convenciones para nombrar restricciones

Aunque podemos elegir libremente el nombre de una restricción, es habitual utilizar prefijos que permitan identificar rápidamente su finalidad.

| Prefijo | Tipo de restricción | Ejemplo |
|---|---|---|
| `pk_` | PRIMARY KEY | `pk_alumnos` |
| `fk_` | FOREIGN KEY | `fk_libros_autores` |
| `uq_` | UNIQUE | `uq_usuarios_email` |
| `chk_` | CHECK | `chk_edad` |

### Eliminar una restricción

Asignar un nombre a una restricción facilita su identificación cuando queremos eliminarla.

Por ejemplo, para eliminar la restricción `uq_usuarios_email` de la tabla `usuarios`, podemos utilizar:

```sql
ALTER TABLE usuarios
DROP INDEX uq_usuarios_email;
```

En MySQL, las restricciones `UNIQUE` se eliminan mediante `DROP INDEX`.

Para eliminar una clave ajena:

```sql
ALTER TABLE libros
DROP FOREIGN KEY fk_libros_autores;
```

Y para eliminar una restricción `CHECK`:

```sql
ALTER TABLE alumnos
DROP CHECK chk_edad;
```

**Recuerda:** La cláusula `CONSTRAINT` no es una restricción por sí misma. Se utiliza para asignar un nombre a una restricción y definir qué regla debe cumplir la tabla o sus columnas.