# Preparación para Entrevista Técnica - Software Engineering

## 1. Conocimiento en bases de datos SQL y NoSQL y pruebas unitarias

### Bases de Datos SQL vs NoSQL
**SQL**: Esquema estructurado con propiedades ACID, ideal para sistemas transaccionales con integridad referencial crítica.
Tablas relacionadas con claves primarias/foráneas, consultas con JOIN para unir datos.
**ACID**: Atomicity (todo o nada), Consistency (reglas cumplidas), Isolation (transacciones separadas), Durability (datos persistentes).
Implementé PostgreSQL en sistema bancario para transferencias donde la consistencia era fundamental - cero discrepancias contables.

**NoSQL**: Flexibilidad de esquema, escalabilidad horizontal masiva para big data y alto tráfico.
Tipos: Documentos (MongoDB), Key-Value (Redis), Columnas (Cassandra), Grafos (Neo4j).
Eventual consistency en lugar de ACID, ideal para aplicaciones web modernas.
Utilicé MongoDB en e-commerce para catálogos con atributos variables y Cassandra en IoT para millones de registros de sensores.

### Redis como Cache
Base de datos en memoria para datos frecuentemente accedidos - reduje latencia de 200ms a 20ms en consultas repetitivas.
Almacena datos en RAM, perfecto para sesiones de usuario y resultados de consultas frecuentes.
Soporta estructuras avanzadas (lists, sets, hashes, sorted sets) para rankings en tiempo real.
**Casos de uso**: Cache de sesiones, contadores, leaderboards, rate limiting.
Implementé cache distribuido en APIs con alta concurrencia mejorando rendimiento significativamente.

### Pruebas Unitarias
Verifican comportamiento de componentes aislados usando mocks para simular dependencias externas.
**Objetivo**: Probar lógica de negocio sin depender de BD, APIs externas o servicios.
Utilizo JUnit 5 + Mockito en Spring Boot para probar servicios sin depender de bases de datos reales.
**Mockito**: Simula comportamiento de dependencias con `when().thenReturn()`.
Implemento TDD escribiendo primero pruebas que definen comportamiento esperado, luego desarrollo código.

## 2. Java 8-11 (mejoras): explicar cada clase de su agregado, nuevas funciones
### Fundamentos de Java
Lenguaje orientado a objetos compilado a bytecode ejecutado en JVM - "write once, run anywhere".
**Compilación**: .java → javac → .class (bytecode) → JVM ejecuta en cualquier SO.
JVM gestiona memoria automáticamente con garbage collection, eliminando gestión manual como C/C++.
**Ventajas**: Multiplataforma, gestión automática de memoria, gran ecosistema de librerías.
Bytecode en archivos .class proporciona portabilidad multiplataforma total.


### Beans y Estereotipos Spring
**Bean**: Objeto que Spring maneja automáticamente (crea, destruye, inyecta dependencias).
Spring Container actúa como factory que crea objetos cuando los necesitas.
**@Service**: Marca clases de lógica de negocio (UserService maneja operaciones de usuario).
Contiene reglas de negocio como validaciones, cálculos y transformaciones.
**@Repository**: Marca clases que acceden a base de datos (UserRepository guarda/busca usuarios).
Spring traduce automáticamente excepciones de BD a excepciones más manejables.
**@Controller/@RestController**: Manejan peticiones web. RestController devuelve JSON directamente.
@Controller devuelve vistas HTML, @RestController devuelve datos para APIs.

### Stack vs Heap Memory
**Stack**: Almacena variables locales temporales, rápido pero pequeño (8MB aprox).
Cada thread tiene su propio stack, se limpia automáticamente al salir del método.
**Heap**: Almacena objetos grandes, más lento pero con más espacio (configurable).
Compartido entre threads, dividido en Young Generation y Old Generation.
**Garbage Collector**: Limpia objetos no referenciados automáticamente.
Ejecuta cuando heap está lleno, puede pausar la aplicación brevemente.

### Interfaces Funcionales y Lambda (Java 8)
**Lambda**: Forma corta de escribir funciones: `(x) -> x * 2` multiplica por 2.
Reemplaza clases anónimas, ideal para operaciones simples de una línea.
**Predicate**: Evalúa condiciones verdadero/falso: `x -> x > 10`.
Usado en filtros: `list.stream().filter(x -> x > 10)` para elementos mayores a 10.
**Function**: Transforma datos: `x -> x.toUpperCase()`.
Usado en mapeos: `list.stream().map(String::toUpperCase)` convierte a mayúsculas.
**Consumer**: Ejecuta acciones: `x -> System.out.println(x)`.
Usado para efectos secundarios como logging o envío de emails.

### Optional Class
Contenedor que evita errores de null (valores vacíos).
Obliga al programador a manejar explícitamente casos donde puede no haber valor.
**Métodos**: `isPresent()` verifica si hay valor, `orElse()` da valor por defecto.
`orElseThrow()` lanza excepción personalizada si está vacío.
**Ejemplo**: `Optional<User> user = findUser(id).orElse(defaultUser)`.

### Colecciones Java
**List**: Lista ordenada que permite duplicados (ArrayList es la más común).
ArrayList usa array interno que crece dinámicamente, LinkedList usa nodos enlazados.
**Set**: Conjunto sin duplicados (HashSet es la más común).
HashSet usa tabla hash para acceso O(1), TreeSet mantiene orden natural.
**Map**: Diccionario clave-valor (HashMap es la más común).
HashMap para acceso rápido, TreeMap para claves ordenadas, LinkedHashMap para orden de inserción.

### Spring vs Spring Boot
**Spring**: Framework básico para crear aplicaciones empresariales.
Requiere configuración XML extensa o anotaciones manuales detalladas.
**Spring Boot**: Versión simplificada de Spring con configuración automática.
Detecta dependencias y configura automáticamente, incluye servidor Tomcat embebido.
**Auto-configuration**: Analiza classpath y configura beans automáticamente.
Ejemplo: si detecta H2, configura automáticamente DataSource.

