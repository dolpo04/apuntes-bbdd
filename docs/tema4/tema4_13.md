# TIPOS DE DATOS EN SQL

Cuando creamos una tabla en una base de datos, debemos indicar qué tipo de información vamos a almacenar en cada columna. Para ello, utilizamos los **tipos de datos**.

Vamos a clasificar los tipos de datos de MySQL en los siguientes grupos:

## 1. NÚMEROS ENTEROS

Los números enteros permiten almacenar valores numéricos sin decimales, como edades, cantidades, identificadores o unidades de productos.

MySQL dispone de cinco tipos de números enteros:

| Tipo de dato | Tamaño | Rango de valores (SIGNED) |
|---|---:|---|
| `TINYINT` | 1 byte | -128 a 127 |
| `SMALLINT` | 2 bytes | -32.768 a 32.767 |
| `MEDIUMINT` | 3 bytes | -8.388.608 a 8.388.607 |
| `INT` | 4 bytes | -2.147.483.648 a 2.147.483.647 |
| `BIGINT` | 8 bytes | -2⁶³ a 2⁶³-1 |

La diferencia entre ellos es el espacio que ocupan y el rango de números que permiten almacenar.

Por ejemplo:

- `TINYINT`: adecuado para almacenar edades.
- `SMALLINT`: adecuado para cantidades pequeñas.
- `INT`: adecuado para identificadores y cantidades habituales.
- `BIGINT`: adecuado para almacenar números enteros muy grandes.

### SIGNED y UNSIGNED

Los números enteros pueden declararse como `SIGNED` o `UNSIGNED`.

- `SIGNED`: permite almacenar números negativos y positivos. Es el comportamiento predeterminado.
- `UNSIGNED`: permite almacenar únicamente números positivos y el cero. De esta forma, se amplía el rango de valores positivos.

**Ejemplo:**

```sql
CREATE TABLE productos (
    id INT UNSIGNED,
    unidades SMALLINT UNSIGNED,
    temperatura TINYINT
);
```

En este ejemplo:

- `id` almacena números desde 0 hasta 4.294.967.295.
- `unidades` almacena números desde 0 hasta 65.535.
- `temperatura` permite almacenar valores negativos y positivos.

### ZEROFILL

`ZEROFILL` es un atributo que permite mostrar los números completando con ceros a la izquierda hasta alcanzar una anchura determinada.

**Ejemplo:**

```sql
CREATE TABLE codigos (
    numero INT(5) ZEROFILL
);
```

Si introducimos el valor `25`, se mostrará:

```text
00025
```

Si introducimos el valor `123`, se mostrará:

```text
00123
```

Los ceros añadidos no modifican el valor numérico real, únicamente su representación.

**Importante:** `ZEROFILL` está obsoleto en MySQL 8.0. Se recomienda utilizar otras técnicas de formato, como `LPAD()`, cuando sea necesario mostrar números con ceros a la izquierda.

### BIT

El tipo `BIT` permite almacenar información mediante bits, es decir, valores binarios representados por ceros y unos.

Su sintaxis es:

```sql
BIT(M)
```

Donde `M` indica el número de bits que se pueden almacenar, entre 1 y 64.

**Ejemplo:**

```sql
CREATE TABLE opciones (
    activo BIT(1)
);
```

La columna `activo` permite almacenar un bit, que puede representar dos estados:

- `0`: desactivado.
- `1`: activado.

### BOOL y BOOLEAN

Los tipos `BOOL` y `BOOLEAN` se utilizan para representar valores lógicos: verdadero o falso.

En MySQL son sinónimos de `TINYINT(1)`.

- `TRUE` equivale a 1.
- `FALSE` equivale a 0.

**Ejemplo:**

```sql
CREATE TABLE alumnos (
    id INT,
    nombre VARCHAR(50),
    matriculado BOOLEAN
);
```

Podemos almacenar:

