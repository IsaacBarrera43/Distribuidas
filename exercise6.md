# Bloque 6. Distribución de datos

## Objetivo

Aplicar técnicas de fragmentación vertical y horizontal utilizando la base de datos salesdb.

---

# Fragmentación Vertical

## Fragmento customerDB

### Esquema del fragmento

Tabla customer

### Script para crear fragmento

```sql
CREATE DATABASE customerDB;
```

### Descargar datos

```sql
SELECT *
FROM customer;
```

### Cargar datos

```sql
INSERT INTO customer
SELECT *
FROM salesdb.customer;
```

---

## Fragmento supplierDB

### Esquema del fragmento

Tabla supplier

### Script para crear fragmento

```sql
CREATE DATABASE supplierDB;
```

### Descargar datos

```sql
SELECT *
FROM supplier;
```

### Cargar datos

```sql
INSERT INTO supplier
SELECT *
FROM salesdb.supplier;
```

---

# Fragmentación Horizontal

## Fragmento zona1DB

Estados:

- CDMX
- Hidalgo

### Script para crear fragmento

```sql
CREATE DATABASE zona1DB;
```

### Descargar datos

```sql
SELECT c.*
FROM customer c
INNER JOIN address a
ON c.addressID = a.addressID
WHERE a.state IN ('CDMX','Hidalgo');
```

### Cargar datos

```sql
INSERT INTO customer
SELECT c.*
FROM salesdb.customer c
INNER JOIN salesdb.address a
ON c.addressID = a.addressID
WHERE a.state IN ('CDMX','Hidalgo');
```

---

## Fragmento zona2DB

Estados:

- Puebla
- Queretaro

### Script para crear fragmento

```sql
CREATE DATABASE zona2DB;
```

### Descargar datos

```sql
SELECT c.*
FROM customer c
INNER JOIN address a
ON c.addressID = a.addressID
WHERE a.state IN ('Puebla','Queretaro');
```

### Cargar datos

```sql
INSERT INTO customer
SELECT c.*
FROM salesdb.customer c
INNER JOIN salesdb.address a
ON c.addressID = a.addressID
WHERE a.state IN ('Puebla','Queretaro');
```

---

## Fragmento zona3DB

Estados:

- Morelos
- Veracruz

### Script para crear fragmento

```sql
CREATE DATABASE zona3DB;
```

### Descargar datos

```sql
SELECT c.*
FROM customer c
INNER JOIN address a
ON c.addressID = a.addressID
WHERE a.state IN ('Morelos','Veracruz');
```

### Cargar datos

```sql
INSERT INTO customer
SELECT c.*
FROM salesdb.customer c
INNER JOIN salesdb.address a
ON c.addressID = a.addressID
WHERE a.state IN ('Morelos','Veracruz');
```

---

## Conclusión

La práctica permitió comprender el funcionamiento de la fragmentación vertical y horizontal, así como la distribución lógica de datos entre diferentes nodos de una base de datos distribuida.