### Application Properties
Archivo donde guardas configuraciones (puertos, base de datos, etc.).
Formatos: application.properties o application.yml para mayor legibilidad.
**Profiles**: Diferentes configuraciones por ambiente (dev, test, prod).
`application-dev.properties` se activa con `spring.profiles.active=dev`.
**Ejemplos**: `server.port=8080`, `spring.datasource.url=jdbc:mysql://localhost/db`.

### Spring Security y JWT vs OAuth
**Spring Security**: Sistema de autenticación/autorización integrado en Spring.
Usa filtros que interceptan requests antes de llegar a controladores.
**JWT**: Token que contiene información del usuario (como un carnet digital).
Token auto-contenido (header.payload.signature) que no requiere estado en servidor.
**OAuth**: Protocolo para login con Google/Facebook sin compartir tu contraseña.
Cliente recibe token de autorización para acceder recursos sin credenciales.

### JPA y Relaciones
**@OneToMany**: Un usuario tiene muchos pedidos (relación 1 a muchos).
Ejemplo: `@OneToMany(mappedBy = "user") List<Order> orders` en clase User.
**@Transient**: Campo que no se guarda en base de datos.
Útil para campos calculados o datos temporales que no necesitan persistencia.
**Lazy Loading**: Carga datos relacionados solo cuando los necesitas (optimiza velocidad).
Evita traer datos innecesarios, pero puede causar LazyInitializationException..

### Problema N+1 y Soluciones
Ejecuta 1 consulta principal + N consultas adicionales para cargar relaciones - problemático en performance.
**@EntityGraph**: Especifica relaciones a cargar en una consulta evitando múltiples round-trips.
Implementé `@EntityGraph(attributePaths = {"orders", "orders.products"})` cargando usuarios+pedidos+productos en una consulta.

### JPA vs Hibernate
JPA: Especificación con interfaces estándar para persistencia Java.
Hibernate: Implementación concreta con características adicionales (cache segundo nivel, criteria API, mapeos personalizados).
Uso especificación JPA para portabilidad pero aprovecho características Hibernate como @Formula para campos calculados.

## 3. Microservicios con Java WebFlux

### ¿Qué son los Microservicios?
Arquitectura donde aplicación se divide en servicios pequeños, independientes y débilmente acoplados.
Implementé e-commerce: user-service, product-service, order-service, payment-service con BD propia cada uno.
**Ventajas**: Escalabilidad independiente, tecnologías heterogéneas, equipos autónomos, tolerancia a fallos aislada.

### Interfaces Java Comunes
**Comparable<T>**: Comparación natural con compareTo() - implemento en Product para ordenar por precio.
**Serializable**: Conversión a bytes para almacenamiento/transmisión.
**Runnable**: Tareas ejecutables por threads mediante run().

### Nginx - Servidor Web y Proxy Reverso
Servidor alto rendimiento: proxy reverso, load balancer, cache HTTP con arquitectura basada en eventos.
Configuré como load balancer distribuyendo tráfico entre múltiples instancias de microservicios.
**Casos de uso**: Load balancing, SSL termination, cache contenido estático, proxy reverso APIs, rate limiting.

### Scrum - Metodología Ágil
Framework ágil con sprints de duración fija (1-4 semanas) - participo en equipos con entregas incrementales cada 2 semanas.
**Roles**: Product Owner (requisitos), Scrum Master (facilita), Development Team (implementa).
**Eventos**: Sprint Planning, Daily Standups, Sprint Review, Sprint Retrospective.

### Jira - Gestión de Proyectos
Tracking de issues, gestión ágil y seguimiento de bugs con workflows personalizables.
Utilizo para planificar sprints, estimar story points (Fibonacci), trackear progreso con boards Kanban/Scrum.
Configuro workflows: To Do → In Progress → Code Review → Testing → Done con transiciones automáticas a Git.

### Programación Reactiva
Paradigma centrado en flujos de datos asíncronos y propagación de cambios - patrón Observer reactivo.
**Observables**: Flujos de datos asíncronos que emiten valores a lo largo del tiempo.
**Operadores**: Transforman/filtran flujos - map, filter, merge, flatMap.
**Contrapresión**: Gestiona flujo evitando saturar consumidores cuando productor es más rápido.

### RxJava vs Project Reactor
**RxJava**: Librería ReactiveX para Java con Observable/Single/Completable - implementé en Android apps con retrofit para llamadas API asíncronas.
**Project Reactor**: Base de Spring WebFlux con Mono<T>/Flux<T> optimizado para aplicaciones server-side con mejor integración Spring.
**Diferencias**: Reactor tiene mejor performance, manejo memoria optimizado y schedulers específicos para aplicaciones web vs RxJava más general.

### WebClient - Cliente HTTP Reactivo
Cliente HTTP no bloqueante que reemplaza RestTemplate en aplicaciones WebFlux - soporte completo programación reactiva.
Implementé comunicación entre microservicios: `webClient.get().uri("/users/{id}", userId).retrieve().bodyToMono(User.class)`.
**Ventajas**: Connection pooling automático, timeouts configurables, retry policies, circuit breaker integration con Resilience4j.
**Configuración**: Custom codecs JSON, headers automáticos, authentication interceptors, load balancing con múltiples instancias.

### Preguntas Frecuentes Programación Reactiva

#### ¿Cuándo usar Mono vs Flux?
**Mono<T>**: 0 o 1 elemento - uso para operaciones que retornan objeto único como `findById()`, respuestas HTTP únicas.
**Flux<T>**: 0 a N elementos - implemento para streams de datos como `findAll()`, eventos real-time, processing batch.
**Ejemplo**: `Mono<User>` para buscar usuario específico, `Flux<Order>` para stream de pedidos en tiempo real.

