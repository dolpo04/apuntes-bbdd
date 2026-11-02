La utilidad principal de un SGBD es su intérprete de comandos. Es una aplicación cliente cuya única misión es enviar comandos al SGBD y mostrar los resultados devueltos por el SGBD en pantalla. El cliente del servidor MySQL (mysql-server) se llama mysql, el de Oracle se llama sqlplus y el de DB2 se llama db2.

Para invocarlos desde el sistema operativo (Windows o Unix), tan solo hay que escribir en un terminal su nombre con ciertas opciones.

Para MySQL, Windows crea un programa cliente MySQL Command-Line. En Ubuntu, abrimos una terminal en la que lo invocamos.

## MySQL: El cliente de MySQL-Server

El comando de conexión para conectarse a MySQL desde el terminal es:

```bash
mysql [options] [database]
```

| Options | Descripción |
|---|---|
| `--help` | Visualiza la ayuda del comando. |
| `-p`, `--password` | Contraseña con la que se conecta. |
| `-P`, `--port` | Puerto TCP/IP remoto al que se conecta. |
| `-h`, `--host` | Nombre del host o dirección IP al que se conecta. |
| `-u`, `--user` | Usuario con el que se conecta. |
| `-S`, `--socket` | Fichero de socket con el que se conecta. |

Por ejemplo si queremos conctarnos con el usuario root y que nos pida la contraseña, sería:

```bash
    mysql -u root -p
```
y automáticamente nos aparecerá:

`Enter password: *********`

A continuación se muestran algunos ejemplos de conexión:

| Comando | Comportamiento |
|---|---|
| `mysql` | Intenta conectarse con el usuario del sistema operativo y sin solicitar explícitamente una contraseña. |
| `mysql -u root` | Intenta conectarse como `root`, sin solicitar explícitamente una contraseña. |
| `mysql -u root -p` | Solicita la contraseña del usuario `root`. |
| `mysql -u usuario -p` | Solicita la contraseña del usuario indicado. |
| `mysql -u usuario -p -h localhost` | Intenta conectarse al servidor local con el usuario indicado y solicita la contraseña. |
| `mysql -u usuario -p -h 192.168.1.100 -P 3306` | Intenta conectarse al servidor remoto indicado, por el puerto 3306, solicitando la contraseña. |
| `mysql -u usuario -p -h 192.168.1.100 miBaseDeDatos -P 3306` | Intenta conectarse al servidor a la base de datos "miBaseDeDatos" del host indicado, por el puerto 3306, solicitando la contraseña. |

Una vez dentro de la terminal todas las sentencias acaban en `;`

```bash
# muestra las bbdd 
SHOW DATABASES;
# Permite seleccionar una bd
USE miBaseDeDatos;
# Muestra las tablas de la bd seleccionada
SHOW TABLES;
# Permite consultar la estructura de una tabla de la bd seleccionada
DESCRIBE nombreTabla;
```

Cuando aparecen estos símbolos en el interprete de comando, normalmente significa que **la instrucción SQL que has empezado a escribir todavía no está completa** y MySQL está esperando que la termines.

### Indicadores del intérprete de MySQL

Durante el uso del cliente de MySQL aparecen diferentes indicadores que permiten conocer el estado de la instrucción introducida.

| Indicador | Descripción |
|---|---|
| `mysql>` | El intérprete está preparado para recibir una nueva instrucción SQL. |
| `->` | La instrucción SQL está incompleta y el intérprete espera que se continúe escribiendo. |
| `'>` | El intérprete espera a que se cierre una comilla simple. |
| `">` | El intérprete espera a que se cierre una comilla doble. |

**Ejemplo:**

Si escribimos una consulta sin terminarla con punto y coma:

```sql
mysql> SELECT * FROM usuarios
    ->
```

MySQL espera a que completemos la instrucción. Para ejecutarla, escribimos el punto y coma (`;`).

Para cancelar una instrucción incompleta, podemos utilizar el comando `\c`:

```sql
mysql> SELECT * FROM usuarios
    -> \c
mysql>
```

Otra forma de ejecutar comandos SQL es almacenarlos en un fichero de texto y mandarlo a ejecución mediante el comando `SOURCE`, que recibe como parámetro un fichero de comandos y ejecuta uno por unos todos los comandos que tenga el fichero:

```sql
#ejecución del script de creación empleados.sql
mysql> SOURCE /home/bbdd/Escritorio/empleados.sql

#ejecución en modo batch
$mysql -u root -p < empleados.sql
```

Estos ficheros de texto que contienen comandos en este caso SQL se les llama SCRIPTS.
