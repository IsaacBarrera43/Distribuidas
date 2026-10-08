## Objetivo

Aplicar consultas SQL básicas utilizando filtros y operadores de comparación sobre una tabla llamada Automovil.

---

## Consulta 1

Listado de todos los vehículos que tienen capacidad de trasladar a más de 4 pasajeros, incluye los datos de marca, municipio y placa.

### Solución

```sql
SELECT marca, municipio, placa
FROM Automovil
WHERE pasajero > 4;
```

### Resultado esperado

|marca|municipio|placa|
|---|---|---|
|Honda|Tulancingo|HJC124E|
|Toyota|Actopan|HJC133E|
|Honda|Tulancingo|HJC223E|

---

## Consulta 2

Listado de vehículos que trabajan en Actopan, incluye los datos de placa, pasajero, modelo y anio.

### Solución

```sql
SELECT placa, pasajero, modelo, anio
FROM Automovil
WHERE municipio = 'Actopan';
```

### Resultado esperado

|placa|pasajero|modelo|anio|
|---|---|---|---|
|HJC125E|3|Corolla|2023|
|HJC133E|5|Corolla|2024|
|HJC223E|3|Corolla|2021|

---

## Consulta 3

Listado de vehículos cuyo año de inicio de operación sea menor o igual a 2023, incluye los datos de marca, modelo y kilometraje.

### Solución

```sql
SELECT marca, modelo, kilometraje
FROM Automovil
WHERE anio <= 2023;
```

### Resultado esperado

|marca|modelo|kilometraje|
|---|---|---|
|Toyota|Corolla|67921|
|Nissan|Versa|63456|
|Nissan|Versa|83456|
|Honda|City|49832|
|Toyota|Corolla|97921|

---

## Consulta 4

Listado de vehículos cuyo kilometraje sea mayor a 5000 y menor a 65000.

### Solución

```sql
SELECT modelo, anio, kilometraje
FROM Automovil
WHERE kilometraje > 5000
AND kilometraje < 65000;
```

### Resultado esperado

|modelo|anio|kilometraje|
|---|---|---|
|Versa|2024|43456|
|City|2025|9832|
|Versa|2023|63456|
|City|2024|19832|
|Corolla|2024|47921|
|City|2023|49832|

---

## Consulta 5

Listado de vehículos que corresponde verificación en septiembre-octubre.

### Solución

```sql
SELECT marca, municipio, placa
FROM Automovil
WHERE placa LIKE '%7E'
OR placa LIKE '%8E';
```

### Resultado esperado

No se encontraron registros que cumplan la condición.

---

## Conclusión

En esta práctica se utilizaron consultas básicas de SQL empleando SELECT, WHERE y operadores lógicos para filtrar información de acuerdo con distintos criterios.