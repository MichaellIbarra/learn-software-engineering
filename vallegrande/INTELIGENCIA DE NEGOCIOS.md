## INTELIGENCIA DE NEGOCIOS

**¿De qué trata?**
- Transformación de datos en información accionable para toma de decisiones
- Análisis, visualización y reporteo de datos empresariales
- Identificación de patrones, tendencias y oportunidades de negocio
- Combinación de tecnología, procesos y conocimiento del negocio

**¿Por qué se utiliza?**
- Tomar decisiones basadas en datos, no en intuición
- Identificar oportunidades de crecimiento y mejora
- Detectar problemas antes de que se agraven
- Optimizar operaciones y reducir costos
- Mejorar competitividad en el mercado
- Predecir comportamientos futuros

**Ventajas/Beneficios:**
- Decisiones más informadas y rápidas
- Visibilidad completa del negocio en tiempo real
- Identificación de tendencias y patrones ocultos
- ROI medible en inversiones
- Mejora de eficiencia operacional
- Ventaja competitiva
- Democratización de datos en la organización

**Desventajas:**
- Inversión inicial significativa (herramientas, infraestructura)
- Requiere calidad de datos consistente
- Curva de aprendizaje para usuarios
- Necesita cultura data-driven en organización
- Mantenimiento continuo de dashboards
- Puede generar parálisis por análisis excesivo
- Riesgo de interpretación incorrecta de datos

**Componentes de BI:**

**1. Fuentes de Datos**
- Bases de datos transaccionales (OLTP)
- CRM, ERP, sistemas legacy
- Archivos (CSV, Excel, JSON)
- APIs y servicios web
- Logs de aplicaciones
- Redes sociales
- IoT y sensores

**2. ETL (Extract, Transform, Load)**
- Extracción de datos de múltiples fuentes
- Transformación y limpieza
- Carga en Data Warehouse

**3. Data Warehouse (DWH)**
- Repositorio centralizado de datos históricos
- Optimizado para consultas analíticas (OLAP)
- Esquemas: Star Schema, Snowflake Schema

**4. Data Mart**
- Subconjunto del DWH enfocado en área específica
- Ventas, Finanzas, Marketing, etc.

**5. Herramientas de Análisis y Visualización**
- Power BI, Tableau, QlikSense
- Excel, Google Sheets
- Python (Pandas, Matplotlib), R

**6. Reportes y Dashboards**
- KPIs y métricas clave
- Visualizaciones interactivas
- Alertas automáticas

**Arquitectura Típica de BI:**
```
┌─────────────────────────────────────┐
│      FUENTES DE DATOS               │
│  [ERP] [CRM] [DB] [API] [Excel]     │
└──────────────┬──────────────────────┘
               │
               ↓
┌──────────────────────────────────────┐
│           ETL PROCESS                │
│  Extract → Transform → Load          │
└──────────────┬───────────────────────┘
               │
               ↓
┌──────────────────────────────────────┐
│       DATA WAREHOUSE                 │
│  ┌────────┐  ┌────────┐  ┌────────┐ │
│  │Sales DM│  │Finance │  │Marketing│ │
│  │        │  │Data    │  │Data Mart│ │
│  └────────┘  └────────┘  └────────┘ │
└──────────────┬───────────────────────┘
               │
               ↓
┌──────────────────────────────────────┐
│    CAPA DE ANÁLISIS Y BI             │
│  [Power BI] [Tableau] [Qlik]         │
└──────────────┬───────────────────────┘
               │
               ↓
┌──────────────────────────────────────┐
│     USUARIOS DE NEGOCIO              │
│  Ejecutivos, Analistas, Gerentes     │
└──────────────────────────────────────┘
```

**KPIs Comunes por Área:**

**Ventas:**
- Revenue (ingresos totales)
- Conversion Rate (tasa de conversión)
- Average Order Value (AOV)
- Customer Acquisition Cost (CAC)
- Sales by Region/Product/Channel

**Marketing:**
- ROI de campañas
- Cost per Lead (CPL)
- Click-through Rate (CTR)
- Customer Lifetime Value (CLV)
- Engagement metrics

**Finanzas:**
- Profit Margin (margen de ganancia)
- Cash Flow
- Operating Expenses
- Budget vs Actual
- Financial Ratios

**Operaciones:**
- Inventory Turnover
- Order Fulfillment Time
- Defect Rate
- Equipment Utilization
- On-time Delivery %

**Recursos Humanos:**
- Employee Turnover Rate
- Time to Hire
- Training Hours per Employee
- Employee Satisfaction Score
- Productivity Metrics

**Ciclo de Vida de Proyecto BI:**

**1. Definición de Requisitos**
```
- Identificar stakeholders y usuarios
- Definir objetivos de negocio
- Establecer KPIs críticos
- Priorizar casos de uso

Ejemplo:
Objetivo: Reducir costos operativos 15% en 6 meses
KPIs: 
- Gasto por departamento
- Efficiency ratio
- Cost per unit produced
```

**2. Diseño de Data Warehouse**
```
- Modelado dimensional (Star/Snowflake)
- Definir tablas de hechos y dimensiones
- Establecer granularidad

Ejemplo Star Schema:
        ┌──────────┐
        │  Tiempo  │
        └────┬─────┘
             │
┌──────┐    │    ┌─────────┐
│Producto├───┼────┤ HECHOS  │
└──────┘    │    │ Ventas  │
            │    └────┬────┘
┌──────┐    │         │
│Cliente├───┘         │
└──────┘         ┌────┴────┐
                 │ Tienda  │
                 └─────────┘
```

**3. Implementación ETL**
```
- Configurar conexiones a fuentes
- Desarrollar transformaciones
- Programar cargas (diarias, semanales)
- Validar calidad de datos
```

**4. Desarrollo de Reportes/Dashboards**
```
- Diseñar visualizaciones
- Crear métricas y cálculos
- Configurar filtros e interactividad
- Establecer permisos de acceso
```

**5. Despliegue y Capacitación**
```
- Publicar dashboards
- Capacitar usuarios finales
- Documentar procesos
- Establecer soporte
```

**6. Mantenimiento y Evolución**
```
- Monitorear performance
- Actualizar con nuevos requisitos
- Optimizar queries lentos
- Agregar nuevas fuentes de datos
```

**Ejemplo Completo: Dashboard de Ventas**

**Caso de Uso:**
```
Empresa retail necesita monitorear ventas en tiempo real
para tomar decisiones sobre inventario y promociones.

Fuentes de Datos:
- Sistema POS (Point of Sale)
- CRM Salesforce
- Inventario en ERP SAP
- Google Analytics (ventas online)

Frecuencia: Actualización cada hora

KPIs Requeridos:
1. Ventas del día vs objetivo
2. Top 10 productos vendidos
3. Ventas por tienda/canal
4. Margen de ganancia
5. Stock disponible
6. Tendencia ventas últimos 30 días
```

**Dashboard Resultante:**
```
┌─────────────────────────────────────────────────────┐
│          DASHBOARD DE VENTAS - 25 ENE 2026          │
├─────────────────────────────────────────────────────┤
│  Ventas Hoy        Objetivo       Cumplimiento      │
│  $125,450          $150,000       83.6% 🟡          │
├─────────────────────────────────────────────────────┤
│  ┌──────────────────┐  ┌───────────────────────┐   │
│  │ TOP PRODUCTOS    │  │  VENTAS POR CANAL     │   │
│  │ 1. Laptop HP     │  │  ████████░ Online 45% │   │
│  │    $25,450       │  │  ██████░░░ Tiendas 35%│   │
│  │ 2. iPhone 15     │  │  ████░░░░░ Tel 20%    │   │
│  │    $18,200       │  │                       │   │
│  │ 3. Monitor Dell  │  └───────────────────────┘   │
│  │    $12,300       │                              │
│  └──────────────────┘                              │
├─────────────────────────────────────────────────────┤
│  TENDENCIA VENTAS (30 DÍAS)                         │
│     │                    *                          │
│  $  │                 *     *                       │
│  1  │              *           *                    │
│  5  │           *                 *                 │
│  0  │        *                       *              │
│  K  │     *                             *           │
│     └────────────────────────────────────────       │
│      1  5  10  15  20  25  30                      │
│                                                     │
│  Alertas:                                           │
│  🔴 Stock bajo: Monitor Dell (5 unidades)           │
│  🟡 Ventas debajo objetivo 16.4%                    │
└─────────────────────────────────────────────────────┘
```

**Tecnologías en BI:**

