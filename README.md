# Introducción a Ingeniería de Software

La **ingeniería de software** es una disciplina que trasciende la simple programación, constituyendo una rama especializada de la ingeniería que aplica principios científicos, metodologías sistemáticas y mejores prácticas para diseñar, desarrollar, implementar, mantener y gestionar sistemas de software complejos y de gran escala.

## ¿Qué es la Ingeniería de Software?

Es el conjunto de **fundamentos teóricos y prácticos** que permite crear software de alta calidad, confiable, eficiente y mantenible. Esta disciplina aborda:

- **Aspectos técnicos**: Arquitectura, diseño, algoritmos, estructuras de datos
- **Gestión de proyectos**: Planificación, estimación, control de calidad, gestión de riesgos
- **Procesos y metodologías**: Frameworks ágiles, DevOps, integración continua
- **Calidad y testing**: Pruebas automatizadas, métricas de calidad, validación
- **Mantenimiento y evolución**: Refactoring, actualizaciones, migración de sistemas

### Diferencia entre Programación e Ingeniería de Software

| **Programación** | **Ingeniería de Software** |
|------------------|-----------------------------|
| Escribir código | Diseñar sistemas complejos |
| Enfoque individual | Trabajo en equipo coordinado |
| Proyectos pequeños | Sistemas empresariales |
| Soluciones inmediatas | Arquitectura a largo plazo |
| Sin documentación formal | Documentación sistemática |
| Testing básico | Estrategias de QA integrales |

## Componentes Clave del Desarrollo de Software

### 1. **Análisis y Especificación de Requisitos**
**Objetivo**: Definir **qué debe hacer** el sistema y **bajo qué condiciones**

- **Requisitos funcionales**: Características específicas que el software debe implementar
  - *Ejemplo*: "El sistema debe permitir login con email y contraseña"
- **Requisitos no funcionales**: Criterios de calidad y rendimiento
  - *Ejemplo*: "El tiempo de respuesta no debe exceder 2 segundos"
- **Elicitación**: Técnicas para extraer requisitos (entrevistas, workshops, prototipado)
- **Documentación**: SRS (Software Requirements Specification), casos de uso, historias de usuario

### 2. **Arquitectura y Diseño de Software**
**Objetivo**: Definir **cómo** se estructurará y organizará el sistema

- **Arquitectura del sistema**: Patrones arquitectónicos (MVC, microservicios, hexagonal)
- **Diseño de componentes**: Módulos, clases, interfaces, APIs
- **Diagramas técnicos**: UML, diagramas de flujo, arquitectura de datos
- **Decisiones tecnológicas**: Stack tecnológico, frameworks, bases de datos

### 3. **Implementación (Codificación)**
**Objetivo**: Traducir el diseño en código ejecutable de alta calidad

- **Estándares de codificación**: Convenciones, nomenclatura, documentación
- **Versionado**: Git workflows, branching strategies, control de cambios
- **Revisión de código**: Code reviews, pair programming, static analysis
- **Integración**: APIs, servicios externos, bases de datos

### 4. **Verificación y Validación (Testing)**
**Objetivo**: Garantizar que el software cumple requisitos y funciona correctamente

- **Niveles de testing**:
  - *Unitarias*: Funciones y métodos individuales
  - *Integración*: Interacción entre componentes
  - *Sistema*: Funcionalidad completa end-to-end
  - *Aceptación*: Validación con usuarios finales
- **Tipos de pruebas**: Funcionales, performance, seguridad, usabilidad
- **Automatización**: CI/CD pipelines, testing frameworks

### 5. **Despliegue y Mantenimiento**
**Objetivo**: Entregar el software y mantenerlo operativo en el tiempo

- **Deployment**: Estrategias de despliegue (blue-green, canary, rolling)
- **Monitoreo**: Logs, métricas, alertas, observabilidad
- **Mantenimiento evolutivo**: Nuevas funcionalidades, mejoras
- **Mantenimiento correctivo**: Bug fixes, patches de seguridad
- **Refactoring**: Mejora continua del código sin cambiar funcionalidad

## Importancia de las Bases Sólidas en Ingeniería de Software

### ¿Por qué son Críticos los Fundamentos?

Las bases sólidas en ingeniería de software no son solo "buenas prácticas" - son **inversiones estratégicas** que determinan el éxito a largo plazo de cualquier proyecto de software.

### 📊 **Eficiencia y Productividad**
**Impacto**: Optimización de recursos humanos, tecnológicos y temporales

