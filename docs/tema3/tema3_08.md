## Restricciones de Integridad de Atributo

Sirven para indicar los valores posibles para un atributo o campo. Consiste en la especificación del tipo de dato sobre el que se define un atributo y otras definiciones del atributo (como por ejemplo: un valor por omisión o si permite nulos o no).

No es necesaria una sentencia de creación explícita de la restricción, sino que forma parte de la definición de atributo dentro de la sentencia de creación de la tabla. Su definición puede consistir en la enumeración de valores posibles (Ej: ‘rojo’, ‘amarillo’, ‘verde’) o en una expresión de definición (Ej: horas > 0 AND horas< 100).

Veamos un ejemplo en el estándar SQL:

```SQL
CREATE TABLE Vivienda (…
    color_pared varchar(9) NOT NULL DEFAULT ‘blanco’,
    color_techo varchar(9) ENUM (‘rojo’,’amarillo’,’verde’),
    superficie integer check (superficie > 0 AND superficie < 200)
);
```

Toda restricción de integridad de atributo es comprobada inmediatamente en cualquier intento de inserción de un nuevo valor o de modificación de ese atributo. La respuesta a una violación de la restricción siempre es el rechazo.

En Oracle,

```SQL
CREATE TABLE vivienda (
    color_pared VARCHAR2(9) NOT NULL DEFAULT ‘blanco’,
    color_techo VARCHAR2(9) CHECK(color_techo IN ('rojo','amarillo','verde')),
    superficie integer CHECK (superficie > 0 AND superficie < 200)
);
```

Tipos principales:

- NOT NULL
- PRIMARY KEY
- UNIQUE
- CHECK
- FOREIGN KEY
- DEFAULT

## Restricciones de Integridad de Tabla

Son reglas que se definen dentro de la creación o modificación de una tabla y que afectan a una o varias columnas al mismo tiempo (no solo a una columna individual)

Se declaran usando la sintaxis:

```SQL
CONSTRAINT nombre_restriccion TIPO_RESTRICCION (columnas);
```

Cuando se realiza una operación de modificación sobre una tabla, se chequean previamente todas las RI-Tabla de esa tabla. La respuesta a una violación de la restricción es por defecto el rechazo, aunque en la definición de la restricción se puede especificar la realización de una acción (la cual puede ser la ejecución de un determinado procedimiento).

Ejemplo:

```SQL
CREATE TABLE pedido (
    id INT PRIMARY KEY, -- Restricción a nivel atributo
    id_cliente INT NOT NULL, -- Restrcción a nivel atributo
    fecha_inicio DATE,
    fecha_fin DATE,
    total DECIMAL(10,2),
    -- Restricciones a nivel tabla
    CONSTRAINT fk_pedido_cliente 
        FOREIGN KEY (id_cliente) 
        REFERENCES cliente(id),

    CONSTRAINT chk_fechas 
        CHECK (fecha_fin > fecha_inicio),

    CONSTRAINT chk_total 
        CHECK (total >= 0)
);
```

## Restricciones de Integridad de Base de Datos

Las restricciones a nivel de base de datos son reglas globales que garantizan la integridad entre múltiples tablas y suelen implementarse mediante triggers