**Bases de Datos:**
- **OLAP:** SQL Server Analysis Services, Oracle OLAP
- **Column-store:** Vertica, Amazon Redshift, Snowflake
- **In-memory:** SAP HANA, MemSQL

**ETL Tools:**
- Talend, Informatica PowerCenter
- Microsoft SSIS
- Apache NiFi, Airflow
- Pentaho Data Integration

**Herramientas de Visualización:**
- Power BI, Tableau, QlikSense
- Google Data Studio (Looker Studio)
- Metabase, Superset (open source)

**Lenguajes:**
- SQL (fundamental)
- Python (Pandas, NumPy, Matplotlib)
- R (análisis estadístico)
- DAX (Power BI), MDX (OLAP)

**Cloud BI:**
- AWS QuickSight
- Google BigQuery + Looker
- Azure Synapse Analytics
- Snowflake + Tableau

**Mejores Prácticas:**

1. **Calidad de Datos**
   - Establecer data governance
   - Validaciones en ETL
   - Master Data Management (MDM)

2. **Diseño de Dashboards**
   - Principio de las 5 segundos (comprensión inmediata)
   - Visualización apropiada para cada tipo de dato
   - Evitar clutter (información excesiva)

3. **Performance**
   - Agregaciones precalculadas
   - Índices en tablas de hechos
   - Particionamiento de datos
   - Caching de queries comunes

4. **Seguridad**
   - Row-level security
   - Encriptación de datos sensibles
   - Auditoría de accesos
   - Cumplimiento GDPR/regulaciones

**Roles en Equipo BI:**
- **BI Architect:** Diseño de arquitectura
- **Data Engineer:** Construcción de pipelines ETL
- **BI Developer:** Desarrollo de reportes/dashboards
- **Data Analyst:** Análisis e insights
- **Data Scientist:** Modelos predictivos y ML

**Habilitación:**
1. Identificar objetivos de negocio claros
2. Evaluar calidad y disponibilidad de datos
3. Seleccionar herramientas según presupuesto/necesidad
4. Diseñar arquitectura de datos (DWH)
5. Implementar ETL para fuentes críticas
6. Desarrollar dashboards prioritarios
7. Capacitar usuarios finales
8. Establecer governance y mantenimiento
9. Iterar basado en feedback

---

### Procesamiento de datos: ETL

**¿De qué trata?**
- **Extract, Transform, Load:** Proceso de integración de datos
- Extracción de múltiples fuentes heterogéneas
- Transformación para limpieza, estandarización y enriquecimiento
- Carga en sistema de destino (Data Warehouse, Data Lake)

**¿Por qué se utiliza?**
- Integrar datos de sistemas dispares
- Garantizar calidad y consistencia de datos
- Centralizar información para análisis
- Automatizar flujos de datos
- Mantener históricos para análisis temporal

**Ventajas/Beneficios:**
- Datos limpios y confiables
- Automatización completa (sin intervención manual)
- Escalabilidad para grandes volúmenes
- Trazabilidad de transformaciones
- Recuperación ante errores
- Programación de ejecuciones

**Desventajas:**
- Complejidad en configuración inicial
- Requiere mantenimiento cuando cambian fuentes
- Puede ser lento con grandes volúmenes
- Costo de herramientas enterprise
- Necesita expertise técnico
- Latencia en datos (no siempre tiempo real)

---

**Fases del Proceso ETL:**

### **1. EXTRACT (Extracción)**

**¿De qué trata?**
- Obtener datos de sistemas fuente sin afectar rendimiento
- Soportar múltiples tipos de fuentes

**Tipos de Extracción:**

**a) Full Extraction (Extracción Completa)**
```
- Se extrae toda la información cada vez
- Simple pero ineficiente
- Útil para tablas pequeñas

Ejemplo:
SELECT * FROM productos
```

**b) Incremental Extraction (Extracción Incremental)**
```
- Solo datos nuevos o modificados
- Eficiente para tablas grandes
- Requiere campo de control (timestamp, ID)

Ejemplo:
SELECT * FROM ventas
WHERE fecha_modificacion > '2026-01-24 00:00:00'
```

**c) Change Data Capture (CDC)**
```
- Captura cambios en tiempo real
- Basado en logs de base de datos
- Mínimo impacto en sistema fuente

Tecnologías: Debezium, Oracle GoldenGate
```

**Fuentes de Extracción:**

**Bases de Datos:**
```sql
-- SQL Server
SELECT customer_id, name, email, created_at
FROM customers
WHERE modified_date >= DATEADD(day, -1, GETDATE())

-- PostgreSQL
SELECT product_id, name, price, stock
FROM products
WHERE updated_at > NOW() - INTERVAL '1 day'

-- Oracle
SELECT order_id, customer_id, total, order_date
FROM orders
WHERE TRUNC(order_date) = TRUNC(SYSDATE)
```

**APIs REST:**
```python
import requests
import pandas as pd

# Extraer datos de API Salesforce
response = requests.get(
    'https://api.salesforce.com/services/data/v52.0/query',
    params={'q': 'SELECT Id, Name, Email FROM Contact'},
    headers={'Authorization': f'Bearer {access_token}'}
)
data = response.json()['records']
df = pd.DataFrame(data)
```

**Archivos CSV/Excel:**
```python
import pandas as pd

# CSV
df_csv = pd.read_csv('ventas_enero.csv', encoding='utf-8')

# Excel
df_excel = pd.read_excel('inventario.xlsx', sheet_name='Stock')

# JSON
df_json = pd.read_json('productos.json')
```

**Web Scraping:**
```python
from bs4 import BeautifulSoup
import requests

response = requests.get('https://example.com/products')
soup = BeautifulSoup(response.content, 'html.parser')
products = soup.find_all('div', class_='product')
```

---

### **2. TRANSFORM (Transformación)**

**¿De qué trata?**
- Aplicar reglas de negocio
- Limpiar y estandarizar datos
- Enriquecer con datos adicionales
- Calcular métricas derivadas

**Tipos de Transformaciones:**

**a) Limpieza de Datos (Data Cleansing)**
```python
import pandas as pd

# Eliminar duplicados
df = df.drop_duplicates(subset=['customer_id'])

# Manejar valores nulos
df['phone'].fillna('No disponible', inplace=True)
df['age'].fillna(df['age'].mean(), inplace=True)

# Eliminar espacios en blanco
df['name'] = df['name'].str.strip()

# Corregir tipos de datos
df['price'] = pd.to_numeric(df['price'], errors='coerce')
df['date'] = pd.to_datetime(df['date'], format='%Y-%m-%d')
```

**b) Estandarización**
```python
# Normalizar nombres
df['name'] = df['name'].str.title()

# Estandarizar formatos de teléfono
df['phone'] = df['phone'].str.replace(r'[^\d]', '', regex=True)

# Códigos de país
df['country_code'] = df['country'].map({
    'Perú': 'PE',
    'Peru': 'PE',
    'PERU': 'PE',
    'Chile': 'CL',
    'Brasil': 'BR'
})

# Categorización
def categorize_age(age):
    if age < 18: return 'Menor'
    elif age < 30: return 'Joven'
    elif age < 50: return 'Adulto'
    else: return 'Senior'

df['age_group'] = df['age'].apply(categorize_age)
```

**c) Agregaciones**
```python
# Ventas totales por producto
sales_by_product = df.groupby('product_id').agg({
    'quantity': 'sum',
    'total_amount': 'sum',
    'order_id': 'count'
}).rename(columns={'order_id': 'num_orders'})

# Promedio de ventas por mes
monthly_avg = df.groupby(
    df['order_date'].dt.to_period('M')
)['total_amount'].mean()
```

**d) Joins y Combinaciones**
```python
# Enriquecer ventas con información de clientes
sales_enriched = pd.merge(
    sales_df,
    customers_df,
    on='customer_id',
    how='left'
)

# Múltiples joins
result = sales_df \
    .merge(customers_df, on='customer_id') \
    .merge(products_df, on='product_id') \
    .merge(regions_df, on='region_id')
```

**e) Derivación de Campos**
```python
# Calcular edad desde fecha de nacimiento
from datetime import datetime

df['age'] = (datetime.now() - pd.to_datetime(df['birth_date'])).dt.days // 365

# Margen de ganancia
df['profit_margin'] = ((df['price'] - df['cost']) / df['price']) * 100

# Flag de cliente VIP
df['is_vip'] = df['total_purchases'] > 10000

# Clasificación ABC
def abc_classification(value, total):
    pct = value / total
    if pct >= 0.8: return 'A'
    elif pct >= 0.95: return 'B'
    else: return 'C'
```