- **Desarrollo más rápido**: Arquitecturas bien diseñadas permiten desarrollo paralelo
- **Menos retrabajo**: Requisitos claros evitan rehacer funcionalidades
- **Automatización**: Pipelines de CI/CD reducen tiempo de deployment de horas a minutos
- **Reutilización**: Componentes modulares se reutilizan en múltiples proyectos

*Ejemplo real*: Un equipo con buenas prácticas puede entregar features 3-5x más rápido que uno sin ellas.

### 🔒 **Calidad y Confiabilidad**
**Impacto**: Software más estable, seguro y confiable

- **Menor tasa de bugs**: Testing sistemático reduce defectos en producción en 60-90%
- **Rendimiento predecible**: Arquitectura escalable mantiene performance bajo carga
- **Seguridad robusta**: Principios secure-by-design previenen vulnerabilidades
- **Disponibilidad**: Sistemas diseñados para alta disponibilidad (99.9%+ uptime)

*Ejemplo real*: Netflix maneja millones de usuarios simultáneos gracias a su arquitectura de microservicios.

### 📈 **Escalabilidad y Crecimiento**
**Impacto**: Capacidad de crecer sin reescribir el sistema completo

- **Escalabilidad horizontal**: Agregar servidores vs reescribir código
- **Modularidad**: Nuevas funcionalidades sin afectar existentes
- **Performance**: Mantener velocidad con millones de usuarios
- **Flexibilidad tecnológica**: Adoptar nuevas tecnologías sin migración completa

*Ejemplo real*: Instagram creció de 0 a 1000M usuarios manteniendo su arquitectura base.

### 🔧 **Mantenibilidad y Evolución**
**Impacto**: Facilita cambios, mejoras y correcciones a lo largo del tiempo

- **Código legible**: Nuevos desarrolladores productivos en días vs meses
- **Documentación actualizada**: Reduce tiempo de onboarding en 70%
- **Refactoring seguro**: Tests automatizados permiten mejoras sin miedo
- **Debugging eficiente**: Logs y monitoreo aceleran resolución de problemas

*Ejemplo real*: Sistemas legacy sin buenas prácticas pueden costar 10x más mantener.

### 💰 **Impacto Económico de las Buenas Prácticas**

| **Aspecto** | **Con Buenas Prácticas** | **Sin Buenas Prácticas** |
|-------------|--------------------------|---------------------------|
| **Tiempo de desarrollo** | Baselines reutilizables | Reinventar cada vez |
| **Costo de bugs** | $100-$1K por bug | $10K-$100K por bug |
| **Time-to-market** | Releases semanales | Releases trimestrales |
| **Costo de mantenimiento** | 20-30% del desarrollo | 70-80% del desarrollo |
| **Escalabilidad** | Crecimiento orgánico | Reescrituras costosas |

### 🎯 **Beneficios Empresariales Tangibles**

1. **Reducción de costos**: 40-60% menos en mantenimiento y soporte
2. **Faster time-to-market**: Entregas 2-3x más frecuentes
3. **Mejor experiencia de usuario**: 50% menos bugs, mejor performance
4. **Competitive advantage**: Capacidad de innovar más rápido
5. **Risk mitigation**: Menor probabilidad de fallos críticos
6. **Team satisfaction**: Desarrolladores más productivos y menos frustrados

### 🚀 **Principios Fundamentales para el Éxito**

