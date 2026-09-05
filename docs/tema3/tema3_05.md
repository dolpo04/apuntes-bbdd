Las **restricciones de integridad** intentan asegurar que la información contenida en la BD es correcta, es decir, que refleja fielmente la realidad. A continuación introduciremos los tipos de restricciones de integridad más importantes en el modelo relacional y algunas propiedades relacionadas con éstas.

En el modelo relacional, las tablas o relaciones tienen las siguientes propiedades y restricciones:

- Toda tabla ha de poseer una **clave primaria**, la cual tiene las siguientes restricciones:

Los atributos que la componen deben ser mínimos en el sentido de que la eliminación de cualquiera de ellos le haría perder su carácter identificador.

No pueden existir dos tuplas de una misma tabla con valores idénticos en su clave primaria (Restricción de integridad de clave).

- El orden de las tuplas es irrelevante.

- El orden de los atributos es irrelevante.

Todo atributo tiene un **tipo de dato** asociado, un conjunto de valores sobre los que toma un valor (dominio). Cuando definimos una tabla, especificaremos el tipo de dato correspondiente a cada uno de sus campos o atributos; a partir de entonces, ese campo o atributo:

- No podrá contener dos o más valores distintos para una misma ocurrencia, es decir, cada atributo puede tomar un único valor, en un momento y ocurrencia determinados. (Evidentemente, ese valor sí podrá cambiar a lo largo del tiempo).

- No podrá contener un valor perteneciente a un tipo de dato distinto del especificado.
