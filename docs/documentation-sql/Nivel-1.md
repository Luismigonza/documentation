# Actividad Progresiva SQL — Subiendo de Nivel

Esta actividad es con el fin de mejorar nuestras habilidades en SQL

---

## Nivel 1 — Fundamentos (Exploración básica)

Aquí ya aprendiste **SELECT**, **WHERE**, **operadores lógicos** y **NULL**.

### Ejercicio #1

Listar todos los usuarios:

```sql
SELECT * FROM users;
```
Este codigo ayuda a visualizar **TODA** la tabla **usuario**.

---

### Ejercicio #2

Mostrar solo first_name, last_name, email: 

```sql
SELECT first_name, last_name, email FROM users;
```
Este codigo ayuda a llamar tablas en espesifico como: **first_name**, **last_name**, **email**.

---

### Ejercicio #3

Filtrar usuarios cuyo role sea 'admin':

```sql
SELECT * FROM users WHERE role = 'admin';
```
Aqui se trae todos los datos de la tabla **users** pero con la condicion de que tengan el rol **admin**.

---

### Ejercicio #4

Ejercicio 4 Filtrar usuarios con document_type = 'CC':

```sql
SELECT * FROM users 
WHERE document_type = 'CC'
```
En este caso se traen todos los datos de los usuarios con tipo de documento **CC**.

---

### Ejercicio #5

Mostrar usuarios mayores de 18 años (calculando edad desde birth_date):

```sql
SELECT *
FROM users
WHERE TIMESTAMPDIFF(YEAR, birth_date , CURDATE()) >= 18;
```

Esta consulta calcula la edad y filtra a los usuarios **mayores de edad**.

---

### Ejercicio #6

Mostrar usuarios cuyo ingreso sea mayor a 5,000,000:

```sql
SELECT * FROM users 
WHERE monthly_income > 5000000;
```
Filtra los usuarios con **ingresos altos**.

---

### Ejercicio #7

Mostrar usuarios cuyo nombre empiece por "A":

```sql
SELECT * FROM users 
WHERE first_name LIKE 'A%';
```
Usa **LIKE** para filtrar por patrón en los nombres.

---

### Ejercicio #8

Mostrar usuarios que no tengan company:

```sql
SELECT * FROM users 
WHERE company IS NULL;
```

Aquí se filtran los usuarios que **no tienen empresa asignada**.

---

## Nivel 2 — Combinando condiciones (AND / OR)

### Ejercicio #1

Usuarios mayores de 25 años que sean 'employee':

```sql
SELECT * FROM users 
WHERE TIMESTAMPDIFF(YEAR, birth_date , CURDATE()) >= 25 
  AND role = 'employee';
```

Combina edad y rol con **AND**.

---

### Ejercicio #2

Usuarios con 'CC' que estén activos:

```sql
SELECT * FROM users 
WHERE document_type = 'CC' 
  AND is_active = 1;
```

Filtra por **tipo de documento y estado activo**.

---

### Ejercicio #3

Usuarios mayores de edad sin empleo:

```sql
SELECT * FROM users
WHERE TIMESTAMPDIFF(YEAR,
birth_date, CURDATE()) >= 18
  AND role != 'employee';
```

**Combina** mayoría de edad y rol diferente de employee.

---

### Ejercicio #4

Usuarios con empleo y con ingresos mayores a 3,000,000:

```sql
SELECT * FROM users 
WHERE role = 'employee' 
  AND monthly_income > 3000000;
```

Filtra por **rol** y **condición** de ingresos.

---

### Ejercicio #5

Usuarios casados con al menos 1 hijo:

```sql
SELECT * FROM users 
WHERE marital_status = 'Casado' 
  AND children_count > 0;
```

Combina estado **civil** y número de **hijos**.

---

### Ejercicio #6

Usuarios entre 30 y 40 años:

```sql
SELECT * FROM users 
WHERE TIMESTAMPDIFF(YEAR, birth_date, CURDATE()) >= 30 
  AND TIMESTAMPDIFF(YEAR, birth_date , CURDATE()) <= 40;
```

Usa dos condiciones de edad con **AND** para definir un rango.

---

### Ejercicio #7

Usuarios 'admin' verificados mayores de 25 años:

```sql
SELECT * FROM users 
WHERE role = 'admin' 
  AND TIMESTAMPDIFF(YEAR, birth_date, CURDATE()) >= 25 
  AND is_verified = 1;
```

Combina tres condiciones con AND (rol, edad y verificación).

---

## Nivel 3 — Funciones de agregación (COUNT, AVG, GROUP BY)

### Ejercicio #1

Contar usuarios por role:

```sql
SELECT role, COUNT(*) AS total
FROM users
GROUP BY role;
```

Agrupa por rol y cuenta **cuántos** usuarios hay en cada uno.

---

### Ejercicio #2

Contar usuarios por document_type:

```sql
SELECT document_type, COUNT(*) AS total
FROM users
GROUP BY document_type;
```

**Agrupa** por tipo de documento y **cuenta** los registros.

---

### Ejercicio #3

Contar cuántos usuarios están desempleados:

```sql
SELECT COUNT(*) AS total_desempleados
FROM users
WHERE role != 'employee';
```

**Cuenta** los usuarios cuyo rol **no** sea employee.

---

### Ejercicio #4

Calcular el promedio general de ingresos:

```sql
SELECT AVG(monthly_income)
FROM users;
```

Obtiene el **promedio** de ingresos de todos los usuarios.

---

### Ejercicio #5

Calcular el promedio de ingresos por role:

```sql
SELECT role, AVG(monthly_income) AS promedio
FROM users
GROUP BY role;
```

