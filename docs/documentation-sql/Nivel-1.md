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

