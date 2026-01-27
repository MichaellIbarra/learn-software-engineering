# GUIA DE CONCEPTOS PARA ANALISTA DE INTEGRACION

## 1. QUE ES UN ANALISTA PROGRAMADOR DE INTEGRACION

Como analista programador de integracion, tu trabajo principal es:

**Monitorear, corregir y relanzar procesos automaticos que conectan sistemas entre si.**

Esto significa que no programas aplicaciones nuevas desde cero, sino que te encargas de:
- Vigilar que los procesos automaticos funcionen correctamente
- Detectar cuando algo falla
- Identificar la causa del error
- Corregir el problema
- Volver a ejecutar (relanzar) el proceso que fallo

### Sistemas que conectas:

- **BSCS70/BSCS7**: Sistema de facturación y gestión de clientes de telefonía
- **SAP**: Sistema de gestion empresarial (ventas, inventarios, finanzas)
- **CRL (Recarga en Linea)**: Sistema de recargas prepago
- **IOTDB**: Base de datos para dispositivos inteligentes (smartwatch)
- **HLR**: Registro de ubicacion de abonados en redes telefonicas
- **SIAC**: Sistema de atencion al cliente

---

## 2. QUE ES UNA BASE DE DATOS ORACLE

Una base de datos Oracle es un sistema que almacena información de manera organizada en tablas.

### Conceptos basicos:0

**TABLA**: Es como una hoja de Excel, con filas y columnas.
- Cada fila es un registro (ejemplo: un cliente, una factura, una orden)
- Cada columna es un campo (ejemplo: nombre, fecha, monto)

**CAMPO/COLUMNA**: Cada dato especifico que guardas.
Ejemplos de campos en tus archivos:
- `IDTRANSFER`: Numero de orden de transferencia
- `ESTADO`: Si el proceso esta PROCESO, CERRADO, ANULADO, etc.
- `FECHAREGISTRO`: Cuando se registro la transaccion
- `MSISDN`: Numero de telefono movil

**REGISTRO/FILA**: Un conjunto completo de datos.
Ejemplo: Una factura especifica con todos sus datos (numero, fecha, cliente, monto)

**ESQUEMA**: Es como una carpeta que agrupa varias tablas relacionadas.
Ejemplos que veras:
- `EAI`: Esquema de integracion empresarial
- `USRACT`: Esquema de acciones de usuario
- `APEAI`: Esquema de aplicaciones EAI
- `AW`: Esquema de Apple Watch / dispositivos inteligentes

---

## 3. QUE ES SQL Y COMO FUNCIONAN LAS QUERIES

**SQL** (Structured Query Language) es el lenguaje que usas para comunicarte con la base de datos.

### Operaciones principales:

#### A. SELECT - CONSULTAR DATOS

Es para ver informacion sin modificar nada.

**Sintaxis basica:**
```sql
SELECT campo1, campo2, campo3
FROM esquema.tabla
WHERE condicion;
```

**Ejemplo real de tu trabajo:**
```sql
SELECT *
FROM EAI.PEDIDO_PRETUP
WHERE IDTRANSFER IN ('OT250623.1117.100001', 'OT250614.1302.100001')
AND ESTADO = 'PROCESO';
```

**Que hace esta query:**
- `SELECT *`: Trae TODOS los campos de la tabla
- `FROM EAI.PEDIDO_PRETUP`: De la tabla PEDIDO_PRETUP del esquema EAI
- `WHERE IDTRANSFER IN (...)`: Solo los registros cuyo numero de orden este en esa lista
- `AND ESTADO = 'PROCESO'`: Y que esten en estado PROCESO

**Otros ejemplos importantes:**

```sql
-- Buscar por fecha
SELECT * FROM USRACT.POSTT_SERVICIOPROG
WHERE TRUNC(SERVD_FECHAPROG) = TRUNC(SYSDATE)
AND SERVC_ESTADO NOT IN (3,5);
```

**Que significan las funciones:**
- `TRUNC(SYSDATE)`: Toma la fecha actual (SYSDATE) y quita la hora, dejando solo el dia
- `NOT IN (3,5)`: Que el estado NO sea 3 ni 5
- `AND`: Ambas condiciones deben cumplirse

```sql
-- Buscar en un rango de fechas
SELECT DN_NUM, CUSTOMER_ID, CO_ID, CH_STATUS
FROM TIM.PP_DATOS_CONTRATO PT
WHERE DN_NUM IN (&linea)
AND FEC_ESTADO = (SELECT MAX(FEC_ESTADO)
                  FROM TIM.PP_DATOS_CONTRATO PT2
                  WHERE PT.DN_NUM = PT2.DN_NUM);
```

**Que hace:**
- `&linea`: Es un parametro que tu reemplazas con el numero de telefono
- `MAX(FEC_ESTADO)`: Obtiene la fecha mas reciente
- La subconsulta `(SELECT ...)` busca solo el registro mas actual de cada linea

**Subconsultas - Query dentro de query:**

Una subconsulta es un SELECT dentro de otro SELECT. Se usa cuando necesitas un dato calculado.

```sql
-- Ejemplo simple de subconsulta
SELECT * FROM USRACT.POSTT_SERVICIOPROG
WHERE SERVV_ID_EAI_SW IN (
    SELECT SERVV_ID_EAI_SW FROM USRACT.EAI_MIGRACIONES
    WHERE ESTADO = 3
);
```

**Como funciona:**
1. Primero se ejecuta la subconsulta (la que esta entre parentesis)
2. La subconsulta devuelve una lista de SERVV_ID_EAI_SW
3. Luego el SELECT principal usa esa lista para filtrar

**INNER JOIN - Unir dos tablas:**

JOIN sirve para combinar datos de dos tablas relacionadas.

```sql
SELECT A.DISAV_MSISDN_EQUIP, A.DISAC_ESTADO, C.MSCLV_MSJRPTA_IMS
FROM AW.IOTAWT_DISPOSITIVO_ASOCIADO A
INNER JOIN AW.IOTAWT_CAB_MESA_CONTROL C
  ON C.MSCLV_MSISDN_EQUIP = A.DISAV_MSISDN_EQUIP
WHERE A.DISAC_ESTADO = 'U';
```

**Como funciona:**
- `FROM AW.IOTAWT_DISPOSITIVO_ASOCIADO A`: Primera tabla, le pones alias "A"
- `INNER JOIN AW.IOTAWT_CAB_MESA_CONTROL C`: Segunda tabla, alias "C"
- `ON C.MSCLV_MSISDN_EQUIP = A.DISAV_MSISDN_EQUIP`: Campo que las relaciona
- Trae datos de ambas tablas en una sola consulta

**Ejemplo visual:**

Tabla A (DISPOSITIVO_ASOCIADO):
```
MSISDN_EQUIP  | ESTADO
51988588727   | U
51999123456   | A
```

Tabla C (CAB_MESA_CONTROL):
```
MSISDN_EQUIP  | MENSAJE
51988588727   | Error en UDB
51999123456   | Operacion Exitosa
```

Resultado del JOIN:
```
MSISDN_EQUIP  | ESTADO | MENSAJE
51988588727   | U      | Error en UDB
51999123456   | A      | Operacion Exitosa
```

**COUNT - Contar registros:**

```sql
SELECT COUNT(1) FROM tabla WHERE condicion;
```

Devuelve un numero: cuantos registros cumplen la condicion.

```sql
-- Ejemplo: Contar cuantas lineas estan en estado unusable
SELECT COUNT(1) FROM AW.IOTAWT_DISPOSITIVO_ASOCIADO
WHERE DISAC_ESTADO = 'U'
AND TRUNC(DISAD_FECHA_CREACION) = TRUNC(SYSDATE);
```

Si devuelve 5, significa que hay 5 lineas unusable creadas hoy.

**ROWNUM - Limitar resultados:**

```sql
WHERE ROWNUM <= 1
```

Solo trae el primer registro. Es como "TOP 1" en otros sistemas.

```sql
-- Traer solo la ultima modificacion
SELECT * FROM (
    SELECT * FROM tabla
    ORDER BY FECHA_MODIFICACION DESC
)
WHERE ROWNUM <= 1;
```

**ORDER BY - Ordenar resultados:**

```sql
ORDER BY campo ASC   -- Ascendente (de menor a mayor)
ORDER BY campo DESC  -- Descendente (de mayor a menor)
```

```sql
-- Traer registros ordenados por fecha, mas recientes primero
SELECT * FROM AW.IOTAWT_DISPOSITIVO_ASOCIADO
WHERE DISAV_MSISDN_EQUIP = '51988588727'
ORDER BY DISAD_FECHA_MODIFICACION DESC;
```

**IS NULL / IS NOT NULL - Validar campos vacios:**

```sql
WHERE campo IS NULL       -- Campo esta vacio
WHERE campo IS NOT NULL   -- Campo tiene valor
```

```sql
-- Buscar registros que tienen fecha de modificacion
SELECT * FROM AW.IOTAWT_DISPOSITIVO_ASOCIADO
WHERE DISAD_FECHA_MODIFICACION IS NOT NULL;
```

#### B. UPDATE - MODIFICAR DATOS

Se usa para cambiar informacion existente. SIEMPRE debes hacer COMMIT despues.

**Sintaxis basica:**
```sql
UPDATE esquema.tabla
SET campo1 = nuevo_valor,
    campo2 = nuevo_valor
WHERE condicion;
COMMIT;
```

**Ejemplo real:**
```sql
UPDATE EAI.PEDIDO_PRETUP
SET ESTADO = 'ANULADO'
WHERE ID IN (718061, 718062, 718063);
COMMIT;
```

**Que hace:**
- Cambia el campo ESTADO a 'ANULADO'
- Solo en los registros con ID 718061, 718062 o 718063
- `COMMIT`: Guarda los cambios permanentemente (MUY IMPORTANTE)

**Otro ejemplo mas complejo:**
```sql
UPDATE USRACT.POSTT_SERVICIOPROG
SET SERVC_ESTADO = 1,
    SERVV_MEN_ERROR = '',
    SERVV_COD_ERROR = '',
    SERVD_FECHA_EJEC = ''
WHERE SERVV_ID_EAI_SW IN ('123456', '789012')
AND SERVI_COD = '3';
COMMIT;
```
**Que hace:**
- Cambia el estado a 1 (pendiente de procesar)
- Limpia los mensajes de error
- Limpia la fecha de ejecucion
- Solo para las transacciones especificas del servicio codigo 3

**REPLACE - Cambiar parte de un texto:**
```sql
UPDATE USRACT.POSTT_SERVICIOPROG
SET SERVV_XMLENTRADA = REPLACE(SERVV_XMLENTRADA,
                               '<fechaProgramacion>2025-04-28</fechaProgramacion>',
                               '<fechaProgramacion>2025-04-29</fechaProgramacion>')
WHERE SERVV_ID_EAI_SW IN ('456789');
COMMIT;
```

**Que hace:**
- En el campo SERVV_XMLENTRADA (que contiene XML)
- Busca el texto viejo `<fechaProgramacion>2025-04-28</fechaProgramacion>`
- Lo reemplaza por `<fechaProgramacion>2025-04-29</fechaProgramacion>`
- Esto cambia la fecha programada sin tocar el resto del XML

----------------------------------------------------------------------1----------------------------------------------------------------------

#### C. DELETE - ELIMINAR DATOS

**CUIDADO**: Elimina registros permanentemente.

**Sintaxis:**
```sql
DELETE FROM esquema.tabla
WHERE condicion;
COMMIT;
```

**Ejemplo:**
```sql
DELETE FROM USRACT.EAI_MIGRACIONES
WHERE IDTRANSACCION IN ('20250265236856');
COMMIT;
```

**Que hace:**
- Elimina completamente el registro con ese ID de transaccion
- COMMIT confirma la eliminacion

#### D. COMMIT - GUARDAR CAMBIOS

**MUY IMPORTANTE**: En Oracle, cuando haces UPDATE o DELETE, los cambios NO se guardan automaticamente.

```sql
COMMIT;
```

**Que hace:**
- Guarda todos los cambios que hiciste desde el ultimo COMMIT
- Si no haces COMMIT, los cambios se pierden cuando cierras la sesion
- **SIEMPRE** debes poner COMMIT despues de UPDATE o DELETE

---

## 4. CONCEPTOS ESPECIFICOS DE TU TRABAJO

### A. ESTADOS DE PROCESOS

En las tablas de programaciones, el campo `SERVC_ESTADO` o `ESTADO` indica en que situacion esta:

- **1**: PENDIENTE - El proceso aun no se ejecuta
- **2**: EN PROCESO - Se esta ejecutando en este momento
- **3**: EXITOSO/CERRADO - Termino correctamente
- **4**: ERROR - Fallo y necesita correccion
- **5**: CANCELADO/ANULADO - Se cancelo y no se va a ejecutar

### B. TIPOS DE SERVICIOS (SERVI_COD)

Cada numero identifica un tipo de operacion:

- **3**: Suspension de linea
- **4**: Reactivacion de linea suspendida
- **18**: Desactivar contrato (dar de baja)
- **19**: Migracion de Postpago a Prepago
- **22**: Cambio de plan
- **50**: Reactivacion de lineas desactivas
- **60**: Cambio de ciclo de facturacion
- **70**: Union/Separacion de recibos
- **72**: Cambio de ciclo facturacion masivo
- **75**: Cambio de titularidad
- **90**: Cambio de tipo de cliente

### C. CAMPOS IMPORTANTES EN LAS TABLAS

**Identificadores:**
- `ID`: Numero unico de registro en la tabla
- `IDTRANSACCION` o `SERVV_ID_EAI_SW`: Codigo unico de la transaccion
- `IDTRANSFER`: Numero de orden de trabajo (ejemplo: OT250623.1117.100001)
- `CO_ID`: Codigo de contrato en BSCS
- `CUSTOMER_ID`: Codigo de cliente

**Datos de telefonia:**
- `MSISDN` o `DN_NUM` o `SERVV_MSISDN`: Numero de telefono (ejemplo: 51988588727)
- `IMSI`: Identificador internacional de suscriptor movil
- `ICCID`: Numero de la tarjeta SIM

**Fechas:**
- `FECHAREGISTRO` o `SERVD_FECHA_REG`: Cuando se registro
- `FECHAPROGRAMACION` o `SERVD_FECHAPROG`: Cuando debe ejecutarse
- `FECHAEJECUCION` o `SERVD_FECHA_EJEC`: Cuando se ejecuto realmente
- `FECHAMODIFICACION`: Cuando se modifico por ultima vez

**Control de errores:**
- `ESTADO` o `SERVC_ESTADO`: Estado del proceso
- `SERVV_MEN_ERROR`: Mensaje de error descriptivo
- `SERVV_COD_ERROR`: Codigo numerico del error

**Datos XML:**
- `SERVV_XMLENTRADA`: Contiene todos los parametros del servicio en formato XML

### D. QUE ES XML

XML es un formato para organizar datos con etiquetas.

**Ejemplo:**
```xml
<fechaProgramacion>2025-04-29</fechaProgramacion>
<msisdn>51988588727</msisdn>
<accion>suspension</accion>
```

Cada dato esta entre etiquetas de apertura `<nombre>` y cierre `</nombre>`.

**EXTRACTVALUE** es una funcion Oracle para leer datos de XML:

```sql
EXTRACTVALUE(xmltype(SERVV_XMLENTRADA),
             'DatosProgramarCambioCicloFactType/csBillcycleNew')
```

**Que hace:**
- Lee el campo SERVV_XMLENTRADA que contiene XML
- Extrae el valor de la ruta especificada
- Es como navegar en carpetas: `carpeta_principal/subcarpeta/dato`

### E. FUNCIONES DE FECHA EN ORACLE

**SYSDATE**: Fecha y hora actual del sistema

**TRUNC(fecha)**: Elimina la hora, deja solo el dia
```sql
TRUNC(SYSDATE) = TRUNC(FECHAREGISTRO)
-- Compara si ambas fechas son del mismo dia, ignorando la hora
```

**TO_DATE**: Convierte texto a fecha
```sql
TO_DATE('29/04/2025', 'DD/MM/YYYY')
-- Convierte el texto a una fecha real
-- DD = dia, MM = mes, YYYY = año de 4 digitos
```

**MAX(fecha)**: Obtiene la fecha mas reciente
```sql
SELECT MAX(FEC_ESTADO) FROM tabla
-- Trae la fecha mas nueva de todas
```

### F. OPERADORES LOGICOS

**AND**: Ambas condiciones deben cumplirse
```sql
WHERE ESTADO = 'PROCESO' AND FECHA = TRUNC(SYSDATE)
-- El estado debe ser PROCESO Y la fecha debe ser hoy
```

**OR**: Al menos una condicion debe cumplirse
```sql
WHERE ESTADO = 'ERROR' OR ESTADO = 'PENDIENTE'
-- El estado puede ser ERROR o PENDIENTE
```

**IN**: El valor esta en una lista
```sql
WHERE ID IN (100, 200, 300)
-- Es lo mismo que: ID = 100 OR ID = 200 OR ID = 300
```

**NOT IN**: El valor NO esta en la lista
```sql
WHERE ESTADO NOT IN (3, 5)
-- El estado no puede ser ni 3 ni 5
```

---

## 5. FLUJO TIPICO DE TU TRABAJO - EJEMPLO PRACTICO

### Caso: Recarga CRL no genero factura en SAP (INT-000-0001)

**Problema reportado:**
Una recarga prepago no genero su factura en SAP.

**Paso 1 - Identificar las ordenes de trabajo:**
Te dan los numeros de OT (Orden de Trabajo):
- OT250623.1117.100001
- OT250614.1302.100001

**Paso 2 - Consultar en base de datos:**
```sql
SELECT *
FROM EAI.PEDIDO_PRETUP
WHERE IDTRANSFER IN ('OT250623.1117.100001', 'OT250614.1302.100001')
AND ESTADO = 'PROCESO';
```

**Que buscas:**
- Ver si la orden existe en la tabla
- En que estado esta
- Cuando se registro

**Paso 3 - Validar la fecha:**
Si `FECHAREGISTRO` tiene mas de 45 dias, el servicio no lo procesara por logica de negocio (es una regla configurada).

