# Bloque 5. Consultas SQL tipo examen

## Objetivo

Resolver consultas SQL utilizando JOIN, GROUP BY, HAVING, subconsultas y funciones de agregación sobre la base de datos salesdb.

---

## RETO 1: Cliente con mayor gasto total

### Solución

```sql
SELECT c.name,
       SUM(o.total) AS total_gastado
FROM customer c
INNER JOIN customerorder o
ON c.customerID = o.customerID
GROUP BY c.customerID, c.name
ORDER BY total_gastado DESC
LIMIT 1;
```

### Resultado esperado

Se mostrará el cliente con el importe total más alto acumulado en pedidos.

---

## RETO 2: Producto más vendido

### Solución

```sql
SELECT p.name,
       SUM(op.quantity) AS unidades_vendidas
FROM product p
INNER JOIN orderproduct op
ON p.productID = op.productID
GROUP BY p.productID, p.name
ORDER BY unidades_vendidas DESC
LIMIT 1;
```

### Resultado esperado

Se mostrará el producto con mayor cantidad de unidades vendidas.

---

## RETO 3: Total de ventas por ciudad

### Solución

```sql
SELECT a.city,
       SUM(o.total) AS total_ventas
FROM customerorder o
INNER JOIN customer c
ON o.customerID = c.customerID
INNER JOIN address a
ON c.addressID = a.addressID
GROUP BY a.city;
```

### Resultado esperado

Se mostrará el total de ventas agrupado por ciudad.

---

## RETO 4: Clientes con más de una dirección

### Solución

```sql
SELECT c.customerID,
       c.name,
       COUNT(ca.addressID) AS total_direcciones
FROM customer c
INNER JOIN customeraddress ca
ON c.customerID = ca.customerID
GROUP BY c.customerID, c.name
HAVING COUNT(ca.addressID) > 1;
```

### Resultado esperado

Se mostrarán los clientes que tienen más de una dirección asociada.

---

## RETO 5: Pedidos con total superior al promedio

### Solución

```sql
SELECT *
FROM customerorder
WHERE total >
(
    SELECT AVG(total)
    FROM customerorder
);
```

### Resultado esperado

Se mostrarán los pedidos con importe mayor al promedio general.

---

## RETO 6: Proveedor con más productos vendidos

### Solución

```sql
SELECT s.name,
       SUM(op.quantity) AS total_vendido
FROM supplier s
INNER JOIN product p
ON s.supplierID = p.supplierID
INNER JOIN orderproduct op
ON p.productID = op.productID
GROUP BY s.supplierID, s.name
ORDER BY total_vendido DESC
LIMIT 1;
```

### Resultado esperado

Se mostrará el proveedor con la mayor cantidad de unidades vendidas.

---

## RETO 7: Clientes que nunca cancelaron pedidos

### Solución

```sql
SELECT DISTINCT c.customerID,
       c.name
FROM customer c
WHERE c.customerID NOT IN
(
    SELECT customerID
    FROM customerorder
    WHERE status = 'Cancelled'
);
```

### Resultado esperado

Se mostrarán los clientes que no tienen pedidos cancelados.

---

## RETO 8: Ingreso total por método de pago

### Solución

```sql
SELECT paymentMethod,
       SUM(total) AS ingreso_total
FROM customerorder
GROUP BY paymentMethod;
```

### Resultado esperado

Se mostrará el ingreso total generado por cada método de pago.

---

## RETO 9: Pedidos con más de un producto distinto

### Solución

```sql
SELECT orderID,
       COUNT(DISTINCT productID) AS productos_distintos
FROM orderproduct
GROUP BY orderID
HAVING COUNT(DISTINCT productID) > 1;
```

### Resultado esperado

Se mostrarán los pedidos que contienen más de un producto diferente.

---

## RETO 10: Clientes con pedidos en más de una ciudad

### Solución

```sql
SELECT c.customerID,
       c.name,
       COUNT(DISTINCT a.city) AS ciudades
FROM customer c
INNER JOIN customeraddress ca
ON c.customerID = ca.customerID
INNER JOIN address a
ON ca.addressID = a.addressID
GROUP BY c.customerID, c.name
HAVING COUNT(DISTINCT a.city) > 1;
```

### Resultado esperado

Se mostrarán los clientes asociados a más de una ciudad.

---

## Conclusión

Esta práctica permitió aplicar subconsultas, agregaciones, agrupación de datos y consultas de nivel intermedio similares a las utilizadas en evaluaciones y escenarios reales. ``