#### ¿Cómo manejar errores en streams reactivos?
**onErrorReturn**: Valor por defecto - `mono.onErrorReturn(User.empty())` cuando falla búsqueda usuario.
**onErrorResume**: Fallback reactivo - `flux.onErrorResume(ex -> alternativeService.getUsers())` para fuente alternativa.
**doOnError**: Logging sin modificar stream - implemento para auditoría errores sin afectar flujo principal.

#### ¿Qué es backpressure y cómo manejarlo?
Mecanismo control flujo cuando productor genera datos más rápido que consumidor puede procesarlos.
**Estrategias**: BUFFER (acumula), DROP (descarta nuevos), LATEST (mantiene último), ERROR (falla cuando buffer lleno).
Implementé en processing logs IoT: `flux.onBackpressureBuffer(1000)` acumulando hasta 1000 eventos antes descartar.

#### ¿Diferencias entre map() y flatMap()?
**map()**: Transformación 1:1 síncrona - `flux.map(user -> user.getName())` convierte User a String directamente.
**flatMap()**: Transformación 1:N asíncrona - `flux.flatMap(user -> getUserOrders(user.getId()))` cada user genera stream Orders.
**Uso**: map para transformaciones simples, flatMap para operaciones que retornan Mono/Flux (llamadas API, BD).

### WebClient vs RestTemplate
**RestTemplate**: Síncrono/bloqueante, thread pool limitado, configuración manual connection pooling - uso en aplicaciones MVC tradicionales.
**WebClient**: Asíncrono/no bloqueante, event loop eficiente, configuración automática recursos - implemento en WebFlux para máxima performance.
**Performance**: WebClient maneja 10,000+ requests concurrentes con 4 threads vs RestTemplate limitado por thread pool size.
**Migration**: Migré APIs legacy RestTemplate a WebClient mejorando latencia 60% y reduciendo uso memoria 40%.

### Spring MVC vs WebFlux
**MVC**: Síncrono/bloqueante, thread por petición, API Servlet - uso para aplicaciones CRUD tradicionales.
**WebFlux**: Asíncrono/no bloqueante, event loop con pocos threads, Project Reactor con Mono<T>/Flux<T>.
Implementé WebFlux en APIs que consumen múltiples servicios externos - redujo tiempo respuesta de 2s a 400ms.
WebFlux maneja 10,000 peticiones concurrentes con solo 4 threads vs MVC limitado por pool threads.

### WebFlux con Spring Data Reactive
Repositorios reactivos retornan Mono<T>/Flux<T> para interacción no bloqueante con BD.
**R2DBC**: Driver reactivo para BD relacionales reemplazando JDBC bloqueante.
**ReactiveMongoRepository**: MongoDB reactivo con operaciones asíncronas nativas.
Implementé servicio que procesa 100,000 registros reactivamente usando backpressure para controlar flujo.

### @Scheduled y Manejo de Peticiones
**@Scheduled**: Ejecuta métodos automáticamente - `@Scheduled(fixedRate = 5000)` cada 5s, `@Scheduled(cron = "0 0 2 * * ?")` diario 2AM.
Implementé jobs para sincronización de datos, limpieza cache y generación reportes automáticos.
**Peticiones POST**: Recibo datos con @RequestBody - `public ResponseEntity<User> createUser(@RequestBody @Valid UserDTO userDTO)`.

### Manejo Global de Excepciones y Seguridad
**@ControllerAdvice**: Maneja excepciones globalmente en todos controladores centralizando manejo de errores.
**@ExceptionHandler**: Especifica qué excepción manejar - implementé captura ValidationException retornando HTTP 400.
**Seguridad**: Validación entrada con Bean Validation (@Valid, @NotNull), HTTPS, headers seguridad (HSTS, CSP), rate limiting.
## 4. Patrones de Diseño en Microservicios (Circuit Breaker, Health Check, Strangler, CQRS, SAGA) y otros patrones
### Patrones Fundamentales
**Singleton**: Una instancia única por aplicación - implementé para gestores de cache compartidos entre componentes.
**Builder**: Construcción de objetos complejos paso a paso - útil con múltiples parámetros opcionales.
**Strategy**: Algoritmos intercambiables en runtime - implementé para procesadores de pago (Visa/MasterCard/PayPal).
**Observer**: Notificación automática cuando cambia estado - patrón base para eventos reactivos.
### Arquitectura Hexagonal
Separa lógica de negocio de tecnologías externas mediante ports/adapters.
**Domain**: Entidades puras sin dependencias, **Application**: Casos de uso, **Infrastructure**: Adapters para BD/APIs.
Beneficio: Testabilidad total y flexibilidad para cambiar tecnologías sin afectar negocio.
### Patrones de Microservicios
#### Circuit Breaker
Interruptor que corta comunicación cuando detecta fallas consecutivas protegiendo sistema de cascada.
**Estados**: Closed (normal) → Open (cortado tras umbral errores) → Half-Open (probando recuperación).
Implementé con resilience4j: umbral 60% errores abre circuito 30 segundos - evita timeouts en cascada.
#### Health Check
Endpoint `/health` que expone estado del servicio y dependencias (BD, servicios externos).
Implementé checks personalizados: Redis, PostgreSQL, servicios downstream.
Kubernetes usa estos endpoints para determinar si pod debe recibir tráfico.
#### Strangler Pattern
Migración gradual de legacy envolviendo funcionalidad y redirigiendo tráfico incrementalmente.
Implementé para migrar monolito a microservicios módulo por módulo sin interrumpir servicio.
#### CQRS con Axon Framework
Separa operaciones lectura/escritura para optimizar rendimiento y escalabilidad.
**Commands**: Escrituras con validaciones de negocio, **Queries**: Lecturas optimizadas con vistas materializadas.
Implementé en proyectos grandes: 90% lecturas (feeds, búsquedas) vs 10% escrituras (crear posts, editar perfil).
**Axon Framework**: Simplifica CQRS/Event Sourcing con anotaciones Java.
**Flujo**: Commands → Command Bus → Handlers → Events → Event Store → Read Models.
**Event Sourcing**: Guarda eventos de modificación en lugar de estado actual - auditoría completa y replay.
#### SAGA Pattern
Transacciones distribuidas como secuencia de transacciones locales con compensación automática.
**Coreografía**: Servicios autónomos reaccionan a eventos - implementé en e-commerce: Order → Payment → Inventory.
**Orquestación**: Coordinador central dirige pasos - usé para procesos críticos con control/visibilidad total.
Ejemplo: Reservar Inventario → Procesar Pago → Crear Orden; si falla: Compensar Pago → Liberar Inventario.
#### API Gateway
Punto de entrada único para peticiones de clientes hacia microservicios con routing dinámico.
Implementé con Spring Cloud Gateway agregando datos usuario+pedidos en una respuesta para móviles.
**Responsabilidades**: Autenticación, rate limiting, circuit breaking, logging, transformación protocolos.
#### Patrones de Creación
**Factory Method**: Delega creación de objetos a subclases sin exponer lógica de construcción.
Implementé NotificationFactory que crea EmailNotification/SMSNotification/PushNotification según canal preferido usuario.
Beneficio: Agregar nuevos tipos sin modificar código existente - principio Open/Closed.
**Builder**: Construye objetos complejos paso a paso con múltiples configuraciones opcionales.
```java
User user = User.builder()
    .name("John")
    .email("john@test.com")
    .role(Role.ADMIN)
    .permissions(Set.of(WRITE, READ))
    .build();
```

