Para crear una base de datos se usa el comando `CREATE DATABASE`:

```sql
CREATE {DATABASE | SCHEMA} [IF NOT EXISTS] nombre_db
[espcificacion_create [, especificacion_create] …]

especificacion_create:
[DEFAULT] CHARECTER SET juego_carateres |
[DEFAULT] COLLATE nombre_colacion
```

Por ejemplo, para crear una base de datos Jardinería, en MariaDB, habrá que teclear la instrucción:

```sql
CREATE DATABASE Jardineria CHARACTER SET utf8mb4 COLLATE utf8mb4_spanish_ci;
```

O también:

```sql
CREATE DATABASE IF NOT EXISTS Jardineria CHARACTER SET utf8mb4 COLLATE utf8mb4_spanish_ci;
```

Nótese que el término a elegir puede ser DATABASE o SCHEMA, da lo mismo.

Por otra parte, el parámetro opcional `especificacion_create` permite elegir el juego de caracteres que va a usar la base de datos (utf8mb4, latin1, latin2, etc) y la colación, especifica cómo tratar el alfabeto del juego de caracteres, es decir, cómo se ordena (por ejemplo, la ñ después de la n y no conforme a la tabla de códigos ascii) y cómo se comparan los caracteres (por ejemplo, si Á es igual que á).

Para indicar al SGBD que BD vamos a utilizar (usar) tenemos el siguiete comando:

`USE name_database;`

ejemplo:

```sql
USE jardineria;
```

Otro comando muy útil es el comando `SHOW DATABASES`, muestra un listao con todas las bases de datos a las que tiene acceso el usuario con el que nos hemos conectado a MySQL o MariaDB.

```sql
SHOW DATABASES;
```

```text
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
```

Al ejecutar este comando podemos ver que sin nosotros haber creado ninguna BD tenemos unas que están siempre presentes, *performance_schema, information_schema y mysql*, que almacenan metadatos e información de usuarios y permisos.

| Base de datos | Función principal |
|---|---|
| `information_schema` | Consultar información sobre la estructura de las bases de datos. |
| `mysql` | Gestionar usuarios, permisos y configuración interna. |
| `performance_schema` | Supervisar el rendimiento y el funcionamiento del servidor. |

**Importante:** No debes eliminar ni modificar manualmente estas bases de datos, ya que MySQL las necesita para funcionar correctamente.

Cuando crees tus propias bases de datos, por ejemplo jardineria, estas aparecerán junto a las tres bases de datos del sistema.
