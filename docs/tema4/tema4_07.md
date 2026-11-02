El comando `ALTER DATABASE´ permite cambiar la BD. Solamente podremos cambiar el juego de caracteres y colación de esta forma 

```sql
ALTER DATABASE jardineria COLLATE latin1_spanish_ci;
```

Con el siguiente comando podemos cosultar configuración de la bd.

```sql
SHOW CREATE DATABASE jardineria;
```