**f) Validaciones**
```python
# Validar formato email
import re

def is_valid_email(email):
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return bool(re.match(pattern, str(email)))

df['valid_email'] = df['email'].apply(is_valid_email)

# Validar rangos
df = df[(df['age'] >= 0) & (df['age'] <= 120)]
df = df[df['price'] > 0]

# Validar integridad referencial
valid_customers = df['customer_id'].isin(customers_df['customer_id'])
df_valid = df[valid_customers]
```

**g) Slowly Changing Dimensions (SCD)**
```python
# Tipo 2: Mantener histórico de cambios
def update_dimension_type2(new_record, existing_df):
    # Cerrar registro anterior
    mask = (existing_df['customer_id'] == new_record['customer_id']) & \
           (existing_df['is_current'] == True)
    existing_df.loc[mask, 'end_date'] = datetime.now()
    existing_df.loc[mask, 'is_current'] = False
    
    # Insertar nuevo registro
    new_record['start_date'] = datetime.now()
    new_record['end_date'] = None
    new_record['is_current'] = True
    
    return existing_df.append(new_record, ignore_index=True)
```

---

### **3. LOAD (Carga)**

**¿De qué trata?**
- Insertar datos transformados en destino
- Garantizar integridad y performance

**Estrategias de Carga:**

**a) Full Load (Carga Completa)**
```sql
-- Truncar y recargar toda la tabla
TRUNCATE TABLE dim_productos;

INSERT INTO dim_productos (product_id, name, category, price)
SELECT product_id, name, category, price
FROM staging.productos;
```

**b) Incremental Load (Carga Incremental)**
```sql
-- Solo nuevos registros
INSERT INTO fact_ventas (order_id, customer_id, amount, date)
SELECT order_id, customer_id, amount, date
FROM staging.ventas
WHERE order_id NOT IN (SELECT order_id FROM fact_ventas);
```

**c) Upsert (Update + Insert)**
```sql
-- SQL Server MERGE
MERGE INTO dim_clientes AS target
USING staging.clientes AS source
ON target.customer_id = source.customer_id
WHEN MATCHED THEN
    UPDATE SET 
        name = source.name,
        email = source.email,
        modified_date = GETDATE()
WHEN NOT MATCHED THEN
    INSERT (customer_id, name, email, created_date)
    VALUES (source.customer_id, source.name, source.email, GETDATE());
```

**Python con Pandas:**
```python
from sqlalchemy import create_engine

# Conexión a base de datos
engine = create_engine('postgresql://user:pass@localhost:5432/dwh')

# Carga completa
df.to_sql('dim_productos', engine, if_exists='replace', index=False)

# Carga incremental (append)
df.to_sql('fact_ventas', engine, if_exists='append', index=False)

# Carga batch para mejor performance
df.to_sql('fact_ventas', engine, if_exists='append', 
          index=False, method='multi', chunksize=1000)
```

**Optimizaciones de Carga:**
```python
# Bulk insert
from sqlalchemy.dialects.postgresql import insert

stmt = insert(fact_ventas_table).values(df.to_dict('records'))
conn.execute(stmt)

# Parallel loading
from concurrent.futures import ThreadPoolExecutor

def load_partition(partition_df, table_name):
    partition_df.to_sql(table_name, engine, if_exists='append')

with ThreadPoolExecutor(max_workers=4) as executor:
    partitions = np.array_split(df, 4)
    executor.map(lambda p: load_partition(p, 'fact_ventas'), partitions)
```

---

**Herramientas ETL:**

### **1. Talend Open Studio**
```
Características:
- Open source con versión enterprise
- Interfaz gráfica drag-and-drop
- Generación automática de código Java
- Conectores para 900+ sistemas

Ejemplo Flujo:
[MySQL Source] → [Filter] → [Map] → [Aggregate] → [PostgreSQL Dest]
```

### **2. Microsoft SSIS (SQL Server Integration Services)**
```
Características:
- Nativo de SQL Server
- Visual Studio integration
- Alto rendimiento con datos grandes
- Programación de jobs

Componentes:
- Data Flow Task
- Control Flow
- Event Handlers
- Package Configurations
```

### **3. Apache NiFi**
```
Características:
- Open source, web-based UI
- Data provenance (trazabilidad completa)
- Flow-based programming
- Tiempo real y batch

Procesadores:
- GetFile, PutFile
- ExecuteSQL
- InvokeHTTP
- ConvertRecord
```

### **4. Python (Pandas + Airflow)**
```python
from airflow import DAG
from airflow.operators.python import PythonOperator
from datetime import datetime
import pandas as pd

def extract_data():
    df = pd.read_sql("SELECT * FROM orders", source_conn)
    df.to_csv('/tmp/orders.csv', index=False)

def transform_data():
    df = pd.read_csv('/tmp/orders.csv')
    df['total'] = df['quantity'] * df['price']
    df.to_csv('/tmp/orders_transformed.csv', index=False)

def load_data():
    df = pd.read_csv('/tmp/orders_transformed.csv')
    df.to_sql('fact_orders', dest_conn, if_exists='append')

with DAG('etl_orders', start_date=datetime(2026,1,1), 
         schedule_interval='@daily') as dag:
    
    extract = PythonOperator(task_id='extract', python_callable=extract_data)
    transform = PythonOperator(task_id='transform', python_callable=transform_data)
    load = PythonOperator(task_id='load', python_callable=load_data)
    
    extract >> transform >> load
```

---

**Ejemplo ETL Completo: E-commerce**

**Requisito:**
```
Consolidar datos de ventas de múltiples canales
para análisis unificado en Data Warehouse.

Fuentes:
- Tienda online (MySQL)
- Tiendas físicas (SQL Server)
- Marketplace (API REST)

Destino: Data Warehouse (PostgreSQL)
Frecuencia: Diario a las 2 AM
```