**Paso 4 - Validar el campo IDPEDIDO:**
Debe ser un numero (ejemplo: ZZ0004072521).
Si no lo es, hay error en los datos y debes derivar al equipo de prepago.

**Paso 5 - Ver el error en los logs:**
Revisas los archivos de log del servidor para ver el error exacto:
```
[idTx=20257214139078169][actualizarFactura]
No existe para el cliente ZZ00040725 ningun maestro de clientes.
```

**Paso 6 - Corregir:**
Segun el error:
- **Error de datos**: Derivas al equipo responsable
- **Error de SAP**: Derivas a SAP
- **Error temporal**: Relanzas tu mismo

**Paso 7 - Relanzar:**
Si puedes relanzar, actualizas el estado a ANULADO:

```sql
UPDATE EAI.PEDIDO_PRETUP
SET ESTADO = 'ANULADO'
WHERE ID IN (718061, 718062, 718063);
COMMIT;
```

**Paso 8 - Ejecutar el JOB:**
Conectas al servidor por SSH y ejecutas:
```bash
sh -x VVS_SH_ACTUALIZARFACTURA
```

Esto vuelve a procesar las ordenes.

**Paso 9 - Validar exito:**
Consultas nuevamente la tabla y verificas que el estado cambio a 'CERRADO':

```sql
SELECT ID, IDTRANSACCION, IDPEDIDO, ESTADO, NROFACTURA, IDTRANSFER
FROM EAI.PEDIDO_PRETUP
WHERE ID IN (718061, 718062, 718063);
```

Si `ESTADO = 'CERRADO'` y `NROFACTURA` tiene valor, el proceso fue exitoso.

---

## 6. QUE ES UN SHELL SCRIPT (.sh)

Un shell script es un archivo con comandos que se ejecutan en servidores Linux/Unix.

**Ejemplo de tu trabajo:**
```bash
sh -x VVS_SH_ACTUALIZARFACTURA
```

**Que hace:**
- `sh`: Ejecuta un script de shell
- `-x`: Modo debug (muestra cada comando mientras se ejecuta)
- `VVS_SH_ACTUALIZARFACTURA`: Nombre del archivo script

**Donde se ejecutan:**
En servidores Linux, conectandote por SSH (conexion remota segura).

**Servidores comunes en tu trabajo:**
- 172.19.67.49: Servidor de migraciones
- 172.19.154.32: Servidor de cancelaciones
- 172.17.27.138: Servidor de portabilidad

**Rutas tipicas:**
- `/home/weblogic/shells/`: Carpeta donde estan los scripts
- `/home/weblogic/shells/POSTPAGO/`: Scripts de servicios postpago
- `/home/weblogic/shells/MIGRACIONES_INICIAR_ACTIVACION/`: Scripts de migraciones

------------------------------------------------------------------------------2-----------------------------------------------------------------------------------

## 7. CONCEPTOS DE TELEFONIA MOVIL

### A. Tipos de servicio:
**PREPAGO**: El cliente paga primero, luego consume.
- Recargas de saldo
- Sin factura mensual

**POSTPAGO**: El cliente consume, luego paga.
- Factura mensual
- Plan con minutos, datos, mensajes

### B. Estados de linea:

**ACTIVA**: La linea funciona normalmente

**SUSPENDIDA**: Temporalmente sin servicio
- Puede ser por falta de pago
- O suspension temporal solicitada

**DESACTIVA**: Dada de baja definitivamente

**UNUSABLE**: No se puede usar (error tecnico)

### C. Operaciones comunes:

**SUSPENSION**: Dejar sin servicio temporal

**REACTIVACION**: Volver a activar una linea suspendida

**DESACTIVACION/BAJA**: Dar de baja permanente

**MIGRACION**: Cambiar de un sistema a otro (ejemplo: de BSCS a CBIO)

**PORTABILIDAD**: Cambiar de operador manteniendo el numero

**CAMBIO DE PLAN**: Modificar el plan de datos/voz

**CAMBIO DE CICLO**: Modificar el dia de facturación

**CAMBIO DE TITULARIDAD**: Cambiar el dueño de la linea

---

## 8. SISTEMAS Y PLATAFORMAS

### A. Bases de datos:

**EAIDB**: Base de datos de integracion empresarial
- Tablas de recargas
- Tablas de pedidos
- Tablas de sincronizacion

**TIMEAI**: Base de datos de programaciones
- Programaciones de servicios
- Migraciones
- Operaciones masivas

**APEAI**: Base de datos de aprovisionamiento
- Activaciones BSCS
- Lineas LTE
- Dispositivos fijos

**BSCS70/BSCS7**: Base de datos del sistema de facturacion
- Contratos
- Clientes
- Estados de linea
- Servicios activos

**IOTDB (IOT)**: Base de datos de dispositivos inteligentes
- Smartwatches
- Lineas asociadas
- Estados de dispositivos

### B. Servicios web:

**Dominio**: Conjunto de servicios en un servidor
- Ejemplo: http://172.19.67.142:7901/console
- Consola de administracion WebLogic

**WebLogic**: Servidor de aplicaciones Java donde corren los servicios

**Nodos**: Servidores individuales dentro de un dominio
- Cuando uno falla, puedes reiniciar solo ese nodo

### C. Archivos importantes:

**LOGS**: Archivos de texto donde se registran todas las operaciones
- Fecha y hora
- ID de transaccion
- Pasos ejecutados
- Errores ocurridos

**Ejemplo de log:**
```
[02-07-2025 14:30:14.198] (EaiDAOImpl.java:107)
[idTx=20257214139078169][actualizarFactura] Inicio de consultaPedidos
```

**Como leer un log:**
- `[02-07-2025 14:30:14.198]`: Fecha y hora exacta
- `(EaiDAOImpl.java:107)`: Archivo y linea de codigo
- `[idTx=20257214139078169]`: ID de transaccion (para rastrear)
- `[actualizarFactura]`: Servicio que se esta ejecutando
- `Inicio de consultaPedidos`: Que esta haciendo en ese momento

---

## 9. PROCESO DE RELANZAMIENTO PASO A PASO

El relanzamiento es volver a ejecutar un proceso que fallo.

### Pasos generales:

**1. Identificar el problema:**
- Revisar la alerta o ticket
- Anotar los IDs de transaccion o numeros de linea

**2. Consultar en base de datos:**
```sql
SELECT * FROM tabla WHERE condicion;
```
- Ver el estado actual
- Identificar el error

**3. Analizar el error:**
- Revisar logs del servicio
- Identificar la causa raiz

**4. Corregir si es necesario:**
- Actualizar datos incorrectos
- Eliminar registros duplicados
- Ajustar fechas

**5. Cambiar estado a pendiente:**
```sql
UPDATE tabla
SET SERVC_ESTADO = 1,
    SERVV_MEN_ERROR = '',
    SERVV_COD_ERROR = ''
WHERE ID IN (lista_de_ids);
COMMIT;
```

**6. Ejecutar el shell de relanzamiento:**
```bash
cd /ruta/del/script
sh -x nombre_script.sh
```

**7. Validar el resultado:**
```sql
SELECT * FROM tabla WHERE ID IN (lista_de_ids);
```
- Verificar que el estado cambio a EXITOSO (3)
- Verificar que se completo la operacion

**8. Documentar:**
- Registrar en el ticket que se hizo
- Cerrar la incidencia

---

## 10. SMARTWATCH - CASO ESPECIAL

Los smartwatch (relojes inteligentes) usan dos lineas telefonicas:

**LINEA PRINCIPAL (EQUIP):**
- Es la linea del telefono movil del cliente
- Numero normal (ejemplo: 51988588727)

**LINEA DUMMY (DISPASOC):**
- Es una linea oculta que usa el smartwatch
- Comparte plan con la linea principal
- El cliente no la ve ni la usa directamente

### Estados en IOTDB:

**Tabla IOTAWT_LINEA_DISPOSITIVO:**
- `LDISC_ESTADO = 0`: Linea libre (disponible)
- `LDISC_ESTADO = 1`: En proceso de activacion
- `LDISC_ESTADO = 2`: Usada correctamente

**Tabla IOTAWT_EQUIPO:**
- `EQUIN_DIPOS_ACT = 0`: Baja total (sin relojes)
- `EQUIN_DIPOS_ACT = 1`: Un reloj activo
- `EQUIN_DIPOS_ACT = 2`: Dos relojes activos

**Tabla IOTAWT_DISPOSITIVO_ASOCIADO:**
- `DISAC_ESTADO = A`: Activo
- `DISAC_ESTADO = U`: Unusable (error, no funciona)
- `DISAC_ESTADO = D`: Desactivado

### Ejemplo de consulta smartwatch:

```sql
SELECT DISAV_MSISDN_EQUIP,      -- Linea principal
       DISAV_IMSI_EQUIP,         -- IMSI principal
       DISAV_MSISDN_DISPASOC,    -- Linea dummy
       DISAV_IMSI_DISPASOC,      -- IMSI dummy
       DISAC_ESTADO,             -- Estado
       DISAD_FECHA_CREACION      -- Fecha creacion
FROM AW.IOTAWT_DISPOSITIVO_ASOCIADO
WHERE DISAV_MSISDN_EQUIP = '51988588727';
```

---

## 11. ERRORES COMUNES Y SOLUCIONES 

### Error 1: "No existe el cliente ZZ00040725"
**Causa:** El codigo de cliente no existe en SAP
**Solucion:** Derivar a SAP para que creen el cliente

### Error 2: "New ISDN in use"
**Causa:** La linea dummy ya esta siendo usada por otro dispositivo
**Solucion:**
```sql
UPDATE AW.IOTAWT_LINEA_DISPOSITIVO
SET LDISC_ESTADO = 2
WHERE LDISV_MSISDN_DUMMY = '51871141600';
COMMIT;
```

### Error 3: "CONTRATO NO ESTA ACTIVO O SUSPENDIDO"
**Causa:** La linea ya esta desactivada
**Solucion:** Actualizar programacion a exitoso (ya se hizo antes)
```sql
UPDATE tabla
SET SERVC_ESTADO = 3,
    SERVV_MEN_ERROR = 'Operacion Exitosa'
WHERE ID = 12345;
COMMIT;
```

### Error 4: Programacion con fecha antigua

**Causa:** La fecha programada es del pasado
**Solucion:** Actualizar a la fecha actual
```sql
UPDATE tabla
SET SERVD_FECHAPROG = TRUNC(SYSDATE),
    SERVV_XMLENTRADA = REPLACE(SERVV_XMLENTRADA,
                               '<fechaProgramacion>2025-01-20</fechaProgramacion>',
                               '<fechaProgramacion>2025-01-21</fechaProgramacion>')
WHERE ID = 12345;
COMMIT;
```

---

## 12. COMANDOS LINUX BASICOS

Cuando te conectas a los servidores por SSH:

**cd**: Cambiar de directorio
```bash
cd /home/weblogic/shells/
```

**ls**: Listar archivos
```bash
ls
ls -l  # Lista detallada con permisos y fechas
```

**vi**: Editor de texto
```bash
vi archivo.txt
```
- Presiona `i` para insertar texto
- Presiona `ESC` luego `:wq` para guardar y salir
- Presiona `ESC` luego `:q!` para salir sin guardar

**cat**: Ver contenido de archivo
```bash
cat archivo.txt
```

**grep**: Buscar texto en archivos
```bash
grep "error" log.txt
grep -i "error" log.txt  # Ignora mayusculas/minusculas
```

**sh**: Ejecutar script
```bash
sh -x script.sh
```

**pwd**: Ver directorio actual
```bash
pwd
```

**exit**: Salir
```bash
exit
```

---

## 13. CONCEPTOS DE CONECTIVIDAD

### SSH (Secure Shell):
Conexion segura a servidores remotos.

**Ejemplo:**
```bash
ssh weblogic@172.19.67.49
```
- `ssh`: Comando de conexion
- `weblogic`: Usuario
- `172.19.67.49`: Direccion IP del servidor

**Proceso de conexion:**
1. Ejecutas el comando ssh
2. El servidor te pide la contraseña
3. Ingresas la contraseña (no se ve mientras escribes)
4. Si es correcta, entras al servidor
5. Ves un prompt como: `[weblogic@servidor ~]$`

### SFTP (Secure File Transfer Protocol):
Transferir archivos entre servidores.

**Ejemplo:**
```bash
sftp weblogic@172.19.67.49
get archivo.txt     # Descargar archivo
put archivo.txt     # Subir archivo
exit                # Salir
```

**Ejemplo real - Transferir archivos de portabilidad:**

```bash
# Conectar al servidor de OSIPTEL
sftp -P 3232 PRSFTPAME@sftp.portabilidad.pe

# Listar archivos
ls

# Cambiar a directorio
cd /app/diarios/202508

# Descargar archivo
get SolicitudesProgramadas_20250804.gz

# Salir
exit
```

**Comandos SFTP importantes:**
- `ls`: Listar archivos remotos
- `lls`: Listar archivos locales
- `cd ruta`: Cambiar directorio remoto
- `lcd ruta`: Cambiar directorio local
- `pwd`: Ver directorio remoto actual
- `lpwd`: Ver directorio local actual
- `get archivo`: Descargar
- `put archivo`: Subir
- `mget *.txt`: Descargar multiples archivos
- `mput *.txt`: Subir multiples archivos

### IP (Direccion IP):
Identificador unico de cada servidor.

**Tipos de servidores en tu trabajo:**

**Red Interna (172.x.x.x):**
- 172.19.67.49: Servidor de migraciones y recargas
- 172.19.154.32: Servidor de cancelaciones CBIO
- 172.17.27.138: Servidor de portabilidad
- 172.17.74.43: Servidor de recepcion archivos CUY
- 172.19.189.17: Servidor WebLogic IOT

**Red Externa/DMZ (192.168.x.x):**
- 192.168.108.100: Servidor intermedio CUY
- 192.168.35.2: Servidor CUY destino

**Bases de datos:**
- EAIDB: Conexion mediante cliente SQL
- TIMEAI: Conexion mediante cliente SQL
- BSCS70: Conexion mediante cliente SQL
- IOTDB: Conexion mediante cliente SQL

### Puerto:
Numero que identifica un servicio en el servidor.

**Puertos comunes:**
- **22**: SSH/SFTP (conexion segura)
- **3232**: SFTP OSIPTEL (personalizado)
- **7901, 7902, 7903**: Consolas WebLogic
- **10000**: Dominio EAI

**Ejemplo:**
```
http://172.19.67.142:7901/console
```
- `172.19.67.142`: IP del servidor
- `7901`: Puerto del servicio
- `/console`: Ruta de la aplicacion

**Donde se usan los puertos:**

**Dominios WebLogic:**
- http://172.19.67.142:7901/console - Dominio de recarga
- http://172.19.189.17:10000/console - Dominio IOT
- http://172.19.67.231:10000/console - Dominio general

**SFTP personalizado:**
- `sftp -P 3232 usuario@servidor` - Puerto 3232 en lugar del 22 default

---

## 14. PROCEDIMIENTOS ALMACENADOS (STORED PROCEDURES)

### Que es un Stored Procedure (SP):

Un SP es un conjunto de instrucciones SQL guardadas en la base de datos que puedes ejecutar como una unidad.

**Ventajas:**
- Mas rapido que ejecutar queries individuales
- Encapsula logica de negocio
- Reutilizable

**Como se invoca desde tu trabajo:**

Los servicios Java llaman a los SP para procesar datos.

**Ejemplo real del instructivo LTE:**

```sql
-- El servicio Java ejecuta este SP
CALL TIM.TIM111_PKG_ACCIONES.SP_DESACTIVAR_CONTRATO_LTE(
    p_co_id => '26414517',
    p_reason => '29',
    p_username => 'E8842027',
    p_cod_msg => ?,
    p_message => ?,
    p_request_id => ?,
    p_request_lte => ?
);
```

**Estructura:**
- `TIM`: Esquema
- `TIM111_PKG_ACCIONES`: Paquete (grupo de SPs)
- `SP_DESACTIVAR_CONTRATO_LTE`: Nombre del SP

**Parametros:**
- `p_co_id`: Entrada - Codigo de contrato
- `p_reason`: Entrada - Motivo de baja (29 = A solicitud del cliente)
- `p_username`: Entrada - Usuario que ejecuta
- `p_cod_msg`: Salida - Codigo de resultado
- `p_message`: Salida - Mensaje de resultado
- `p_request_id`: Salida - ID de request generado
- `p_request_lte`: Salida - ID de request LTE

**Resultado en logs:**

```
p_cod_msg = -2
p_message = CONTRATO NO ESTA ACTIVO O SUSPENDIDO
p_request_id = 0
p_request_lte = 0
```

**Interpretacion:**
- Codigo -2 = Error
- Mensaje = El contrato ya estaba inactivo
- Request 0 = No se genero request (ya estaba dado de baja)

**Otro ejemplo - Registro de estado:**

```sql
-- SP para registrar estado de proceso
CALL apeai.PKG_EAI_PROCESO_LTE.SP_REGISTRA_ESTADO_FASE(
    P_ID_PROCESO => '20230712090743739',
    P_CO_ID => '26414517',
    P_MSISDN => '871305492',
    P_FASE => '4',
    P_CODIGO_ERROR => '21',
    P_MENSAJE_ERROR => 'El estado actual no permite ejecutar la accion'
);
```

**Que hace:**
- Registra en que fase del proceso esta
- Guarda el error que ocurrio
- Permite hacer seguimiento del flujo

### Como validar si un SP funciono:

**1. Revisar codigo de retorno:**
- Codigo 0 o positivo = Exitoso
- Codigo negativo = Error

**2. Revisar mensaje:**
- "Operacion Exitosa" = OK
- Cualquier otro = Leer el mensaje para entender el error

**3. Revisar request_id:**
- Si es 0 = No se genero request (posible error)
- Si es mayor a 0 = Se creo el request (consultar estado)

---

## 15. TABLAS RELACIONADAS Y DEPENDENCIAS

### Como funcionan las tablas relacionadas:

En tu trabajo, muchas operaciones afectan varias tablas a la vez. Debes conocer estas relaciones.

### Ejemplo 1: Programacion de servicios CBIO

**Tabla principal: POSTT_SERVICIOPROG_CBIO**
- Guarda la programacion (que se va a hacer y cuando)

