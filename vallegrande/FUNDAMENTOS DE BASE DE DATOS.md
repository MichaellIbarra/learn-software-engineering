## FUNDAMENTOS DE BASE DE DATOS

**Introducción:** Sistemas organizados para almacenar, gestionar y recuperar información de manera eficiente, segura y consistente.

**Por qué se utiliza:** Centralizar datos, evitar redundancia, garantizar integridad, permitir acceso concurrente, facilitar análisis.

**Ventajas:**
- Integridad y consistencia de datos
- Reducción de redundancia
- Acceso concurrente controlado
- Seguridad y permisos
- Backup y recuperación

**Desventajas:**
- Complejidad de configuración
- Costos de licencias y hardware
- Requiere administración especializada
- Posible cuello de botella
- Dependencia del sistema

### Sistema Gestor de Base de Datos

**Qué trata:** Software que permite crear, manipular y administrar bases de datos (DBMS - Database Management System).

**Componentes principales:**
- Motor de almacenamiento
- Procesador de consultas
- Gestor de transacciones
- Gestor de seguridad

**Funciones clave:**
- **DDL (Data Definition Language):** CREATE, ALTER, DROP
- **DML (Data Manipulation Language):** INSERT, UPDATE, DELETE, SELECT
- **DCL (Data Control Language):** GRANT, REVOKE
- **TCL (Transaction Control Language):** COMMIT, ROLLBACK

**Ejemplos de SGBD:**
- **Relacionales:** MySQL, PostgreSQL, Oracle, SQL Server
- **NoSQL:** MongoDB, Cassandra, Redis
- **Cloud:** Amazon RDS, Azure SQL, Google Cloud SQL

**Ejemplo de uso:** PostgreSQL gestionando base de datos de e-commerce con usuarios, productos, pedidos y pagos.

### Análisis, Modelamiento y Diseño de Base de Datos

**Fases del proceso:**

**1. Análisis de Requisitos:**
- **Qué trata:** Identificar qué datos necesita almacenar el sistema
- **Ejemplo:** Entrevistas para sistema escolar - necesita estudiantes, cursos, notas
- **Ejecución:** Documentar entidades, atributos, relaciones, reglas de negocio

**2. Modelo Conceptual (ER - Entidad-Relación):**
- **Qué trata:** Representación gráfica de entidades y sus relaciones
- **Elementos:** Entidades, atributos, relaciones, cardinalidad
- **Ejemplo:** Entidad CLIENTE (id, nombre, email) relacionada 1:N con PEDIDO

**3. Modelo Lógico:**
- **Qué trata:** Transformación del modelo ER a tablas relacionales
- **Normalización:** Aplicar formas normales (1FN, 2FN, 3FN, BCNF)
- **Ejemplo:** CLIENTE(id_cliente PK, nombre, email UNIQUE)

**4. Modelo Físico:**
- **Qué trata:** Implementación en SGBD específico
- **Incluye:** Tipos de datos, índices, particiones, constraints
- **Ejemplo:** 
```sql
CREATE TABLE cliente (
    id_cliente SERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    fecha_registro TIMESTAMP DEFAULT NOW()
);
CREATE INDEX idx_email ON cliente(email);
```

**Ciclo de vida:**
1. Requisitos → 2. Diseño conceptual → 3. Diseño lógico → 4. Diseño físico → 5. Implementación → 6. Mantenimiento

### Gestión consultas con lenguaje SQL

**Qué trata:** Lenguaje estándar para interactuar con bases de datos relacionales.

**Operaciones básicas (CRUD):**

**SELECT (Lectura):**
```sql
-- Consulta simple
SELECT nombre, email FROM clientes WHERE activo = true;

-- Con ordenamiento
SELECT * FROM productos ORDER BY precio DESC LIMIT 10;

-- Agregación
SELECT categoria, COUNT(*) as total, AVG(precio) as promedio
FROM productos GROUP BY categoria HAVING COUNT(*) > 5;
```

**INSERT (Creación):**
```sql
INSERT INTO clientes (nombre, email) 
VALUES ('Juan Pérez', 'juan@email.com');
```

**UPDATE (Actualización):**
```sql
UPDATE productos SET precio = precio * 1.1 
WHERE categoria = 'Electrónica';
```

**DELETE (Eliminación):**
```sql
DELETE FROM pedidos WHERE fecha < '2024-01-01';
```

**Consultas avanzadas:**
- Subconsultas: `SELECT * FROM clientes WHERE id IN (SELECT cliente_id FROM pedidos)`
- UNION: Combinar resultados
- CASE: Lógica condicional
- Window Functions: RANK(), ROW_NUMBER()

**Ejemplo práctico:** Sistema de biblioteca consulta libros disponibles, actualiza estado al prestar, registra historial de préstamos.

### Tipos tecnologías de base de datos: Relacional, NoSQL, Storage y distribuidas

**Base de Datos Relacionales (RDBMS):**
- **Características:** Tablas con esquema fijo, relaciones, ACID
- **Uso:** Sistemas transaccionales, datos estructurados
- **Ejemplos:** PostgreSQL, MySQL, Oracle
- **Ventaja:** Integridad referencial, transacciones
- **Desventaja:** Escalabilidad horizontal limitada

**NoSQL:**

**Documentales:**
- **Características:** Almacenan documentos JSON/BSON
- **Ejemplo:** MongoDB - colecciones de usuarios con estructura flexible
- **Uso:** Aplicaciones web, catálogos de productos

**Clave-Valor:**
- **Características:** Pares key-value simples, muy rápido
- **Ejemplo:** Redis - cache de sesiones, contadores
- **Uso:** Caché, sesiones, configuraciones

