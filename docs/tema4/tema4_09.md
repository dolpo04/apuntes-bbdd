La instrucción `CREATE TABLE` permite definir una tabla nueva, sus campos y los tipos de datos de esos campos.

Sintaxis:

```sql
CREATE [TEMPORARY] TABLE [IF NOT EXISTS][esquema.]tabla (
campo1 tipo [(tamaño)] [NOT NULL | NULL] [DEFAULT valor] [UNIQUE [KEY] |PRIMARY KEY]
[FOREIGN KEY (campo) REFERENCES tablaexterna [(campoexterno1, campoexterno2)]
[ON DELETE {CASCADE | SET NULL | NO ACTION}]
[ON UPDATE {CASCADE | SET NULL | NO ACTION}],
....,
[CONSTRAINT de múltiples campos]
);
```

El token `TEMPORARY` se utiliza para crear tablas temporales, esto es, una tabla invisible al resto de usuarios y que se borrará en el momento de la desconexión del usuario que la creó.

Si se especifica `NOT NULL` para un campo estamos obligando a que dicho campo tome siempre un valor (que sea obligatorio), es decir, que no pueda tomar valores nulos.

Ejemplo:

```sql
CREATE TABLE planta (
nombre CHAR(20) NOT NULL,
proveedor INT NULL
);
```

`DEFAULT` indica el valor por defecto que toma el campo si no es especificado de forma explícita. Por ejemplo, si se declara la siguiente columna:

```sql
CodigoPostal DECIMAL(5,0) NOT NULL DEFAULT 28941
```

Indica que el campo CodigoPostal es un número de 5 dígitos enteros, que no admite valores nulos y que, en caso de no especificarlo en una inserción, el valor que tomará será 28941.

Ejemplo:

```sql
CREATE TABLE planta (
nombre CHAR(20) NOT NULL,
proveedor INT DEFAULT 100
);
```

`PRIMARY KEY` sirve para especificar la creación de una clave primaria a nivel de tabla. Existe la opción de crearla a nivel de columna o al final de la tabla.

Ejemplo: 

```sql
CREATE TABLE planta (
nombre CHAR(20) PRIMARY KEY,
proveedor INT DEFAULT 100
);
```

o

```sql
CREATE TABLE planta (
nombre CHAR(20),
proveedor INT DEFAULT 100,
PRIMARY KEY(nombre)
);
```

Esta última opción es la única que permite crear claves primarias compuestas:

```sql
CREATE TABLE detalle_pedido(
codigo_pedido int(11),
codigo_producto VARCHAR(15),
cantidad int(11),
precio_unidad decimal(15,2),
numero_linea smallint(6),
PRIMARY KEY (codigo_pedido,codigo_producto)
);
```

`UNIQUE KEY` especifica la creación de un índice, esto es, una estructura de datos que permite un acceso rápido a la información de una tabla y, además, controla que no haya ningún valor repetido un el campo. Se utiliza para las claves alternativas. Se producirá un error si se intenta insertar un elemento que ya coincida con un valor anterior. A efectos prácticos, la diferencia con una clave primaria es básicamente que un campo `UNIQUE` puede admitir valores `NULL`, mientras que un campo que se define como clave primaria no admite nulos.

Ejemplo:

```sql
CREATE TABLE mitabla (
id INT PRIMARY KEY,
nombre CHAR(19) UNIQUE 
);
```

`CHECK` permite realizar restricciones sobre una columna.

Ejemplo:

```sql
CREATE TABLE detalle_pedido(
codigo_pedido int(11),
codigo_producto VARCHAR(15),
cantidad int(11) CHECK (catidad >0),
precio_unidad decimal(15,2),
numero_linea smallint(6),
PRIMARY KEY (codigo_pedido,codigo_producto)
);
```

`AUTO_INCREMENT` sirve para indicar que es una columna autonumérica. Su valor se incrementa automáticamente en cada inserción de una fila. Sólo se utiliza en campo de tipo entero.
Ejemplo:

```sql
CREATE TABLE mitabla2 (
id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
nombre CHAR(19) UNIQUE 
);
```