- **SOLID principles**: Base para código mantenible y extensible
- **DRY (Don't Repeat Yourself)**: Evita duplicación de lógica
- **KISS (Keep It Simple, Stupid)**: Simplicidad sobre complejidad innecesaria
- **YAGNI (You Aren't Gonna Need It)**: No sobre-ingenierizar
- **Testing pyramid**: Unit > Integration > E2E tests
- **Continuous improvement**: Retrospectivas y mejora continua

## Metodologías y Frameworks de Desarrollo

### 🔄 **Metodologías Ágiles**
- **Scrum**: Framework iterativo con sprints de 1-4 semanas
- **Kanban**: Flujo continuo con límites de trabajo en progreso
- **Extreme Programming (XP)**: Enfoque en calidad técnica y feedback frecuente
- **SAFe**: Scaled Agile para organizaciones grandes

### 🏗️ **Enfoques de Arquitectura**
- **Monolítica**: Aplicación única y desplegable
- **Microservicios**: Servicios independientes y comunicación por APIs
- **Serverless**: Funciones sin gestión de infraestructura
- **Event-driven**: Arquitectura basada en eventos asíncronos

### 📊 **Modelos de Ciclo de Vida**
- **Waterfall**: Secuencial y predictivo
- **Iterativo**: Refinamiento progresivo
- **Incremental**: Entregas parciales funcionales
- **Spiral**: Gestión de riesgos y prototipado

## Herramientas y Tecnologías Esenciales

### 🛠️ **Control de Versiones**
- **Git**: Sistema distribuido de control de versiones
- **GitHub/GitLab/Bitbucket**: Plataformas de desarrollo colaborativo
- **Branching strategies**: GitFlow, GitHub Flow, trunk-based

### 🤖 **DevOps y Automatización**
- **CI/CD**: Jenkins, GitHub Actions, Azure DevOps
- **Containerización**: Docker, Kubernetes
- **Infrastructure as Code**: Terraform, Ansible
- **Monitoring**: Prometheus, Grafana, ELK Stack

### 🧪 **Testing y Calidad**
- **Unit Testing**: Jest, JUnit, pytest
- **Integration Testing**: Postman, REST Assured
- **End-to-end Testing**: Selenium, Cypress, Playwright
- **Code Quality**: SonarQube, ESLint, Codecov

## Competencias Clave del Ingeniero de Software

### 💻 **Competencias Técnicas**
- **Lenguajes de programación**: Dominio de múltiples paradigmas
- **Estructuras de datos y algoritmos**: Fundamentos computacionales
- **Bases de datos**: SQL/NoSQL, modelado de datos
- **Redes y sistemas**: TCP/IP, HTTP, arquitectura web
- **Seguridad**: OWASP, criptografía, autenticación

### 🧠 **Competencias Blandas**
- **Resolución de problemas**: Análisis sistemático y debugging
- **Comunicación**: Documentación técnica y presentaciones
- **Trabajo en equipo**: Colaboración y liderazgo técnico
- **Aprendizaje continuo**: Adaptación a nuevas tecnologías
- **Pensamiento crítico**: Evaluación de soluciones alternativas







## Términos comunes
- wrappers: Es una pieza de software que "envuelve" otra pieza de software para proporcionar una interfaz diferente o adicional, facilitando la interacción entre sistemas.
- refactorización: Es el proceso de reestructurar el código existente sin cambiar su comportamiento externo, con el objetivo de mejorar su legibilidad, mantenibilidad y rendimiento.
- stakeholders: Son todas las personas, grupos u organizaciones que tienen un interés o están afectados por un proyecto o sistema de software.
- Elicitación: Es el proceso de recopilar y definir los requisitos del software a través de la interacción con los stakeholders.
- Cuantitativos y cualitativos: Se refiere a dos tipos de datos; los cuantitativos son datos numéricos que pueden medirse y analizarse estadísticamente, mientras que los cualitativos son datos descriptivos que proporcionan información sobre características, atributos o cualidades.
- Acrónimos: Son palabras formadas por las letras iniciales de un conjunto de palabras, utilizadas para abreviar términos largos o complejos.
- Funcionalidades funcionales y no funcionales: Los requisitos funcionales describen lo que el sistema debe hacer, mientras que los requisitos no funcionales describen cómo debe comportarse el sistema en términos de rendimiento, seguridad, usabilidad, entre otros.
- Interfaz de clase: Es una definición que especifica un conjunto de métodos y propiedades que una clase debe implementar, sin definir cómo se implementan esos métodos.
- Propotipo: Es una representación preliminar de un producto o sistema que permite a los diseñadores y desarrolladores visualizar y probar conceptos antes de la implementación completa.
- MVP (Minimum Viable Product): Es la versión más básica de un producto que incluye solo las características esenciales necesarias para satisfacer a los primeros usuarios y obtener retroalimentación para futuras mejoras.

## Recursos
- https://ocw.unican.es/pluginfile.php/2168/course/section/1988/plantilla_formato_ieee830.pdf
- https://saga.so/95fc47a2-27bc-466f-b7ad-233940b499e9
- https://es.scribd.com/document/469148576/Plantilla-Proyecto-de-Desarrollo-de-Sw
- https://mpsm.gob.pe/public/mesavirtual/mv_2336_guia_para_la_documentacion_de_proyectos_de_software.pdf
- https://es.scribd.com/document/422195528/Guia-Para-La-Documentacion-de-Proyectos-2