**Implementación Python:**
```python
import pandas as pd
from sqlalchemy import create_engine
import requests
from datetime import datetime, timedelta

# ========== EXTRACT ==========

def extract_online_sales():
    """Extraer ventas de tienda online"""
    engine = create_engine('mysql://user:pass@localhost/ecommerce')
    yesterday = datetime.now() - timedelta(days=1)
    
    query = f"""
    SELECT 
        order_id,
        customer_id,
        product_id,
        quantity,
        price,
        order_date,
        'online' as channel
    FROM orders
    WHERE DATE(order_date) = '{yesterday.date()}'
    """
    
    return pd.read_sql(query, engine)

def extract_physical_sales():
    """Extraer ventas de tiendas físicas"""
    engine = create_engine('mssql://user:pass@server/retail')
    
    query = """
    SELECT 
        sale_id as order_id,
        client_id as customer_id,
        product_code as product_id,
        qty as quantity,
        unit_price as price,
        sale_timestamp as order_date,
        store_id,
        'physical' as channel
    FROM sales
    WHERE CAST(sale_timestamp AS DATE) = CAST(DATEADD(day, -1, GETDATE()) AS DATE)
    """
    
    return pd.read_sql(query, engine)

def extract_marketplace_sales():
    """Extraer ventas de marketplace via API"""
    response = requests.get(
        'https://api.marketplace.com/v1/orders',
        params={
            'date': (datetime.now() - timedelta(days=1)).strftime('%Y-%m-%d'),
            'status': 'completed'
        },
        headers={'Authorization': f'Bearer {API_KEY}'}
    )
    
    data = response.json()['orders']
    df = pd.DataFrame(data)
    
    # Mapear campos
    df = df.rename(columns={
        'id': 'order_id',
        'buyer_id': 'customer_id',
        'item_id': 'product_id',
        'qty': 'quantity',
        'created_at': 'order_date'
    })
    df['channel'] = 'marketplace'
    
    return df[['order_id', 'customer_id', 'product_id', 
               'quantity', 'price', 'order_date', 'channel']]

# ========== TRANSFORM ==========

def transform_sales(df):
    """Limpiar y transformar datos de ventas"""
    
    # 1. Limpiar datos
    df = df.drop_duplicates(subset=['order_id', 'channel'])
    df = df.dropna(subset=['customer_id', 'product_id'])
    
    # 2. Estandarizar tipos
    df['order_id'] = df['order_id'].astype(str)
    df['customer_id'] = df['customer_id'].astype(int)
    df['product_id'] = df['product_id'].astype(str)
    df['quantity'] = df['quantity'].astype(int)
    df['price'] = df['price'].astype(float)
    df['order_date'] = pd.to_datetime(df['order_date'])
    
    # 3. Calcular campos derivados
    df['total_amount'] = df['quantity'] * df['price']
    df['order_year'] = df['order_date'].dt.year
    df['order_month'] = df['order_date'].dt.month
    df['order_day'] = df['order_date'].dt.day
    df['order_weekday'] = df['order_date'].dt.dayofweek
    
    # 4. Validaciones
    df = df[df['quantity'] > 0]
    df = df[df['price'] > 0]
    df = df[df['total_amount'] > 0]
    
    # 5. Enriquecer con dimensiones
    # Obtener info de productos
    products = pd.read_sql("SELECT product_id, category FROM dim_products", dwh_engine)
    df = df.merge(products, on='product_id', how='left')
    
    # Obtener info de clientes
    customers = pd.read_sql("SELECT customer_id, segment FROM dim_customers", dwh_engine)
    df = df.merge(customers, on='customer_id', how='left')
    
    # 6. Generar surrogate key
    df['fact_id'] = range(1, len(df) + 1)
    
    # 7. Agregar metadata
    df['etl_created_at'] = datetime.now()
    df['etl_batch_id'] = f"BATCH_{datetime.now().strftime('%Y%m%d_%H%M%S')}"
    
    return df

# ========== LOAD ==========

def load_to_warehouse(df, table_name='fact_sales'):
    """Cargar datos a Data Warehouse"""
    
    dwh_engine = create_engine('postgresql://user:pass@localhost:5432/dwh')
    
    # Cargar en staging primero
    df.to_sql('staging_sales', dwh_engine, if_exists='replace', index=False)
    
    # Validar integridad en staging
    validation_query = """
    SELECT COUNT(*) as invalid_count
    FROM staging_sales
    WHERE customer_id NOT IN (SELECT customer_id FROM dim_customers)
       OR product_id NOT IN (SELECT product_id FROM dim_products)
    """
    
    invalid = pd.read_sql(validation_query, dwh_engine)['invalid_count'][0]
    
    if invalid > 0:
        raise Exception(f"Found {invalid} records with invalid references")
    
    # Insertar a tabla final
    insert_query = """
    INSERT INTO fact_sales (
        order_id, customer_id, product_id, quantity, price,
        total_amount, order_date, channel, category, segment,
        etl_created_at, etl_batch_id
    )
    SELECT 
        order_id, customer_id, product_id, quantity, price,
        total_amount, order_date, channel, category, segment,
        etl_created_at, etl_batch_id
    FROM staging_sales
    WHERE order_id NOT IN (
        SELECT order_id FROM fact_sales WHERE channel = staging_sales.channel
    )
    """
    
    with dwh_engine.connect() as conn:
        result = conn.execute(insert_query)
        print(f"Inserted {result.rowcount} records")
    
    # Limpiar staging
    with dwh_engine.connect() as conn:
        conn.execute("TRUNCATE TABLE staging_sales")

# ========== ORQUESTACIÓN ==========

def run_etl():
    """Ejecutar proceso ETL completo"""
    
    try:
        print(f"[{datetime.now()}] Starting ETL process...")
        
        # Extract
        print("Extracting data...")
        df_online = extract_online_sales()
        print(f"  - Online: {len(df_online)} records")
        
        df_physical = extract_physical_sales()
        print(f"  - Physical: {len(df_physical)} records")
        
        df_marketplace = extract_marketplace_sales()
        print(f"  - Marketplace: {len(df_marketplace)} records")
        
        # Combinar todas las fuentes
        df_all = pd.concat([df_online, df_physical, df_marketplace], 
                           ignore_index=True)
        print(f"Total extracted: {len(df_all)} records")
        
        # Transform
        print("Transforming data...")
        df_transformed = transform_sales(df_all)
        print(f"After transformation: {len(df_transformed)} records")
        
        # Load
        print("Loading to warehouse...")
        load_to_warehouse(df_transformed)
        
        print(f"[{datetime.now()}] ETL process completed successfully!")
        
    except Exception as e:
        print(f"[{datetime.now()}] ETL process failed: {str(e)}")
        # Enviar alerta
        send_alert(f"ETL failed: {str(e)}")
        raise

if __name__ == "__main__":
    run_etl()
```

**Monitoreo y Logging:**
```python
import logging

# Configurar logging
logging.basicConfig(
    filename=f'etl_{datetime.now().strftime("%Y%m%d")}.log',
    level=logging.INFO,
    format='%(asctime)s - %(levelname)s - %(message)s'
)

def log_etl_metrics(phase, record_count, duration):
    """Registrar métricas del ETL"""
    logging.info(f"Phase: {phase}, Records: {record_count}, Duration: {duration}s")
    
    # Guardar en tabla de auditoría
    metrics = {
        'etl_date': datetime.now(),
        'phase': phase,
        'record_count': record_count,
        'duration_seconds': duration,
        'status': 'SUCCESS'
    }
    
    pd.DataFrame([metrics]).to_sql('etl_audit', dwh_engine, 
                                    if_exists='append', index=False)
```

---

**Mejores Prácticas ETL:**

1. **Idempotencia**
   - ETL debe poder re-ejecutarse sin duplicar datos
   - Usar UPSERT en lugar de solo INSERT

2. **Manejo de Errores**
   - Logging detallado
   - Alertas en caso de fallo
   - Rollback en caso de error

3. **Performance**
   - Procesar en lotes (batch)
   - Índices en campos de join
   - Particionamiento de tablas grandes
   - Paralelización cuando sea posible

4. **Data Quality**
   - Validaciones en cada fase
   - Rechazar registros inválidos
   - Alertar cuando calidad baja de umbral

5. **Metadata y Auditoría**
   - Rastrear origen de cada registro
   - Timestamp de carga
   - Batch ID para agrupación

**Habilitación:**
1. Identificar fuentes de datos
2. Diseñar modelo dimensional destino
3. Seleccionar herramienta ETL
4. Desarrollar mappings de transformación
5. Implementar validaciones de calidad
6. Programar ejecuciones
7. Configurar monitoreo y alertas
8. Documentar procesos

---

### Google Sheet para análisis y visualización de datos

**¿De qué trata?**
- Hojas de cálculo en la nube de Google
- Herramienta colaborativa para análisis de datos
- Alternativa gratuita a Excel con funcionalidades BI
- Integración nativa con ecosistema Google

**¿Por qué se utiliza?**
- Acceso gratuito y desde cualquier dispositivo
- Colaboración en tiempo real (múltiples usuarios)
- Integración fácil con Google Forms, Analytics, Ads
- No requiere instalación
- Actualización automática de datos
- Compartir con permisos granulares

**Ventajas/Beneficios:**
- Gratuito para uso personal y pequeñas empresas
- Colaboración simultánea en tiempo real
- Historial de versiones automático
- Acceso desde web, móvil, tablet
- Funciones y fórmulas potentes
- Add-ons para extender funcionalidad
- Integración Google Apps Script (automatización)
- Gráficos dinámicos e interactivos

**Desventajas:**
- Límite de 10 millones de celdas por hoja
- Performance limitado con datasets grandes (>50k filas)
- Funcionalidades menos avanzadas que Excel
- Requiere conexión a internet
- Privacidad de datos en cloud de Google
- Fórmulas complejas pueden ser lentas
- No reemplaza herramientas BI profesionales

---

**Funcionalidades Principales:**

### **1. Fórmulas y Funciones**

**Funciones Básicas:**
```excel
// Suma
=SUM(A1:A10)

// Promedio
=AVERAGE(B1:B100)

// Contar
=COUNT(C1:C50)
=COUNTA(D1:D50)  // No vacías
=COUNTIF(E1:E100, ">100")  // Con condición

// Máximo y Mínimo
=MAX(F1:F1000)
=MIN(G1:G1000)
```

**Funciones de Búsqueda:**
```excel
// VLOOKUP (búsqueda vertical)
=VLOOKUP(A2, Productos!A:D, 3, FALSE)
// Busca A2 en columna A de hoja Productos, devuelve columna 3

// HLOOKUP (búsqueda horizontal)
=HLOOKUP("Enero", A1:M5, 3, FALSE)

// INDEX + MATCH (más flexible que VLOOKUP)
=INDEX(C:C, MATCH(A2, A:A, 0))

// FILTER (filtrar datos)
=FILTER(A2:D100, C2:C100 > 1000)
// Devuelve filas donde columna C > 1000
```

