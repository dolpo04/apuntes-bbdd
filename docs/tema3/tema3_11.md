Cuando exista este tipo de dependencia, la clave primaria de la entidad fuerte debe introducirse en la tabla de la entidad débil y formar parte de la clave primaria de ésta, actuando además como clave ajena.

![imgT3_18.png](IMG/imgT3_18.png){.center}

<div class="highlight compact">
<p><strong>TICKET</strong> (<span class="subrayado">id_ticket</span>, tipo, fecha)</p>
<p>PK: id_ticket</p>
<p><strong>LINEAS DE TICKET</strong> (<span class="subrayado">id_linea</span>, cantidad, precio_unitario)</p>
<p>PK: (id_linea, id_ticket)</p>
<p>FK: id_ticket → TICKET</p>
</div>

!!!danger "CUIDADO"
    Fijaros que el **campo derivado** o calculado no se ha pasado al modelo relacional, es decir, no se almacena ya que se calculará a partir de los datos almacenados.
