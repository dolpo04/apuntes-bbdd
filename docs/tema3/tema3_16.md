**INTRODUCCIÓN**

¿Crees que tu base de datos ya podría construirse directamente sobre el SGBD relacional que hayas elegido? La respuesta podría ser afirmativa, pero si queremos que nuestra base de datos funcione con plena fiabilidad, es necesario antes llevar a cabo un proceso de normalización de las tablas que la componen. Así pues, una vez que se ha obtenido el Esquema Relacional del sistema, este debe ser analizado para comprobar que no presenta pérdida de información e inconsistencias. Es la Teoría de la Normalización la que nos permite identificar esos casos y nos muestra la forma de convertir esas tablas a una forma más deseable.

Veamos un ejemplo: en la figura siguiente se muestra una tabla denominada ESCRIBE que almacena datos sobre autores de libros y sobre los propios libros, con una clave primaria formada por: Autor y Cod_libro.

| AUTOR        | NACIONALIDAD      | COD_LIBRO | TITULO             | EDITORIAL   | AÑO  |
|--------------|------------------|----------|--------------------|-------------|------|
| DATE, C.     | NORTE AMERICANA  | 98987    | DATABASES          | ADDISON-W   | 1990 |
| DATE, C.     | NORTE AMERICANA  | 97777    | SQL STANDARD       | ADDISON-W   | 1986 |
| DATE, C.     | NORTE AMERICANA  | 98988    | A GUIDE TO INGRES  | ADDISON-W   | 1988 |
| CODD, E.     | NORTE AMERICANA  | 7980     | RELATIONAL MOD.    | ADDISON-W   | 1990 |
| GARDARIN     | FRANCESA         | 12345    | BASES DE DATOS     | PARANINFO   | 1986 |
| GARDARIN     | FRANCESA         | 67890    | COMPARACION BD     | EYROLLES    | 1984 |
| VALDURIEZ    | FRANCESA         | 67890    | COMPARACION BD     | EYROLLES    | 1984 |
| KIM, W.      | NORTE AMERICANA  | 11223    | 0-0 DATABASES      | ACM PRESS   | 1989 |
| LOCHOVSKY    | CANADIENSE       | 11223    | 0-0 DATABASES      | ACM PRESS   | 1989 |

Si observamos con atención esta tabla, vemos que presenta varios problemas:

Gran cantidad de **redundancia**, ya que la nacionalidad del autor se repite por cada ocurrencia del mismo, y algo análogo sucede, cuando un libro tiene más de un autor, con la editorial y el año de publicación.

**Anomalías de modificación**, ya que, inadvertidamente podemos, por ejemplo, cambiar el nombre de la editorial en una tupla sin modificarlo en el resto de las que corresponden al mismo libro, lo que da lugar a incoherencias.

**Anomalías de inserción**, ya que si se quisiera incluir información sobre algún autor del que no hubiera ningún libro en la base de datos, no sería posible, al formar el atributo `cod_libro` parte de la clave primaria de la tabla, ni tampoco podríamos introducir obras anónimas (la regla de integridad de entidad no permite nulos en ningún atributo que forme parte de una clave primaria). Además, la inserción de un libro que tuviera dos autores obligaría a incluir dos tuplas en la base de datos.

**Anomalías de borrado**, ya que si quisiéramos dar de baja un libro, también se perderían datos sobre sus autores (si estos no habían escrito nada más que un libro) y, viceversa, si borramos un autor desaparecerían de nuestra base de datos los libros escritos por él (a no ser que tuviera el libro más de un autor).

Vemos, por tanto, que la actualización (alta, baja o modificación) de un solo libro o de un solo autor nos puede obligar a actualizar más de una tupla, dejándose la integridad en manos del usuario; además de la falta de eficiencia asociada a estas múltiples actualizaciones.

Esta tabla presenta todos estos problemas, y alguno más, debido a que atenta contra un principio básico en todo diseño: *“hechos distintos se deben almacenar en objetos distintos”*, en este caso, en tablas distintas, con lo que se habrían evitado redundancias y, por tanto, anomalías de actualización.

Si se hubiera seguido la metodología adecuada, realizando un diseño conceptual en el modelo E/R, seguido de una cuidadosa transformación al modelo relacional, se evitarían estos problemas y se obtendría un esquema relacional exento de errores. Sin embargo, ante las posibles dudas respecto a si un determinado esquema relacional es correcto, será preferible aplicar a dicho esquema un método formal de análisis que determine lo que pueda estar equivocado en el mismo y nos permita deducir otro que nos asegure el cumplimiento de ciertos requisitos. Ese método formal es la teoría de la normalización.

**FORMAS NORMALES DE CODD**

La **teoría de la normalización** trata de evitar las redundancias y las anomalías de actualización, obteniendo tablas más estructuradas que no presenten los problemas que comentábamos anteriormente. Así, en lugar de la tabla del ejemplo anterior, se podría haber diseñado el siguiente esquema relacional:

<div class="highlight compact">
<p><strong>LIBRO</strong> (<span class="subrayado">Cod_libro</span>, título, editorial, año)</p>
<p><strong>AUTOR</strong> (<span class="subrayado">Nombre</span>, nacionalidad)</p>
<p><strong>ESCRIBE</strong> (<span class="subrayado">Cod_libro*</span>, Nombre*)
</div>

Uno de los conceptos fundamentales en la normalización es el de **dependencia funcional**. Una dependencia funcional es una relación entre atributos de una misma tabla. Veamos:

Si x e y son atributos de la tabla T, se dice que **y es funcionalmente dependiente de x** (se denota por: x→ y) si cada valor de x tiene asociado un sólo valor de y. Dicho de otra forma, para un determinado valor de x, siempre se dará el mismo y único valor de y.

x e y pueden constar de uno o varios atributos.

A x se le denomina **determinante**, ya que x determina el valor de y.

Se dice que el atributo y es **completamente dependiente** de x si depende funcionalmente de x y no depende de ningún subconjunto de x.

Por ejemplo, podemos decir que el código de un libro determina el título del mismo:

**cod_libro → título**

Ejemplo:

EMPLEADO (NIF, Nombre, Dirección, Fecha-Nac)

En la tabla Empleado, los atributos nombre, dirección y fecha de nacimiento dependen funcionalmente del atributo NIF, porque dado un valor específico de NIF existe sólo un valor correspondiente para cada uno. Esto se representa:

NIF → Nombre

NIF → Dirección

NIF → Fecha-Nac

