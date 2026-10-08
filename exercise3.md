# Bloque 3. Consultas SQL nivel básico

## Objetivo

Aplicar consultas básicas sobre la base de datos salesdb utilizando filtros, ordenamiento, límites y relaciones entre tablas.

---

## Consulta 1

Listar todos los clientes.

### Solución

```sql
SELECT customerID, name, email
FROM customer;
```

### Resultado esperado

Se mostrará el identificador, nombre y correo electrónico de todos los clientes registrados.

---

## Consulta 2

Direcciones en una ciudad específica.

### Solución

```sql
SELECT *
FROM address
WHERE city = 'Madrid';
```

### Resultado esperado

Se mostrarán las direcciones registradas en la ciudad de Madrid. Si no existen registros, la consulta devolverá una tabla vacía.

---

## Consulta 3

Productos con precio mayor a 200.

### Solución

```sql
SELECT productID, name, price
FROM product
WHERE price > 200;
```

### Resultado esperado

Se mostrarán los productos cuyo precio sea superior a 200.

---

## Consulta 4

Pedidos ordenados por fecha.

### Solución

```sql
SELECT *
FROM customerorder
ORDER BY date DESC;
```

### Resultado esperado

Se mostrarán todos los pedidos ordenados desde la fecha más reciente hasta la más antigua.

---

## Consulta 5

Primeros 5 proveedores.

### Solución

```sql
SELECT *
FROM supplier
ORDER BY name ASC
LIMIT 5;
```

### Resultado esperado

Se mostrarán los primeros cinco proveedores ordenados alfabéticamente.

---

## Consulta 6

Clientes y su ciudad.

### Solución

```sql
SELECT c.name,
       a.city
FROM customer c
INNER JOIN address a
ON c.addressID = a.addressID;
```

### Resultado esperado

Se mostrará el nombre de cada cliente junto con la ciudad asociada a su dirección.

---

## Consulta 7

Productos y su proveedor.

### Solución

```sql
SELECT p.name AS producto,
       s.name AS proveedor
FROM product p
INNER JOIN supplier s
ON p.supplierID = s.supplierID;
```

### Resultado esperado

Se mostrará el nombre de cada producto junto con su proveedor correspondiente.

---

## Consulta 8

Pedidos realizados por el cliente con customerID = 10.

### Solución

```sql
SELECT *
FROM customerorder
WHERE customerID = 10;
```

### Resultado esperado

Se mostrarán todos los pedidos realizados por el cliente con identificador 10.

---

## Consulta 9

Cantidad de productos en cada pedido.

### Solución

```sql
SELECT orderID,
       COUNT(productID) AS cantidad_productos
FROM orderproduct
GROUP BY orderID;
```

### Resultado esperado

Se mostrará cada pedido junto con la cantidad de productos asociados.

---

## Consulta 10

Clientes con dirección Shipping.

### Solución

```sql
SELECT c.customerID,
       c.name,
       ca.type
FROM customer c
INNER JOIN customeraddress ca
ON c.customerID = ca.customerID
WHERE ca.type = 'Shipping';
```

### Resultado esperado

Se mostrarán los clientes que cuentan con una dirección de tipo Shipping.

---

## Conclusión

Las consultas realizadas permitieron utilizar filtros, ordenamiento de registros, límites de resultados y relaciones entre tablas mediante INNER JOIN.