#### Patrones Estructurales
**Repository**: Interfaz uniforme para CRUD independiente de tecnología persistencia.
```java
public interface UserRepository {
    Optional<User> findById(String id);
    List<User> findByStatus(UserStatus status);
    void save(User user);
    void delete(String id);
}
```
Implemento UserJpaRepository y UserMongoRepository con misma interfaz - cambio persistencia sin afectar servicios.
Beneficio: Testabilidad con mocks y flexibilidad para migrar tecnologías BD.

**Adapter**: Convierte interfaz incompatible en otra esperada por cliente.
Implementé PayPalAdapter que adapta PayPal SDK a interfaz PaymentProcessor estándar.
Uso para integrar sistemas legacy con arquitectura moderna sin modificar código existente.

**Decorator**: Agrega funcionalidad dinámicamente sin alterar estructura original.
Implementé LoggingDecorator y CachingDecorator envolviendo servicios con logging/cache transparentes.
```java
PaymentService decoratedService = new CachingDecorator(
    new LoggingDecorator(new PaymentServiceImpl())
);
```

**Facade**: Simplifica interfaz compleja proporcionando punto de entrada unificado.
Implementé OrderFacade que coordina User/Product/Payment/Inventory services para crear pedidos.
Cliente solo llama `orderFacade.createOrder()` sin conocer complejidad interna.

**Proxy**: Controla acceso a objeto proporcionando placeholder con funcionalidad adicional.
Implementé SecurityProxy que valida permisos antes de acceder servicios sensibles.
Uso para lazy loading, cache, logging, seguridad sin modificar objeto original.

#### Patrones de Comportamiento
**Command**: Encapsula peticiones como objetos permitiendo parametrizar, encolar y deshacer operaciones.
Implementé en CQRS: CreateUserCommand, UpdateUserCommand con CommandHandler respectivos.
```java
@CommandHandler
public void handle(CreateUserCommand command) {
    User user = new User(command.getUserId(), command.getName());
    userRepository.save(user);
    eventBus.publish(new UserCreatedEvent(user.getId()));
}
```

**Strategy**: Algoritmos intercambiables en runtime sin modificar contexto.
Implementé PaymentStrategy con implementaciones VisaStrategy/MasterCardStrategy/PayPalStrategy.
Cliente selecciona estrategia dinámicamente según método pago preferido.

**Observer**: Notifica automáticamente a dependientes cuando cambia estado de objeto.
Base de programación reactiva - implementé para eventos de dominio con múltiples listeners.
Uso en microservicios para comunicación asíncrona entre servicios débilmente acoplados.

**Template Method**: Define esqueleto de algoritmo permitiendo subclases implementar pasos específicos.
Implementé DataProcessor abstracto con process() que llama validate(), transform(), save().
Subclases implementan lógica específica manteniendo flujo consistente.

**Chain of Responsibility**: Pasa peticiones a cadena de manejadores hasta encontrar uno apropiado.
Implementé para validación de requests: AuthenticationHandler → AuthorizationHandler → ValidationHandler.
Cada handler decide si procesa o pasa al siguiente - flexibilidad total.

**State**: Cambia comportamiento de objeto cuando cambia estado interno.
Implementé para Order con estados: Pending → Processing → Shipped → Delivered.
Cada estado define acciones válidas - evita if/else complejos con lógica estado.

**Mediator**: Centraliza comunicación compleja entre objetos relacionados.
Implementé ChatMediator que coordina User/Channel/Message sin dependencias directas.
Reduce acoplamiento cuando múltiples objetos interactúan frecuentemente.


## 5. Observabilidad (Prometheus, Grafana)

### Prometheus - Monitoreo de Métricas
Sistema de monitoreo que recopila métricas (CPU, memoria, latencia, errores) mediante HTTP pulls desde `/metrics`.
Implementé en microservicios: redujo picos de memoria de 2GB a 500MB tras identificar optimizaciones.
Almacena en TSDB optimizada para series temporales con formato: `http_requests_total{method="GET"} 1234`.
Configuré scrape intervals: 15s servicios críticos, 1min servicios normales.

