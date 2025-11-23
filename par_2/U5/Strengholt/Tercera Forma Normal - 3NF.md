La **Tercera Forma Normal (3NF)** es una regla de diseño de bases de datos que asegura que **todos los datos de una tabla dependan únicamente de su clave principal completa**.

### Definición Sencilla

Una tabla está en 3NF si:

1. **Dependencia Total:** Cada columna (atributo) de la tabla depende de la **clave principal**.
    
2. **No Transitividad:** No hay columnas que dependan de **otras columnas que no son la clave principal**.
    

> [!note] Regla Práctica
> 
> Esto significa que no debes guardar información redundante que no está directamente relacionada con la clave.
> 
> **Ejemplo:** En una tabla de **pedidos**, la **dirección** del cliente no debe estar, porque esa dirección depende del **cliente**, no del pedido específico. Debe ir en una tabla separada de **clientes**.

El objetivo de 3NF es **eliminar la redundancia** (duplicación de datos) y **mejorar la integridad** (facilitar la actualización de los datos).