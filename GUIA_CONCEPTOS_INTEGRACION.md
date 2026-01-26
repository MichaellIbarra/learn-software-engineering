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
indicndias transversanesl : ocupan varias personas , dispatcher para distribuir, destrabar, 
indicendica escalable, son jefes, si es un tike, una pronta intración,
se debe entender de las 24 horas, 8 estados críticos  de las 4 horas
carmencitas (dispatcher) ->  roció y Royer () - >
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