**Tablas relacionadas:**

**ACT_CBIO_TX_INFO:**
- Guarda informacion de la transaccion en proceso
- Si falla el proceso, queda registro aqui
- Debes limpiarla antes de relanzar

**OMT_OPERAC_CALLBACK:**
- Guarda operaciones pendientes de callback
- Estados: REGISTRADO, ENVIADO
- Si falla, queda en REGISTRADO o ENVIADO
- Debes limpiarla antes de relanzar

**GTEOCT_ORDEN:**
- Guarda ordenes de trabajo generadas
- Estados: 1=Pendiente, 2=En proceso, 5=Exitoso
- Si la programacion termina OK pero la orden queda en 2, debes actualizarla a 5

**Ejemplo practico - Relanzar cambio de plan:**

```sql
-- Paso 1: Ver programacion
SELECT * FROM EAIPIVOT.POSTT_SERVICIOPROG_CBIO
WHERE SERVI_COD = 22
AND TRUNC(SERVD_FECHAPROG) = TRUNC(SYSDATE)
AND SERVC_ESTADO = 4;

-- Paso 2: Ver si hay datos en tablas auxiliares
SELECT * FROM EAIPIVOT.ACT_CBIO_TX_INFO
WHERE ID_TRANSACCION IN ('20250265236856');

SELECT * FROM EAIPIVOT.OMT_OPERAC_CALLBACK
WHERE OPCAV_COID_PUB = 'CONTR9927865080';

-- Paso 3: Limpiar tablas auxiliares
DELETE FROM EAIPIVOT.ACT_CBIO_TX_INFO
WHERE ID_TRANSACCION IN ('20250265236856');
COMMIT;

DELETE FROM EAIPIVOT.OMT_OPERAC_CALLBACK
WHERE OPCAV_COID_PUB IN ('CONTR9927865080')
AND OPCAV_ESTADO IN ('REGISTRADO', 'ENVIADO');
COMMIT;

-- Paso 4: Actualizar programacion a pendiente
UPDATE EAIPIVOT.POSTT_SERVICIOPROG_CBIO
SET SERVC_ESTADO = 1,
    SERVV_MEN_ERROR = '',
    SERVV_COD_ERROR = ''
WHERE SERVV_ID_EAI_SW IN ('20250265236856');
COMMIT;

-- Paso 5: Relanzar con shell
-- sh -x SH_MigracionPlanCBIO.sh
```

### Ejemplo 2: Migracion Postpago a Prepago

**Tablas involucradas:**

**POSTT_SERVICIOPROG (ASIS):**
- Programacion en sistema antiguo ASIS
- Estado 1=Pendiente, 2=En proceso baja, 3=Exitoso

**POSTT_SERVICIOPROG_CBIO (CBIO):**
- Programacion en sistema nuevo CBIO
- Mismo esquema de estados

**EAI_MIGRACIONES:**
- Tabla de control de migracion
- Estado 1=Iniciado, 5=Desactivado ASIS, 3=Activado CBIO
- TICKLERBSCS: ID del tickler en BSCS
- REQUESTBSCS: ID del request de aprovisionamiento

**Flujo completo:**

```sql
-- 1. Inicia migracion (estado 1)
-- La programacion POSTT_SERVICIOPROG se crea en estado 1
-- Se crea registro en EAI_MIGRACIONES en estado 1

-- 2. Desactiva en ASIS (estado 2 -> 5)
UPDATE USRACT.POSTT_SERVICIOPROG SET SERVC_ESTADO = 2;
-- Shell ejecuta desactivacion en BSCS
-- Al terminar, EAI_MIGRACIONES pasa a estado 5

-- 3. Activa en CBIO (estado 5 -> 3)
-- Shell ejecuta activacion en prepago
-- Al terminar, EAI_MIGRACIONES pasa a estado 3
-- POSTT_SERVICIOPROG pasa a estado 3
```

**Validacion de estados:**

```sql
-- Ver estado de la migracion completa
SELECT P.SERVV_MSISDN,
       P.SERVC_ESTADO AS ESTADO_PROG,
       M.ESTADO AS ESTADO_MIGRA,
       M.TICKLERBSCS,
       M.REQUESTBSCS,
       M.MENSAJEESTADO
FROM USRACT.POSTT_SERVICIOPROG P
INNER JOIN USRACT.EAI_MIGRACIONES M
  ON P.SERVV_ID_EAI_SW = M.IDTRANSACCION
WHERE P.SERVV_MSISDN = '962745753';
```

**Interpretacion:**

```
MSISDN       | ESTADO_PROG | ESTADO_MIGRA | TICKLER | REQUEST
962745753    | 2           | 5            | 123456  | 0
```

Esto significa:
- Programacion en proceso (2)
- Migracion desactivo ASIS exitoso (5)
- Tiene tickler creado (123456)
- Aun no tiene request de prepago (0)
- Siguiente paso: Activar en prepago

---

## 16. TERMINOS IMPORTANTES

**OT (Orden de Trabajo):** Codigo unico de una operacion
- Formato: OT250623.1117.100001
- OT + fecha + hora + correlativo

**COID:** Codigo de contrato en BSCS
- Identifica unicamente un contrato de cliente

**MSISDN:** Mobile Station International Subscriber Directory Number
- Es el numero de telefono completo con codigo pais
- Ejemplo: 51988588727 (51 = Peru)

**IMSI:** International Mobile Subscriber Identity
- Identifica la tarjeta SIM
- No es visible para el usuario

**ICCID:** Integrated Circuit Card Identifier
- Numero fisico de la tarjeta SIM
- Esta impreso en la SIM

**DN_NUM:** Directory Number
- Otro nombre para el numero telefonico

**REQUEST:** Solicitud enviada a un sistema
- Tiene un ID unico
- Se usa para rastrear operaciones

**TICKLER:** Recordatorio o tarea pendiente en BSCS
- Estado OPEN: Pendiente
- Estado CLOSED: Completado

**HLR:** Home Location Register
- Base de datos de la red movil
- Guarda donde esta el cliente
- Que servicios tiene activos

**PDV:** Punto De Venta
- Tienda o agente que vende servicios

**RFC:** Remote Function Call
- Llamada a funcion remota en SAP
- Ejemplo: ZPSD_RFC_TRS_PEDIDOS

**CLOB:** Character Large Object
- Campo de base de datos para texto muy largo
- Ahi se guarda el XML con todos los parametros

**ROWID:** Identificador fisico de una fila en Oracle
- Es unico y permanente
- Sirve para actualizar un registro especifico

**PKG (Package):** Paquete de Oracle
- Agrupa varios procedimientos almacenados relacionados
- Ejemplo: PKG_EAI_PROCESO_LTE contiene todos los SP de LTE

**SP (Stored Procedure):** Procedimiento almacenado
- Codigo SQL pre-compilado que ejecuta tareas
- Ejemplo: SP_REGISTRA_ESTADO_FASE

**CALLBACK:** Notificacion de respuesta
- Cuando un sistema llama a otro, espera un callback con el resultado
- Estados: REGISTRADO (pendiente), ENVIADO (notificado)

**TICKLER:** Recordatorio o tarea en BSCS
- Se crea cuando hay una accion pendiente
- Estado OPEN: Pendiente de ejecutar
- Estado CLOSED: Completado
- Ejemplo: TICKLER de suspension que se debe cerrar al reactivar

**WA (Work Around):** Solucion temporal
- Script o proceso manual para resolver un problema
- Mientras se implementa la solucion definitiva

**JOB:** Proceso automatico programado
- Se ejecuta periodicamente (cada hora, cada dia, etc.)
- Ejemplo: Job que actualiza facturas cada 15 minutos

**SHELL:** Script de comandos Linux
- Archivo .sh con instrucciones para el servidor
- Automatiza tareas repetitivas

**DOMINIO:** Agrupacion de servicios WebLogic
**7. Logs del servicio:**
- Siempre revisa los logs para entender el error exacto
- Busca el ID de transaccion en los logs
- Lee el mensaje de error completo

**8. Horarios permitidos:**
- Algunos procesos solo se pueden ejecutar en horarios especificos
- Validar si estamos en ventana de mantenimiento
- Validar si hay procesos batch corriendo

---------------------------------------------------------------------3---------------------------------------------------

## 19. HERRAMIENTAS DE TRABAJO DIARIO

### Cliente SQL Developer (para Oracle):

Es la herramienta para conectarte a las bases de datos Oracle.

**Como conectarte:**

1. Abrir SQL Developer
2. Nueva conexion
3. Configurar:
   - Nombre: EAIDB_PROD
   - Usuario: tu_usuario
   - Password: tu_password
   - Tipo: TNS o Basic
   - Hostname: IP del servidor

---

## 22. CHECKLIST DIARIO DE TRABAJO

### Al iniciar tu turno:

**1. Revisar alertas pendientes:**
- Correos de monitoreo APM
- Tickets asignados
- WhatsApp/Teams del equipo

**2. Revisar dashboards:**
- Herramienta de monitoreo
- Verificar servicios criticos activos
- Validar jobs ejecutandose

**3. Conectar herramientas:**
- SQL Developer a bases de datos principales
- PuTTY a servidores mas usados
- Abrir consolas WebLogic importantes

### Durante el trabajo:

**Checklist para cada incidencia:**

- [ ] Leer descripcion completa del problema
- [ ] Anotar datos clave (lineas, OTs, fechas, IDs)
- [ ] Identificar sistema afectado (BSCS, CBIO, IOT, etc.)
- [ ] Consultar estado en base de datos
- [ ] Revisar logs del servicio
- [ ] Identificar causa raiz
- [ ] Determinar accion: relanzar, derivar, corregir
- [ ] Si relanzas: validar datos, limpiar tablas, actualizar estados
- [ ] Ejecutar relanzamiento
- [ ] Validar resultado exitoso
- [ ] Documentar en ticket
- [ ] Cerrar ticket con solucion clara

### Al finalizar tu turno:

**1. Documentar pendientes:**
- Tickets que quedan abiertos
- Coordinaciones pendientes
- Procesos en ejecucion

**2. Comunicar al siguiente turno:**
- Problemas conocidos
- Acciones en progreso
- Alertas recurrentes del dia

**3. Validar procesos criticos:**
- Jobs importantes completados
- No hay procesos detenidos
- Servicios criticos activos

---

## 23. GLOSARIO RAPIDO

**APM:** Application Performance Management - Herramienta de monitoreo
**ASIS:** Sistema legado antiguo de telefonia
**AUC:** Authentication Center - Sistema de autenticacion movil
**Baseline:** Linea base de configuracion
**BSCS:** Billing and Customer Care System - Sistema de facturacion
**Callback:** Notificacion de respuesta de un servicio
**CBIO:** Convergent Billing - Sistema nuevo de facturacion
**COID:** Contract ID - Identificador de contrato
**CRL:** Cajero Recarga en Linea - Sistema de recargas
**CUY:** Cuy Movil - Operador movil virtual
**DMM:** Data Management & Monitoring
**DN:** Directory Number - Numero telefonico
**Dummy:** Linea secundaria oculta (en smartwatch)
**EAI:** Enterprise Application Integration - Integracion empresarial
**EQUIP:** Linea principal (en smartwatch)
**GTEOCT:** Sistema de gestion de ordenes
**HLR:** Home Location Register - Registro de abonados
**ICCID:** Numero fisico de la SIM
**IMS:** IP Multimedia Subsystem - Sistema de multimedia
**IMSI:** International Mobile Subscriber Identity - ID del suscriptor
**IOT:** Internet of Things - Dispositivos inteligentes
**Job:** Proceso automatico programado
**LTE:** Long Term Evolution - Tecnologia 4G
**MSISDN:** Numero de telefono completo internacional
**OT:** Orden de Trabajo
**PDV:** Punto De Venta
**PKG:** Package - Paquete de procedimientos Oracle
**Prepago:** Servicio de pago anticipado
**Postpago:** Servicio de pago posterior
**RFC:** Remote Function Call - Llamada a funcion SAP
**SAP:** Sistema de gestion empresarial
**Shell:** Script de comandos Linux
**SIAC:** Sistema de atencion al cliente
**SIM:** Subscriber Identity Module - Tarjeta del telefono
**SP:** Stored Procedure - Procedimiento almacenado
**SQL:** Lenguaje de consulta de bases de datos
**SSH:** Conexion segura a servidores
**TOBE:** Sistema objetivo nuevo
**TROS:** Sistema de aprovisionamiento
**UDB:** User Database - Base de datos de usuarios
**Unusable:** Estado de error no utilizable
**WA:** Work Around - Solucion temporal
**WebLogic:** Servidor de aplicaciones Java
**XML:** Formato de datos con etiquetas

---

## 24. RECURSOS ADICIONALES

### Contactos importantes:

**Equipo Prepago:**
- Para: Alineacion de datos PRETUPS
- Para: Errores en CRL
- Para: Validacion de pedidos

**Equipo CBIO:**
- Para: Activaciones ONE
- Para: Errores en servicios TOBE
- Para: Tramas de aprovisionamiento

**Equipo SAP:**
- Para: Errores en RFC
- Para: Maestros de clientes
- Para: Creacion de PDV

**Equipo Ejecuciones (OPE CONTINUIDAD):**
- Para: Cambios de plan manuales ASIS
- Para: Procesamiento TROS
- Para: Operaciones masivas

**Equipo BSCS:**
- Para: Validacion de SP
- Para: Contratos y ticklers
- Para: Estados de linea

### Donde encontrar informacion:

**Logs de servicios:**
- Cada servidor en: `/logs/` o `/app/logs/`
- Rotan por fecha: `servidor_20260121.log`
- Buscar por ID de transaccion

**Documentacion:**
- Instructivos en carpeta compartida
- Diagramas de flujo de procesos
- Runbooks de procedimientos

**Bases de conocimiento:**
- Wiki del equipo
- Tickets resueltos anteriormente
- Casos similares documentados

---

## 25. AMAZON WEB SERVICES (AWS) - CONCEPTOS BASICOS

### Que es AWS:

Amazon Web Services es una plataforma de servicios en la nube donde se alojan servidores, bases de datos y aplicaciones.

**Ventajas:**
- No necesitas servidores fisicos
- Puedes crear y destruir recursos facilmente
- Escalabilidad automatica
- Alta disponibilidad

### Servicios AWS que usas:

**EC2 (Elastic Compute Cloud):**
- Servidores virtuales en la nube
- Donde corren tus aplicaciones
- Ejemplo: BASTION-PRODUCCION

**RDS (Relational Database Service):**
- Bases de datos MySQL, MongoDB, etc.
- Gestionadas por AWS
- Backups automaticos

**VPC (Virtual Private Cloud):**
- Red privada virtual
- Aísla tus recursos
- Control de acceso por IP

**Grupos de Seguridad:**
- Firewall virtual
- Define quien puede conectarse
- Reglas de entrada y salida

### EC2 - Instancias (Servidores virtuales):

**Que es una instancia:**
Es un servidor virtual corriendo en AWS.

**Tipos que veras:**
- BASTION-PRODUCCION: Servidor de acceso seguro
- MONGODB-SLAVE: Servidor de base de datos replica
- MONGODB-MASTER: Servidor de base de datos principal

**Estados de una instancia:**
- Running: Funcionando
- Stopped: Detenida
- Terminated: Eliminada permanentemente

**Como acceder a EC2 en AWS:**
1. Iniciar sesion en AWS Console
2. Buscar servicio "EC2"
3. Click en "Instancias"
4. Ver lista de servidores

**Informacion importante de cada instancia:**
- ID de instancia: i-0123456789abcdef0
- IP publica: 34.235.220.97
- IP privada: 172.31.45.67
- Estado: running/stopped
- Tipo: t2.medium, t3.large, etc.

### RDS - Bases de datos gestionadas:

**Que es RDS:**
Servicio de bases de datos en la nube.

**Como acceder:**
1. AWS Console
2. Buscar "RDS"
3. "Bases de datos"
4. Seleccionar la BD

**Informacion clave:**
- Identificador de BD: nombre unico
- Punto de enlace (endpoint): URL para conectarse
- Puerto: 3306 (MySQL), 27017 (MongoDB)
- Motor: MySQL, PostgreSQL, MongoDB
- Usuario maestro: admin, root, etc.

**Ejemplo de endpoint:**
```
database-prod-mysql.c9akciq32w.us-east-1.rds.amazonaws.com
```

Esto es como una IP, pero para base de datos.

### Grupos de Seguridad - Firewall:

**Que son:**
Reglas que definen quien puede conectarse a tus recursos.

**Reglas de entrada (Inbound Rules):**
- SSH (Puerto 22): Para conexion de terminal
- MySQL (Puerto 3306): Para base de datos MySQL
- HTTP (Puerto 80): Para web
- HTTPS (Puerto 443): Para web segura
- Custom: Puertos personalizados

**Como agregar tu IP al grupo de seguridad:**

**Paso 1:** Ir a EC2 > Instancias > BASTION-PRODUCCION

**Paso 2:** Tab "Seguridad" > Click en grupo de seguridad

**Paso 3:** "Editar reglas de entrada"

**Paso 4:** "Agregar regla"
- Tipo: SSH
- Protocolo: TCP
- Puerto: 22
- Origen: Mi IP (se detecta automaticamente)
- Descripcion: Tu nombre y apellido

**Paso 5:** "Guardar reglas"

**Importante:**
- Tu IP publica cambia si cambias de red (casa, oficina, cafe)
- Debes actualizar la regla cada vez que cambies de ubicacion
- Sin esta regla, no podras conectarte al servidor

**Como saber tu IP publica:**
- Google: "cual es mi ip"
- O en AWS, al seleccionar "Mi IP", la detecta automaticamente

---

## 26. BASTION HOST - SERVIDOR DE ACCESO SEGURO

### Que es un Bastion:

Un Bastion (o Jump Server) es un servidor especial que actua como puerta de entrada segura a tu red privada.

**Por que existe:**
- Las bases de datos y servidores internos NO deben ser accesibles directamente desde internet
- El Bastion es el unico servidor expuesto a internet
- Desde el Bastion, te conectas a los servidores internos
- Es como un "recepcionista" que valida quien entra

**Diagrama de conexion:**

```
Tu computadora --> Internet --> Bastion --> Servidores internos (BD, apps)
```