**Funciones Lógicas:**
```excel
// IF (condicional)
=IF(A2 > 100, "Alto", "Bajo")

// IF anidado
=IF(A2 < 50, "Bajo", IF(A2 < 100, "Medio", "Alto"))

// IFS (múltiples condiciones)
=IFS(A2 < 50, "Bajo", A2 < 100, "Medio", A2 >= 100, "Alto")

// AND, OR
=IF(AND(A2 > 50, B2 < 100), "Válido", "Inválido")
=IF(OR(C2 = "Premium", D2 > 1000), "VIP", "Regular")
```

**Funciones de Texto:**
```excel
// Concatenar
=CONCATENATE(A2, " ", B2)
=A2 & " " & B2  // Alternativa

// Mayúsculas/Minúsculas
=UPPER(A2)  // MAYÚSCULAS
=LOWER(B2)  // minúsculas
=PROPER(C2)  // Título

// Extraer texto
=LEFT(A2, 3)   // Primeros 3 caracteres
=RIGHT(A2, 4)  // Últimos 4
=MID(A2, 2, 5) // Desde posición 2, 5 caracteres

// Buscar y reemplazar
=SUBSTITUTE(A2, "viejo", "nuevo")
```

**Funciones de Fecha:**
```excel
// Fecha actual
=TODAY()
=NOW()  // Con hora

// Extraer componentes
=YEAR(A2)
=MONTH(A2)
=DAY(A2)
=WEEKDAY(A2)  // Día de la semana

// Calcular diferencias
=DATEDIF(A2, B2, "D")  // Días entre fechas
=NETWORKDAYS(A2, B2)   // Días hábiles

// Formateo
=TEXT(A2, "DD/MM/YYYY")
=TEXT(NOW(), "YYYY-MM-DD HH:MM:SS")
```

**Funciones de Bases de Datos:**
```excel
// SUMIF (suma condicional)
=SUMIF(B:B, "Electrónica", C:C)
// Suma columna C donde B = "Electrónica"

// SUMIFS (múltiples condiciones)
=SUMIFS(D:D, B:B, "Electrónica", C:C, ">100")

// AVERAGEIF / AVERAGEIFS
=AVERAGEIF(A:A, ">1000", B:B)

// COUNTIFS
=COUNTIFS(A:A, ">=2026-01-01", A:A, "<=2026-01-31", B:B, "Completado")
```

**QUERY (SQL-like)**
```excel
// Consulta tipo SQL
=QUERY(A1:E100, "SELECT A, B, SUM(C) WHERE D = 'Activo' GROUP BY A, B")

// Ejemplos avanzados
=QUERY(Ventas!A:F, "SELECT B, SUM(E) WHERE C = 'Enero' GROUP BY B ORDER BY SUM(E) DESC")

=QUERY(A:E, "SELECT A, AVG(D) WHERE B CONTAINS 'Premium' GROUP BY A LABEL AVG(D) 'Promedio'")
```

**ARRAYFORMULA (aplicar fórmula a rango)**
```excel
// Sin ARRAYFORMULA (copiar a cada celda)
=A2 * B2

// Con ARRAYFORMULA (una sola fórmula)
=ARRAYFORMULA(A2:A100 * B2:B100)

// Condicionales en array
=ARRAYFORMULA(IF(A2:A100 > 100, "Alto", "Bajo"))

// Combinaciones
=ARRAYFORMULA(A2:A & " " & B2:B)
```

---

### **2. Tablas Dinámicas (Pivot Tables)**

**Crear Tabla Dinámica:**
```
1. Seleccionar datos (Ctrl+A)
2. Menú: Insertar → Tabla dinámica
3. Configurar:
   - Filas: Categoría, Producto
   - Columnas: Mes
   - Valores: SUM de Ventas
   - Filtros: Región, Estado
```

**Ejemplo de Datos:**
```
| Fecha      | Categoría    | Producto    | Región | Ventas |
|------------|--------------|-------------|--------|--------|
| 2026-01-15 | Electrónica  | Laptop HP   | Norte  | 1200   |
| 2026-01-16 | Electrónica  | Mouse Dell  | Sur    | 25     |
| 2026-01-17 | Ropa         | Camisa      | Norte  | 45     |
```

**Tabla Dinámica Resultante:**
```
Categoría    | Enero  | Febrero | Total
-------------|--------|---------|-------
Electrónica  | 15,450 | 12,300  | 27,750
Ropa         | 3,200  | 4,100   | 7,300
Hogar        | 5,600  | 6,200   | 11,800
-------------|--------|---------|-------
Total        | 24,250 | 22,600  | 46,850
```

---

### **3. Gráficos y Visualizaciones**

**Tipos de Gráficos:**

**a) Gráfico de Barras/Columnas**
```
Uso: Comparar categorías
Ejemplo: Ventas por producto, por región

Configuración:
- Eje X: Categoría (Producto)
- Eje Y: Valor (Ventas)
- Serie: Mes (opcional para comparar)
```

**b) Gráfico de Líneas**
```
Uso: Tendencias en el tiempo
Ejemplo: Evolución de ventas mensual

Configuración:
- Eje X: Tiempo (Fecha, Mes)
- Eje Y: Métrica (Ventas, Usuarios)
- Series: Múltiples líneas para comparar
```

**c) Gráfico Circular (Pie)**
```
Uso: Proporciones de un total
Ejemplo: Distribución de ventas por categoría

Configuración:
- Etiquetas: Categorías
- Valores: Porcentajes o valores absolutos
```

**d) Gráfico de Dispersión (Scatter)**
```
Uso: Correlaciones entre variables
Ejemplo: Relación entre inversión marketing y ventas

Configuración:
- Eje X: Variable independiente
- Eje Y: Variable dependiente
- Línea de tendencia opcional
```

**e) Gráfico de Cascada (Waterfall)**
```
Uso: Análisis de variaciones
Ejemplo: Desglose de profit (ingresos - costos)
```

**Ejemplo Configuración:**
```
1. Seleccionar datos
2. Insertar → Gráfico
3. Tipo de gráfico: Líneas
4. Personalizar:
   - Título: "Tendencia de Ventas 2026"
   - Eje Y: "Ventas ($)"
   - Eje X: "Mes"
   - Leyenda: Posición inferior
   - Serie: Color #4285F4 (azul Google)
5. Opciones avanzadas:
   - Línea de tendencia
   - Etiquetas de datos
   - Cuadrícula
```

---

### **4. Formateo Condicional**

**Aplicar Formato Basado en Valores:**
```
Formato → Formateo condicional

Reglas:
1. Si el valor es mayor que 1000 → Verde
2. Si el valor es menor que 500 → Rojo
3. Si el texto contiene "Pendiente" → Amarillo

Escalas de Color:
- Verde → Amarillo → Rojo
- Barras de datos
- Escala de 3 colores con punto medio
```

**Ejemplo:**
```
| Producto    | Ventas | Formato          |
|-------------|--------|------------------|
| Laptop HP   | 1,500  | ████ Verde       |
| Mouse       | 300    | █ Rojo           |
| Teclado     | 750    | ██ Amarillo      |
```

---

### **5. Validación de Datos**

```
Datos → Validación de datos

Criterios:
- Lista de elementos: "Pendiente, En Proceso, Completado"
- Número: Entre 0 y 100
- Fecha: Mayor que hoy
- Texto: Longitud mínima 5 caracteres
- Personalizado: Fórmula =A2 > B2
```

---

### **6. Importación de Datos**

**IMPORTRANGE (importar de otra hoja)**
```excel
=IMPORTRANGE("URL_de_otra_hoja", "Hoja1!A1:C100")

// Ejemplo
=IMPORTRANGE("https://docs.google.com/spreadsheets/d/ABC123", "Ventas!A:E")
```

**IMPORTDATA (importar CSV/TSV)**
```excel
=IMPORTDATA("https://ejemplo.com/datos.csv")
```

**IMPORTXML (importar desde web)**
```excel
=IMPORTXML("https://ejemplo.com", "//div[@class='precio']")
```

**IMPORTHTML (tablas de web)**
```excel
=IMPORTHTML("https://wikipedia.org/tabla", "table", 1)
```

**Google Forms Integration:**
```
1. Crear Google Form
2. Respuestas → Ver respuestas en Sheets
3. Datos automáticamente en hoja
4. Análisis con fórmulas y gráficos
```

---

### **7. Google Apps Script (Automatización)**

**Acceder:**
```
Extensiones → Apps Script
```

