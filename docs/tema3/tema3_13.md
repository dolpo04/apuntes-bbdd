La forma de actuar será la explicada para las relaciones binarias, dependiendo de la cardinalidad de la relación.

Si hay que añadir la clave principal como clave ajena en la misma tabla, se debe renombrar.

![imgT3_20.png](IMG/imgT3_20.png){.center}

<div class="highlight compact">
<p><strong>TICKET</strong> (<span class="subrayado">id_ticket</span>, tipo, fecha, subtotal, iva, num_tarjeta, id_ticket_devolucion)</p>
<p>PK: id_ticket</p>
<p>FK: id_ticket_devoluacion → TICKET</p>
<p>UK: id_ticket_devolucion</p>
</div>