**Atributos Compuestos**

Se transforman en los atributos que los componen. Tenemos dos opciones:

- “Eliminar” el atributo compuesto y considerar todos sus componentes como	atributos simples.
- “Eliminar” los componentes y considerar el atributo compuesto como un único atributo.

**Atributos Multivaluados**

Dan lugar a una nueva tabla cuyo clave principal es el propio campo multivaluado y añadimos una clave ajena a modo relación 1:M.

![imgT3_21.png](IMG/imgT3_21.png){.center}

<div class="highlight compact">
<p><strong>CLIENTE</strong> (<span class="subrayado">dni</span>, nombre, apellidos, direccion, email)</p>
<p>PK: dni</p>
<p><strong>TELEFONO</strong> (<span class="subrayado">numero</span>, dni)</p>
<p>PK: numero </p>
<p>FK: dni → CLIENTE</p>
</div>