Sin Bastion:
```
Tu computadora --X--> Internet --X--> Servidor interno (BLOQUEADO)
```

### Requisitos para conectarte al Bastion:

**1. Tener la llave privada (.pem):**

La carpeta de llaves debe estar en tu escritorio, ejemplo:
```
C:\Users\micha\Desktop\llaves\bastion-host-prod-v2.pem
```

**Que es un archivo .pem:**
- Es una llave privada criptografica
- Se usa en lugar de password
- Es mas seguro que una contraseña
- Nunca la compartas ni la subas a internet

**2. Estar registrado en el grupo de seguridad:**

Como vimos antes, debes agregar tu IP publica al grupo de seguridad del Bastion.

**3. Tener cliente SSH:**

**Windows:**
- PuTTY: Cliente grafico
- PowerShell/CMD: Cliente de linea de comandos (Windows 10+)
- Git Bash: Alternativa popular

**Mac/Linux:**
- Terminal nativo (ya incluye ssh)

### Como conectarte al Bastion:

**Metodo 1 - Linea de comandos (PowerShell, Terminal):**

```bash
cd C:\Users\micha\Desktop\llaves
ssh -i "bastion-host-prod-v2.pem" ec2-user@ec2-34-235-220-97.compute-1.amazonaws.com
```

**Desglosando el comando:**
- `cd C:\Users\micha\Desktop\llaves`: Ir a la carpeta de llaves
- `ssh`: Comando de conexion segura
- `-i "bastion-host-prod-v2.pem"`: Usar esta llave privada
- `ec2-user`: Usuario del servidor (por defecto en Amazon Linux)
- `@ec2-34-235-220-97.compute-1.amazonaws.com`: Direccion del Bastion

**Primera vez:**
Te preguntara si confias en el servidor:
```
The authenticity of host can't be established.
Are you sure you want to continue connecting (yes/no)?
```
Escribe: `yes`

**Si conecta exitosamente:**
```
[ec2-user@bastion ~]$
```

Ya estas dentro del Bastion.

**Metodo 2 - PuTTY (Windows grafico):**

**Configuracion:**
1. Abrir PuTTY
2. Session:
   - Host Name: ec2-34-235-220-97.compute-1.amazonaws.com
   - Port: 22
   - Connection type: SSH
3. Connection > SSH > Auth:
   - Private key file: Buscar tu archivo .pem
4. Session:
   - Saved Sessions: Bastion-Prod
   - Save
5. Open

**Usuario al conectar:** ec2-user

### Desde el Bastion, conectarte a otros servidores:

Una vez dentro del Bastion, puedes conectarte a servidores internos.

**Ejemplo - Conectar a MongoDB SLAVE:**

**Paso 1:** Buscar la instancia en AWS EC2 > Instancias > "MONGODB SLAVE"

**Paso 2:** Click en "Conectar" > Tab "Cliente SSH"

**Paso 3:** Copiar el comando, ejemplo:
```bash
ssh -i "mongodb-key.pem" ec2-user@10.0.1.45
```

**Paso 4:** Desde el Bastion, ejecutar:
```bash
ssh ec2-user@10.0.1.45
```

**Nota:** Desde el Bastion no necesitas la llave porque estas en la red interna.

**Ahora estas dentro del servidor MongoDB:**
```
[ec2-user@mongodb-slave ~]$
```

---

## 27. MONGODB - BASE DE DATOS NO RELACIONAL

### Que es MongoDB:

MongoDB es una base de datos NoSQL (No SQL = No solo SQL).

**Diferencias con Oracle:**
- Oracle: Base de datos relacional (tablas con filas y columnas)
- MongoDB: Base de datos de documentos (almacena JSON)

**Estructura:**

**Oracle:**
```
Base de datos
  └─ Esquema
      └─ Tabla
          └─ Fila (Registro)
              └─ Columna (Campo)
```

**MongoDB:**
```
Base de datos
  └─ Coleccion
      └─ Documento (JSON)
          └─ Campo
```

**Ejemplo de documento en MongoDB:**
```json
{
  "_id": "507f1f77bcf86cd799439011",
  "msisdn": "51988588727",
  "nombre": "Juan Perez",
  "plan": "Postpago 50GB",
  "estado": "activo",
  "fecha_activacion": "2025-01-15"
}
```

### Arquitectura Master-Slave (Replica Set):

**MASTER (Principal):**
- Recibe todas las escrituras (INSERT, UPDATE, DELETE)
- Envia cambios a los SLAVES
- Si falla, un SLAVE se convierte en MASTER

**SLAVE (Replica):**
- Copia exacta del MASTER
- Solo lectura (SELECT)
- Sirve para backup y distribuir carga de consultas
- Si el MASTER falla, uno se promueve a MASTER

**Ventaja:**
- Alta disponibilidad
- Si el MASTER cae, el servicio continua
- Backups automaticos

### Gestionar MongoDB:

**Conectarte al servidor MongoDB:**
1. SSH al Bastion
2. SSH al servidor MongoDB (SLAVE o MASTER)

**Convertirte en super usuario:**
```bash
sudo su
```

Ahora eres root (administrador).

**Ver estado del servicio MongoDB:**
```bash
systemctl status mongod
```

**Resultado:**
```
Active: active (running)  --> Esta funcionando
Active: inactive (dead)   --> Esta detenido
Active: failed           --> Fallo
```

**Iniciar MongoDB:**
```bash
systemctl start mongod
```

**Detener MongoDB:**
```bash
systemctl stop mongod
```

**Reiniciar MongoDB:**
```bash
systemctl restart mongod
```

**Cuando usar cada comando:**

**start:** Cuando el servicio esta detenido y quieres iniciarlo

**stop:** Cuando necesitas detenerlo para mantenimiento

**restart:** Cuando hay un problema y necesitas reiniciarlo
- Mejor que solo restart, haz: stop, espera 5 segundos, start
- Asi aseguras que se cierre completamente antes de iniciar

**Ver logs de MongoDB:**

```bash
cd /mongodb/logs
ls -ltr
```

Esto lista los logs ordenados por fecha.

```bash
tail -100 mongod.log
```

Ver ultimas 100 lineas del log.

```bash
grep -i "error" mongod.log
```

Buscar errores en el log.

**Errores comunes en MongoDB:**

**Error 1: "Cannot allocate memory"**
- Causa: Sin memoria RAM
- Solucion: Reiniciar o escalar el servidor

**Error 2: "Connection refused"**
- Causa: MongoDB no esta corriendo
- Solucion: systemctl start mongod

**Error 3: "No primary node"**
- Causa: Problema en el replica set
- Solucion: Revisar configuracion del cluster

---

## 28. CONEXION A BASES DE DATOS CON DBEAVER

### Que es DBeaver:

DBeaver es una herramienta grafica universal para conectarte a cualquier base de datos.

**Ventajas sobre SQL Developer:**
- Soporta MySQL, PostgreSQL, MongoDB, Oracle, SQL Server, etc.
- Interfaz moderna
- Gratuito y open source

### Como conectarte a una BD en AWS via DBeaver:

**Requisitos:**
1. Estar conectado al Bastion (o en VPN)
2. Tener las credenciales de la BD
3. Conocer el endpoint de la BD

**Paso 1 - Obtener informacion de la BD:**

**En AWS Console:**
1. RDS > Bases de datos
2. Click en el identificador de la BD
3. Tab "Conectividad y seguridad"

**Datos a anotar:**
- Punto de enlace: `database-prod.c9akciq32w.us-east-1.rds.amazonaws.com`
- Puerto: `3306`

4. Tab "Configuracion"
- Nombre de BD: `produccion_db`

**Paso 2 - Obtener credenciales:**

Buscar en tu archivo de credenciales (Excel) por el endpoint.

**Ejemplo:**
```
Endpoint: database-prod.c9akciq32w.us-east-1.rds.amazonaws.com
Usuario: admin_user
Password: P@ssw0rd123!
```

**Paso 3 - Configurar SSH Tunnel en DBeaver:**

**Por que SSH Tunnel:**
La BD no es accesible directamente desde internet. Debes pasar por el Bastion.

**Configuracion:**
1. Abrir DBeaver
2. Nueva conexion > MySQL (o el motor que sea)
3. Tab "Main":
   - Server Host: `database-prod.c9akciq32w.us-east-1.rds.amazonaws.com`
   - Port: `3306`
   - Database: `produccion_db`
   - Username: `admin_user`
   - Password: `P@ssw0rd123!`

4. Tab "SSH":
   - [X] Use SSH Tunnel
   - Host/IP: `34.235.220.97` (IP del Bastion)
   - Port: `22`
   - User Name: `ec2-user`
   - Authentication Method: `Public Key`
   - Private key: Buscar tu archivo `bastion-host-prod-v2.pem`

5. Test Connection

Si todo esta bien, dira "Connected".

6. Finish

**Paso 4 - Usar la conexion:**

1. En el panel izquierdo, expandir la conexion
2. Ver bases de datos, tablas, etc.
3. Click derecho > SQL Editor > New SQL Script
4. Escribir tu query:
```sql
SELECT * FROM usuarios WHERE msisdn = '51988588727';
```
5. Ejecutar (Ctrl + Enter)

**Ventajas del SSH Tunnel:**
- Tu conexion va: Tu PC > Bastion > BD
- No necesitas que la BD sea publica
- Mas seguro

---

## 29. COMANDOS LINUX AVANZADOS PARA GESTION DE PROCESOS

### ps - Ver procesos en ejecucion:

**ps** (Process Status) muestra los procesos corriendo.

**Sintaxis basica:**
```bash
ps -ef
```

Muestra TODOS los procesos del sistema.

**Resultado:**
```
UID        PID  PPID  C STIME TTY      TIME CMD
root         1     0  0 Jan20 ?        00:00:05 /sbin/init
weblogic  1234     1  0 08:30 ?        00:15:23 java -jar app.jar
weblogic  5678     1  2 14:25 ?        01:45:12 java weblogic.Server
```

**Columnas importantes:**
- **UID**: Usuario que ejecuta el proceso
- **PID**: Process ID (numero unico del proceso)
- **PPID**: Parent PID (proceso padre)
- **STIME**: Hora de inicio
- **TIME**: Tiempo de CPU usado
- **CMD**: Comando ejecutado

**Buscar procesos especificos con grep:**

```bash
ps -ef | grep java
```

Muestra solo procesos que contengan "java".

```bash
ps -ef | grep weblogic.Server
```

Muestra solo los servidores WebLogic.

**Ejemplo real de tu trabajo:**
```bash
ps -ef | grep java | grep weblogic.Server
```

**Resultado:**
```
weblogic  87718     1  2 08:30 ?   01:23:45 java -Dweblogic.Name=AdminServer weblogic.Server
weblogic  88234     1  1 08:32 ?   00:45:23 java -Dweblogic.Name=ManagedServer1 weblogic.Server
weblogic  88567     1  3 08:33 ?   02:15:34 java -Dweblogic.Name=ManagedServer2 weblogic.Server
```

Cada linea es un servidor WebLogic diferente.

### pwdx - Ver directorio de trabajo de un proceso:

**pwdx** muestra en que carpeta esta trabajando un proceso.

**Sintaxis:**
```bash
pwdx PID
```

**Ejemplo:**
```bash
pwdx 87718
```

**Resultado:**
```
87718: /opt/oracle/config/domains/esb_adapter_002
```

Esto te dice que el proceso 87718 esta corriendo desde esa carpeta.

**Uso practico:**
Cuando tienes varios servidores WebLogic, identificas cual es cual por su directorio.

### kill - Terminar un proceso:

**kill** envia una señal a un proceso para terminarlo.

**Sintaxis:**
```bash
kill PID
```

**Ejemplo suave:**
```bash
kill 87718
```

Intenta cerrar el proceso de manera ordenada (SIGTERM).

**Ejemplo forzado:**
```bash
kill -9 87718
```

Mata el proceso inmediatamente (SIGKILL). Usar solo si el kill normal no funciona.

**Cuando usar:**
- Servidor WebLogic no responde
- Consola cargando infinitamente (error 503, 500)
- Proceso colgado

**Proceso completo:**
1. Identificar el PID: `ps -ef | grep weblogic.Server`
2. Matar el proceso: `kill -9 87718`
3. Reiniciar el servidor: `sh startWebLogic.sh`

### nohup - Ejecutar comando en background:

**nohup** (No Hang Up) ejecuta un comando que continua corriendo aunque cierres la sesion SSH.

**Sintaxis:**
```bash
nohup comando &
```

**Ejemplo:**
```bash
nohup sh startWebLogic.sh &
```

**Que hace:**
- `nohup`: No se detiene si cierras SSH
- `sh startWebLogic.sh`: Ejecuta el script
- `&`: Lo ejecuta en background (no bloquea tu terminal)

**La salida se guarda en:**
```
nohup.out
```

**Ver la salida en tiempo real:**
```bash
tail -f nohup.out
```

**Cuando usar:**
- Iniciar servidores WebLogic
- Ejecutar scripts largos
- Procesos que no deben interrumpirse

### tail - Ver final de archivos:

**tail** muestra las ultimas lineas de un archivo.

**Ver ultimas 100 lineas:**
```bash
tail -100 archivo.log
```

**Ver archivo en tiempo real (modo seguimiento):**
```bash
tail -f archivo.log
```

Esto muestra las nuevas lineas que se van agregando al archivo. Muy util para ver logs mientras se ejecuta un proceso.

**Detener el tail -f:**
Presiona `Ctrl + C`

**Ejemplo practico:**
```bash
cd /opt/oracle/config/domains/esb_adapter_002
nohup sh startWebLogic.sh & tail -f nohup.out
```

1. Cambiar a directorio del WebLogic
2. Iniciar WebLogic en background
3. Ver el log en tiempo real

**Buscar en logs mientras ves en tiempo real:**

En otra sesion SSH:
```bash
grep "ERROR" /ruta/log/server.log
```

### locate - Buscar archivos en el sistema:

**locate** encuentra archivos por nombre en todo el sistema.

**Sintaxis:**
```bash
locate nombre_archivo
```

**Ejemplo:**
```bash
locate startWebLogic.sh
```

**Resultado:**
```
/opt/oracle/config/domains/domain1/startWebLogic.sh
/opt/oracle/config/domains/esb_adapter_001/startWebLogic.sh
/opt/oracle/config/domains/esb_adapter_002/startWebLogic.sh
```

Te muestra todas las ubicaciones donde existe ese archivo.

**Uso practico:**
Cuando no sabes en que dominio WebLogic esta el servidor que necesitas reiniciar.

**Actualizar la base de datos de locate:**
```bash
sudo updatedb
```

Ejecutar si locate no encuentra archivos recientes.

---

## 30. GESTION DE SERVIDORES WEBLOGIC

### Que es WebLogic:

WebLogic es un servidor de aplicaciones Java (igual que Tomcat, JBoss).

**Componentes:**
- **Dominio**: Agrupacion logica de servidores
- **Admin Server**: Servidor de administracion (consola web)
- **Managed Server**: Servidores donde corren las aplicaciones

### Estructura de directorios:

```
/opt/oracle/
├── config/
│   └── domains/
│       ├── esb_adapter_001/
│       │   ├── startWebLogic.sh
│       │   ├── stopWebLogic.sh
│       │   └── servers/
│       │       ├── AdminServer/
│       │       └── ManagedServer1/
│       └── esb_adapter_002/
│           ├── startWebLogic.sh
│           └── servers/
└── logs/
```

### Iniciar servidor WebLogic:

**Paso 1 - Ubicar el dominio:**
```bash
locate startWebLogic.sh
```

**Paso 2 - Ir al directorio:**
```bash
cd /opt/oracle/config/domains/esb_adapter_002
```

**Paso 3 - Iniciar servidor:**
```bash
nohup sh startWebLogic.sh & tail -f nohup.out
```

**Paso 4 - Esperar mensaje "RUNNING":**
```
<Server state changed to RUNNING>
```

Esto indica que el servidor inicio correctamente.

**Paso 5 - Validar consola:**
Abrir en navegador:
```
http://IP_SERVIDOR:7001/console
```

### Detener servidor WebLogic:

**Metodo 1 - Script de parada:**
```bash
cd /opt/oracle/config/domains/esb_adapter_002
sh stopWebLogic.sh
```

**Metodo 2 - Kill del proceso:**
```bash
ps -ef | grep weblogic.Server | grep esb_adapter_002
kill -9 PID_ENCONTRADO
```

### Errores comunes WebLogic:

**Error 503 - Service Unavailable:**

**Causa:** El managed server esta caido o no responde

**Solucion:**
1. Ver procesos: `ps -ef | grep weblogic.Server`
2. Si el proceso existe pero no responde: `kill -9 PID`
3. Si no existe el proceso: iniciar con `startWebLogic.sh`

**Error 500 - Internal Server Error:**

**Causa:** Error en la aplicacion o servidor sobrecargado

**Solucion:**
1. Revisar logs: `/opt/oracle/config/domains/DOMINIO/servers/SERVIDOR/logs/`
2. Buscar errores: `grep -i "error" server.log`
3. Si es problema de memoria: reiniciar servidor
4. Si es error de aplicacion: revisar stack trace en log

**Consola no carga (colgada):**

**Sintomas:**
- Navegador cargando infinitamente
- Timeout despues de varios minutos

**Solucion completa:**

**1. Identificar servidor:**
```bash
ps -ef | grep java | grep weblogic.Server
```

**2. Ver directorio de trabajo:**
```bash
pwdx 87718
```

Resultado: `/opt/oracle/config/domains/esb_adapter_002`

**3. Matar proceso:
   - Puerto: 1521 (default Oracle)
   - SID o Service Name: EAIDB

4. Probar conexion
5. Guardar

**Ejecutar queries:**
1. Abrir worksheet
2. Escribir o pegar tu query
3. Ejecutar con F5 (script) o Ctrl+Enter (statement)
4. Ver resultados en la parte inferior

**Tips importantes:**
- Siempre pon punto y coma (;) al final
- Para UPDATE/DELETE, haz COMMIT despues
- Para ver datos, usa F5 que muestra mas claro
- Puedes exportar resultados a Excel

### PuTTY o terminal SSH:

Herramienta para conectarte a servidores Linux.