### Grafana - Visualización y Alertas
Plataforma que conecta con múltiples data sources (Prometheus, InfluxDB, MySQL) para dashboards y alertas.
Creé dashboards con KPIs: tiempo procesamiento órdenes, tasa conversión, usuarios activos simultáneos.
Alertas automáticas vía email/Slack cuando métricas superan umbrales - reduje detección problemas de 30min a 2min.

### Implementación Stack Prometheus+Grafana
**Flujo**: Spring Boot expone `/actuator/prometheus` → Prometheus scrape → Grafana consulta con PromQL → Dashboards/Alertas.
**Dependencies**: `spring-boot-starter-actuator` + `micrometer-registry-prometheus` en pom.xml.
**Configuración**: `management.endpoints.web.exposure.include=health,metrics,prometheus` en application.yml.
**Docker Setup**: Imágenes personalizadas con configuraciones pre-cargadas por ambiente (dev/staging/prod).
**Alertas**: CPU > 80%, memoria > 85%, errores 5xx > 5%, latencia P95 > 2s con retention 30 días.

```yaml
# prometheus.yml
global:
  scrape_interval: 15s
scrape_configs:
  - job_name: 'spring-boot'
    static_configs:
      - targets: ['app:8080']
```

## 6. Experiencia y conocimiento en Cloud - Docker, Kubernetes Pods, AKS (Azure de preferencia)

### Docker - Contenedorización
**¿Qué es Docker?**: Plataforma que empaqueta aplicaciones con dependencias en imágenes portables compartiendo kernel del host.
Virtualización a nivel de OS más eficiente que VMs tradicionales - menos recursos, arranque rápido.
Implementé para standardizar ambientes dev/prod eliminando "funciona en mi máquina".
**Dockerfile**: Archivo texto con instrucciones para construir imagen automáticamente.
Creé Dockerfiles multi-stage reduciendo imágenes de 800MB a 150MB con Alpine Linux.
**Layers**: Cada comando crea layer cacheable, optimizando builds subsecuentes.
**Comandos clave**: `docker build -t app:v1 .`, `docker run -d -p 8080:8080 app:v1`, `docker-compose up -d`.

### Kubernetes - Orquestación
Orquestador que automatiza deployment/scaling de aplicaciones containerizadas declarando estado deseado.
**Arquitectura**: Master nodes (API Server, etcd, Scheduler) + Worker nodes (kubelet, kube-proxy, Container Runtime).
Implementé auto-scaling horizontal: 3 a 15 pods durante picos de tráfico con HPA basado en CPU 70%.

**Pods**: Unidad mínima con 1+ contenedores compartiendo red/storage, efímeros y reemplazables.
Cada pod tiene IP única, volúmenes compartidos, contenedores comunicados vía localhost.
Configuré resource limits (CPU: 500m, Memory: 512Mi) y requests (CPU: 100m, Memory: 256Mi).

**ConfigMaps**: Almacenan configuración no confidencial (URLs, flags, parámetros) separada del código.
Implementé `kubectl create configmap app-config --from-file=config.properties` para externalizar configuraciones.
Montados como volúmenes o variables de entorno: `envFrom: configMapRef: name: app-config`.

**Secrets**: Almacenan información sensible (passwords, tokens, keys) codificada base64.
Configuré secrets para BD: `kubectl create secret generic db-secret --from-literal=password=mypass123`.
Más seguro que ConfigMaps con cifrado en reposo y acceso RBAC estricto.

**Services**: Exponen pods internamente (ClusterIP) o externamente (LoadBalancer/NodePort/Ingress).
Service discovery automático vía DNS: `http://my-service.default.svc.cluster.local:8080`.
**Beneficios**: Alta disponibilidad, rolling updates sin downtime, service discovery DNS interno.

### Azure Kubernetes Service (AKS)
Kubernetes AKS es un servicio gestionado que simplifica despliegue/operación de clusters Kubernetes en Azure.
**Control Plane**: API Server, etcd, Scheduler gestionados automáticamente por Microsoft.
Configuré node pools separados: Standard_D2s_v3 para apps web, Standard_F4s_v2 para procesamiento.

**Virtual Network Integration**: AKS integrado con VNets Azure para conectividad híbrida.
Implementé Advanced Networking (Azure CNI) para asignación IPs directa desde subnet.
**Subnets**: AKS requiere subnet dedicada con suficientes IPs (/24 mínimo para cluster pequeño).

**Azure Container Registry (ACR)**: Registry privado para imágenes Docker integrado con AKS.
Configuré trust automático sin credenciales: AKS pull images directo de ACR con identidad administrada.
**Service Principal**: Identidad que permite AKS acceder recursos Azure (ACR, Storage, Networks).

**Características**: Cluster autoscaler, integración Azure AD/ACR/Monitor, network policies.
**RBAC**: Role-Based Access Control integrado con Azure Active Directory.
Implementé cluster auto-scaling que redujo costos 40% ajustando nodos en horarios baja demanda.
**Azure Monitor**: Logs centralizados, métricas performance, alertas automáticas integradas.

## 7. Azure (Functions, Contenedores/AKS, Data Factory, Databricks) Otras nubes (AWS / GCP)

### Serverless

#### AWS Lambda vs Azure Functions
**¿Qué es Serverless?**: Código que se ejecuta sin gestionar servidores, auto-escala y solo pagas por tiempo de ejecución.
Ideal para microservicios, procesamiento eventos y APIs con tráfico variable.