**Agrupa** por rol y **calcula el promedio** de ingresos en cada grupo.

---

## Nivel 4 — HAVING, ORDER BY y análisis comparativo

### Ejercicio #1

Mostrar profesiones con más de 20 personas:

```sql
SELECT profession, COUNT(*) AS total
FROM users
GROUP BY profession
HAVING COUNT(*) > 20;
```

Usa **HAVING** para filtrar después del GROUP BY.

---

### Ejercicio #2

Mostrar la ciudad con más usuarios:

```sql
SELECT city, COUNT(*) AS total
FROM users
GROUP BY city
ORDER BY total DESC
LIMIT 1;
```

**Ordena** de **mayor** a **menor** y muestra solo el primer resultado.

---

### Ejercicio #3

Comparar cantidad de menores vs mayores de edad:

```sql
SELECT
    SUM(TIMESTAMPDIFF(YEAR, birth_date, CURDATE()) >= 18) AS mayores,
    SUM(TIMESTAMPDIFF(YEAR, birth_date, CURDATE()) < 18) AS menores
FROM users;
```

**Suma** condiciones booleanas para comparar grupos.

---

### Ejercicio #4

Promedio de ingresos por ciudad ordenado de mayor a menor:

```sql
SELECT city, AVG(monthly_income) AS promedio
FROM users
GROUP BY city
ORDER BY promedio DESC;
```

**Agrupa** por ciudad y ordena por promedio descendente.

---

### Ejercicio #5

Mostrar las 5 personas con mayor ingreso:

```sql
SELECT first_name, last_name, monthly_income
FROM users
ORDER BY monthly_income DESC
LIMIT 5;
```

**Ordena** por ingresos y limita el resultado.

---

## Nivel 5 — CASE, Subconsultas y Análisis avanzado

### Ejercicio #1

Clasificar usuarios como:

"Menor"

"Adulto"

"Adulto mayor"

Solo mostrar información en la impresión (no afecta la tabla real):

```sql
SELECT 
    id,
    first_name,
    birth_date,
    CASE
        WHEN TIMESTAMPDIFF(YEAR, birth_date, CURDATE()) < 18 THEN 'Menor'
        WHEN TIMESTAMPDIFF(YEAR, birth_date, CURDATE()) BETWEEN 18 AND 64 THEN 'Adulto'
        ELSE 'Adulto mayor'
    END AS categoria_edad
FROM users;
```

Usa **CASE** para crear una clasificación dinámica.

Si quisiera agregar una columna realmente sería:

```sql
ALTER TABLE users ADD COLUMN categoria_edad VARCHAR(20);

UPDATE users
SET categoria_edad = CASE
    WHEN TIMESTAMPDIFF(YEAR, birth_date, CURDATE()) < 18 THEN 'Menor'
    WHEN TIMESTAMPDIFF(YEAR, birth_date, CURDATE()) BETWEEN 18 AND 64 THEN 'Adulto'
    ELSE 'Adulto mayor'
END;
```

---

### Ejercicio #2

Mostrar cuántos usuarios hay en cada clasificación anterior:

```sql
SELECT 
    CASE
        WHEN TIMESTAMPDIFF(YEAR, birth_date, CURDATE()) < 18 THEN 'Menor'
        WHEN TIMESTAMPDIFF(YEAR, birth_date, CURDATE()) BETWEEN 18 AND 64 THEN 'Adulto'
        ELSE 'Adulto mayor'
    END AS categoria_edad,
    COUNT(*) AS total_usuarios
FROM users
GROUP BY categoria_edad
ORDER BY total_usuarios DESC;
```

Agrupa por la clasificación generada con **CASE**.

Ejercicio #3

Ranking de ingresos por ciudad:

```sql
SELECT 
    city,
    monthly_income
FROM users
ORDER BY monthly_income DESC;
```

Ordena los ingresos de **mayor** a **menor**.

---

### Ejercicio #4

Ranking de ingresos por ciudad (sumando):

```sql
SELECT 
    city,
    SUM(monthly_income) AS total_ingresos
FROM users
GROUP BY city
ORDER BY total_ingresos DESC;
```

**Suma** los ingresos por ciudad y ordena.

---

### Ejercicio #5

Cantidad de usuarios y suma de ingresos juntos:

```sql
SELECT 
    city,
    COUNT(*) AS total_usuarios,
    SUM(monthly_income) AS total_ingresos,
    AVG(monthly_income) AS ingreso_promedio
FROM users
GROUP BY city
ORDER BY total_ingresos DESC;
```

Combina **múltiples funciones** de agregación en una sola consulta.

---

### Ejercicio #6

Profesión con mayor ingreso promedio:

```sql
SELECT 
    profession,
    AVG(monthly_income) AS ingreso_promedio
FROM users
GROUP BY profession
ORDER BY ingreso_promedio DESC
LIMIT 1;
```

Encuentra el promedio más alto usando **ORDER BY** y **LIMIT**.

---

### Ejercicio #7

Mostrar usuarios cuyo ingreso esté por encima del promedio general:

```sql
SELECT *
FROM users
WHERE monthly_income > (
    SELECT AVG(monthly_income) 
    FROM users
);
```

Usa una **subconsulta** para comparar contra el promedio global.

### Ejercicio #8

Mostrar usuarios cuyo ingreso esté por encima del promedio general mostrando solo id, nombre e ingresos:

```sql
SELECT id, first_name, last_name, monthly_income
FROM users
WHERE monthly_income > (
    SELECT AVG(monthly_income) 
    FROM users
)
ORDER BY monthly_income DESC;
```

Combina **subconsulta** y **ordenamiento** para análisis más claro.