**Configuracion PuTTY:**
1. Abrir PuTTY
2. En "Host Name": 172.19.67.49
3. Puerto: 22
4. Connection type: SSH
5. Click "Open"
6. Aceptar el certificado (primera vez)
7. Login: weblogic
8. Password: tu_password

**Una vez conectado:**
- Ves un prompt: `[weblogic@servidor ~]$`
- Puedes escribir comandos Linux
- Navegar con `cd`
- Ver archivos con `ls`
- Ejecutar scripts con `sh`

### WinSCP o FileZilla (SFTP):

Para transferir archivos graficamente.

**Configuracion WinSCP:**
1. Nuevo sitio
2. Protocolo: SFTP
3. Servidor: 172.19.67.49
4. Puerto: 22
5. Usuario: weblogic
6. Password: tu_password
7. Conectar

**Interfaz:**
- Lado izquierdo: Tu computadora
- Lado derecho: Servidor remoto
- Arrastras archivos entre ambos lados
- Puedes editar archivos directamente

### Visor de logs:

**Notepad++ o Sublime Text:**
- Para abrir archivos de log grandes
- Buscar por ID de transaccion
- Ver con colores de sintaxis

**Comando grep en Linux:**
```bash
# Buscar ID de transaccion en logs
grep "20257214139078169" /path/to/log/*.log

# Buscar errores del dia
grep -i "error" /path/to/log/server_$(date +%Y%m%d).log

# Ver ultimas 100 lineas del log
tail -100 /path/to/log/server.log

# Ver log en tiempo real
tail -f /path/to/log/server.log
```

### Consola WebLogic:

Interfaz web para administrar dominios.

**Acceso:**
- URL: http://172.19.67.142:7901/console
- Usuario: weblogic o admin
- Password: password_admin

**Que puedes ver:**
- Estado de servicios (deployments)
- Nodos activos/inactivos
- Logs del servidor
- Reiniciar servicios
- Ver hilos (threads) en ejecucion

**Como ver logs desde consola:**
1. Domain Structure > Servers
2. Click en el servidor (ej: wls03-EAIDomainRecarga02)
3. Tab "Logging"
4. View log files
5. Buscar tu ID de transaccion

---

## 20. CASOS PRACTICOS PASO A PASO

### Caso 1: Smartwatch - Linea unusable (INT-000-0007)

**Problema:** Recibiste alerta de linea en estado unusable

**Paso a paso completo:**

**1. Leer el correo de alerta:**
```
Alerta: Linea unusable detectada
Fecha: 2025-01-21
Hora: 14:30
```

**2. Conectarte a IOTDB:**
- Abrir SQL Developer
- Conectarte a base de datos IOT

**3. Ejecutar query para contar unusable:**
```sql
SELECT COUNT(1) FROM (
    SELECT * FROM (
        SELECT A.DISAV_IMSI_DISPASOC,
               A.DISAV_MSISDN_DISPASOC,
               A.DISAV_MSISDN_EQUIP,
               A.DISAC_ESTADO,
               C.MSCLV_MSJRPTA_IMS
        FROM AW.IOTAWT_DISPOSITIVO_ASOCIADO A
        INNER JOIN AW.IOTAWT_CAB_MESA_CONTROL C
          ON C.MSCLV_MSISDN_EQUIP = A.DISAV_MSISDN_EQUIP
        WHERE A.DISAD_FECHA_MODIFICACION IS NOT NULL
          AND C.MSCLV_MSJRPTA_IMS NOT IN ('Exito', 'Operacion Exitosa')
          AND TRUNC(C.MSCLD_FECHA_CREACION) = TRUNC(SYSDATE)
          AND TRUNC(A.DISAD_FECHA_CREACION) = TRUNC(SYSDATE)
        ORDER BY A.DISAD_FECHA_MODIFICACION DESC
    )
    WHERE ROWNUM <= 1
)
WHERE DISAC_ESTADO = 'U';
```

**Resultado esperado:**
```
COUNT(1)
   1
```

Hay 1 linea unusable.

**4. Ver detalles de las altas fallando:**
```sql
SELECT DISAV_MSISDN_DISPASOC,
       DISAV_IMSI_DISPASOC,
       DISAV_MSISDN_EQUIP,
       DISAV_IMSI_EQUIP,
       DISAC_ESTADO,
       DISAD_FECHA_MODIFICACION
FROM AW.IOTAWT_DISPOSITIVO_ASOCIADO
WHERE DISAD_FECHA_MODIFICACION IS NOT NULL
ORDER BY DISAD_FECHA_MODIFICACION DESC;
```

**Resultado:**
```
DUMMY         | IMSI_DUMMY      | EQUIP       | IMSI_EQUIP      | ESTADO | FECHA
51871141600   | 716101682308301 | 51988588727 | 716101201779656 | U      | 21-01-2026 14:25
```

Anotar la dummy: 51871141600

**5. Ver el error especifico:**
```sql
SELECT A.DISAC_ESTADO,
       C.MSCLV_MSJRPTA_IMS,
       A.DISAD_FECHA_MODIFICACION
FROM AW.IOTAWT_DISPOSITIVO_ASOCIADO A
INNER JOIN AW.IOTAWT_CAB_MESA_CONTROL C
  ON C.MSCLV_MSISDN_EQUIP = A.DISAV_MSISDN_EQUIP
WHERE A.DISAV_MSISDN_DISPASOC = '51871141600'
  AND TRUNC(C.MSCLD_FECHA_CREACION) = TRUNC(SYSDATE)
ORDER BY A.DISAD_FECHA_MODIFICACION DESC;
```

**Resultado:**
```
ESTADO | MENSAJE
U      | Error al consumir UDBConnector, Error: [ERR3051: New ISDN in use]
```

**6. Validar si la dummy tiene activacion real:**
```sql
SELECT * FROM AW.IOTAWT_DISPOSITIVO_ASOCIADO
WHERE DISAV_MSISDN_DISPASOC = '51871141600'
AND DISAC_ESTADO = 'A';
```

**Resultado:** No devuelve registros (0 rows)

Conclusion: La dummy NO tiene activacion real, pero el sistema piensa que esta en uso.

**7. Liberar la dummy:**
```sql
UPDATE AW.IOTAWT_LINEA_DISPOSITIVO
SET LDISC_ESTADO = '2'
WHERE LDISV_MSISDN_DUMMY = '51871141600';
COMMIT;
```

**Resultado:**
```
1 fila actualizada.
```

**8. Validar el cambio:**
```sql
SELECT LDISC_ESTADO, LDISV_MSISDN_DUMMY
FROM AW.IOTAWT_LINEA_DISPOSITIVO
WHERE LDISV_MSISDN_DUMMY = '51871141600';
```

**Resultado:**
```
ESTADO | DUMMY
2      | 51871141600
```

Estado 2 = Linea utilizada correctamente (ya no esta bloqueada)

**9. Documentar en el ticket:**
```
Solucion aplicada:
- Linea dummy 51871141600 estaba marcada como en uso
- Validado que no tiene activacion real
- Actualizado estado a 2 (liberada)
- Query ejecutada: UPDATE AW.IOTAWT_LINEA_DISPOSITIVO SET LDISC_ESTADO='2'...
- La proxima alta ya deberia funcionar correctamente
- Alerta se resolvera con la siguiente alta exitosa
```

---

### Caso 2: Programacion de desactivacion CBIO (INT-000-0003)

**Problema:** Hay programaciones de desactivacion en estado error

**Paso a paso completo:**

**1. Consultar programaciones con error:**
```sql
SELECT SERVV_ID_EAI_SW,
       SERVV_MSISDN,
       SERVC_ESTADO,
       SERVV_MEN_ERROR,
       SERVD_FECHAPROG
FROM EAIPIVOT.POSTT_SERVICIOPROG_CBIO
WHERE SERVI_COD = '18'
  AND TRUNC(SERVD_FECHAPROG) = TRUNC(SYSDATE)
  AND SERVC_ESTADO NOT IN (3,5);
```

**Resultado:**
```
ID_EAI              | MSISDN    | ESTADO | ERROR              | FECHA
20250121140532801   | 988588727 | 4      | Timeout en proceso | 21-01-2026
20250121140532802   | 999123456 | 4      | Timeout en proceso | 21-01-2026
```

2 programaciones en error por timeout.

**2. Validar estado real de las lineas:**
- Conectar al servidor 172.17.27.216
- Navegar a: /home/usrcbio/ONEAMX/SHELL/SHELLS_MOTOR/Shell_Consulta_IX
- Editar archivo mm.txt con las lineas:

```bash
ssh usrcbio@172.17.27.216
cd /home/usrcbio/ONEAMX/SHELL/SHELLS_MOTOR/Shell_Consulta_IX
vi mm.txt
```

Contenido del archivo mm.txt:
```
51988588727
51999123456
```

Guardar (ESC :wq)

**3. Ejecutar la consulta:**
```bash
sh IX.sh
```

**4. Ver resultado:**
```bash
cat resultado.txt
```

**Resultado:**
```
51988588727|DESACTIVO|29|2026-01-21
51999123456|ACTIVO|00|
```

Primera linea: Ya esta desactiva (motivo 29 = A solicitud del cliente)
Segunda linea: Aun esta activa

**5. Actualizar programacion de linea ya desactiva:**
```sql
UPDATE EAIPIVOT.POSTT_SERVICIOPROG_CBIO
SET SERVC_ESTADO = 3,
    SERVV_MEN_ERROR = 'Operacion Exitosa - Linea ya estaba desactiva',
    SERVV_COD_ERROR = ''
WHERE SERVV_MSISDN = '988588727'
  AND SERVI_COD = '18'
  AND TRUNC(SERVD_FECHAPROG) = TRUNC(SYSDATE);
COMMIT;
```

**6. Para la linea aun activa, armar trama TROS:**

Formato: "DROP2_DESACTIVACION","numero",29

En Excel:
```
=CONCATENAR("""DROP2_DESACTIVACION"",""";B2;""",29")
```

Donde B2 = 51999123456

Resultado:
```
"DROP2_DESACTIVACION","51999123456",29
```

**7. Crear archivo para TROS:**
```bash
vi desactivacion_manual.txt
```

Pegar la trama:
```
"DROP2_DESACTIVACION","51999123456",29
```

Guardar y ejecutar proceso TROS (coordinar con Ejecuciones)

**8. Despues que TROS confirme la baja, actualizar programacion:**
```sql
UPDATE EAIPIVOT.POSTT_SERVICIOPROG_CBIO
SET SERVC_ESTADO = 3,
    SERVV_MEN_ERROR = 'Operacion Exitosa - Procesado manual via TROS',
    SERVV_COD_ERROR = ''
WHERE SERVV_MSISDN = '999123456'
  AND SERVI_COD = '18'
  AND TRUNC(SERVD_FECHAPROG) = TRUNC(SYSDATE);
COMMIT;
```

**9. Actualizar ordenes en GTEOCT:**
```sql
UPDATE EAIPIVOT.GTEOCT_ORDEN
SET ORDV_ESTADO = 5
WHERE ORDV_NRO_LINEA IN ('51988588727', '51999123456')
  AND ORDV_TRANS_NEG = 'desactMov'
  AND TRUNC(ORDD_FEC_REG) = TRUNC(SYSDATE)
  AND ORDV_ESTADO = 2;
COMMIT;
```

---

## 21.
**NODO:** Servidor individual dentro de un dominio
- Ejecuta los servicios web
- Si falla, se puede reiniciar sin afectar otros nodos

---

## 17. COMO INTERPRETAR ERRORES COMUNES

### Errores de datos:

**Error: "No existe el cliente ZZ00040725"**

**Causa:** El codigo de cliente no esta registrado en SAP

**Accion:**
1. Validar si el codigo es correcto
2. Buscar el cliente en SAP
3. Si no existe, derivar a SAP para que lo creen
4. Si existe con codigo diferente, corregir en la tabla origen

**Como derivar:**
Asunto: Cliente ZZ00040725 no existe en SAP
Detalle: Se requiere creacion de maestro de cliente
OT afectadas: OT250623.1117.100001
Error: No existe para el cliente ZZ00040725 ningun maestro de clientes
Log: [adjuntar extracto del log]

---

**Error: "New ISDN in use"**

**Causa:** La linea dummy ya esta siendo usada por otro smartwatch

**Accion:**
1. Validar si realmente esta activa:
```sql
SELECT * FROM AW.IOTAWT_DISPOSITIVO_ASOCIADO
WHERE DISAV_MSISDN_DISPASOC = '51871141600'
AND DISAC_ESTADO = 'A';
```

2. Si NO esta activa (no devuelve registros), liberar la linea:
```sql
UPDATE AW.IOTAWT_LINEA_DISPOSITIVO
SET LDISC_ESTADO = '2'
WHERE LDISV_MSISDN_DUMMY = '51871141600';
COMMIT;
```

3. Si SI esta activa, buscar otra linea dummy disponible

---

**Error: "CONTRATO NO ESTA ACTIVO O SUSPENDIDO"**

**Causa:** Intentas desactivar un contrato que ya esta desactivo

**Accion:**
1. Validar estado actual:
```sql
SELECT DN_NUM, CO_ID, CH_STATUS, DES_MOTIVO_EST
FROM TIM.PP_DATOS_CONTRATO
WHERE DN_NUM = '51988588727'
AND FEC_ESTADO = (SELECT MAX(FEC_ESTADO)
                  FROM TIM.PP_DATOS_CONTRATO PT2
                  WHERE DN_NUM = '51988588727');
```

2. Si ya esta desactivo, actualizar programacion a exitoso:
```sql
UPDATE APEAI.POSTT_SERVICIOPROG_FIJA_LTE
SET SERVC_ESTADO = 3,
    SERVV_MEN_ERROR = 'Operacion Exitosa - Linea ya estaba desactiva'
WHERE CO_ID = '26414517'
AND SERVI_COD = 18;
COMMIT;
```

---

### Errores de proceso:
**Error: "El documento de venta no se modifica"**
**Causa:** Error general de SAP, puede tener varias causas

**Accion:**
1. Ver el error especifico anterior en el log
2. Generalmente viene acompañado de otro error mas especifico
3. Resolver el error especifico primero

---

**Error: "No se ha creado el solicitante 4075168 para area de ventas PE02 12 13"**

**Causa:** El punto de venta (PDV) no esta registrado para esa area

**Accion:**
1. Derivar al usuario de negocio
2. Solicitar que registren el PDV correctamente en SAP
3. Adjuntar el codigo del solicitante y area de ventas

---

### Errores de validacion:

**Error: Fecha programacion mayor a 45 dias**

**Causa:** La logica de negocio no permite procesar ordenes muy antiguas

**Accion:**
1. Validar si es correcto reprocesar
2. Si es necesario, coordinar con el area de negocio
3. Generalmente estas ordenes se cancelan:
```sql
UPDATE EAI.PEDIDO_PRETUP
SET ESTADO = 'ANULADO',
    MENSAJE = 'Cancelado por antiguedad - Fuera de SLA'
WHERE ID IN (718061, 718062);
COMMIT;
```

---

## 18. VALIDACIONES QUE DEBES HACER

Antes de relanzar siempre valida:

**1. Fecha de programación:** // buscar que es la fecha de programación
- No debe ser muy antigua (máximo 45 dias segun servicio)
- Debe ser fecha valida (no festivos si aplica)

**2. Estado del servicio:**
- Linea debe existir
- Debe estar en el estado correcto para la operacion

**3. Datos correctos:**
- Numeros de telefono validos
- Clientes existan en los sistemas
- Planes y servicios sean compatibles

**4. No duplicados:**
- No debe haber otra programacion igual pendiente
- No debe estar procesando en ese momento

**5. Dependencias:**
- Si es migracion, validar que primero se desactive en un sistema
- Luego validar que se active en el otro

**6. Tablas relacionadas:**
- A veces hay que limpiar tablas auxiliares antes de relanzar
- Ejemplo: ACT_CBIO_TX_INFO, OMT_OPERAC_CALLBACK

---

## RESUMEN FINAL

Como analista de integracion tu trabajo es:

1. **Recibir alertas** de procesos que fallaron
2. **Consultar bases de datos** con SELECT para ver que paso
3. **Analizar logs** para identificar el error exacto
4. **Corregir datos** si es necesario con UPDATE
5. **Limpiar tablas** auxiliares con DELETE si aplica
6. **Relanzar procesos** ejecutando scripts en servidores
7. **Validar** que el proceso termino exitosamente
8. **Documentar** lo que hiciste

Las herramientas principales son:
- **SQL** para consultar y modificar bases de datos
- **Shell scripts** para ejecutar procesos automaticos
- **SSH** para conectarte a servidores
- **Logs** para entender que fallo

Los conceptos mas importantes son:
- Estados de procesos (pendiente, proceso, exitoso, error, cancelado)
- Tipos de servicios (suspension, reactivacion, baja, migracion, etc.)
- Estructura de tablas Oracle (esquema.tabla, campos, registros)
- Operaciones SQL (SELECT, UPDATE, DELETE, COMMIT)

Con esta guia tienes la base para entender los instructivos y empezar a trabajar. Cada caso es diferente pero el proceso general es siempre el mismo: identificar, analizar, corregir, relanzar, validar.

---

## 31. ESCALAMIENTO DE CORREOS Y CASOS

### Que es escalar:

**ESCALAR** significa subir un caso o incidencia a un nivel superior cuando:
- No puedes resolverlo con tus accesos/conocimientos
- El problema requiere decision de negocio
- Supera el tiempo de resolucion permitido
- Es critico y afecta a muchos usuarios

### Niveles de escalamiento:

**NIVEL 1 (N1) - Analista de Integracion (TU):**
- Monitoreo de alertas
- Correccion de errores conocidos
- Relanzamiento de procesos
- Tiempo de resolucion: 2-4 horas

**NIVEL 2 (N2) - Equipo Especializado:**
- Problemas en sistemas especificos (SAP, BSCS, HLR)
- Errores de configuracion
- Bugs en servicios web
- Tiempo de resolucion: 4-8 horas

**NIVEL 3 (N3) - Desarrollo/Arquitectura:**
- Errores de codigo (bugs)
- Cambios en logica de negocio
- Problemas de infraestructura
- Tiempo de resolucion: 1-3 dias