**Ejemplo: Enviar Email Automático**
```javascript
function enviarReporteVentas() {
  var sheet = SpreadsheetApp.getActiveSheet();
  var data = sheet.getRange("A2:C100").getValues();
  
  var totalVentas = 0;
  for (var i = 0; i < data.length; i++) {
    totalVentas += data[i][2]; // Columna C (Ventas)
  }
  
  var mensaje = "Reporte de Ventas\n\n";
  mensaje += "Total de ventas: $" + totalVentas.toFixed(2);
  
  MailApp.sendEmail({
    to: "gerente@empresa.com",
    subject: "Reporte Diario de Ventas",
    body: mensaje
  });
}

// Programar para ejecutar diariamente
// Edit → Triggers → Add Trigger → Time-driven → Day timer
```

**Ejemplo: Actualizar Datos Automáticamente**
```javascript
function actualizarDesdeAPI() {
  var url = "https://api.empresa.com/ventas/hoy";
  var response = UrlFetchApp.fetch(url);
  var json = JSON.parse(response.getContentText());
  
  var sheet = SpreadsheetApp.getActiveSheet();
  sheet.clear();
  
  // Escribir encabezados
  sheet.appendRow(["ID", "Producto", "Cantidad", "Precio"]);
  
  // Escribir datos
  json.forEach(function(item) {
    sheet.appendRow([item.id, item.producto, item.cantidad, item.precio]);
  });
}
```

**Ejemplo: Botón Personalizado**
```javascript
function onOpen() {
  var ui = SpreadsheetApp.getUi();
  ui.createMenu('Mis Funciones')
      .addItem('Actualizar Datos', 'actualizarDesdeAPI')
      .addItem('Enviar Reporte', 'enviarReporteVentas')
      .addToUi();
}
```

---

### **8. Add-ons Útiles**

**Power Tools:**
- Limpieza de datos
- Deduplicación
- Split text to columns
- Merge sheets

**Supermetrics:**
- Integración con Google Analytics
- Facebook Ads, Google Ads
- Automatizar reportes de marketing

**Autocrat:**
- Generación automática de documentos
- Mail merge desde Google Sheets

**Data Connector:**
- Conectar a bases de datos externas
- MySQL, PostgreSQL, MongoDB

---

### **9. Ejemplo Práctico: Dashboard de Ventas**

**Datos Base (Hoja "Ventas"):**
```
| Fecha      | Vendedor | Producto    | Categoría   | Cantidad | Precio | Total  | Región |
|------------|----------|-------------|-------------|----------|--------|--------|--------|
| 2026-01-15 | Juan     | Laptop HP   | Electrónica | 1        | 1200   | 1200   | Norte  |
| 2026-01-15 | María    | Mouse Dell  | Electrónica | 3        | 25     | 75     | Sur    |
| 2026-01-16 | Juan     | Teclado     | Electrónica | 2        | 80     | 160    | Norte  |
| 2026-01-16 | Pedro    | Silla       | Muebles     | 1        | 150    | 150    | Este   |
```

**Hoja "Dashboard":**

**1. KPIs Principales (Row 1-3):**
```
| Métrica         | Fórmula                                              | Resultado |
|-----------------|------------------------------------------------------|-----------|
| Total Ventas    | =SUM(Ventas!G:G)                                     | $15,450   |
| Promedio Ticket | =AVERAGE(Ventas!G:G)                                 | $245      |
| Cantidad Ventas | =COUNTA(Ventas!A:A)-1                                | 63        |
| Top Vendedor    | =INDEX(Ventas!B:B, MATCH(MAX(SUMIF...)))             | Juan      |
```

**2. Ventas por Categoría (Tabla Dinámica):**
```
Categoría    | Total    | % del Total
-------------|----------|------------
Electrónica  | $8,450   | 54.7%
Muebles      | $4,200   | 27.2%
Otros        | $2,800   | 18.1%
```

**3. Gráfico de Tendencia:**
```
Gráfico de Líneas: Ventas Diarias
Eje X: Fecha
Eje Y: Total Ventas
```

**4. Top 5 Productos:**
```
=QUERY(Ventas!A:G, "SELECT C, SUM(G) GROUP BY C ORDER BY SUM(G) DESC LIMIT 5")
```

**5. Ventas por Vendedor (Gráfico de Barras):**
```
Horizontal Bar Chart
Juan:    $5,450
María:   $4,200
Pedro:   $3,800
Ana:     $2,000
```

**6. Formateo Condicional:**
```
- Ventas > $1000: Verde
- Ventas < $100: Rojo
- Barras de datos en columna Total
```

---

**Mejores Prácticas:**

1. **Organización:**
   - Una hoja para datos raw
   - Hojas separadas para análisis
   - Nombrar rangos (Data → Named ranges)

2. **Performance:**
   - Evitar fórmulas volátiles (NOW, RAND) innecesarias
   - Usar ARRAYFORMULA en lugar de copiar fórmulas
   - Limitar IMPORTRANGE a datos necesarios

3. **Colaboración:**
   - Proteger rangos críticos
   - Comentarios para explicar fórmulas complejas
   - Versioning con "Ver historial de versiones"

4. **Visualización:**
   - Usar colores consistentes
   - Etiquetas claras en gráficos
   - Dashboard en primera hoja

**Habilitación:**
1. Crear cuenta Google (gratuita)
2. Acceder a sheets.google.com
3. Practicar con datasets de ejemplo
4. Explorar templates de Google
5. Aprender Apps Script para automatización
6. Instalar add-ons útiles
7. Integrar con otras herramientas Google

---

### Herramientas para análisis y visualización de datos: PowerBI, Tableau y QlikSense

**¿De qué trata?**
- Plataformas profesionales de Business Intelligence
- Visualización interactiva y análisis avanzado de datos
- Dashboards empresariales con capacidades de drill-down
- Conexión a múltiples fuentes de datos

**¿Por qué se utiliza?**
- Análisis de grandes volúmenes de datos (millones de registros)
- Visualizaciones profesionales e interactivas
- Compartir insights con stakeholders
- Toma de decisiones data-driven
- Monitoreo de KPIs en tiempo real
- Análisis predictivo y tendencias

**Comparación General:**

| Característica      | Power BI        | Tableau         | QlikSense       |
|---------------------|-----------------|-----------------|-----------------|
| **Precio**          | $$ (Económico)  | $$$ (Costoso)   | $$$ (Costoso)   |
| **Facilidad Uso**   | ⭐⭐⭐⭐⭐          | ⭐⭐⭐⭐            | ⭐⭐⭐             |
| **Performance**     | ⭐⭐⭐⭐            | ⭐⭐⭐⭐⭐           | ⭐⭐⭐⭐⭐           |
| **Visualizaciones** | ⭐⭐⭐⭐            | ⭐⭐⭐⭐⭐           | ⭐⭐⭐⭐            |
| **Cloud**           | Azure nativo    | Tableau Online  | Qlik Cloud      |
| **Mobile**          | Excelente       | Muy Bueno       | Bueno           |
| **Comunidad**       | Muy Grande      | Grande          | Mediana         |

---

## **POWER BI (Microsoft)**

**¿De qué trata?**
- Herramienta BI de Microsoft integrada con ecosistema Azure
- Desktop gratuito, servicio cloud de pago
- Enfoque en usuarios de negocio (low-code)

**Ventajas:**
- Precio competitivo ($10/usuario/mes Pro)
- Integración perfecta con Microsoft (Excel, Azure, Office365)
- Interfaz intuitiva drag-and-drop
- Power Query para transformaciones ETL
- DAX para cálculos avanzados
- Actualizaciones mensuales de funcionalidades
- Gran comunidad y recursos de aprendizaje

**Desventajas:**
- Limitado fuera del ecosistema Microsoft
- Performance con datasets muy grandes (>10M filas)
- Versión desktop solo para Windows
- Algunas visualizaciones requieren custom visuals

---

### **Componentes de Power BI:**

**1. Power BI Desktop (Aplicación Windows)**
- Desarrollo de reportes localmente
- Conexión a fuentes de datos
- Transformación y modelado
- Creación de visualizaciones

**2. Power BI Service (Cloud)**
- Publicación de reportes
- Compartir dashboards
- Colaboración en equipo
- Programar actualizaciones
- URL: app.powerbi.com

**3. Power BI Mobile**
- Aplicación iOS/Android
- Dashboards optimizados para móvil
- Notificaciones y alertas

**4. Power BI Report Server (On-Premise)**
- Versión on-premise para empresas
- Sin necesidad de cloud

---

### **Flujo de Trabajo Power BI:**

