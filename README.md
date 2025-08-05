# Laboratorio de Seguridad en Bases de Datos (SQL Injection y Control de Accesos)

Este repositorio documenta un conjunto de prácticas realizadas en un entorno seguro con fines educativos. Se abordan aspectos fundamentales de seguridad en bases de datos como: consultas básicas, cifrado y enmascaramiento de datos, control de accesos con permisos, e identificación de vulnerabilidades como la **inyección SQL**.

---

## Contenido del repositorio

| Carpeta | Descripción |
|--------|-------------|
| `01_consultas_basicas/` | Consultas básicas en SQL para explorar tablas y relaciones |
| `02_cifrado_enmascaramiento/` | Ejercicios de cifrado AES, descifrado y enmascaramiento parcial |
| `03_permisos/` | Gestión de usuarios MySQL, asignación y revocación de permisos |
| `04_inyeccion_sql/` | Demostraciones de inyecciones SQL usando entradas sin sanitizar |
| `evidencias/` | Capturas de pantalla de la ejecución de cada actividad |

---

## Tarea 1: Consultas básicas en la base de datos `Secureshop`

- Visualización de datos en las tablas `payment_details`, `customers`, `orders` y `products`.
- Consulta específica por `order_id`.
- Búsqueda de pedidos por nombre del cliente.

Ver carpeta: `01_consultas_basicas/`

---

## Tarea 2: Cifrado y enmascaramiento

- **Cifrado de número telefónico** con `AES_ENCRYPT()`.
- **Descifrado** usando `AES_DECRYPT()`:

```sql
SELECT customer_id, phone, AES_DECRYPT(encrypted_phone, 'clave123') AS decrypted_phone 
FROM customers;
````

* **Enmascaramiento de código postal**: solo muestra los últimos dos dígitos (`***45`, `***00`, etc).

Ver carpeta: `02_cifrado_enmascaramiento/`

---

## Tarea 3: Control de acceso

* Creación del usuario `DeliveryExecutive`.
* Otorgamiento de permisos `SELECT`, `UPDATE`, `DELETE` a la tabla `customers`.
* Revocación del permiso `DELETE`.

Se utilizó:

```sql
GRANT SELECT, UPDATE ON Secureshop.customers TO 'DeliveryExecutive'@'localhost';
REVOKE DELETE ON Secureshop.customers FROM 'DeliveryExecutive'@'localhost';
```

Ver carpeta: `03_permisos/`

---

## Tarea 4: Inyección SQL

Se construyeron consultas **vulnerables a SQL Injection** para demostrar cómo una entrada sin validación puede ser explotada.

### 4.1.1 Consulta vulnerable simple:

```sql
SELECT * FROM orders WHERE order_id = 1 OR 1=1;
```

### 4.1.2 Consulta vulnerable con JOIN:

```sql
SELECT * 
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
WHERE o.order_id = 1 OR 1=1;
```

Ambas muestran resultados no autorizados al manipular la entrada.

Ver carpeta: `04_inyeccion_sql/`

---

## Evidencias

Cada subcarpeta contiene capturas de pantalla nombradas de forma descriptiva:

* `evidencias/inyeccion_simple.png`
* `evidencias/telefono_cifrado.png`
* `evidencias/join_vulnerable.png`
* Etc.

---

## Disclaimer

> Este repositorio fue creado únicamente con fines **educativos**.
> Todas las demostraciones fueron realizadas en un entorno controlado.
> No se promueve ni se autoriza el uso de estos conocimientos con fines maliciosos.

---

## Autor

**Martínez Vega Emiliano**
Egresado de Ingeniería en Comunicaciones y Electrónica
Especializado en Redes y Ciberseguridad
GitHub: [portgasdvega](https://github.com/portgasdvega)

```