**NIVEL 4 (N4) - Proveedores/Vendors:**
- Oracle, IBM, SAP (soporte oficial)
- Problemas de licenciamiento
- Bugs de producto
- Tiempo de resolucion: 3-10 dias

### Cuando escalar:

**Escala INMEDIATAMENTE si:**
- Servicio caido que afecta a clientes (severidad critica)
- No tienes accesos para resolver
- El error es de otro sistema (SAP, HLR, BSCS)
- Detectas un bug en el codigo

**Escala DENTRO DE 2 HORAS si:**
- Intentaste resolver pero no funciona
- Necesitas validacion de negocio
- El error se repite constantemente

**Escala DENTRO DE 4 HORAS si:**
- Esta fuera de tu alcance
- Requiere cambio en configuracion
- Necesitas permisos especiales

### Como escalar correctamente:

**1. Recopilar informacion:**
```
- ID de transaccion
- Numero de ticket (INT-000-XXXX)
- Lineas/clientes afectados
- Fecha y hora del error
- Queries ejecutadas
- Logs del error (extracto relevante)
- Que intentaste hacer
```

**2. Redactar correo de escalamiento:**

**Asunto:**
```
[URGENTE] Escalamiento N2 - INT-000-1234 - Error en facturacion SAP
```

**Cuerpo del correo:**
```
Estimado equipo SAP,

Requiero soporte para resolver el siguiente caso:

TICKET: INT-000-1234
SEVERIDAD: Alta
SISTEMA AFECTADO: SAP - Modulo de facturacion
IMPACTO: 15 clientes sin factura generada

DESCRIPCION DEL PROBLEMA:
Las ordenes de recarga CRL no generan factura en SAP.
Error reportado: "No existe el cliente ZZ00040725"

EVIDENCIAS:
- OT afectadas: OT250623.1117.100001, OT250614.1302.100001
- Query ejecutada:
  SELECT * FROM EAI.PEDIDO_PRETUP 
  WHERE IDTRANSFER IN ('OT250623.1117.100001')
  
- Log de error:
  [idTx=20257214139078169][actualizarFactura]
  No existe para el cliente ZZ00040725 ningun maestro de clientes

ACCIONES REALIZADAS:
1. Validado que IDPEDIDO es correcto: ZZ0004072521
2. Consultado tabla EAI.PEDIDO_PRETUP - registro existe
3. Intentado relanzar - mismo error

REQUERIMIENTO:
Validar si cliente ZZ00040725 existe en SAP
Si no existe, crear maestro de cliente
Si existe con otro codigo, informar codigo correcto

Adjunto: log completo, screenshot de query

Saludos,
[Tu nombre]
Analista de Integracion
```

**3. Hacer seguimiento:**
- Cada 2 horas para casos criticos
- Cada 4 horas para casos altos
- Cada 8 horas para casos medios

### Indicadores de gestion (SLA):

**SLA = Service Level Agreement (Acuerdo de Nivel de Servicio)**

Son los tiempos maximos para resolver segun severidad:

**CRITICO (P1):**
- Impacto: Servicio caido, afecta a todos los clientes
- Tiempo de respuesta: 15 minutos
- Tiempo de resolucion: 4 horas
- Ejemplo: WebLogic caido, nadie puede hacer recargas

**ALTO (P2):**
- Impacto: Funcionalidad importante afectada
- Tiempo de respuesta: 30 minutos  
- Tiempo de resolucion: 8 horas
- Ejemplo: Programaciones de suspension fallando

**MEDIO (P3):**
- Impacto: Problema funcional menor
- Tiempo de respuesta: 2 horas
- Tiempo de resolucion: 24 horas
- Ejemplo: Una linea smartwatch en estado unusable

**BAJO (P4):**
- Impacto: Consulta o mejora
- Tiempo de respuesta: 4 horas
- Tiempo de resolucion: 72 horas
- Ejemplo: Reportar mejora en un proceso

### Indicadores transversales:

**Dispatcher (Despachador):**
- Persona que distribuye los tickets
- Asigna casos segun especialidad
- Destraba casos bloqueados
- Ejemplo: Carmencita distribuye entre Rocio y Royer

**Indicador escalable:**
- Metrica que mide si se escalo correctamente
- % de casos escalados en tiempo
- % de casos resueltos sin escalar
- Tiempo promedio de resolucion

---

## 32. UMBRALES Y GRAFICOS EN AWS CLOUDWATCH

### Que es AWS CloudWatch:

**CloudWatch** es el servicio de monitoreo de Amazon Web Services (AWS).

**Para que sirve:**
- Monitorear servidores en la nube
- Ver graficos de uso de CPU, memoria, disco
- Crear alertas cuando algo supera un limite
- Ver logs de aplicaciones

### Que es un UMBRAL:

**UMBRAL** es el limite maximo/minimo permitido antes de generar alerta.

**Ejemplo:**
- Umbral de CPU: 80%
- Si el servidor llega a 85% de CPU → Se genera alerta

**Tipos de umbrales:**

**UMBRAL ALTO:**
```
CPU > 80% por mas de 5 minutos → ALERTA
```

**UMBRAL BAJO:**
```
Transacciones por segundo < 10 → ALERTA
(Posible caida del servicio)
```

**UMBRAL DE CAMBIO:**
```
Errores aumentan 300% en 10 minutos → ALERTA
```

### Como ver graficos en CloudWatch:

**1. Acceder a AWS Console:**
```
URL: https://console.aws.amazon.com
Usuario: tu_usuario_aws
Password: tu_password
```

**2. Ir a CloudWatch:**
- Servicios → CloudWatch
- O buscar "CloudWatch" en la barra superior

**3. Ver metricas:**
- Click en "Metrics" (Metricas)
- Seleccionar categoria:
  - EC2 (servidores)
  - RDS (bases de datos)
  - Lambda (funciones)
  - Custom (personalizadas)

**4. Crear grafico:**
- Seleccionar metrica (ejemplo: CPUUtilization)
- Seleccionar instancia (servidor especifico)
- Ajustar periodo (1 min, 5 min, 1 hora)
- Ver grafico generado

### Metricas importantes para tu trabajo:

**CPU Utilization:**
- Uso de procesador
- Normal: 20-60%
- Alerta si > 80%
- Critico si > 95%

**Memory Utilization:**
- Uso de memoria RAM
- Normal: 40-70%
- Alerta si > 85%
- Critico si > 95%

**Disk Space:**
- Espacio en disco
- Alerta si > 80% usado
- Critico si > 90% usado

**Network In/Out:**
- Trafico de red entrante/saliente
- Detecta picos anomalos
- Identifica ataques DDoS

**Application Metrics (Custom):**
- Transacciones por segundo
- Tiempo de respuesta promedio
- Cantidad de errores
- Programaciones exitosas vs fallidas

### Como crear una alerta:

**1. Ir a Alarms en CloudWatch**

**2. Create Alarm**

**3. Select Metric:**
```
EC2 → Per-Instance Metrics → CPUUtilization
Seleccionar instancia: i-0123456789
```

**4. Configurar condicion:**
```
Tipo: Static (estatico)
When: Greater than (mayor que)
Threshold: 80
```

**5. Configurar periodo:**
```
Datapoints to alarm: 2 out of 2
(Alerta si 2 de 2 puntos superan el umbral)

Period: 5 minutes
(Evaluar cada 5 minutos)
```

**6. Configurar accion:**
```
Notification: Send email to → tu_email@empresa.com
Message: CPU superior a 80% en servidor WebLogic
```

**7. Crear alarma**

### Interpretar graficos:

**Grafico normal:**
```
CPU (%)
100 |
 80 |              
 60 |    ___    ___
 40 | __/   \__/   \__
 20 |
  0 |___________________
     10am  12pm  2pm  4pm
```
Uso variable pero dentro de limites.

**Grafico con problema:**
```
CPU (%)
100 |        ________
 80 |    ___/        \
 60 |   /             
 40 | _/              
 20 |
  0 |___________________
     10am  12pm  2pm  4pm
```
CPU sostenida al 100% → Problema de rendimiento.

**Grafico de error intermitente:**
```
Errors
 50 |    *
 40 |    *
 30 |    *  *
 20 |    *  *
 10 |*   *  *  *
  0 |___________________
     10am  12pm  2pm  4pm
```
Picos de errores → Investigar logs en esos horarios.

---

## 33. PRUEBAS DE QUERIES

### Por que probar queries:

**Antes de ejecutar en PRODUCCION, siempre prueba:**
- En ambiente de DESARROLLO o QA
- Con datos de prueba
- Con ROWNUM <= 1 para limitar impacto

**Riesgos de queries sin probar:**
- Borrar datos incorrectos
- Actualizar registros equivocados
- Bloquear tablas en produccion
- Generar errores masivos

### Tipos de pruebas:

**1. PRUEBA DE SINTAXIS:**

Verificar que la query no tenga errores de escritura.

```sql
-- Query con error de sintaxis
SELECT * FORM tabla WHERE id = 1;
-- Error: FORM deberia ser FROM
```

**Como probar:**
- Ejecutar en SQL Developer
- Ver mensaje de error
- Corregir antes de usar en produccion

**2. PRUEBA DE RESULTADO:**

Verificar que devuelve lo esperado.

```sql
-- Quiero ver solo 1 registro de prueba
SELECT * FROM EAI.PEDIDO_PRETUP
WHERE IDTRANSFER = 'OT250623.1117.100001'
AND ROWNUM <= 1;
```

**Validar:**
- Cantidad de registros (debe ser 1)
- Campos correctos
- Valores esperados

**3. PRUEBA DE IMPACTO:**

Verificar cuantos registros afectara un UPDATE/DELETE.

```sql
-- ANTES de hacer UPDATE, contar cuantos afectara
SELECT COUNT(1) FROM EAI.PEDIDO_PRETUP
WHERE ESTADO = 'PROCESO'
AND TRUNC(FECHAREGISTRO) < TRUNC(SYSDATE) - 45;
```

**Resultado: 150 registros**

Si esperabas 5 y te sale 150 → NO EJECUTES EL UPDATE, revisa la condicion.

**4. PRUEBA CON ROLLBACK:**

Hacer UPDATE pero deshacerlo para ver que pasaria.

```sql
-- Iniciar transaccion
UPDATE EAI.PEDIDO_PRETUP
SET ESTADO = 'ANULADO'
WHERE ID = 718061;

-- Ver el resultado
SELECT * FROM EAI.PEDIDO_PRETUP WHERE ID = 718061;
-- Muestra: ESTADO = 'ANULADO'

-- DESHACER (no guardar)
ROLLBACK;

-- Ver nuevamente
SELECT * FROM EAI.PEDIDO_PRETUP WHERE ID = 718061;
-- Muestra: ESTADO = 'PROCESO' (volvio al estado original)
```

**IMPORTANTE:**
- COMMIT = Guardar cambios (permanente)
- ROLLBACK = Deshacer cambios (volver atras)

### Metodologia de prueba:

**Paso 1 - Hacer SELECT primero:**
```sql
-- Ver los registros ANTES de modificar
SELECT ID, ESTADO, IDTRANSFER
FROM EAI.PEDIDO_PRETUP
WHERE IDTRANSFER IN ('OT250623.1117.100001', 'OT250614.1302.100001');
```

**Resultado:**
```
ID      | ESTADO  | IDTRANSFER
718061  | PROCESO | OT250623.1117.100001
718062  | PROCESO | OT250614.1302.100001
```

**Paso 2 - Convertir SELECT en UPDATE:**
```sql
UPDATE EAI.PEDIDO_PRETUP
SET ESTADO = 'ANULADO'
WHERE IDTRANSFER IN ('OT250623.1117.100001', 'OT250614.1302.100001');
```

**Paso 3 - Ver cuantos afectara:**
Oracle dice: "2 rows updated"

**Paso 4 - Validar con SELECT:**
```sql
SELECT ID, ESTADO, IDTRANSFER
FROM EAI.PEDIDO_PRETUP
WHERE IDTRANSFER IN ('OT250623.1117.100001', 'OT250614.1302.100001');
```

**Resultado:**
```
ID      | ESTADO  | IDTRANSFER
718061  | ANULADO | OT250623.1117.100001
718062  | ANULADO | OT250614.1302.100001
```

**Paso 5 - Si esta correcto, hacer COMMIT:**
```sql
COMMIT;
```

**Paso 6 - Si esta incorrecto, hacer ROLLBACK:**
```sql
ROLLBACK;
```

### Errores comunes al probar:

**Error 1: No usar WHERE**
```sql
-- MAL - Actualiza TODA la tabla
UPDATE EAI.PEDIDO_PRETUP
SET ESTADO = 'ANULADO';

-- BIEN - Solo registros especificos
UPDATE EAI.PEDIDO_PRETUP
SET ESTADO = 'ANULADO'
WHERE ID IN (718061, 718062);
```

**Error 2: Condicion muy amplia**
```sql
-- MAL - Puede afectar miles de registros
UPDATE USRACT.POSTT_SERVICIOPROG
SET SERVC_ESTADO = 1
WHERE SERVI_COD = 3;

-- BIEN - Condicion mas especifica
UPDATE USRACT.POSTT_SERVICIOPROG
SET SERVC_ESTADO = 1
WHERE SERVI_COD = 3
AND SERVV_ID_EAI_SW = '20250121140532801'
AND TRUNC(SERVD_FECHAPROG) = TRUNC(SYSDATE);
```

**Error 3: Hacer COMMIT sin validar**
```sql
-- MAL
UPDATE tabla SET campo = valor WHERE condicion;
COMMIT; -- Sin revisar si quedo bien

-- BIEN
UPDATE tabla SET campo = valor WHERE condicion;
SELECT * FROM tabla WHERE condicion; -- Validar primero
COMMIT; -- Confirmar solo si esta correcto
```

### Herramientas para pruebas:

**SQL Developer - Modo Worksheet:**
- Permite ejecutar queries sin commitear automaticamente
- Muestra cantidad de filas afectadas
- Permite hacer ROLLBACK facilmente

**Explicar query (EXPLAIN PLAN):**
```sql
EXPLAIN PLAN FOR
SELECT * FROM EAI.PEDIDO_PRETUP WHERE ESTADO = 'PROCESO';

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY);
```

Te muestra:
- Como Oracle ejecutara la query
- Si usara indices
- Costo estimado (tiempo)

**Probar rendimiento:**
```sql
SET TIMING ON;

SELECT COUNT(1) FROM EAI.PEDIDO_PRETUP
WHERE TRUNC(FECHAREGISTRO) = TRUNC(SYSDATE);

-- Muestra: Elapsed: 00:00:02.34
```

Si tarda mas de 5 segundos, optimizar la query.

---

## 34. POST VENTA

### Que es Post Venta:

**POST VENTA** es el area que atiende clientes que YA compraron un producto/servicio.

**Diferencia con Ventas:**
- **VENTA**: Cliente nuevo, contrata servicio
- **POST VENTA**: Cliente existente, solicita cambios/soporte

### Operaciones de Post Venta:

**1. CAMBIOS DE PLAN:**
- Cliente quiere mas datos
- Cliente quiere menos minutos
- Cambiar de prepago a postpago (migracion)

**2. CAMBIOS DE TITULAR:**
- Transferir linea a otra persona
- Cambiar datos del propietario
- Fusion de cuentas

**3. SUSPENSION/REACTIVACION:**
- Cliente viaja, quiere suspender temporalmente
- Cliente pago, reactivar servicio

**4. DESACTIVACION/BAJA:**
- Cliente cancela el servicio
- Dar de baja permanente

**5. CAMBIO DE CICLO:**
- Cliente quiere factura otro dia del mes
- Cambio de fecha de corte

**6. RECLAMOS:**
- Facturacion incorrecta
- Servicio no funciona
- Cobros indebidos

### Como impacta a Integracion:

**Tu trabajo conecta:**
- Sistema de Post Venta (SIAC, CRM)
- Sistema de facturacion (BSCS, SAP)
- Sistema tecnico (HLR, UDB)

**Ejemplo de flujo:**

**1. Cliente llama a Post Venta:**
```
"Quiero suspender mi linea por 30 dias porque viajo"
```

**2. Ejecutivo crea orden en SIAC:**
```
Orden: OT250625.1000.100001
Tipo: Suspension temporal
Linea: 51988588727
Fecha programada: 25-01-2026
```

**3. SIAC envia a sistema de integracion (EAI):**
```
Se crea registro en USRACT.POSTT_SERVICIOPROG
SERVI_COD = 3 (suspension)
SERVC_ESTADO = 1 (pendiente)
```

**4. Tu servicio procesa automaticamente:**
```
- Lee la programacion
- Valida datos
- Llama a HLR para suspender
- Actualiza BSCS
- Marca como exitoso
```

**5. Si falla, tu intervienes:**
```
- Recibes alerta
- Revisas el error
- Corriges
- Relanzas
```

### Tipos de tickets de Post Venta:

**ORDEN DE TRABAJO (OT):**
- Formato: OT + YYMMDD + HHMM + numero
- Ejemplo: OT250625.1000.100001
- Representa una solicitud de cliente

**TICKET DE INCIDENCIA (INT):**
- Formato: INT-NNN-NNNN
- Ejemplo: INT-000-1234
- Representa un problema/error

**CASO DE SOPORTE:**
- Cuando un proceso falla
- Tu creas el caso
- Documentas la solucion

### SLA de Post Venta:

**Cambio de plan:** 4 horas

**Suspension/Reactivacion:** 2 horas

**Cambio de titular:** 24 horas

**Desactivacion:** 4 horas

**Portabilidad:** 24 horas (por regulacion)

Si no cumples el SLA:
- Cliente puede reclamar
- Empresa paga multa
- Se registra como incumplimiento

### Validaciones de Post Venta:

Antes de procesar, validar:

**1. Cliente existe:**
```sql
SELECT CUSTOMER_ID, CO_ID FROM TIM.PP_DATOS_CONTRATO
WHERE DN_NUM = '51988588727'
AND FEC_ESTADO = (SELECT MAX(FEC_ESTADO) 
                  FROM TIM.PP_DATOS_CONTRATO 
                  WHERE DN_NUM = '51988588727');
```