```sql
INSERT INTO alumnos VALUES
(1, 'Ana', TRUE),
(2, 'Luis', FALSE);
```

En este ejemplo, indicamos si un alumno está matriculado o no.

Aunque utilizamos `TRUE` y `FALSE`, MySQL almacena realmente los valores numéricos 1 y 0.

## 2. NÚMEROS EN PUNTO FLOTANTE

Los números en punto flotante permiten almacenar números con decimales de forma aproximada.

Se utilizan cuando necesitamos almacenar cantidades que pueden tener decimales y no es imprescindible que el resultado sea completamente exacto.

MySQL dispone de dos tipos principales:

| Tipo de dato | Tamaño | Precisión aproximada |
|---|---:|---|
| `FLOAT` | 4 bytes | 7 cifras significativas. |
| `DOUBLE` | 8 bytes | 15-16 cifras significativas. |

### FLOAT

Permite almacenar números decimales con una precisión aproximada de 7 cifras significativas.

**Ejemplo:**

```sql
CREATE TABLE temperaturas (
    temperatura FLOAT
);
```

Podemos utilizarlo para almacenar temperaturas, mediciones físicas, etc.

### DOUBLE

Permite almacenar números decimales con mayor precisión que `FLOAT`.

**Ejemplo:**

```sql
CREATE TABLE mediciones (
    distancia DOUBLE
);
```

Se utiliza cuando necesitamos una mayor precisión en cálculos científicos o matemáticos.

**Importante:** Los valores `FLOAT` y `DOUBLE` son aproximados. Por tanto, pueden producirse pequeñas diferencias en los resultados de las operaciones matemáticas.

## 3. NÚMEROS EN PUNTO FIJO (VALORES EXACTOS)

Los números en punto fijo permiten almacenar números con decimales de forma exacta.

MySQL dispone de los tipos `DECIMAL` y `NUMERIC`, que son equivalentes.

Su sintaxis es:

```sql
DECIMAL(M,D)
```

Donde:

- `M`: número máximo de cifras totales.
- `D`: número de cifras decimales.

**Ejemplo:**

```sql
CREATE TABLE productos (
    nombre VARCHAR(50),
    precio DECIMAL(8,2)
);
```

En este caso:

- Se pueden almacenar hasta 8 cifras en total.
- Dos de ellas corresponden a la parte decimal.

Podemos almacenar valores como:

```text
1250.50
999999.99
```

### ¿Cuándo se utiliza DECIMAL?

Se utiliza principalmente cuando necesitamos almacenar cantidades que deben ser exactas, como:

- Precios de productos.
- Salarios.
- Impuestos.
- Importes de facturas.

### Diferencia entre FLOAT y DECIMAL

| FLOAT / DOUBLE | DECIMAL |
|---|---|
| Almacenan valores aproximados. | Almacena valores exactos. |
| Se utilizan en cálculos científicos. | Se utilizan en cálculos económicos. |
| Pueden producir pequeñas diferencias de precisión. | Evitan los errores propios de la representación aproximada. |

## 4. FECHAS Y TIEMPO

Los tipos de datos de fecha y tiempo permiten almacenar fechas, horas o ambas.

MySQL dispone de los siguientes tipos:

| Tipo de dato | Formato | Utilización |
|---|---|---|
| `DATE` | AAAA-MM-DD | Almacena una fecha. |
| `TIME` | HH:MM:SS | Almacena una hora o intervalo de tiempo. |
| `DATETIME` | AAAA-MM-DD HH:MM:SS | Almacena una fecha y una hora. |
| `TIMESTAMP` | AAAA-MM-DD HH:MM:SS | Almacena una fecha y hora con conversiones de zona horaria. |
| `YEAR` | AAAA | Almacena un año. |

### DATE

Permite almacenar únicamente fechas.

**Ejemplo:**

```sql
CREATE TABLE alumnos (
    nombre VARCHAR(50),
    fecha_nacimiento DATE
);
```

Un valor válido sería:

```text
2005-04-15
```