**AWS Lambda**: Serverless con escalado automático - desarrollé API Gateway+Lambda procesando 1M requests/día, latencia 200ms.
**Características**: Soporte múltiples lenguajes (Python, Node.js, Java, C#), timeout máximo 15 minutos.
**Triggers**: S3 events, DynamoDB streams, API Gateway, CloudWatch events, SQS/SNS.
Implementé pipeline procesamiento imágenes S3→Lambda→redimensionar automático y monitoring CloudWatch→alertas Slack.
**Ejemplo**: Función que redimensiona imágenes automáticamente cuando se suben a S3 bucket.

**Azure Functions**: Basada en eventos con integración Microsoft - conecté Dynamics 365 con sistemas externos como middleware.

**¿Qué es Azure Functions?**: Servicio serverless donde solo despliegas código, sin gestionar servidores.
Escribes funciones pequeñas que se ejecutan cuando algo las activa (evento, petición HTTP, timer).
**Ventaja principal**: Solo pagas por el tiempo que tu código realmente se ejecuta.

**Cómo funciona**:
1. Escribes una función (código Python, C#, Java, Node.js)
2. Defines qué la activa (trigger): HTTP request, timer, mensaje en cola, archivo en storage
3. Azure detecta el trigger y ejecuta tu función automáticamente
4. Función procesa la tarea y se detiene
5. Azure escala automáticamente si hay muchas peticiones simultáneas

**Ejemplo práctico - Procesamiento de imágenes**:
Usuario sube foto → trigger Blob Storage → función redimensiona imagen → guarda resultado → función termina.
Todo automático, sin gestionar servidores, solo pagando milisegundos de ejecución.

**Características clave**:
**Triggers**: HTTP, Timer, Blob Storage, Service Bus, Event Grid, Cosmos DB.
**Bindings**: Input/output automático desde BD, storage, queues sin código boilerplate.
**Stateless**: Cada ejecución es independiente, no mantiene estado entre llamadas.
**Auto-scaling**: Si llegan 1000 requests simultáneos, Azure crea 1000 instancias automáticamente.

**Ventajas vs Servidores tradicionales**:
- No gestionar infraestructura (actualizaciones, parches, escalado)
- Costos reducidos (solo tiempo ejecución real vs servidor 24/7)
- Escalado automático instantáneo (de 0 a 1000 instancias)
- Integración nativa con ecosistema Microsoft

**Ejemplo completo - Notificación Email**:
```csharp
[FunctionName("SendEmail")]
public static void Run(
    [QueueTrigger("orders")] Order order,
    [SendGrid] out SendGridMessage message)
{
    message.Subject = $"Order {order.Id} confirmed";
    message.SetText($"Thank you for order ${order.Total}");
}
```
Trigger: nuevo mensaje en cola "orders" → función ejecuta → envía email → termina (duración: 200ms).

### Servicios Datos Azure

#### Azure Data Factory
- Azure Factorury es un servicio de integración de datos en la nube que permite crear, programar y orquestar flujos de trabajo de datos a gran escala.
**¿Qué es ETL?**: Extract (extraer datos), Transform (transformar formato), Load (cargar destino final).
Servicio en la nube que orquesta movimiento y transformación de datos entre múltiples fuentes.
ETL en nube orquestando múltiples fuentes - implementé pipeline SQL Server on-premises→Spark→Synapse Analytics.

**Componentes principales**:
**Datasets**: Definen estructura de datos (CSV, JSON, SQL tables, APIs).
**Linked Services**: Conexiones a fuentes de datos (SQL Server, Oracle, Azure Storage).
**Pipelines**: Flujos de trabajo que definen secuencia de actividades.
**Activities**: Operaciones individuales (copy data, run stored procedure, execute pipeline).

**Data Flows**: Transformaciones visuales sin código usando drag-and-drop interface.
Configuré triggers programados procesando CSV proveedores madrugadas sincronizando inventarios y data flows visuales sin código.
**Triggers**: Schedule (cron), tumbling window, storage events para ejecución automática.
**Monitoring**: Dashboard con métricas de ejecución, alertas por email/Teams cuando fallan jobs.

**Casos de uso**: Migration datos on-premises→cloud, sincronización entre sistemas, data warehousing.
**Ejemplo**: Cada madrugada extrae ventas de SQL Server, transforma formato, carga a Synapse para reportes.

#### Azure Databricks
**¿Qué es Apache Spark?**: Motor procesamiento distribuido que procesa big data en paralelo usando múltiples máquinas.
**¿Qué es Machine Learning?**: Algoritmos que aprenden patrones de datos para hacer predicciones automáticas.

Plataforma Spark para ML/analytics - implementé modelo recomendaciones procesando 10M transacciones, precisión 85%.
**Arquitectura**: Clusters auto-scaling con drivers/workers, notebooks colaborativos web-based.
**Lenguajes**: Python, Scala, R, SQL con librerías optimizadas para big data y ML.

**Notebooks**: Documentos interactivos que combinan código, visualizaciones y texto explicativo.
Desarrollé notebooks colaborativos Python/Scala/R y jobs automatizados entrenando modelos semanalmente.
**Colaboración**: Múltiples usuarios editando simultáneamente, version control integrado, comentarios.
**Visualización**: Gráficos integrados, dashboards interactivos, export a PowerBI.

**Machine Learning Workflows**:
1. **Data Exploration**: Análisis exploratorio identificando patrones y calidad datos.
2. **Feature Engineering**: Creación variables relevantes para modelos ML.
3. **Model Training**: Entrenamiento algoritmos (regression, classification, clustering).
4. **Model Evaluation**: Validación precisión usando métricas como accuracy, precision, recall.
5. **Model Deployment**: Puesta producción modelos como APIs REST.

**MLflow Integration**: Tracking experimentos, versionado modelos, deployment automático.
**AutoML**: Automated machine learning que encuentra mejores algoritmos y parámetros automáticamente.
**Delta Lake**: Storage layer que garantiza ACID transactions en data lakes.

**Ejemplo real**: Modelo recomendación productos analiza historial compras usuarios para sugerir nuevos productos.
Pipeline automatizado: datos transaccionales→limpieza→feature engineering→entrenamiento modelo→evaluación→deployment API.

## 8. Seguridad (OWASP, SonarQube) y CI/CD (Jenkins, GitLab)

### ¿Qué es OWASP?
Open Web Application Security Project - organización sin fines de lucro enfocada en mejorar seguridad software.
Publica Top 10 vulnerabilidades web más críticas actualizadas cada 3-4 años basadas en datos reales industria.
**Recursos**: OWASP Testing Guide, OWASP Code Review Guide, herramientas como ZAP para penetration testing.
**Importancia**: Estándar industria para security compliance, auditorías, training developers en secure coding practices.

### ¿Qué es SonarQube?
Plataforma análisis estático código que detecta bugs, vulnerabilities, code smells y mide cobertura tests automáticamente.
**Funcionalidad**: Continuous inspection código durante desarrollo, quality gates configurables, métricas detalladas.
**Lenguajes**: Soporte 25+ lenguajes incluyendo Java, C#, JavaScript, Python, PHP, Go.
**Integration**: Plugins para IDEs, CI/CD pipelines, webhooks para notificaciones automáticas.

### ¿Qué es Jenkins?
Servidor automation open-source para continuous integration/continuous deployment (CI/CD) con arquitectura plugin-based.
**Características**: Pipeline as Code con Jenkinsfile, distributed builds, integration 1000+ plugins.
**Uso**: Automatiza build, test, deploy applications reduciendo tiempo manual y errores humanos.
**Competidores**: GitLab CI, GitHub Actions, Azure DevOps, CircleCI.

### ¿Qué es GitLab CI/CD?
Platform DevOps integrada que combina Git repository, CI/CD pipelines, container registry, security scanning en una solución.
**Ventajas**: Todo-en-uno vs múltiples herramientas, GitLab Runners auto-scaling, built-in security scanning.
**Pipeline**: Definido en `.gitlab-ci.yml` con stages, jobs, artifacts, caching automático.
**Deployment**: Support múltiples environments, review apps, feature flags, monitoring integrado.

### Seguridad - OWASP Top 10

#### Injection Attacks (SQL, NoSQL, LDAP)
Validación exhaustiva entrada usuario previniendo inyección código malicioso en consultas base de datos.
Implementé prepared statements y parameterized queries eliminando 100% vulnerabilidades SQL injection detectadas en auditoría.
**Ejemplo**: `PreparedStatement ps = connection.prepareStatement("SELECT * FROM users WHERE id = ?")` en lugar de concatenación strings.
**Mitigación**: Input sanitization, whitelist validation, ORM frameworks como Hibernate que escapan automáticamente parámetros.

#### Broken Authentication
Implementé autenticación robusta con JWT tokens, session timeout automático, multi-factor authentication obligatorio roles admin.
Configuré Spring Security con rate limiting para login attempts: máximo 5 intentos por IP en 15 minutos.
**Medidas**: Password policies (mínimo 12 caracteres, mayúsculas/minúsculas/números/símbolos), encrypted storage con BCrypt, session invalidation.
**Monitoreo**: Logs detallados failed logins, alertas automáticas para patrones sospechosos de acceso.

#### Sensitive Data Exposure
Encriptación end-to-end para datos sensibles: PII, información financiera, credenciales usando AES-256.
Implementé encryption at rest en BD PostgreSQL con Transparent Data Encryption y encryption in transit con TLS 1.3.
**Clasificación**: Datos públicos/internos/confidenciales/restringidos con políticas acceso diferenciadas por categoría.
**Compliance**: GDPR compliance con data masking en ambientes no-productivos y derecho al olvido implementado.

#### XML External Entities (XXE)
Configuré parsers XML deshabilitando external entity processing previniendo ataques de lectura archivos sistema.
**Configuración**: `DocumentBuilderFactory.setFeature("http://apache.org/xml/features/disallow-doctype-decl", true)` en Java.
**Validación**: Schema validation con XSD, whitelist de elementos permitidos, size limits para payloads XML.

#### Security Misconfiguration
Hardening servers con configuraciones seguras por defecto: puertos innecesarios cerrados, servicios mínimos ejecutándose.
Automaticé security scanning con Nessus en pipelines CI/CD detectando misconfigurations antes despliegue producción.
**Gestión**: Configuration management con Ansible, infrastructure as code, regular security assessments.
**Monitoreo**: SIEM con Splunk para detección anomalías configuración, alertas cambios no autorizados.

#### Vulnerabilidades Comunes Adicionales
**Cross-Site Scripting (XSS)**: Content Security Policy (CSP) headers, input encoding, output sanitization.
**Cross-Site Request Forgery (CSRF)**: CSRF tokens en formularios, SameSite cookies, verificación origin headers.
**Insecure Direct Object References**: Authorization checks en cada request, object-level permissions.
**Security Headers**: HSTS, X-Frame-Options, X-Content-Type-Options configurados en todas responses.

### SonarQube - Análisis Código

#### Calidad Código y Vulnerabilidades
Integré SonarQube en pipelines analizando 500K+ líneas código detectando bugs, vulnerabilities, code smells automáticamente.
Configuré Quality Gates bloqueando merge requests con coverage <80%, duplicación >3%, vulnerabilidades críticas pendientes.
**Métricas**: Technical debt reducido 40% en 6 meses, maintainability rating mejorado de C a A.
**Rules**: Custom rules organizacionales, security hotspots review obligatorio, OWASP compliance verificado automáticamente.

#### Code Coverage y Testing
Implementé jacoco plugin generando reports coverage enviados a SonarQube, target minimum 85% line coverage.
**Branch coverage**: Verificación all paths ejecutados en unit tests, integration tests obligatorios servicios críticos.
**Mutation testing**: PIT testing validando calidad tests detectando tests débiles que no atrapan bugs reales.

#### Métricas Clave SonarQube
**Reliability**: Bug count, reliability rating (A-E basado en severity bugs).
**Security**: Vulnerability count, security rating, security hotspots requiring manual review.
**Maintainability**: Code smells, technical debt ratio, maintainability rating.
**Coverage**: Line coverage, branch coverage, duplicated lines percentage.

### CI/CD - Jenkins Pipeline

#### Pipeline as Code
Definí Jenkinsfiles declarativos en repositorios aplicación controlando build/test/deploy stages como código versionado.
**Stages**: Checkout → Unit Tests → Integration Tests → SonarQube Analysis → Build Docker → Security Scan → Deploy.
Implementé parallel execution reduciendo tiempo pipeline de 45min a 12min ejecutando tests en paralelo.
**Artifact management**: Nexus Repository storing artifacts, semantic versioning automático, promotion entre ambientes.

#### Automated Testing y Quality Gates
Configuré automated testing: unit (JUnit), integration (TestContainers), end-to-end (Selenium), performance (JMeter).
**Quality gates**: Pipeline falla si tests <95% pass rate, performance regression >20%, security vulnerabilities high/critical.
**Notifications**: Slack integration notificando equipos sobre build failures, deployment success, quality metrics.

#### Blue-Green Deployment
Implementé blue-green deployments con zero downtime: traffic switch automático tras health checks successful.
**Rollback**: Automated rollback si health checks fallen por 2min consecutivos, manual rollback en <30 segundos.
**Database migrations**: Flyway migrations backward-compatible, feature flags para new functionality gradual rollout.

#### Jenkins - Conceptos Fundamentales
**Master/Agent**: Master coordina builds, agents ejecutan jobs distribuido - configuré 5 agents Linux para parallel execution.
**Workspace**: Directorio temporal por job donde Jenkins ejecuta builds, limpiado automáticamente tras completion.
**Build Triggers**: SCM polling, webhooks GitHub/GitLab, scheduled builds con cron expressions.
**Plugin Ecosystem**: 1800+ plugins disponibles para integration tools, notifications, deployment targets.

### GitLab CI/CD

#### GitLab Runners y Container Registry
Configuré GitLab Runners en Kubernetes auto-scaling basado en build queue, máximo 10 concurrent jobs.
**Container registry**: Private registry integrado almacenando images Docker con vulnerability scanning automático.
**Security scanning**: SAST/DAST automated, dependency scanning, license compliance checks en cada merge request.

#### Pipeline Optimization
Implementé caching estrategias: Maven dependencies cache, Docker layer caching reduciendo build times 60%.
**Parallelization**: Jobs paralelos por environment (dev/staging/prod), matrix builds para multiple Java versions.
**Resource management**: Resource classes por tipo job: small (1 CPU, 2GB) testing, large (4 CPU, 8GB) builds.

#### GitLab - Características Distintivas
**Integrated DevOps**: Source code, CI/CD, security, monitoring en single platform - reduce tool sprawl.
**Built-in Security**: SAST, DAST, dependency scanning, container scanning incluidos sin plugins adicionales.
**Review Apps**: Temporary environments automáticos para feature branches facilitando code review.
**Auto DevOps**: Pipeline templates automáticos detectando project type, configuración cero para proyectos estándar.

### Programación Orientada a Objetos - Pilares
**Encapsulación**: Oculta detalles internos, expone solo lo necesario.
Atributos privados con getters/setters 
**Herencia**: Reutilización de código mediante relación "es-un" entre clases.
Clase hija hereda atributos/métodos de padre, puede sobrescribir métodos específicos.
Creé jerarquía Payment con CreditCardPayment y PayPalPayment compartiendo comportamientos comunes.
**Polimorfismo**: Objetos diferentes responden al mismo mensaje de forma específica.
Misma interfaz, implementaciones diferentes - decidido en tiempo de ejecución.
Uso PaymentProcessor donde Visa/MasterCard/PayPal procesan distinto con mismo método process().
**Abstracción**: Contratos mediante interfaces que definen qué hacer, no cómo hacerlo.
Interfaces especifican métodos que las clases deben implementar obligatoriamente.
Defino NotificationService implementada por EmailService/SMSService/PushNotificationService.
### Principios SOLID
**S - Single Responsibility**: Cada clase tiene una única razón para cambiar - separo UserValidator, UserRepository, UserService con responsabilidades específicas.
**O - Open/Closed**: Abierto para extensión, cerrado para modificación - uso interfaces PaymentProcessor para agregar nuevos métodos pago sin cambiar código existente.
**L - Liskov Substitution**: Subclases reemplazables por superclase sin afectar funcionalidad - cualquier PaymentMethod funciona donde se espera PaymentProcessor.
**I - Interface Segregation**: Interfaces específicas mejor que una general - separo UserReader, UserWriter en lugar de UserRepository monolítico.
**D - Dependency Inversion**: Depender de abstracciones, no implementaciones - UserService depende de UserRepository interface, no UserJpaRepository concreto.
### Azure Kubernetes Service (AKS)
Kubernetes AKS es un servicio gestionado que simplifica despliegue/operación de clusters Kubernetes en Azure.
#### AWS Lambda vs Azure Functions
**¿Qué es Serverless?**: Código que se ejecuta sin gestionar servidores, auto-escala y solo pagas por tiempo de ejecución.
**¿Qué es Azure Functions?**: Servicio serverless donde solo despliegas código, sin gestionar servidores.
Escribes funciones pequeñas que se ejecutan cuando algo las activa (evento, petición HTTP, timer).
#### Azure Data Factory
- Azure Factorury es un servicio de integración de datos en la nube que permite crear, programar y orquestar flujos de trabajo de datos a gran escala.
**¿Qué es ETL?**: Extract (extraer datos), Transform (transformar formato), Load (cargar destino final).
Azure Databricks es una plataforma de análisis de big data basada en Apache Spark que permite procesar grandes volúmenes de datos en paralelo usando múltiples máquinas. Incluye notebooks colaborativos web para escribir código en Python/Scala/R/SQL y facilita la creación de modelos de machine learning con MLflow integrado. Es ideal para ETL de datos masivos, análisis exploratorio y despliegue de modelos predictivos a escala empresarial.