**2. Linea esta activa:**
```sql
SELECT CH_STATUS FROM TIM.PP_DATOS_CONTRATO
WHERE DN_NUM = '51988588727';
-- CH_STATUS debe ser 'a' (activo) o 's' (suspendido)
```

**3. No hay otra operacion pendiente:**
```sql
SELECT COUNT(1) FROM USRACT.POSTT_SERVICIOPROG
WHERE SERVV_MSISDN = '988588727'
AND SERVC_ESTADO IN (1, 2); -- Pendiente o En Proceso
```

Si devuelve > 0, hay otra operacion en curso, esperar.

**4. Plan destino existe:**
```sql
-- Validar que el plan al que quiere migrar existe
SELECT PLAN_CODE, PLAN_NAME FROM BSCS.PLAN_CATALOG
WHERE PLAN_CODE = 'PLAN_ILIM_89';
```

---

## 35. CYBERARK - GESTION DE CREDENCIALES

### Que es CyberArk:

**CyberArk** es un sistema de gestion segura de contraseñas y credenciales.

**Para que sirve:**
- Almacenar contraseñas de forma segura
- Rotar contraseñas automaticamente
- Auditar quien uso que credencial
- Evitar compartir contraseñas en texto plano

### Por que se usa:

**ANTES (sin CyberArk):**
- Contraseñas en archivos .txt
- Contraseñas compartidas por email
- Misma contraseña por años
- No se sabe quien la uso

**DESPUES (con CyberArk):**
- Contraseñas encriptadas
- Cada usuario pide la contraseña cuando la necesita
- Contraseñas cambian automaticamente cada 30 dias
- Log completo de uso

### Como funciona:

**1. Solicitar credencial:**
```
Usuario → CyberArk → Solicita credencial de "BSCS_ADMIN"
CyberArk → Valida que usuario tiene permiso
CyberArk → Devuelve contraseña actual
```

**2. Usar credencial:**
```
Usuario se conecta a BSCS con la contraseña
CyberArk registra: Fecha, Hora, Usuario, Sistema
```

**3. Rotacion automatica:**
```
Cada 30 dias, CyberArk:
- Genera nueva contraseña aleatoria
- Actualiza en el sistema (BSCS, SAP, Oracle)
- Actualiza en su base de datos
```

### Como usar CyberArk:

**Paso 1 - Acceder al portal:**
```
URL: https://cyberark.empresa.com
Usuario: tu_usuario_corporativo
Password: tu_password_corporativo
```

**Paso 2 - Buscar credencial:**
```
Search: "BSCS"
Resultados:
- BSCS_ADMIN
- BSCS_READONLY  
- BSCS_INTEGRATION
```

**Paso 3 - Solicitar acceso:**
```
Click en "BSCS_ADMIN"
Click en "Request Access"
Reason: "Ejecutar mantenimiento de contratos"
Duration: 2 hours
```

**Paso 4 - Aprobar solicitud:**
```
Si requiere aprobacion:
- Tu jefe recibe notificacion
- Aprueba o rechaza
- Tu recibes la credencial
```

**Paso 5 - Ver credencial:**
```
Click en "Show Password"
Password: X$9mK!2pL@4n
Copy password (se copia al portapapeles)
```

**Paso 6 - Conectar:**
```
Abrir SQL Developer
User: BSCS_ADMIN
Password: Pegar (Ctrl+V)
```

**Paso 7 - Devolver credencial:**
```
Cuando termines:
Click en "Check In"
La credencial se revoca automaticamente
```

### Tipos de acceso:

**PERMANENT ACCESS:**
- Tu usuario siempre puede ver esa credencial
- Para sistemas que usas diariamente

**TEMPORARY ACCESS:**
- Solicitas acceso temporal (1-8 horas)
- Para tareas especificas

**ONE-TIME PASSWORD:**
- Password de un solo uso
- Se invalida despues de usarlo

### Politicas de seguridad:

**Rotacion de contraseñas:**
- Cada 30 dias (standard)
- Cada 90 dias (bajo riesgo)
- Cada 7 dias (critico - produccion)

**Complejidad:**
- Minimo 12 caracteres
- Mayusculas, minusculas, numeros, simbolos
- No puede contener nombre de usuario

**Auditoria:**
- Cada uso queda registrado
- Reportes mensuales de accesos
- Alertas si hay uso fuera de horario

### Cuentas comunes en CyberArk:

**Para bases de datos:**
- ORACLE_EAI_ADMIN
- ORACLE_BSCS_READONLY
- ORACLE_IOT_INTEGRATION

**Para servidores:**
- WEBLOGIC_ADMIN (usuario weblogic)
- ROOT_SERVER_172_19_67_49
- USRCBIO_SERVER

**Para aplicaciones:**
- SAP_INTEGRATION_USER
- HLR_API_USER
- SIAC_ADMIN

### Buenas practicas:

**1. Nunca guardar contraseñas:**
- No las anotes
- No las copies a archivos
- No las compartas por chat

**2. Pedir solo lo necesario:**
- Si solo necesitas leer: pide cuenta READONLY
- Si necesitas escribir: pide cuenta ADMIN

**3. Devolver cuando termines:**
- No dejes sesiones abiertas
- Check-in en CyberArk cuando acabes

**4. Reportar problemas:**
- Si la contraseña no funciona
- Si no tienes acceso a una cuenta que necesitas
- Si ves uso sospechoso

---

## 36. ELASTIC (ELK STACK) - BUSQUEDA DE LOGS

### Que es Elastic:

**Elastic** (o ELK Stack) es una plataforma para:
- **E**lasticsearch: Motor de busqueda
- **L**ogstash: Recolector de logs
- **K**ibana: Visualizador grafico

**Para que sirve:**
- Buscar en millones de lineas de log en segundos
- Crear graficos de errores/transacciones
- Hacer seguimiento de transacciones (trazabilidad)
- Detectar patrones anomalos

### Como funciona:

**1. Logstash recolecta logs:**
```
Servidores generan logs →
Logstash lee archivos →
Procesa y estructura →
Envia a Elasticsearch
```

**2. Elasticsearch indexa:**
```
Recibe logs estructurados →
Los indexa (como Google indexa paginas web) →
Permite busqueda rapida
```

**3. Kibana visualiza:**
```
Usuario busca en Kibana →
Kibana consulta Elasticsearch →
Muestra resultados graficamente
```

### Como buscar en Kibana:

**Paso 1 - Acceder:**
```
URL: https://kibana.empresa.com
Usuario: tu_usuario
Password: tu_password
```

**Paso 2 - Seleccionar indice:**
```
Index pattern: logstash-eai-*
Time range: Last 15 minutes
```

**Paso 3 - Buscar por ID de transaccion:**
```
Buscar: "20257214139078169"
```

**Resultado:**
```
[02-07-2025 14:30:14] [idTx=20257214139078169] Inicio de consultaPedidos
[02-07-2025 14:30:15] [idTx=20257214139078169] Pedido encontrado: ZZ0004072521
[02-07-2025 14:30:16] [idTx=20257214139078169] Error al actualizar factura
[02-07-2025 14:30:16] [idTx=20257214139078169] No existe el cliente
```

Ves TODA la traza de esa transaccion.

**Paso 4 - Filtrar por nivel:**
```
Filtros:
- level: ERROR
- service: actualizarFactura
- idTx: 20257214139078169
```

**Paso 5 - Exportar:**
```
Export → CSV
Descargar para adjuntar en ticket
```

### Busquedas avanzadas:

**Buscar errores de hoy:**
```
level: ERROR AND @timestamp: [now-24h TO now]
```

**Buscar por numero de linea:**
```
msisdn: "51988588727"
```

**Buscar por servicio:**
```
service: "suspension" AND level: ERROR
```

**Buscar por rango de tiempo:**
```
@timestamp: [2026-01-25T10:00:00 TO 2026-01-25T11:00:00]
AND idTx: 20257214*
```

**Buscar patron:**
```
message: *"No existe el cliente"*
```

### Crear visualizaciones:

**Grafico de errores por hora:**
```
Visualization type: Line chart
Y-axis: Count
X-axis: @timestamp (per hour)
Filter: level: ERROR
```

**Grafico de top errores:**
```
Visualization type: Pie chart
Slice by: message.keyword
Filter: level: ERROR
Time: Last 24 hours
```

**Dashboard de monitoreo:**
```
Panel 1: Total transacciones (Counter)
Panel 2: Errores por servicio (Bar chart)
Panel 3: Tiempo de respuesta promedio (Line chart)
Panel 4: Top 10 errores (Table)
```

### Campos importantes:

**timestamp:** Fecha y hora del log

**level:** ERROR, WARN, INFO, DEBUG

**service:** Nombre del servicio (suspension, migracion, etc.)

**idTx:** ID de transaccion

**msisdn:** Numero de telefono

**message:** Mensaje completo del log

**host:** Servidor que genero el log

**application:** Aplicacion (EAI, CBIO, IOT)

### Casos de uso:

**Caso 1: Seguir una transaccion completa**
```
1. Cliente reporta: "Mi suspension no funciono"
2. Te dan la linea: 51988588727
3. Buscas en Kibana: msisdn: "51988588727" AND service: "suspension"
4. Encuentras el idTx: 20257214139078169
5. Buscas por idTx y ves todo el flujo
6. Identificas el error exacto
```

**Caso 2: Detectar patron de errores**
```
1. Recibes 10 alertas de smartwatch
2. Buscas: service: "iot" AND level: ERROR AND @timestamp: [now-1h TO now]
3. Ves que todos tienen el mismo error: "UDBConnector timeout"
4. Conclusión: Problema en UDB, no en cada linea individual
5. Escalas a equipo UDB
```

**Caso 3: Validar si un proceso ejecuto**
```
1. Ejecutaste relanzamiento: sh VVS_SH_ACTUALIZARFACTURA
2. Buscas: service: "actualizarFactura" AND @timestamp: [now-5m TO now]
3. Ves los logs de ejecucion
4. Confirmas que proceso correctamente
```

---

## 37. DYNATRACE - MONITOREO DE RENDIMIENTO

### Que es Dynatrace:

**Dynatrace** es una plataforma de APM (Application Performance Monitoring).

**Para que sirve:**
- Monitorear rendimiento de aplicaciones
- Detectar cuellos de botella
- Ver toda la traza de una transaccion (end-to-end)
- Diagnosticar problemas de lentitud

### Diferencia con CloudWatch y Elastic:

**CloudWatch:**
- Monitorea infraestructura (CPU, memoria, disco)
- Nivel de servidor

**Elastic:**
- Busca en logs
- Nivel de aplicacion (que dice el codigo)

**Dynatrace:**
- Monitorea flujo completo de transacciones
- Nivel de negocio (que experimenta el usuario)
- Ve base de datos, servicios web, servidores, todo junto

### Como funciona:

**OneAgent instalado en servidores:**
```
Servidor WebLogic → OneAgent captura:
- Tiempo de respuesta de cada servicio
- Llamadas a base de datos
- Llamadas a APIs externas
- Errores y excepciones
```

**Dashboard central:**
```
Dynatrace recibe datos →
Correlaciona toda la informacion →
Muestra mapa completo de la transaccion
```

### Como usar Dynatrace:

**Paso 1 - Acceder:**
```
URL: https://dynatrace.empresa.com
Usuario: tu_usuario
Password: tu_password
```

**Paso 2 - Ver panorama general (Smartscape):**
```
Menu: Smartscape
```

Ves mapa de todos los sistemas:
```
SIAC → EAI Services → BSCS Database
           ↓
         SAP API
           ↓
        HLR Service
```

**Paso 3 - Buscar transaccion especifica:**
```
Menu: Diagnostics → Distributed traces
Filter: Service name = "SuspensionService"
Time: Last 2 hours
```

**Resultado:**
```
10:30:15 - SuspensionService - 2.3s - SUCCESS
10:31:22 - SuspensionService - 45s - ERROR
10:32:10 - SuspensionService - 1.8s - SUCCESS
```

**Paso 4 - Ver detalle de transaccion lenta:**
```
Click en transaccion de 45s
```

**Dynatrace muestra:**
```
SuspensionService (total: 45s)
├─ Query BSCS (0.5s)
├─ Call HLR API (43s) ← AQUI ESTA EL PROBLEMA
└─ Update BSCS (1.5s)
```

Identificas que HLR API tardo 43 segundos.

### Analisis de problemas:

**Problema 1: Servicio lento**

**Sintoma en Dynatrace:**
```
Tiempo de respuesta promedio: 500ms
Pico: 15 segundos
```

**Click en el pico:**
```
Request: POST /suspension
Duration: 15s
  ├─ Code execution: 0.1s
  ├─ Database query: 14.8s ← PROBLEMA
  └─ Response: 0.1s
```

**Query especifico:**
```
SELECT * FROM BSCS.CONTRACT
WHERE STATUS = 'A'
-- Esta query tarda 14.8s (no tiene indice)
```

**Solucion:** Crear indice en campo STATUS

**Problema 2: Tasa de errores aumenta**

**Dashboard muestra:**
```
Errores por minuto:
10am: 2 errores/min
11am: 45 errores/min ← Anomalia
12pm: 3 errores/min
```

**Click en periodo 11am:**
```
Error principal: NullPointerException
Origen: SAPIntegrationService
Causa: SAP no responde (timeout)
```

**Correlacion con otros sistemas:**
Dynatrace muestra que SAP tambien tiene alertas en ese horario.

**Solucion:** Coordinar con equipo SAP

### Alertas automaticas:

**Dynatrace detecta anomalias:**

**Alerta: "Response time degradation"**
```
Service: MigracionService
Baseline: 2s promedio
Current: 8s promedio (+300%)
Time: 2026-01-25 14:30
```

**Accion:**
```
1. Revisar Dynatrace: ver que componente se degrade
2. Revisar Elastic: buscar errores en logs
3. Revisar CloudWatch: ver si CPU/memoria estan altas
```

**Alerta: "Error rate increase"**
```
Service: DesactivacionService
Baseline: 0.1% errores
Current: 15% errores
Affected users: 120
```

**Accion:**
```
1. Ver error especifico en Dynatrace
2. Si afecta a muchos usuarios: escalar inmediatamente
3. Si es error conocido: aplicar fix conocido
```

### Metricas clave:

**APDEX (Application Performance Index):**
- Mide satisfaccion del usuario
- 0.0 - 1.0
- > 0.9: Excelente
- 0.7 - 0.9: Bueno
- < 0.7: Problema

**Response Time:**
- Tiempo que tarda en responder
- P50: 50% de requests tardan menos de X
- P95: 95% de requests tardan menos de Y
- P99: 99% de requests tardan menos de Z

**Throughput:**
- Transacciones por segundo
- Normal: 100 tps
- Pico: 500 tps
- Si baja mucho: posible caida

**Error Rate:**
- % de transacciones con error
- Normal: < 1%
- Alerta: > 5%
- Critico: > 10%

---

## 38. LARGE DATA EDITOR (CILO) - SEGUIMIENTO DE TRAZAS

### Que es Large Data Editor:

Herramienta para abrir y analizar archivos de log muy grandes.

**Problema:**
- Logs de produccion: 2-5 GB
- Notepad no puede abrir archivos > 500 MB
- Sublime Text se congela con archivos grandes

**Solucion:**
- Large Data Editor (LDE) o CILO
- Puede abrir archivos de 10+ GB
- Busqueda rapida
- No carga todo en memoria

### Como instalar:

**Opcion 1: Large File Editor**
```
Descargar: http://www.getfreefile.com/large-file-editor
Instalar: Siguiente, Siguiente, Finalizar
```

**Opcion 2: EmEditor (pago pero mejor)**
```
URL: https://www.emeditor.com
Version trial: 30 dias gratis
```

**Opcion 3: glogg (gratis y liviano)**
```
URL: https://glogg.bonnefon.org
Portable, no requiere instalacion
```

### Como usar para seguir trazas:

**Paso 1 - Descargar log del servidor:**
```bash
# Conectar por SFTP (WinSCP)
Servidor: 172.19.67.49
Ruta: /opt/oracle/domains/EAI/servers/wls01/logs/
Archivo: server_20260125.log (2.3 GB)
Descargar a: C:\Logs\
```

**Paso 2 - Abrir con Large Data Editor:**
```
File → Open Large File
Seleccionar: C:\Logs\server_20260125.log
Esperar indexacion (30 segundos)
```

**Paso 3 - Buscar ID de transaccion:**
```
Ctrl+F (Find)
Search: "20257214139078169"
Find All
```

**Resultado:**
```
Line 1,234,567: [idTx=20257214139078169] Inicio suspension
Line 1,234,580: [idTx=20257214139078169] Query BSCS ejecutado
Line 1,234,595: [idTx=20257214139078169] Error: Timeout en HLR
Line 1,234,600: [idTx=20257214139078169] Rollback transaccion
```

**Paso 4 - Exportar solo esas lineas:**
```
Filter: "20257214139078169"
Export filtered → traza_completa.txt
```

**Paso 5 - Analizar flujo:**

**Inicio:**
```
[14:30:14.123] [idTx=20257214139078169] Recibido request suspension
[14:30:14.125] MSISDN: 51988588727
[14:30:14.126] FECHA_PROG: 2026-01-25
```

**Validaciones:**
```
[14:30:14.200] Consultando estado en BSCS
[14:30:14.450] Estado: ACTIVO - OK para suspender
[14:30:14.451] Validando fecha programacion
[14:30:14.452] Fecha valida: SI
```

**Ejecucion:**
```
[14:30:14.500] Llamando HLR API
[14:30:14.501] Endpoint: http://hlr.empresa.com/suspend
[14:30:14.502] Timeout configurado: 30s
[14:30:44.503] ERROR: Read timeout after 30s
```

**Error:**
```
[14:30:44.504] HLR no responde
[14:30:44.505] Iniciando rollback
[14:30:44.600] Rollback completado
[14:30:44.601] Transaccion marcada como ERROR
```

**Conclusion:**
HLR API tiene timeout de 30s, tardo mas y fallo.

### Patrones de busqueda:

**Buscar todos los errores:**
```
Regex: \[ERROR\]|\[EXCEPTION\]
```

**Buscar por linea telefonica:**
```
Search: "51988588727"
```

**Buscar por fecha/hora especifica:**
```
Search: "2026-01-25 14:30"
```