### TIME

Permite almacenar horas, minutos y segundos.

**Ejemplo:**

```sql
CREATE TABLE horarios (
    hora_inicio TIME,
    hora_fin TIME
);
```

Un valor válido sería:

```text
08:30:00
```

### DATETIME

Permite almacenar conjuntamente una fecha y una hora.

**Ejemplo:**

```sql
CREATE TABLE eventos (
    nombre VARCHAR(100),
    fecha_hora DATETIME
);
```

Un valor válido sería:

```text
2026-10-30 10:30:00
```

### TIMESTAMP

Permite almacenar una fecha y hora. Una de sus características es que MySQL realiza conversiones entre la zona horaria de la sesión y UTC.

También puede utilizarse para registrar automáticamente cuándo se crea o modifica un registro.

**Ejemplo:**

```sql
CREATE TABLE registros (
    id INT PRIMARY KEY,
    fecha_creacion TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

En este caso, MySQL asignará automáticamente la fecha y hora actuales cuando se inserte un registro.

### YEAR

Permite almacenar un año.

**Ejemplo:**

```sql
CREATE TABLE peliculas (
    titulo VARCHAR(100),
    anio YEAR
);
```

Un valor válido sería:

```text
2025
```

**Importante:** En MySQL se recomienda introducir las fechas utilizando el formato `AAAA-MM-DD`, por ejemplo, `2005-04-15`.

## 5. CADENAS DE CARACTERES

Las cadenas de caracteres permiten almacenar información de tipo texto, como nombres, apellidos, direcciones, correos electrónicos o descripciones.

MySQL dispone de diferentes tipos:

| Tipo de dato | Descripción |
|---|---|
| `CHAR(M)` | Cadena de longitud fija. |
| `VARCHAR(M)` | Cadena de longitud variable. |
| `TINYTEXT` | Texto de hasta 255 bytes. |
| `TEXT` | Texto de hasta 65.535 bytes. |
| `MEDIUMTEXT` | Texto de hasta 16.777.215 bytes. |
| `LONGTEXT` | Texto de hasta 4.294.967.295 bytes. |

### CHAR

Permite almacenar cadenas de caracteres de longitud fija.

**Ejemplo:**

```sql
CREATE TABLE alumnos (
    codigo CHAR(5)
);
```

Si almacenamos el valor `AB12`, MySQL lo completa con espacios hasta alcanzar la longitud definida.

Se utiliza cuando sabemos que los datos tienen una longitud fija.

Por ejemplo:

- Códigos.
- Abreviaturas.
- Identificadores de longitud conocida.

### VARCHAR

Permite almacenar cadenas de caracteres de longitud variable.

**Ejemplo:**

```sql
CREATE TABLE alumnos (
    nombre VARCHAR(50),
    apellidos VARCHAR(100)
);
```

En este caso, el nombre puede tener hasta 50 caracteres y los apellidos hasta 100.

Se utiliza habitualmente para almacenar:

- Nombres.
- Apellidos.
- Direcciones.
- Correos electrónicos.
- Títulos.

### TEXT

Permite almacenar textos más largos que los habituales de `VARCHAR`.

MySQL dispone de cuatro variantes:

| Tipo | Capacidad máxima |
|---|---:|
| `TINYTEXT` | 255 bytes |
| `TEXT` | 65.535 bytes |
| `MEDIUMTEXT` | 16.777.215 bytes |
| `LONGTEXT` | 4.294.967.295 bytes |

**Ejemplo:**

```sql
CREATE TABLE noticias (
    titulo VARCHAR(150),
    contenido TEXT
);
```

En este caso, utilizamos `VARCHAR` para el título y `TEXT` para el contenido de la noticia.

## 6. DATOS BINARIOS

Los tipos de datos binarios permiten almacenar información en forma de bytes, en lugar de cadenas de caracteres.

Se pueden utilizar para almacenar archivos, imágenes, documentos, sonidos y otros contenidos binarios.

MySQL dispone de los siguientes tipos:

| Tipo de dato | Descripción |
|---|---|
| `BINARY(M)` | Cadena binaria de longitud fija. |
| `VARBINARY(M)` | Cadena binaria de longitud variable. |
| `TINYBLOB` | Datos binarios de hasta 255 bytes. |
| `BLOB` | Datos binarios de hasta 65.535 bytes. |
| `MEDIUMBLOB` | Datos binarios de hasta 16.777.215 bytes. |
| `LONGBLOB` | Datos binarios de hasta 4.294.967.295 bytes. |

### BINARY y VARBINARY

Funcionan de forma similar a `CHAR` y `VARCHAR`, pero almacenan datos binarios.

**Ejemplo:**

```sql
CREATE TABLE codigos (
    codigo BINARY(4),
    identificador VARBINARY(100)
);
```

- `BINARY` almacena una cantidad fija de bytes.
- `VARBINARY` almacena una cantidad variable de bytes.

### BLOB

`BLOB` significa *Binary Large Object* (objeto binario grande).

Permite almacenar grandes cantidades de información binaria.

Existen cuatro variantes:

- `TINYBLOB`.
- `BLOB`.
- `MEDIUMBLOB`.
- `LONGBLOB`.

**Ejemplo:**

```sql
CREATE TABLE documentos (
    id INT PRIMARY KEY,
    nombre VARCHAR(100),
    archivo LONGBLOB
);
```

En este caso, la columna `archivo` permite almacenar el contenido binario de un documento o una imagen.

**Diferencia entre TEXT y BLOB:**

- `TEXT` se utiliza para almacenar cadenas de caracteres.
- `BLOB` se utiliza para almacenar datos binarios.


## 7. TIPOS ENUM Y SET

Los tipos `ENUM` y `SET` permiten definir un conjunto de valores posibles para una columna.

La diferencia principal es:

- `ENUM`: permite seleccionar un único valor de la lista.
- `SET`: permite seleccionar uno o varios valores de la lista.

### ENUM

Permite almacenar únicamente uno de los valores definidos previamente.

**Sintaxis:**

```sql
ENUM('valor1', 'valor2', 'valor3')
```

**Ejemplo:**

```sql
CREATE TABLE alumnos (
    nombre VARCHAR(50),
    curso ENUM('1DAW', '2DAW', '1DAM', '2DAM')
);
```

En este caso, la columna `curso` únicamente puede almacenar uno de los cuatro valores definidos.

Podemos insertar:

```sql
INSERT INTO alumnos VALUES
('Ana', '1DAW');
```

No podremos introducir un valor como `3DAW`, porque no está incluido en la lista.

Otros ejemplos de utilización de `ENUM` son:

- Estado de un pedido: pendiente, enviado o entregado.
- Estado de una reserva: confirmada o cancelada.
- Categoría de un producto.

### SET

Permite almacenar uno o varios valores de una lista predefinida.

**Sintaxis:**

```sql
SET('valor1', 'valor2', 'valor3')
```

**Ejemplo:**

```sql
CREATE TABLE usuarios (
    nombre VARCHAR(50),
    permisos SET('lectura', 'escritura', 'eliminacion')
);
```

En este caso, un usuario puede tener uno o varios permisos.

Podemos insertar:

```sql
INSERT INTO usuarios VALUES
('Ana', 'lectura'),
('Luis', 'lectura,escritura'),
('Marta', 'lectura,escritura,eliminacion');
```

Por tanto, un usuario puede tener:

- Solamente permiso de lectura.
- Permisos de lectura y escritura.
- Los tres permisos.

### Diferencias entre ENUM y SET

| Característica | ENUM | SET |
|---|---|---|
| Valores permitidos | Lista predefinida. | Lista predefinida. |
| Número de valores que se pueden seleccionar | Uno. | Uno o varios. |
| Ejemplo | Estado de un pedido. | Permisos de un usuario. |
