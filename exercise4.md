# Bloque 4. Consultas SQL nivel intermedio

## Objetivo

Aplicar funciones de agregación, agrupamiento de datos y consultas con JOIN para obtener información estadística de la base de datos salesdb.

---

## Consulta 1

Total de pedidos por cliente.

### Solución

```sql
SELECT c.name,
       COUNT(o.orderID) AS total_pedidos
FROM customer c
INNER JOIN customerorder o
ON c.customerID = o.customerID
GROUP BY c.customerID, c.name;
```

### Resultado esperado

Se mostrará el nombre de cada cliente y la cantidad de pedidos que ha realizado.

---

## Consulta 2

Total gastado por cliente.

### Solución

```sql
SELECT c.name,
       SUM(o.total) AS total_gastado
FROM customer c
INNER JOIN customerorder o
ON c.customerID = o.customerID
GROUP BY c.customerID, c.name;
```

### Resultado esperado

Se mostrará el importe total acumulado gastado por cada cliente.

---

## Consulta 3

Productos más caros por proveedor.

### Solución

```sql
SELECT s.name,
       MAX(p.price) AS precio_maximo
FROM supplier s
INNER JOIN product p
ON s.supplierID = p.supplierID
GROUP BY s.supplierID, s.name;
```

### Resultado esperado

Se mostrará el precio máximo de los productos suministrados por cada proveedor.

---

## Consulta 4

Pedidos con más de 3 productos.

### Solución

```sql
SELECT orderID,
       SUM(quantity) AS total_productos
FROM orderproduct
GROUP BY orderID
HAVING SUM(quantity) > 3;
```

### Resultado esperado

Se mostrarán únicamente los pedidos cuya cantidad total de productos sea superior a tres unidades.

---

## Consulta 5

Ventas totales por producto.

### Solución

```sql
SELECT p.name,
       SUM(op.quantity) AS unidades_vendidas
FROM product p
INNER JOIN orderproduct op
ON p.productID = op.productID
GROUP BY p.productID, p.name;
```

### Resultado esperado

Se mostrará la cantidad total vendida de cada producto.

---

## Consulta 6

Clientes que han gastado más de $1000.

### Solución

```sql
SELECT c.name,
       SUM(o.total) AS gasto_total
FROM customer c
INNER JOIN customerorder o
ON c.customerID = o.customerID
GROUP BY c.customerID, c.name
HAVING SUM(o.total) > 1000;
```

### Resultado esperado

Se mostrarán los clientes cuyo gasto acumulado sea superior a 1000.

---

## Consulta 7

Promedio de precio por tipo de producto.

### Solución

```sql
SELECT type,
       AVG(price) AS promedio_precio
FROM product
GROUP BY type;
```

### Resultado esperado

Se mostrará el precio promedio agrupado por cada tipo de producto.

---

## Consulta 8

Proveedores con más de 5 productos.

### Solución

```sql
SELECT s.name,
       COUNT(p.productID) AS cantidad_productos
FROM supplier s
INNER JOIN product p
ON s.supplierID = p.supplierID
GROUP BY s.supplierID, s.name
HAVING COUNT(p.productID) > 5;
```

### Resultado esperado

Se mostrarán los proveedores que suministran más de cinco productos.

---

## Consulta 9

Pedidos con información del cliente.

### Solución

```sql
SELECT o.orderID,
       o.date,
       c.name
FROM customerorder o
INNER JOIN customer c
ON o.customerID = c.customerID;
```

### Resultado esperado

Se mostrará el identificador del pedido, la fecha y el nombre del cliente asociado.

---

## Consulta 10

Clientes sin pedidos.

### Solución

```sql
SELECT c.customerID,
       c.name
FROM customer c
LEFT JOIN customerorder o
ON c.customerID = o.customerID
WHERE o.orderID IS NULL;
```

### Resultado esperado

Se mostrarán los clientes que no tienen pedidos registrados.

---

## Conclusión

En esta práctica se utilizaron funciones de agregación como COUNT, SUM, AVG y MAX, además de GROUP BY, HAVING e INNER JOIN para realizar análisis de información almacenada en diferentes tablas.