**Buscar llamadas a base de datos:**
```
Regex: SELECT.*FROM|UPDATE.*SET|DELETE.*FROM
```

**Buscar timeouts:**
```
Search: "timeout" (case insensitive)
```

### Analisis de performance:

**Buscar queries lentas:**
```
Regex: \[SQL\].*\[(\d{4,})\s*ms\]
```

Encuentra queries que tardaron > 1000ms (4 digitos)

**Ejemplo encontrado:**
```
[14:30:15.123] [SQL] SELECT * FROM BSCS.CONTRACT WHERE CO_ID=123 [4523 ms]
```

4.5 segundos → Query lenta, optimizar.

### Comparar dos archivos de log:

**Caso:** Relanzaste un proceso, quieres comparar

**Log 1:** Primera ejecucion (fallo)
**Log 2:** Segunda ejecucion (relanzamiento)

**WinMerge (gratuito):**
```
Descargar: https://winmerge.org
Abrir WinMerge
File → Open
Left: server_14-30.log
Right: server_15-45.log
```

**Diferencias marcadas en colores:**
- Verde: Solo en archivo 2 (nuevo)
- Rojo: Solo en archivo 1 (viejo)
- Amarillo: Diferente en ambos

Identificas que cambio entre ejecuciones.

---

## 39. GRAFICOS EN GOOGLE SHEETS - REPORTES

### Por que hacer graficos:

**Para reportes diarios/semanales:**
- Mostrar cantidad de casos resueltos
- % de exito vs fallas
- Tiempo promedio de resolucion
- Tendencias (mejora o empeora)

### Conectar Sheets con datos:

**Opcion 1: Export manual desde Oracle**
```sql
SELECT 
  TRUNC(SERVD_FECHA_REG) AS FECHA,
  COUNT(CASE WHEN SERVC_ESTADO = 3 THEN 1 END) AS EXITOSOS,
  COUNT(CASE WHEN SERVC_ESTADO = 4 THEN 1 END) AS ERRORES,
  COUNT(1) AS TOTAL
FROM USRACT.POSTT_SERVICIOPROG
WHERE SERVD_FECHA_REG >= TRUNC(SYSDATE) - 30
GROUP BY TRUNC(SERVD_FECHA_REG)
ORDER BY 1;
```

Exportar a CSV → Importar en Sheets

**Opcion 2: Google Sheets + Apps Script**

Conectar directamente a Oracle (requiere configuracion):
```javascript
function obtenerDatos() {
  var conn = Jdbc.getConnection("jdbc:oracle:thin:@IP:PORT:SID", "user", "pass");
  var stmt = conn.createStatement();
  var rs = stmt.executeQuery("SELECT * FROM tabla");
  
  while (rs.next()) {
    // Procesar datos
  }
  rs.close();
  stmt.close();
  conn.close();
}
```

### Tipos de graficos:

**1. LINEA - Tendencia en el tiempo**

**Datos:**
```
FECHA       | EXITOSOS | ERRORES
2026-01-20  | 450      | 25
2026-01-21  | 480      | 18
2026-01-22  | 520      | 12
2026-01-23  | 490      | 30
2026-01-24  | 510      | 15
```

**Grafico de linea:**
- Eje X: FECHA
- Eje Y: EXITOSOS y ERRORES (dos lineas)

**Como crear:**
```
1. Seleccionar datos (A1:C6)
2. Insert → Chart
3. Chart type: Line chart
4. Customize:
   - Title: "Procesos Diarios - Ultima Semana"
   - X-axis: Fecha
   - Series 1: Exitosos (color verde)
   - Series 2: Errores (color rojo)
```

**2. BARRA - Comparar categorias**

**Datos:**
```
SERVICIO       | CANTIDAD
Suspension     | 120
Reactivacion   | 95
Migracion      | 45
Cambio Plan    | 80
Desactivacion  | 60
```

**Grafico de barras:**
- Eje X: SERVICIO
- Eje Y: CANTIDAD

**3. PIE - Distribucion porcentual**

**Datos:**
```
ESTADO    | CANTIDAD
Exitoso   | 850
Error     | 120
Pendiente | 30
```

**Grafico circular:**
- Exitoso: 85%
- Error: 12%
- Pendiente: 3%

**4. COMBO - Mezcla linea y barra**

**Datos:**
```
FECHA       | TOTAL | % EXITO
2026-01-20  | 475   | 94.7%
2026-01-21  | 498   | 96.4%
2026-01-22  | 532   | 97.7%
```

**Grafico combo:**
- Barras: TOTAL (eje Y izquierdo)
- Linea: % EXITO (eje Y derecho)

### Formulas utiles:

**Calcular % de exito:**
```
=B2/(B2+C2)*100
```
Donde B2=EXITOSOS, C2=ERRORES

**Contar casos por estado:**
```
=COUNTIF(A:A,"EXITOSO")
```

**Promedio de tiempo de resolucion:**
```
=AVERAGE(B2:B100)
```

**Sumar total del mes:**
```
=SUMIF(A:A,">=2026-01-01",B:B)
```

**Conditional formatting:**
```
Si % exito < 90% → Color rojo
Si % exito >= 95% → Color verde
Si % exito entre 90-95% → Color amarillo
```

### Dashboard automatizado:

**Template recomendado:**

**Hoja 1: Datos brutos**
- Exportacion de Oracle
- No tocar manualmente

**Hoja 2: Calculos**
- Formulas que procesan datos
- Pivots, SUMIFs, COUNTIFs

**Hoja 3: Dashboard**
- Solo graficos
- Actualiza automaticamente

**Ejemplo practico:**

**Datos (Sheet 1):**
```
| FECHA      | TICKET      | ESTADO  | TIEMPO_MIN |
|------------|-------------|---------|------------|
| 2026-01-25 | INT-000-123 | EXITOSO | 45         |
| 2026-01-25 | INT-000-124 | ERROR   | 120        |
| 2026-01-25 | INT-000-125 | EXITOSO | 30         |
```

**Calculos (Sheet 2):**
```
Total hoy: =COUNTIF(Datos!A:A,TODAY())
Exitosos: =COUNTIFS(Datos!A:A,TODAY(),Datos!C:C,"EXITOSO")
% Exito: =B2/B1*100
Tiempo promedio: =AVERAGEIF(Datos!C:C,"EXITOSO",Datos!D:D)
```

**Dashboard (Sheet 3):**
```
┌─────────────────────────────────────┐
│ DASHBOARD INTEGRACION - HOY         │
├─────────────────────────────────────┤
│ Total casos: 45                     │
│ Exitosos: 39 (87%)                  │
│ Errores: 6 (13%)                    │
│ Tiempo prom: 52 minutos             │
├─────────────────────────────────────┤
│ [Grafico de linea: ultimos 7 dias] │
│ [Grafico pie: distribucion estados] │
│ [Grafico barra: casos por servicio] │
└─────────────────────────────────────┘
```

### Compartir reportes:

**Opcion 1: Compartir link**
```
File → Share
Permisos: View only (solo lectura)
Copiar link → Enviar por email
```

**Opcion 2: Programar email automatico**
```
Extensions → Apps Script
Codigo:
function enviarReporte() {
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var hoja = ss.getSheetByName("Dashboard");
  var pdf = hoja.getAs('application/pdf');
  
  MailApp.sendEmail({
    to: "jefe@empresa.com",
    subject: "Reporte Diario Integracion",
    body: "Adjunto reporte del dia",
    attachments: [pdf]
  });
}
```

Programar trigger: Todos los dias a las 6pm

---

## 40. DATAPOWER GATEWAY - GATEWAY DE SERVICIOS

### Que es DataPower:

**IBM DataPower Gateway** es un dispositivo (appliance) que actua como intermediario entre sistemas.

**Funcion principal:**
- Recibe peticiones de un sistema (SIAC)
- Valida, transforma, enruta
- Envia a otro sistema (BSCS, SAP, HLR)
- Devuelve respuesta

**Por que se usa:**
- Seguridad (firewall de aplicacion)
- Transformacion de mensajes (XML ↔ JSON)
- Enrutamiento inteligente
- Auditoria de transacciones

### Como funciona:

**Flujo sin DataPower:**
```
SIAC → BSCS (conexion directa)
```
Problemas:
- SIAC debe conocer IP/puerto de BSCS
- Si BSCS cambia, hay que reconfigurar SIAC
- No hay auditoria centralizada

**Flujo con DataPower:**
```
SIAC → DataPower → BSCS
```
Ventajas:
- SIAC solo conoce DataPower
- DataPower enruta al backend correcto
- Log centralizado en DataPower

### Componentes:

**Frontend Handler:**
- Recibe peticiones
- Protocolo: HTTP, HTTPS, MQ, FTP

**Processing Policy:**
- Que hacer con el mensaje
- Validar, transformar, enrutar

**Backend:**
- A donde enviar
- BSCS, SAP, HLR, etc.

### Ejemplo practico:

**Caso:** Suspension de linea

**1. SIAC envia request:**
```xml
POST https://datapower.empresa.com/suspension
<suspension>
  <msisdn>51988588727</msisdn>
  <fecha>2026-01-25</fecha>
</suspension>
```

**2. DataPower recibe (Frontend Handler):**
```
Puerto: 8443 (HTTPS)
Certificado: Valido ✓
Autenticacion: Basic Auth ✓
```

**3. DataPower procesa (Policy):**

**a) Validar esquema:**
```
¿XML bien formado? SI
¿Tiene campo msisdn? SI
¿Fecha es valida? SI
```

**b) Transformar:**
```xml
<!-- SIAC envia formato simple -->
<suspension>
  <msisdn>51988588727</msisdn>
</suspension>

<!-- DataPower transforma a formato BSCS -->
<BSCS_SuspensionRequest>
  <header>
    <timestamp>2026-01-25T10:30:00</timestamp>
    <system>SIAC</system>
  </header>
  <body>
    <DN_NUM>51988588727</DN_NUM>
    <ACTION>SUSPEND</ACTION>
  </body>
</BSCS_SuspensionRequest>
```

**c) Enrutar:**
```
Destino: http://bscs.empresa.com:8080/api/suspension
Metodo: POST
Headers: Content-Type: text/xml
```

**4. BSCS procesa y responde:**
```xml
<BSCS_Response>
  <status>SUCCESS</status>
  <code>0</code>
</BSCS_Response>
```

**5. DataPower transforma respuesta:**
```xml
<!-- BSCS responde formato complejo -->
<BSCS_Response>
  <status>SUCCESS</status>
</BSCS_Response>

<!-- DataPower simplifica para SIAC -->
<response>
  <resultado>OK</resultado>
</response>
```

**6. SIAC recibe:**
```xml
<response>
  <resultado>OK</resultado>
</response>
```

### Logs en DataPower:

**Como ver logs:**

**Opcion 1: Consola Web**
```
URL: https://datapower-admin.empresa.com:9090
Login: admin
Password: admin_password

Status → Logs → System Logs
```

**Opcion 2: SFTP**
```
Conectar a DataPower por SFTP
Directorio: /var/log
Archivos:
- default.log (general)
- webgui.log (accesos consola)
- service.log (transacciones)
```

**Contenido del log:**
```
[2026-01-25 10:30:14] [Suspension_MP] Frontend request received
[2026-01-25 10:30:14] INPUT: <suspension><msisdn>51988588727</msisdn></suspension>
[2026-01-25 10:30:14] Schema validation: PASS
[2026-01-25 10:30:14] Transform applied: SIAC_to_BSCS.xsl
[2026-01-25 10:30:14] Backend call: http://bscs.empresa.com:8080/api/suspension
[2026-01-25 10:30:15] Backend response: SUCCESS
[2026-01-25 10:30:15] OUTPUT: <response><resultado>OK</resultado></response>
```

### Casos de error en DataPower:

**Error 1: Backend no responde**

**Log:**
```
[ERROR] Backend timeout after 30s
[ERROR] Target: http://bscs.empresa.com:8080/api/suspension
```

**Accion:**
```
1. Validar si BSCS esta arriba: ping bscs.empresa.com
2. Validar puerto: telnet bscs.empresa.com 8080
3. Si no responde: escalar a equipo BSCS
```

**Error 2: Transformacion falla**

**Log:**
```
[ERROR] XSLT transformation failed
[ERROR] Variable 'fecha' not found in input
```

**Accion:**
```
1. Validar request de origen (SIAC)
2. Si falta campo obligatorio: rechazar request
3. Si DataPower espera campo que ya no existe: actualizar XSLT
```

**Error 3: Certificado SSL expirado**

**Log:**
```
[ERROR] SSL handshake failed
[ERROR] Certificate expired on 2026-01-20
```

**Accion:**
```
1. Renovar certificado
2. Cargar nuevo certificado en DataPower
3. Reiniciar servicio
```

### Comandos utiles (CLI):

**Conectar por SSH:**
```bash
ssh admin@datapower.empresa.com
Password: ******
```

**Ver estado de servicio:**
```
show service-status
```

**Ver version de firmware:**
```
show version
```

**Ver uso de memoria:**
```
show system
```

**Ver estadisticas de transacciones:**
```
show statistics
```

**Exportar configuracion:**
```
export config://
```

### Tu rol con DataPower:

**NO configuras DataPower directamente** (lo hace equipo de infraestructura)

**Tu rol:**
1. Ver logs cuando hay errores
2. Identificar si el problema es:
   - Frontend (SIAC envia mal)
   - DataPower (transformacion falla)
   - Backend (BSCS no responde)
3. Escalar al equipo correcto

**Ejemplo de escalamiento:**

**Error encontrado:**
```
DataPower log: Backend BSCS returning HTTP 500
```

**Tu analisis:**
```
1. Request de SIAC: Correcto ✓
2. DataPower transforma: Correcto ✓
3. BSCS responde 500: ERROR ← Problema en BSCS
```

**Escalamiento:**
```
Para: Equipo BSCS
Asunto: Error 500 en API suspension
Detalle: DataPower envia request correcto pero BSCS responde 500
Evidencia: Log de DataPower adjunto
Request enviado: [XML del request]
Response recibido: [HTTP 500 Internal Server Error]
```

---

## RESUMEN DE HERRAMIENTAS

**MONITOREAMIENTO:**
- **CloudWatch**: Infraestructura (CPU, RAM, disco)
- **Dynatrace**: Rendimiento de aplicaciones (end-to-end)
- **Elastic/Kibana**: Busqueda en logs

**SEGURIDAD:**
- **CyberArk**: Gestion de contraseñas

**ANALISIS:**
- **Large Data Editor**: Archivos de log grandes
- **Google Sheets**: Reportes y graficos

**INTEGRACION:**
- **DataPower**: Gateway de servicios

**ESCALAMIENTO:**
- **Sistema de tickets**: Registro y seguimiento
- **Correos**: Comunicacion con equipos

**Cada herramienta tiene su proposito especifico. Usarlas en conjunto te da vision completa del sistema.**

---

**FIN DE LA GUIA DE CONCEPTOS PARA ANALISTA DE INTEGRACION**
Devolver un IDF o EDT:
VER LOGS,  REVISAR EL TRAZA y flujos
✅ Respuestas exitosas
200 OK  
La petición fue procesada correctamente. Es la respuesta estándar cuando todo salió bien (por ejemplo, al consultar una página web y recibir su contenido).

⚠️ Errores del cliente (4xx)
400 Bad Request  
La solicitud está mal formada o contiene errores de sintaxis. El servidor no puede procesarla.
401 Unauthorized  
El cliente no está autenticado o no tiene credenciales válidas.
403 Forbidden  
El servidor entendió la petición, pero niega el acceso (falta de permisos).
404 Not Found  
El recurso solicitado no existe en el servidor.

❌ Errores del servidor (5xx)
500 Internal Server Error  
Error genérico del servidor: ocurrió algo inesperado que impide completar la solicitud.

502 Bad Gateway  
El servidor actuó como puerta de enlace y recibió una respuesta inválida de otro servidor.

503 Service Unavailable  
El servidor no está disponible temporalmente (sobrecarga, mantenimiento).

504 Gateway Timeout  
El servidor actuó como puerta de enlace y no recibió respuesta a tiempo de otro servidor.
----------------------------------------
📌 ¿Qué es un IDF?

IDF = Informe de Datos Funcionales (en algunos contextos también: Interfaz de Datos Funcional).

👉 ¿De qué trata?
Es un objeto estructurado que devuelve información procesada, normalmente como:

DTO / POJO en Java

JSON

XML

Respuesta de un servicio (REST / SOAP)

💡 En Java, “devolver un IDF” suele significar:

Retornar un objeto con datos específicos, bien definidos y listos para consumo por otra capa (frontend, API, otro sistema).

🔹 Ejemplo en Java
public class ClienteIDF {
    private Long id;
    private String nombre;
    private String email;

    // getters y setters
}

public ClienteIDF obtenerCliente(Long id) {
    ClienteIDF idf = new ClienteIDF();
    idf.setId(id);
    idf.setNombre("Juan Perez");
    idf.setEmail("juan@mail.com");
    return idf;
}


👉 Eso ya es devolver un IDF.

📌 ¿Qué es un EDT?

EDT = Estructura de Datos de Transferencia (muy similar a un DTO).

👉 ¿De qué trata?

Es una estructura de datos plana

No contiene lógica de negocio

Se usa para transportar datos entre capas o sistemas

💡 En Java:

POJO

DTO

Record (Java 16+)

🔹 Ejemplo EDT en Java
public record PedidoEDT(
    Long id,
    String producto,
    int cantidad
) {}

public PedidoEDT obtenerPedido() {
    return new PedidoEDT(1L, "Laptop", 2);
}

🧠 Diferencia rápida IDF vs EDT
Concepto	Qué es	Uso
IDF	Informe / Interfaz de datos funcional	Respuesta con significado funcional
EDT	Estructura de transporte	Pasar datos entre capas
DTO	Equivalente moderno	Muy usado en APIs REST
----------------------------
escalar coorreos,escale
umbral, que es el graficos de aws
pruebas de querys
weblogic server Oracle (x)
putty ssh server
aws cloud watch (x)
post venta
CYBERARK
elastic (x)
DYNATRACE 
large dta editor cilo , para seguir la traza
aprender hacer gráficos en sheet
datapower Gateway

----------------------------------------
# Por Documentar
- SISAC