**Columnares:**
- **Características:** Datos por columnas, análisis eficiente
- **Ejemplo:** Cassandra, HBase - logs, métricas
- **Uso:** Big data, time series

**Grafos:**
- **Características:** Nodos y relaciones
- **Ejemplo:** Neo4j - redes sociales, recomendaciones
- **Uso:** Relaciones complejas, shortest path

**Storage (Almacenamiento de objetos):**
- **Características:** Archivos/blobs con metadata
- **Ejemplos:** Amazon S3, Azure Blob, Google Cloud Storage
- **Uso:** Imágenes, videos, backups, data lakes

**Distribuidas:**
- **Características:** Datos replicados en múltiples nodos
- **Ejemplos:** Google Spanner, CockroachDB
- **Ventajas:** Alta disponibilidad, escalabilidad
- **Uso:** Aplicaciones globales, alta concurrencia

**Comparación de uso:**
- **E-commerce:** RDBMS (transacciones) + Redis (caché) + S3 (imágenes)
- **Social media:** NoSQL documental (posts) + Grafos (conexiones) + S3 (media)
- **Analytics:** Columnar (procesamiento) + Data Lake (S3)

### Utilización de Joins, Funciones y Procedimientos Almacenados

**JOINS:**

**Qué trata:** Combinar datos de múltiples tablas basándose en relaciones.

**Tipos:**

**INNER JOIN:**
```sql
-- Solo registros con coincidencias en ambas tablas
SELECT c.nombre, p.producto, p.total
FROM clientes c
INNER JOIN pedidos p ON c.id = p.cliente_id;
```

**LEFT JOIN:**
```sql
-- Todos los clientes, incluso sin pedidos
SELECT c.nombre, COUNT(p.id) as total_pedidos
FROM clientes c
LEFT JOIN pedidos p ON c.id = p.cliente_id
GROUP BY c.id, c.nombre;
```

**RIGHT JOIN:** Todos de la derecha, matches de la izquierda

**FULL OUTER JOIN:** Todos los registros de ambas tablas

**CROSS JOIN:** Producto cartesiano

**Ejemplo complejo:**
```sql
SELECT c.nombre, p.producto, d.descripcion, cat.nombre_categoria
FROM clientes c
INNER JOIN pedidos p ON c.id = p.cliente_id
LEFT JOIN detalles d ON p.id = d.pedido_id
INNER JOIN categorias cat ON d.categoria_id = cat.id
WHERE p.fecha >= '2025-01-01'
ORDER BY c.nombre, p.fecha DESC;
```

**FUNCIONES:**

**Funciones de agregación:**
```sql
SELECT 
    COUNT(*) as total,
    SUM(precio) as suma_total,
    AVG(precio) as promedio,
    MIN(precio) as minimo,
    MAX(precio) as maximo
FROM productos;
```

**Funciones de cadena:**
```sql
SELECT 
    UPPER(nombre) as mayusculas,
    LOWER(email) as minusculas,
    CONCAT(nombre, ' - ', email) as completo,
    SUBSTRING(descripcion, 1, 50) as resumen
FROM clientes;
```

**Funciones de fecha:**
```sql
SELECT 
    NOW() as ahora,
    DATE_PART('year', fecha_registro) as año,
    AGE(fecha_nacimiento) as edad,
    DATE_TRUNC('month', created_at) as mes
FROM usuarios;
```

**Funciones personalizadas:**
```sql
CREATE FUNCTION calcular_descuento(precio DECIMAL, porcentaje INT)
RETURNS DECIMAL AS $$
BEGIN
    RETURN precio * (1 - porcentaje/100.0);
END;
$$ LANGUAGE plpgsql;

-- Uso
SELECT producto, calcular_descuento(precio, 15) as precio_descuento
FROM productos;
```

**PROCEDIMIENTOS ALMACENADOS:**

**Qué trata:** Código SQL reutilizable almacenado en el servidor de base de datos.

**Ejemplo completo:**
```sql
-- Crear procedimiento para registrar venta
CREATE PROCEDURE registrar_venta(
    IN p_cliente_id INT,
    IN p_producto_id INT,
    IN p_cantidad INT,
    OUT p_pedido_id INT
)
BEGIN
    DECLARE v_precio DECIMAL(10,2);
    DECLARE v_stock INT;
    
    -- Verificar stock
    SELECT stock, precio INTO v_stock, v_precio
    FROM productos WHERE id = p_producto_id;
    
    IF v_stock >= p_cantidad THEN
        -- Crear pedido
        INSERT INTO pedidos (cliente_id, fecha, total)
        VALUES (p_cliente_id, NOW(), v_precio * p_cantidad);
        
        SET p_pedido_id = LAST_INSERT_ID();
        
        -- Reducir stock
        UPDATE productos 
        SET stock = stock - p_cantidad
        WHERE id = p_producto_id;
        
        COMMIT;
    ELSE
        SIGNAL SQLSTATE '45000' 
        SET MESSAGE_TEXT = 'Stock insuficiente';
    END IF;
END;

-- Ejecutar
CALL registrar_venta(1, 5, 2, @nuevo_pedido);
SELECT @nuevo_pedido;
```

**Ventajas de procedimientos:**
- Reutilización de código
- Mejor rendimiento (pre-compilados)
- Seguridad (encapsulación)
- Lógica de negocio centralizada
- Reducción de tráfico red

**Desventajas:**
- Acoplamiento a SGBD específico
- Difícil de versionar y probar
- Debug más complejo
- Puede sobrecargar el servidor DB

**Ejemplo de uso real:** Sistema bancario usa procedimiento almacenado para transferencias, garantizando atomicidad: debita cuenta origen, acredita cuenta destino, registra movimiento - todo en una transacción.
