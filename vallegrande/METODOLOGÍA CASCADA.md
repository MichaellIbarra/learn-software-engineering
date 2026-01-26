## METODOLOGÍA CASCADA

**Introducción:** Modelo de desarrollo secuencial donde cada fase debe completarse antes de iniciar la siguiente. Flujo unidireccional similar a una cascada.

**Por qué se utiliza:** Proyectos con requisitos claros y estables, entornos regulados, equipos que necesitan estructura rígida.

**Ventajas:**
- Documentación exhaustiva en cada fase
- Fácil de entender y gestionar
- Hitos claros y medibles
- Ideal para proyectos con requisitos fijos

**Desventajas:**
- Inflexible ante cambios
- Cliente ve el producto al final
- Difícil corregir errores de fases anteriores
- No apto para proyectos complejos o inciertos

### Fases de la metodología

**1. Requisitos:**
- **Qué trata:** Recopilación y documentación de todas las necesidades del sistema
- **Ejemplo:** Entrevistas con stakeholders, análisis de necesidades del negocio
- **Ejecución:** Reuniones, encuestas, documentos de especificación de requisitos (SRS)

**2. Diseño:**
- **Qué trata:** Creación de arquitectura del sistema y especificaciones técnicas
- **Ejemplo:** Diagramas UML, diseño de base de datos, arquitectura de componentes
- **Ejecución:** Diseño de alto nivel (HLD) y diseño de bajo nivel (LLD)

**3. Implementación:**
- **Qué trata:** Codificación del sistema según las especificaciones de diseño
- **Ejemplo:** Desarrollo de módulos, clases, funciones según el diseño
- **Ejecución:** Escribir código, revisiones de código, control de versiones

**4. Verificación/Pruebas:**
- **Qué trata:** Validación que el sistema cumple con los requisitos
- **Ejemplo:** Pruebas unitarias, integración, sistema, aceptación
- **Ejecución:** Ejecución de casos de prueba, registro de defectos, corrección

**5. Mantenimiento:**
- **Qué trata:** Soporte post-implementación y corrección de errores
- **Ejemplo:** Actualizaciones, parches, mejoras evolutivas
- **Ejecución:** Monitoreo, corrección de bugs, adaptación a nuevos requisitos

### Aplicación de la metodología en proyectos de desarrollo de Software

**Escenarios ideales:**
- Sistemas embebidos con hardware específico
- Proyectos gubernamentales con regulaciones estrictas
- Software médico o aeroespacial (certificaciones)
- Sistemas con requisitos completamente definidos

**Ciclo de vida típico:**
1. Contrato/inicio del proyecto (mes 1)
2. Análisis de requisitos (2-3 meses)
3. Diseño completo (2-3 meses)
4. Desarrollo (4-6 meses)
5. Pruebas (2-3 meses)
6. Despliegue y mantenimiento

**Ejemplo de uso:** Sistema de nómina empresarial donde los requisitos legales son fijos, la estructura es clara y los cambios son mínimos durante el desarrollo.

### Pros y contras de esta metodología en comparación con Agile

**Pros vs Agile:**
- Mayor documentación y trazabilidad
- Mejor para proyectos con alcance fijo
- Presupuesto y cronograma más predecible
- Menos dependencia de disponibilidad del cliente
- Adecuado para equipos distribuidos sin comunicación constante

**Contras vs Agile:**
- No permite cambios durante el desarrollo
- Mayor riesgo de fracaso si requisitos mal definidos
- Feedback tardío del cliente
- No entrega valor incremental
- Menos colaboración continua
- Difícil adaptarse a tecnologías emergentes
