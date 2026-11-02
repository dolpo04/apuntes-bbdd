Para definir la clave ajena (FK) en una tabla utilizaremos la cláusula `FOREIGN KEY`.

## Sintaxis

```sql
FOREIGN KEY (campo) REFERENCES tablaexterna (campoexterno).
```

## Ejemplo

```sql
CREATE TABLE detalle_pedido(
codigo_pedido int(11),
codigo_producto VARCHAR(15),
cantidad int(11),
precio_unidad decimal(15,2),
numero_linea smallint(6),
PRIMARY KEY (codigo_pedido,codigo_producto),
FOREIGN KEY (codigo_pedido) REFERENCES pedido(id),
FOREIGN KEY (codigo_producto) REFERENCES producto(codigo)
);
```

Cuando definimos una clave ajena tenemos que tener en cuenta que tiene que hacer el SGBD cuando se producen borrados o actualizaciones en las tablas padres.

Las opciones `ON DELETE` y `ON UPDATE` establecen el comportamiento del gestor en caso de que las filas de las tabla padre (es decir, la tabla referenciada en las claves ajenas) se borren o se actualicen. Los comportamientos pueden ser `CASCADE`, `SET NULL` y `NO ACTION`.

Si se usa `NO ACTION` y se intenta un borrado o actualización sobre la tabla padre, la operación se impide, rechazando el borrado o la actualización.

Si se especifica `CASCADE`, la operación se propaga en cascada a la tabla hija, es decir, si se actualiza la tabla padre, se actualizan los registros relacionados de la tabla hija, y si se borra un registro de la tabla padre, se borran aquellos registros de la tabla hija que estén referenciando al registro borrado.

Si se indica `SET NULL`, se establece a `NULL` la clave foránea afectada por un borrado o modificación de la tabla padre.

Si no se especifica `ON DELETE` u `ON UPDATE` por defecto se actúa como `NO ACTION` o `RESTRICT`.

## Ejemplo

```sql
CREATE TABLE pedido(
id int PRIMARY KEY,
fecha date,
observaciones text
);

CREATE TABLE producto (
codigo VARCHAR(15) PRIMARY KEY,
nombre VARCHAR (50),
gama VARCHAR(50),
proveedor varchar(50)
);

CREATE TABLE detalle_pedido(
codigo_pedido int(11),
codigo_producto VARCHAR(15),
cantidad int(11),
precio_unidad decimal(15,2),
numero_linea smallint(6),
PRIMARY KEY (codigo_pedido,codigo_producto),
FOREIGN KEY (codigo_pedido) REFERENCES pedido(id) ON DELETE CASCADE ON UPDATE CASCADE,
FOREIGN KEY (codigo_producto) REFERENCES producto(codigo) ON DELETE NO ACTION ON UPDATE CASDADE
);

INSERT INTO pedido VALUES ( 1, 2024/01/01,’observación 1’);  
INSERT INTO pedido VALUES ( 2, 2024/02/01,’observación 2’);
INSERT INTO pedido VALUES ( 3, 2024/03/01,’observación 3’);

INSERT INTO producto VALUES( ‘ARB01’, ‘olivo’,’árbol’,’Viveros la oliva’);
INSERT INTO producto VALUES(‘PLANT01’,‘jazmín’,’planta’,’Plantación JJ’);
INSERT INTO producto VALUES( ‘PLANT02’, ‘tomillo’,’planta’,’Viveros Felix’);

INSERT INTO detalle_pedido VALUES( 1, ‘ARB01’, 10, 25.50, 1);
INSERT INTO detalle_pedido VALUES( 1, ‘PLANT01’, 60, 5.25, 2);
INSERT INTO detalle_pedido VALUES( 2, ‘ARB01’, 4, 25.5, 1);
```
!!!question "¿que pasaría en estos casos"
    - ¿Podríamos borrar el pedido 1 de la tabla pedido? 
    - ¿Qué ocurre con los pedidos 1 de la tabla detalle_pedido?
    - ¿Podríamos actualizar el pedido 1 de la tabla pedido?
    - ¿Qué ocurre con los pedidos 1 de la tabla detalle_pedido?
    - ¿Podríamos borrar el producto ARB01 de la tabla producto?
    - ¿Qué ocurre con los productos ARB01 de la tabla detalle_pedido?
    - ¿Podríamos actualizar el producto ARB01 de la tabla producto?
    - ¿Qué ocurre con los productos ARB01 de la tabla detalle_pedido?