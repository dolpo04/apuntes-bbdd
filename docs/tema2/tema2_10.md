A continuación se presenta una guía metodológica para crear un diagrama entidad relación a partir de un análisis de requisitos:

1. Leer varias veces el problema.

2. Obtener una lista inicial de candidatos a entidades, relaciones y atributos. Se realiza siguiendo los siguientes consejos:

    - Identificar las entidades. Suelen ser aquello nombres comunes que son importantes para el desarrollo del problema. Por ejemplo, empleado, vehículo, agencia, etc.

    - No hay que obsesionarse en los primeros pasos por distinguir las entidades fuertes de las débiles.

    - Extraer los atributos de cada entidad, identificando aquellos que pueden ser clave. Se suelen distinguir por ser adjetivos asociados a un nombre común seleccionado como entidad. Por ejemplo, color (de un vehículo).

    - Identificar los atributos de las relaciones, si es que los hay. Suelen ser adjetivos también pero aplicables a la relación y no a ninguna de las entidades relacionadas.

    - Si un nombre común aparece pero no tenemos información de él, podrá ser un atributo de otra entidad. Por ejemplo, si aparece el autor de un libro, pero no tenemos información adicional (fecha de nacimiento, nacionalidad, …) será un atributo de la entidad libro.

    - Identificar las relaciones. Se pueden ver extrayendo los verbos del texto del problema. Por ejemplo: agente inmobiliario vende edificio. En este caso, agente inmobiliario y edificio serían las entidades y vender sería la relación.

3. Averiguar las participaciones y cardinalidades. Generalmente se extraen del propio enunciado del problema. Si no vienen especificadas, se elegirá la que almacene mayor cantidad de información en la base de datos.

4. Poner todos los elementos listados en el paso 2 en un esquema (diagrama) y volver a considerar la pertenencia de cada uno de los elementos listados a su categoría.

5. Refinar el diagrama hasta que se eliminen todas las incoherencias posibles repasando los pasos anteriores en caso de encontrar algún atasco o concepto dudoso.