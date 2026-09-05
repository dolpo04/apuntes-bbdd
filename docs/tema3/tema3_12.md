Se crea una nueva tabla con la unión de las claves primarias de las entidades relaciones. Si una de las entidades tiene cardinalidad máxima 1, se queda fuera de la PK, con la única salvedad que la PK tiene que estar formada como mínimo por dos campos en el caso 1:1:N la PK de la nueva tabla está formada por la PK de la parte del muchos y una de la PK (la que queramos) de la parte del 1.
Se crean tantas claves ajenas como entidades relacionadas.

![imgT3_19.png](IMG/imgT3_19.png){.center}

<div class="highlight compact">
<p><strong>CLIENTE</strong> (<span class="subrayado">dni</span>, nombre)</p>
<p>PK: dni</p>
<p><strong>PRODUCTO</strong> (<span class="subrayado">codigo</span>, nombre, precio)</p>
<p>PK: codigo</p>
<p><strong>FARMACIA</strong> (<span class="subrayado">codigo</span>, direccion)</p>
<p>PK: codigo</p>
<p><strong>COMPRAR</strong> (<span class="subrayado">dni, cod_prod, cod_far</span>, cantidad</p>
<p>PK: (dni, cod_prod, cod_far)</p>
<p>FK: dni → CLIENTE</p>
<p>FK: cod_prod → PRODUCTO</p>
<p>FK: cod_far → FARMACIA</p>
</div>