**1. Conectar a Datos**
```
Get Data → Seleccionar origen

Orígenes Soportados:
- Archivos: Excel, CSV, JSON, XML
- Bases de Datos: SQL Server, MySQL, PostgreSQL, Oracle
- Cloud: Azure, AWS, Google BigQuery, Snowflake
- Servicios: Salesforce, Google Analytics, Dynamics 365
- Web: APIs REST, SharePoint, páginas web
- Otros: 150+ conectores
```

**Ejemplo Conexión SQL Server:**
```
1. Get Data → SQL Server
2. Server: sql-server.empresa.com
3. Database: VentasDB
4. Modo: Import (datos en memoria) o DirectQuery (consulta en vivo)
5. Seleccionar tablas
6. Load o Transform Data
```

**2. Transformar Datos (Power Query)**
```
Power Query Editor permite:
- Filtrar filas
- Eliminar columnas
- Cambiar tipos de datos
- Merge de tablas
- Append (unir verticalmente)
- Group By (agregar)
- Unpivot/Pivot
- Columnas condicionales
- Custom columns con M language
```

**Ejemplo Transformación:**
```M
// M Language (Power Query)
let
    Source = Sql.Database("server", "database"),
    Ventas = Source{[Schema="dbo",Item="Ventas"]}[Data],
    
    // Filtrar año actual
    FiltrarFecha = Table.SelectRows(Ventas, 
        each Date.Year([Fecha]) = Date.Year(DateTime.LocalNow())),
    
    // Agregar columna calculada
    AgregarMes = Table.AddColumn(FiltrarFecha, "Mes", 
        each Date.MonthName([Fecha]), type text),
    
    // Agrupar por producto
    Agrupar = Table.Group(AgregarMes, {"Producto"}, 
        {{"TotalVentas", each List.Sum([Monto]), type number}})
in
    Agrupar
```

**3. Modelado de Datos**
```
Model View en Power BI Desktop

- Definir relaciones entre tablas
- Crear medidas (DAX)
- Crear columnas calculadas
- Definir jerarquías (Año → Trimestre → Mes → Día)
- Organizar tablas y campos
```

**Relaciones:**
```
Fact_Ventas (1 →) dim_Clientes (*)
    customer_id  →  customer_id

Fact_Ventas (1 →) dim_Productos (*)
    product_id  →  product_id

Fact_Ventas (1 →) dim_Tiempo (*)
    date_id  →  date_id
```

**4. Crear Medidas con DAX**

**DAX (Data Analysis Expressions):**
```dax
// Medida simple: Total de Ventas
Total Ventas = SUM(Fact_Ventas[Monto])

// Medida con filtro
Ventas 2026 = CALCULATE(
    SUM(Fact_Ventas[Monto]),
    YEAR(Fact_Ventas[Fecha]) = 2026
)

// Medida year-over-year
Ventas Año Anterior = CALCULATE(
    [Total Ventas],
    SAMEPERIODLASTYEAR(dim_Tiempo[Fecha])
)

Crecimiento YoY = 
DIVIDE(
    [Total Ventas] - [Ventas Año Anterior],
    [Ventas Año Anterior],
    0
)

// Top N productos
Top 5 Productos = 
VAR TopProducts = 
    TOPN(
        5,
        VALUES(dim_Productos[Producto]),
        [Total Ventas],
        DESC
    )
RETURN
    CALCULATE(
        [Total Ventas],
        TopProducts
    )

// Ventas acumuladas
Ventas Acumuladas = 
CALCULATE(
    [Total Ventas],
    FILTER(
        ALL(dim_Tiempo[Fecha]),
        dim_Tiempo[Fecha] <= MAX(dim_Tiempo[Fecha])
    )
)

// Promedio móvil 3 meses
Promedio Móvil 3M = 
AVERAGEX(
    DATESINPERIOD(
        dim_Tiempo[Fecha],
        LASTDATE(dim_Tiempo[Fecha]),
        -3,
        MONTH
    ),
    [Total Ventas]
)
```

**5. Crear Visualizaciones**

**Tipos de Visualizaciones:**
```
Básicas:
- Bar Chart (Barras)
- Column Chart (Columnas)
- Line Chart (Líneas)
- Pie Chart (Circular)
- Donut Chart (Anillo)
- Table (Tabla)
- Matrix (Matriz/Pivot)

Avanzadas:
- Map (Mapa geográfico)
- Treemap
- Waterfall
- Funnel (Embudo)
- Gauge (Indicador)
- KPI Card
- Ribbon Chart
- Scatter Plot

Interactivas:
- Slicer (Filtro)
- Drill-through
- Tooltips personalizados
- Bookmarks

Custom Visuals:
- Gantt Chart
- Word Cloud
- Calendar
- 200+ en AppSource
```

**Ejemplo Dashboard Power BI:**
```
┌─────────────────────────────────────────────────────────┐
│         DASHBOARD DE VENTAS - ENERO 2026                │
├─────────────────────────────────────────────────────────┤
│ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐   │
│ │Total Ventas│ Objetivo  │ Cumpl.   │Crecim YoY│   │
│ │ $1.5M ↑  │ $1.3M     │ 115%     │  +12%  ↑ │   │
│ └──────────┘ └──────────┘ └──────────┘ └──────────┘   │
├─────────────────────────────────────────────────────────┤
│ ┌─────────────────────┐ ┌───────────────────────────┐ │
│ │ TENDENCIA MENSUAL   │ │  VENTAS POR CATEGORÍA     │ │
│ │                     │ │  Electrónica    45% ████  │ │
│ │   *          *      │ │  Ropa           30% ███   │ │
│ │      *    *         │ │  Hogar          15% ██    │ │
│ │  *      *           │ │  Otros          10% █     │ │
│ │──────────────────── │ │                           │ │
│ │ E F M A M J J A S O │ └───────────────────────────┘ │
│ └─────────────────────┘                               │
├─────────────────────────────────────────────────────────┤
│ FILTROS:  [Región ▼] [Vendedor ▼] [Rango Fechas]       │
├─────────────────────────────────────────────────────────┤
│ TOP 10 PRODUCTOS                                        │
│ ┌─────────────────────────────────────────────────┐    │
│ │ Producto      │ Ventas  │ Unidades │ Margen    │    │
│ │ Laptop HP     │ $245K   │ 204      │ 28%       │    │
│ │ iPhone 15     │ $189K   │ 210      │ 35%       │    │
│ │ Monitor Dell  │ $112K   │ 280      │ 22%       │    │
│ └─────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────┘
```

**6. Publicar y Compartir**
```
1. Power BI Desktop → Publish
2. Seleccionar workspace en Power BI Service
3. Configurar:
   - Permisos de acceso (View/Edit)
   - Scheduled Refresh (actualización programada)
   - Row-level security
4. Compartir:
   - Enviar link a dashboard
   - Embed en SharePoint/Teams
   - Publicar en web (público)
   - Exportar a PDF/PowerPoint
```

---

## **TABLEAU**

**¿De qué trata?**
- Líder del mercado en visualización de datos
- Enfoque en exploración visual interactiva
- Muy potente para análisis ad-hoc

**Ventajas:**
- Visualizaciones más estéticas y flexibles
- Performance excepcional con big data
- Interfaz muy intuitiva
- Tableau Public gratuito (publicación pública)
- Cálculos de tabla potentes
- Integración con R y Python
- Comunidad muy activa

**Desventajas:**
- Precio alto ($70/user/mes Creator)
- Menos integración con ecosistema corporate
- Curva de aprendizaje para funciones avanzadas
- ETL limitado (usar Tableau Prep)

---

### **Componentes de Tableau:**

**1. Tableau Desktop**
- Aplicación principal de desarrollo
- Dos versiones: Creator ($70/mes) y Viewer

**2. Tableau Prep**
- ETL visual
- Limpieza y transformación de datos

**3. Tableau Server**
- Hosting on-premise
- Compartir y colaborar

**4. Tableau Online**
- Versión cloud de Tableau Server

**5. Tableau Public**
- Versión gratuita
- Publicación pública únicamente

**6. Tableau Mobile**
- Apps iOS/Android

---

### **Flujo de Trabajo Tableau:**

**1. Conectar a Datos**
```
Connect → Seleccionar fuente

Similar a Power BI, soporta 100+ conectores
- Extract (.hyper): Datos en memoria, rápido
- Live Connection: Consulta en tiempo real
```

**2. Preparar Datos**
```
Data Source tab:
- Joins entre tablas
- Unions (append)
- Data Interpreter (limpieza automática Excel)
- Filters
- Custom SQL
- Calculated Fields
```

**3. Crear Visualizaciones**

**Conceptos Tableau:**
```
Pills (Píldoras):
- Dimensions (azul): Campos categóricos (Producto, Región)
- Measures (verde): Campos numéricos (Ventas, Cantidad)

Shelves (Estantes):
- Columns: Eje X
- Rows: Eje Y
- Marks: Color, Size, Label, Detail, Tooltip
- Filters: Filtrar datos
- Pages: Animaciones temporales
```

**Ejemplo: Gráfico de Barras**
```
1. Arrastrar "Categoría" a Columns
2. Arrastrar "Ventas" a Rows
3. Arrastrar "Región" a Color
4. Show Me → Bar Chart
5. Sort descending
```

**Cálculos en Tableau:**
```
// Calculated Field
Profit Ratio = SUM([Profit]) / SUM([Sales])

// Level of Detail (LOD)
Average Sales per Customer = 
{ FIXED [Customer] : SUM([Sales]) }

// Table Calculation
Running Total = RUNNING_SUM(SUM([Sales]))

// Date Functions
Year over Year Growth = 
(SUM([Sales]) - LOOKUP(SUM([Sales]), -12)) / LOOKUP(SUM([Sales]), -12)

// Conditional
Sales Category = 
IF SUM([Sales]) > 10000 THEN "High"
ELSEIF SUM([Sales]) > 5000 THEN "Medium"
ELSE "Low"
END
```

**4. Dashboards**
```
Dashboard → New Dashboard

- Arrastrar sheets (visualizaciones)
- Layout containers (Horizontal/Vertical)
- Objects: Text, Image, Web Page, Blank
- Actions: Filter, Highlight, URL, Parameter
- Device Designer (responsive)
```

**Dashboard Actions:**
```
Dashboard → Actions → Add Action

Filter Action:
- Click en gráfico A filtra gráfico B
- Ejemplo: Click región → filtrar productos

Highlight Action:
- Hover resalta datos relacionados

URL Action:
- Click abre URL externa
- Ejemplo: Click cliente → abrir CRM

Parameter Action:
- Cambiar parámetro basado en selección
```

**5. Storytelling**
```
Story → New Story

- Crear narrativa con múltiples dashboards
- Story Points (páginas)
- Agregar captions y anotaciones
- Presentar insights secuencialmente
```

**6. Publicar**
```
Server → Publish Workbook

Tableau Server/Online:
- Permisos granulares
- Scheduled refresh
- Subscriptions (email reportes)
- Tableau Mobile
```

---

## **QLIKSENSE**

**¿De qué trata?**
- Motor asociativo único (explora relaciones automáticamente)
- Enfoque en self-service BI
- Análisis guiado por AI (Insight Advisor)

**Ventajas:**
- Motor asociativo (sin modelo de datos predefinido)
- In-memory ultra rápido
- Selecciones globales (filtros actúan en todo)
- Qlik Sense Cloud gratuito (30 días)
- Visualizaciones responsivas automáticas
- Data storytelling integrado

**Desventajas:**
- Menos intuitivo para principiantes
- Comunidad más pequeña que Power BI/Tableau
- Precio alto
- Menos visualizaciones out-of-the-box
- Scripting QlikView puede ser complejo

---

### **Características Únicas de Qlik:**

**1. Motor Asociativo**
```
A diferencia de Power BI/Tableau (modelo dimensional),
Qlik asocia automáticamente todos los datos.

Selección en cualquier campo:
- Filtra automáticamente todo relacionado
- Muestra en gris datos no relacionados
- Verde: Seleccionado
- Blanco: Relacionado
- Gris: No relacionado
```

**2. Insight Advisor (AI)**
```
Insight Advisor sugiere visualizaciones automáticamente
basado en los datos seleccionados.

"Muéstrame ventas por región"
→ Genera gráfico automáticamente
```

**3. Scripting**
```
Script de carga (QlikView Script):

LOAD
    OrderID,
    CustomerID,
    OrderDate,
    Sales
FROM [lib://DataFiles/Orders.csv]
(txt, utf8, embedded labels, delimiter is ',');

// Calendario automático
Calendar:
LOAD
    Date,
    Year(Date) as Year,
    Month(Date) as Month,
    Week(Date) as Week
RESIDENT Orders;
```

---

### **Comparación de Funcionalidades:**

| Funcionalidad         | Power BI    | Tableau     | QlikSense   |
|-----------------------|-------------|-------------|-------------|
| **Precio Entry**      | $10/mes     | $70/mes     | $30/mes     |
| **ETL Integrado**     | Power Query | Tableau Prep| Script      |
| **Lenguaje Cálculo**  | DAX         | Calculated F| Script      |
| **Modelo Datos**      | Star Schema | Relacional  | Asociativo  |
| **AI/ML**             | Azure ML    | Tableau AI  | Insight Adv |
| **Mobile**            | ⭐⭐⭐⭐⭐        | ⭐⭐⭐⭐        | ⭐⭐⭐⭐        |
| **Embedded**          | Excelente   | Bueno       | Muy Bueno   |
| **Colaboración**      | Teams       | Tableau Srv | Qlik Cloud  |
| **Open Source**       | No          | Tableau Pub | Trial       |

---

### **Ejemplo Caso de Uso: Dashboard Ejecutivo**

**Requisito:**
```
CEO necesita dashboard para monitorear:
1. Ventas vs Objetivo mensual
2. Top 10 clientes por revenue
3. Margen de ganancia por producto
4. Distribución geográfica de ventas
5. Tendencia de nuevos clientes
```

**Implementación en Power BI:**
```dax
// Medidas DAX
Total Sales = SUM(Sales[Amount])

Target = SUM(Targets[Monthly_Target])

Achievement = DIVIDE([Total Sales], [Target], 0)

Profit Margin = 
DIVIDE(
    SUM(Sales[Profit]),
    SUM(Sales[Revenue]),
    0
)

New Customers = 
CALCULATE(
    DISTINCTCOUNT(Sales[CustomerID]),
    FILTER(
        Sales,
        Sales[FirstPurchaseDate] >= EOMONTH(TODAY(), -1) + 1
    )
)

// Visualizaciones:
1. Card: Total Sales, Achievement %
2. Bar Chart: Top 10 Customers
3. Matrix: Product × Profit Margin
4. Map: Sales by Region
5. Line Chart: New Customers Trend
```

**Implementación en Tableau:**
```
// Calculated Fields
Profit Margin = SUM([Profit]) / SUM([Sales])

YTD Sales = 
TOTAL(
    IF YEAR([Order Date]) = YEAR(TODAY())
    THEN [Sales]
    END
)

// Dashboard:
- KPI Cards con BANs (Big Ass Numbers)
- Filled Map para geografía
- Horizontal Bar para Top 10
- Heat Map para productos
- Dual Axis para tendencia
```

---

**Habilitación por Herramienta:**

**Power BI:**
1. Descargar Power BI Desktop (gratis)
2. Seguir tutoriales Microsoft Learn
3. Practicar con datos de ejemplo
4. Aprender DAX (fundamental)
5. Obtener licencia Pro ($10/mes)
6. Certificación: PL-300 (Power BI Data Analyst)

**Tableau:**
1. Descargar Tableau Public (gratis)
2. Seguir Tableau Learning Paths
3. Practicar con Superstore dataset
4. Unirse a Tableau Community
5. Participar en Makeover Monday
6. Certificación: Tableau Desktop Specialist

**QlikSense:**
1. Crear cuenta Qlik Sense Cloud (trial)
2. Seguir Qlik Continuous Classroom
3. Aprender Qlik Script
4. Practicar con Qlik Demos
5. Certificación: Qlik Sense Data Architect

---

**Recomendaciones de Elección:**

**Elegir Power BI si:**
- Ecosistema Microsoft (Office365, Azure, SQL Server)
- Presupuesto limitado
- Usuarios de negocio sin experiencia técnica
- Necesitas integración con Teams, SharePoint

**Elegir Tableau si:**
- Visualizaciones son prioridad #1
- Análisis exploratorio ad-hoc intenso
- Presupuesto disponible
- Performance con big data crítica
- Quieres las mejores visualizaciones del mercado

**Elegir QlikSense si:**
- Análisis asociativo (explorar sin modelo predefinido)
- Self-service BI para usuarios avanzados
- Necesitas AI-driven insights
- Migración desde QlikView

**Usar Google Sheets si:**
- Datos pequeños (<50k filas)
- Presupuesto cero
- Colaboración simple
- Usuarios no técnicos
- Análisis básico suficiente