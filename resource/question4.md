# Guía para Entrevista Técnica - Angular y Bases de Datos

## ¿Qué es Angular?

### Definición y Propósito
Angular es un framework de desarrollo web de código abierto basado en TypeScript, creado y mantenido por Google, diseñado para construir aplicaciones web de página única (SPA) robustas y escalables.
Lo he utilizado para crear aplicaciones empresariales complejas donde la estructura, el tipado fuerte y las herramientas integradas aceleran el desarrollo y facilitan el mantenimiento a largo plazo.
Angular proporciona un ecosistema completo con soluciones integradas para routing, formularios, llamadas HTTP, testing y más, eliminando la necesidad de integrar múltiples bibliotecas de terceros.
Es un framework opinionado que establece convenciones y mejores prácticas, lo cual he encontrado beneficioso en equipos grandes donde la consistencia del código es crucial.

### Historia y Evolución
Angular comenzó como AngularJS (Angular 1.x) en 2010, pero fue completamente reescrito en 2016 como Angular 2, abandonando JavaScript por TypeScript y adoptando una arquitectura basada en componentes.
He trabajado tanto con AngularJS legacy como con Angular moderno, y la migración a la arquitectura de componentes mejoró significativamente la mantenibilidad y el rendimiento de las aplicaciones.
Desde Angular 2, el equipo de Google sigue un ciclo de lanzamientos predecible cada 6 meses, permitiendo planificar actualizaciones y adoptar nuevas características de forma gradual.
Las versiones actuales mantienen compatibilidad hacia atrás en su mayoría, facilitando las actualizaciones incrementales sin necesidad de reescribir aplicaciones completas.

### Ventajas de Angular

#### Framework Completo
Angular incluye todo lo necesario out-of-the-box: routing, manejo de estado, formularios, HTTP client, testing, sin necesidad de elegir e integrar bibliotecas externas como en otros ecosistemas.
He aprovechado esta completitud para comenzar proyectos rápidamente sin perder tiempo configurando el stack tecnológico o resolviendo incompatibilidades entre bibliotecas.
La CLI de Angular automatiza tareas comunes como generar componentes, ejecutar tests, y construir para producción, aumentando la productividad del equipo.

#### TypeScript
Angular está construido con TypeScript, proporcionando tipado estático que detecta errores en tiempo de desarrollo antes de ejecutar el código.
He usado autocompletado inteligente del IDE y refactorización segura gracias al tipado fuerte, reduciendo bugs y facilitando el mantenimiento de código legacy.
Las interfaces y tipos TypeScript sirven como documentación viva del código, haciendo más fácil entender qué datos espera cada función o componente.
El compilador de TypeScript atrapa errores comunes como propiedades undefined, parámetros incorrectos o tipos incompatibles antes de que lleguen a producción.

#### Arquitectura Basada en Componentes
La arquitectura de componentes promueve reutilización y modularidad, donde cada componente encapsula su lógica, vista y estilos de forma independiente.
He creado bibliotecas de componentes reutilizables que uso en múltiples proyectos, como sistemas de diseño empresariales con botones, formularios y tablas estandarizadas.
La separación clara de responsabilidades facilita el testing unitario, permitiendo probar componentes de forma aislada sin necesidad de levantar toda la aplicación.

#### Two-Way Data Binding
Angular soporta enlace bidireccional de datos donde cambios en el modelo se reflejan automáticamente en la vista y viceversa, simplificando la sincronización UI-datos.
He usado [(ngModel)] en formularios para mantener sincronizados inputs con el modelo sin escribir código manual de actualización, reduciendo boilerplate.

#### Inyección de Dependencias
El sistema de inyección de dependencias de Angular gestiona la creación y provisión de servicios automáticamente, promoviendo código desacoplado y testeable.
Implemento servicios que declaro sus dependencias en el constructor y Angular los instancia e inyecta automáticamente, facilitando testing con mocks.

#### Ecosistema y Comunidad
Angular tiene una comunidad masiva con abundantes recursos, tutoriales, bibliotecas de terceros como Angular Material, PrimeNG, NgRx para manejo de estado avanzado.
He encontrado soluciones a problemas complejos en Stack Overflow, documentación oficial y blogs de la comunidad, acelerando el desarrollo cuando enfrento desafíos nuevos.
Google proporciona soporte a largo plazo (LTS) para versiones específicas, importante para aplicaciones empresariales que requieren estabilidad y mantenimiento prolongado.

#### Performance
Angular optimiza el rendimiento con técnicas como Ahead-of-Time (AOT) compilation que compila templates durante el build en lugar de en el navegador.
He implementado lazy loading de módulos para reducir el tamaño del bundle inicial, cargando código solo cuando el usuario navega a rutas específicas.
Tree-shaking elimina automáticamente código no usado del bundle final, reduciendo el tamaño de descarga y mejorando tiempos de carga.
Change detection optimizada con OnPush strategy reduce el número de verificaciones de cambios, mejorando el rendimiento en aplicaciones con muchos componentes.

#### Testing Integrado
Angular incluye herramientas de testing con Jasmine y Karma configuradas por defecto, facilitando escribir tests unitarios desde el inicio del proyecto.
He escrito tests de componentes usando TestBed que simula el entorno de Angular, permitiendo probar componentes con sus dependencias inyectadas.
End-to-end testing con Protractor (ahora Cypress o Playwright) está soportado, permitiendo automatizar pruebas de flujos completos de usuario.

### Cuándo Usar Angular

#### Aplicaciones Empresariales Grandes
Angular brilla en aplicaciones enterprise con múltiples módulos, equipos grandes y requisitos de mantenimiento a largo plazo donde la estructura y convenciones son valiosas.
He trabajado en proyectos bancarios y de seguros donde la arquitectura robusta de Angular facilita colaboración entre equipos distribuidos geográficamente.

#### Proyectos con Requisitos Complejos
Para aplicaciones con formularios complejos, validaciones intrincadas, manejo de estado sofisticado y múltiples roles de usuario, Angular proporciona soluciones integradas.
Implemento dashboards administrativos con tablas editables, gráficos interactivos, exportación de datos y permisos granulares aprovechando el ecosistema de Angular.

#### Equipos que Valoran TypeScript
Si el equipo prefiere tipado fuerte y herramientas de refactorización robustas, Angular con TypeScript obligatorio es ideal.
He migrado proyectos JavaScript a Angular TypeScript y la reducción de bugs en producción justificó la curva de aprendizaje inicial.

### Cuándo Considerar Alternativas
Para aplicaciones pequeñas o prototipos rápidos, frameworks más ligeros como Vue o Svelte pueden ser más apropiados por su menor curva de aprendizaje.
Proyectos que priorizan máxima flexibilidad y control fino pueden preferir React con su ecosistema de bibliotecas independientes en lugar del enfoque opinionado de Angular.
Si el equipo ya domina otro framework y el proyecto no requiere específicamente las fortalezas de Angular, mantener el stack existente puede ser más eficiente.

## Angular - Conceptos Fundamentales

### Componentes
Un componente en Angular es una clase TypeScript decorada con @Component que encapsula la lógica, la plantilla HTML y los estilos de una parte de la interfaz de usuario.
En mis proyectos he creado componentes reutilizables como un componente de tarjeta de producto que recibe datos mediante @Input y emite eventos con @Output para notificar al componente padre cuando el usuario hace clic en "Agregar al carrito".
He trabajado con el ciclo de vida de componentes implementando ngOnInit para cargar datos iniciales desde una API y ngOnDestroy para cancelar suscripciones y evitar fugas de memoria.
Utilizo la comunicación entre componentes mediante servicios compartidos cuando necesito que componentes no relacionados directamente intercambien información, como un servicio de carrito de compras accesible desde múltiples módulos.

### Comandos Angular CLI (ng g)
ng g component nombre crea un nuevo componente con su TypeScript, HTML, CSS y archivo de pruebas, además de actualizarlo automáticamente en el módulo correspondiente.
ng g service nombre genera un servicio inyectable que utilizo para centralizar la lógica de negocio y las llamadas HTTP, manteniéndola separada de los componentes.
ng g module nombre --routing crea un módulo con su archivo de rutas asociado, lo cual he usado para implementar lazy loading y mejorar el tiempo de carga inicial de aplicaciones grandes.
ng g guard nombre genera un guard que he implementado para proteger rutas y verificar autenticación antes de permitir el acceso a ciertas páginas.
ng g interface nombre crea interfaces TypeScript que uso para definir la estructura de datos y aprovechar el tipado fuerte, reduciendo errores en tiempo de desarrollo.
ng g directive nombre genera directivas personalizadas que he creado para manipular el DOM, como una directiva para validación visual de campos de formulario.
ng g pipe nombre crea pipes personalizados que he utilizado para formatear datos en las vistas, como convertir timestamps a fechas legibles o formatear monedas.

### Módulos (NgModule)
NgModule es un decorador que define un módulo de Angular, organizando componentes, directivas, pipes y servicios relacionados en bloques funcionales cohesivos.
En el array declarations declaro componentes, directivas y pipes que pertenecen al módulo y solo estarán disponibles dentro de ese contexto.
En el array imports incluyo otros módulos que necesito, como CommonModule para directivas básicas, FormsModule para formularios template-driven o HttpClientModule para realizar peticiones HTTP.
En el array providers registro servicios que quiero que estén disponibles mediante inyección de dependencias, aunque desde Angular 6+ prefiero usar providedIn: 'root' en el decorador @Injectable.
En el array exports declaro qué componentes, directivas o pipes quiero hacer públicos para que otros módulos que importen este módulo puedan utilizarlos.
He implementado feature modules para organizar funcionalidades específicas como un módulo de autenticación, un módulo de productos y un módulo de administración, cada uno con sus propias rutas y servicios.

### Routing y Navegación
El sistema de routing de Angular permite crear aplicaciones de página única (SPA) donde la navegación entre vistas ocurre sin recargar la página completa.
He configurado rutas en el RouterModule usando el array de rutas con objetos que definen path, component y opcionalmente canActivate para aplicar guards de protección.
Implemento lazy loading con loadChildren para cargar módulos bajo demanda solo cuando el usuario navega a esa ruta, reduciendo el tamaño del bundle inicial de la aplicación.
Utilizo parámetros de ruta con la sintaxis :id para crear rutas dinámicas como /productos/:id y luego accedo a estos parámetros usando ActivatedRoute en el componente.
He trabajado con rutas hijas (children) para crear layouts anidados donde un componente padre actúa como contenedor y renderiza diferentes componentes hijos según la ruta.
Uso routerLink en lugar de href en las plantillas para mantener la navegación dentro del contexto de Angular sin recargar la página.
Implemento navegación programática con this.router.navigate() cuando necesito redirigir al usuario después de una acción, como después de guardar un formulario o después de login exitoso.

### Guards (Protección de Rutas)
Los guards son servicios que implementan interfaces específicas para controlar el acceso a las rutas y proteger partes de la aplicación según reglas de negocio.
CanActivate es el guard más común que he usado para verificar si un usuario está autenticado antes de permitir acceso a rutas protegidas, redirigiendo al login si no tiene un token válido.
CanDeactivate lo he implementado para advertir al usuario cuando intenta salir de un formulario con cambios sin guardar, mostrando un diálogo de confirmación antes de permitir la navegación.
CanLoad lo uso con lazy loading para evitar que se descargue el código de un módulo completo si el usuario no tiene permisos, optimizando seguridad y rendimiento.
En mis implementaciones, los guards consultan servicios de autenticación para verificar tokens, roles de usuario o permisos específicos antes de retornar true o false.
He usado guards que retornan Observables para realizar verificaciones asíncronas, como validar un token con el servidor antes de permitir el acceso a una ruta.

### JWT (JSON Web Tokens)
JWT es un estándar de tokens que uso para manejar autenticación sin estado en aplicaciones Angular, donde el servidor genera un token firmado que el cliente almacena y envía en cada petición.
Implemento el flujo donde tras login exitoso, guardo el token en localStorage o sessionStorage y lo incluyo en el header Authorization: Bearer <token> de cada petición HTTP subsiguiente.
He creado interceptores HTTP que automáticamente agregan el token JWT a todas las peticiones salientes, centralizando esta lógica en lugar de repetirla en cada servicio.
Implemento la decodificación del payload del JWT para extraer información del usuario como roles o permisos sin hacer llamadas adicionales al servidor.
Manejo la expiración del token verificando el campo exp del payload y redirigiendo al login cuando el token expira, o implementando refresh token para renovarlo automáticamente.
He configurado guards que validan la presencia y validez del JWT antes de permitir acceso a rutas protegidas, mejorando la seguridad de la aplicación.

### Servicios e Inyección de Dependencias
Los servicios son clases TypeScript decoradas con @Injectable que encapsulan lógica de negocio, llamadas HTTP y estado compartido entre componentes.
Utilizo providedIn: 'root' en el decorador @Injectable para crear servicios singleton disponibles en toda la aplicación sin necesidad de registrarlos en providers de ningún módulo.
He creado servicios para manejar llamadas HTTP donde centralizo todas las peticiones a una API específica, como un AuthService para login/registro o ProductService para operaciones CRUD de productos.
Implemento servicios de estado cuando necesito compartir datos entre componentes no relacionados, usando BehaviorSubject de RxJS para crear observables que emiten el estado actual a nuevos suscriptores.
La inyección de dependencias en Angular permite que inyecte servicios en constructores de componentes, y el framework se encarga de crear y proveer las instancias necesarias automáticamente.

### HttpClient y Manejo de APIs
HttpClient es el módulo de Angular para realizar peticiones HTTP que reemplaza el antiguo Http y retorna Observables en lugar de Promesas.
Implemento métodos GET con this.http.get<Producto[]>(url) especificando el tipo de respuesta esperado para obtener autocompletado y verificación de tipos en TypeScript.
Uso POST con this.http.post<Respuesta>(url, body) para enviar datos al servidor, como cuando creo nuevos registros o envío formularios de registro de usuario.
He configurado interceptores para manejar errores globalmente, capturando respuestas 401 para redirigir al login, 403 para mostrar mensajes de permisos insuficientes, y errores 500 para logging.
Implemento manejo de errores con catchError de RxJS para capturar errores de peticiones HTTP y mostrar mensajes amigables al usuario en lugar de dejar que la aplicación falle silenciosamente.
Utilizo retry de RxJS para reintentar automáticamente peticiones que fallan por problemas de red temporales antes de mostrar un error al usuario.

### Formularios Reactivos
Los formularios reactivos son una forma de manejar formularios en Angular donde la lógica y validaciones se definen en el componente TypeScript en lugar de en la plantilla HTML.
Utilizo FormBuilder para crear FormGroups de manera concisa, definiendo controles con valores iniciales y validadores en una estructura de objeto.
Implemento validaciones síncronas usando Validators de Angular como Validators.required, Validators.email, Validators.minLength que se ejecutan inmediatamente cuando el usuario modifica un campo.
He creado validadores personalizados para reglas de negocio específicas, como verificar que dos contraseñas coincidan o validar formatos específicos de documentos de identificación.
Uso validadores asíncronos para verificaciones que requieren consultar el servidor, como comprobar si un nombre de usuario ya existe en la base de datos.
Implemento validación dinámica donde habilito o deshabilito controles, agrego o quito validadores según las selecciones del usuario en otros campos del formulario.
Utilizo FormArray para manejar listas dinámicas de controles, como cuando el usuario puede agregar múltiples direcciones o teléfonos en un mismo formulario.

### Formularios Template-Driven
Los formularios template-driven son más declarativos y definen la mayor parte de la lógica directamente en la plantilla HTML usando directivas como ngModel.
Los uso para formularios simples donde las validaciones son básicas y no requiero la flexibilidad completa de los formularios reactivos.
Implemento validaciones usando atributos HTML5 como required, email, minlength que Angular convierte automáticamente en validadores.
Accedo al estado del formulario usando variables de template (#form="ngForm") para deshabilitar el botón de submit hasta que el formulario sea válido.

### Directivas
Las directivas son instrucciones en el DOM que he utilizado de tres tipos: componentes, directivas estructurales y directivas de atributo.
Directivas estructurales como *ngIf las uso para mostrar u ocultar elementos según condiciones, como mostrar un mensaje de carga solo mientras se obtienen datos del servidor.
*ngFor lo implemento para iterar sobre arrays y renderizar listas dinámicas, como mostrar una lista de productos donde cada elemento tiene la misma estructura.
*ngSwitch lo uso cuando tengo múltiples condiciones mutuamente excluyentes, como mostrar diferentes componentes según el rol del usuario (admin, editor, viewer).
Directivas de atributo como ngClass las uso para agregar o quitar clases CSS dinámicamente según el estado, como agregar clase 'error' a campos de formulario inválidos.
ngStyle me permite establecer estilos inline dinámicamente, como cambiar el color de fondo de una tarjeta según el estado de un pedido (pendiente, procesado, enviado).
He creado directivas personalizadas para encapsular comportamientos reutilizables del DOM, como una directiva que agrega un tooltip personalizado o que resalta texto al hacer hover.

### Pipes
Los pipes son funciones puras que transforman datos en las plantillas para mostrarlos de forma diferente sin modificar el dato original.
Uso pipes incorporados como date para formatear fechas en formatos legibles (date:'dd/MM/yyyy'), currency para mostrar valores monetarios con símbolos de moneda apropiados.
uppercase y lowercase los aplico para normalizar la presentación de texto sin modificar el dato subyacente.
He implementado pipes personalizados para transformaciones específicas del dominio, como un pipe que convierte códigos de estado en etiquetas legibles o que trunca textos largos agregando puntos suspensivos.
Uso el operador pipe (|) en las plantillas para encadenar múltiples transformaciones, aplicando primero una conversión y luego un formato.
Los pipes async los utilizo extensivamente para suscribirme automáticamente a Observables en la plantilla y limpiar la suscripción cuando el componente se destruye, evitando fugas de memoria.

### RxJS y Observables
RxJS es la biblioteca de programación reactiva que Angular usa extensivamente para manejar operaciones asíncronas mediante Observables en lugar de Promesas o callbacks.
Los Observables representan flujos de datos que puedo suscribirme para recibir valores a lo largo del tiempo, perfectos para eventos de usuario, peticiones HTTP o websockets.
Utilizo operadores como map para transformar datos emitidos por un Observable, como convertir la respuesta de una API a un formato específico que necesita mi componente.
El operador switchMap lo uso cuando una emisión debe cancelar la petición anterior, como en un campo de búsqueda donde cada letra escrita debe cancelar la búsqueda previa.
mergeMap lo implemento cuando quiero ejecutar múltiples peticiones en paralelo y combinar sus resultados, como cuando necesito datos de varios endpoints simultáneamente.
filter lo uso para emitir solo valores que cumplan una condición, como filtrar eventos de teclado para procesar solo cuando el usuario presiona Enter.
debounceTime lo aplico en búsquedas para esperar que el usuario deje de escribir antes de hacer la petición al servidor, reduciendo el número de llamadas HTTP innecesarias.
Subject y BehaviorSubject los uso para crear Observables personalizados que puedo controlar manualmente, emitiendo valores cuando necesito notificar cambios de estado a múltiples suscriptores.
takeUntil lo implemento con un Subject que emite en ngOnDestroy para cancelar todas las suscripciones automáticamente cuando el componente se destruye.

### Change Detection
Change Detection es el mecanismo por el cual Angular detecta cambios en el estado de la aplicación y actualiza el DOM para reflejar esos cambios.
Uso ChangeDetectionStrategy.OnPush en componentes para optimizar rendimiento, indicando a Angular que solo revise el componente cuando sus inputs cambien o se dispare un evento.
Implemento detección manual con ChangeDetectorRef.detectChanges() cuando trabajo con código asíncrono fuera de la zona de Angular y necesito forzar una actualización de la vista.
markForCheck lo uso en componentes OnPush cuando actualizo propiedades desde callbacks o suscripciones y necesito que Angular revise el componente en el próximo ciclo de detección.

### Standalone Components (Angular 15+)
Los standalone components son una nueva forma de crear componentes sin necesidad de declararlos en NgModule, simplificando la arquitectura de aplicaciones Angular.
Defino un componente standalone con standalone: true en el decorador @Component y especifico sus dependencias directamente en el array imports del componente.
He migrado aplicaciones tradicionales a standalone components para reducir el boilerplate de NgModules y hacer el código más modular y fácil de entender.
Uso la función bootstrapApplication en main.ts para iniciar aplicaciones completamente standalone sin necesidad de un AppModule raíz.
Implemento lazy loading de componentes standalone directamente en las rutas sin necesidad de crear módulos wrapper, simplificando la configuración de routing.

## Diferencias entre Angular 16 y Angular 17

### Cambios de Arquitectura
Angular 17 introduce un nuevo builder esbuild por defecto que reemplaza a webpack, reduciendo drásticamente los tiempos de compilación en desarrollo y producción.
El sistema de hidratación del lado del servidor (SSR) se mejoró significativamente, permitiendo que aplicaciones renderizadas en servidor se hidraten más rápido en el navegador sin parpadeos visuales.
Angular 17 marca la culminación de la transición a standalone components como el enfoque recomendado, mientras que Angular 16 aún trataba NgModules como la opción principal.

### Cambios en NgModule y Dependencias
En Angular 17, crear nuevas aplicaciones con Angular CLI genera proyectos standalone por defecto sin AppModule, mientras que Angular 16 aún generaba la estructura tradicional con módulos.
La importación de CommonModule ya no es necesaria en componentes standalone de Angular 17 para usar *ngIf y *ngFor, ya que ahora se importan individualmente o están incluidos por defecto.
RouterModule se reemplaza en aplicaciones standalone por importaciones directas de provideRouter en la configuración de la aplicación, eliminando la necesidad del módulo.
HttpClientModule se reemplaza por provideHttpClient() que se configura en el array de providers del bootstrap, alineándose con el modelo funcional de configuración.

### Nuevo Sistema de Control Flow
Angular 17 introduce sintaxis nativa de control flow con @if, @for, @switch que reemplaza las directivas estructurales *ngIf, *ngFor, *ngSwitch con mejor rendimiento y menos sintaxis verbosa.
La nueva sintaxis @if (condición) { } proporciona mejor tipado y permite bloques @else if y @else más naturales sin necesidad de ng-template.
@for (item of items; track item.id) { } introduce el concepto de track obligatorio para optimización, reemplazando el trackBy opcional de *ngFor.
@switch (expresión) con @case y @default proporciona una sintaxis más cercana a JavaScript nativo y mejor rendimiento que *ngSwitch.
Estas nuevas sintaxis se compilan a código más eficiente y producen mensajes de error más claros durante el desarrollo.

### Signals (Introducido en Angular 16, Mejorado en 17)
Signals son un nuevo sistema de reactividad introducido en Angular 16 y mejorado en 17 que permite gestionar estado reactivo de forma más eficiente que los Observables para ciertos casos.
Un signal se crea con signal(valorInicial) y se lee llamándolo como función count(), proporcionando reactividad granular que solo actualiza partes específicas del DOM.
computed() crea signals derivados que se recalculan automáticamente cuando sus dependencias cambian, similar a Observables combinados pero con mejor rendimiento.
effect() permite ejecutar código cuando signals específicos cambian, similar a suscribirse a Observables pero más eficiente para actualizaciones del DOM.
Angular 17 mejora la integración de signals con el sistema de change detection, permitiendo usar OnPush por defecto con mejor rendimiento cuando se usan signals.

### Mejoras en Developer Experience
Angular 17 introduce una nueva documentación en angular.dev con tutoriales interactivos y playground integrado que reemplaza la documentación anterior en angular.io.
El CLI de Angular 17 genera proyectos con vite en modo desarrollo por defecto para recarga en caliente más rápida que el servidor de desarrollo anterior.
Los mensajes de error se mejoraron significativamente con sugerencias más claras y links a documentación relevante directamente desde la consola.
Angular 17 introduce mejor soporte para Server-Side Rendering con nuevas funciones como transferState automático que elimina peticiones duplicadas entre servidor y cliente.

### Cambios en Routing
provideRouter reemplaza RouterModule.forRoot en la configuración de aplicaciones standalone, proporcionando una API funcional más moderna.
Las funciones de configuración como withDebugTracing, withPreloading se pueden componer fácilmente en el nuevo modelo funcional.
Route guards se simplifican pudiendo ser funciones puras en lugar de clases, reduciendo el boilerplate necesario para proteger rutas.

### Deferrable Views (Angular 17)
Angular 17 introduce @defer para lazy loading declarativo de bloques de componentes directamente en templates sin necesidad de configurar routes.
La sintaxis @defer (on viewport) { } permite cargar componentes solo cuando son visibles en pantalla, optimizando el rendimiento inicial.
Triggers como on idle, on immediate, on timer permiten controlar cuándo se carga el contenido diferido según diferentes estrategias.
@placeholder muestra contenido mientras se carga el bloque diferido y @loading muestra un indicador de carga durante la descarga del código.

## Bases de Datos Relacionales

### Conceptos Fundamentales
Las bases de datos relacionales organizan datos en tablas con filas y columnas, donde cada fila representa un registro y cada columna representa un atributo con un tipo de dato específico.
Implemento relaciones entre tablas usando claves primarias (Primary Keys) que identifican únicamente cada registro y claves foráneas (Foreign Keys) que establecen conexiones con registros de otras tablas.
El modelo relacional permite normalización de datos para reducir redundancia, dividiendo información en múltiples tablas relacionadas en lugar de duplicar datos.
SQL (Structured Query Language) es el lenguaje estándar que uso para interactuar con bases de datos relacionales, permitiendo operaciones de consulta, inserción, actualización y eliminación de datos.

### SQL y Operaciones CRUD
SELECT lo uso para consultar datos con la sintaxis SELECT columnas FROM tabla WHERE condiciones, aplicando filtros, ordenamiento y joins para combinar datos de múltiples tablas.
INSERT INTO lo implemento para agregar nuevos registros con INSERT INTO tabla (columnas) VALUES (valores), validando que los datos cumplan las restricciones de la tabla.
UPDATE lo utilizo para modificar registros existentes con UPDATE tabla SET columna = valor WHERE condiciones, siendo cuidadoso con la cláusula WHERE para no actualizar registros no deseados.
DELETE lo aplico para eliminar registros con DELETE FROM tabla WHERE condiciones, usando transacciones cuando necesito asegurar que múltiples operaciones se completen o reviertan juntas.

### Joins y Relaciones
INNER JOIN lo uso para combinar tablas retornando solo registros que tienen coincidencias en ambas tablas, como obtener pedidos con información del cliente asociado.
LEFT JOIN lo implemento cuando necesito todos los registros de la tabla izquierda incluso si no tienen coincidencia en la derecha, como listar todos los clientes incluyendo aquellos sin pedidos.
RIGHT JOIN es el inverso de LEFT JOIN, útil cuando necesito asegurar que aparezcan todos los registros de la tabla derecha.
FULL OUTER JOIN lo uso raramente para obtener todos los registros de ambas tablas, mostrando NULL donde no hay coincidencias.
He diseñado relaciones uno-a-muchos (un cliente tiene muchos pedidos), muchos-a-muchos (estudiantes y cursos con tabla intermedia) y uno-a-uno (usuario y perfil).

### Índices y Optimización
Los índices son estructuras que aceleran búsquedas en tablas grandes creando referencias ordenadas a los datos, similar a un índice en un libro.
Implemento índices en columnas que uso frecuentemente en cláusulas WHERE, JOIN u ORDER BY para mejorar el rendimiento de consultas.
He analizado planes de ejecución (EXPLAIN) para identificar consultas lentas y determinar qué índices crear para optimizar el rendimiento.
Balanceo el uso de índices considerando que aceleran lecturas pero ralentizan inserciones y actualizaciones, por lo que no indexo todas las columnas.
Utilizo índices compuestos cuando frecuentemente filtro por múltiples columnas simultáneamente, como buscar por ciudad y categoría.

### Transacciones y ACID
Las transacciones agrupan múltiples operaciones SQL en una unidad atómica que se completa totalmente o se revierte completamente, manteniendo consistencia de datos.
ACID son las propiedades que garantizan confiabilidad: Atomicidad (todo o nada), Consistencia (reglas válidas), Aislamiento (transacciones concurrentes no interfieren), Durabilidad (cambios confirmados persisten).
Implemento transacciones cuando múltiples operaciones deben ejecutarse juntas, como transferir dinero entre cuentas donde debito de una debe ir acompañado de crédito en otra.
Uso BEGIN TRANSACTION, COMMIT para confirmar cambios y ROLLBACK para deshacer cambios cuando ocurre un error en cualquier paso de la transacción.

### Normalización
La normalización es el proceso de organizar datos para reducir redundancia y mejorar integridad mediante la división en tablas relacionadas.
Primera Forma Normal (1NF) requiere que cada columna contenga valores atómicos y cada fila sea única, eliminando grupos repetitivos de columnas.
Segunda Forma Normal (2NF) elimina dependencias parciales asegurando que columnas no clave dependan de toda la clave primaria, no solo de parte de ella.
Tercera Forma Normal (3NF) elimina dependencias transitivas donde columnas no clave dependen de otras columnas no clave en lugar de la clave primaria.
He aplicado normalización hasta 3NF en la mayoría de proyectos para balance entre integridad y rendimiento, desnormalizando selectivamente cuando las consultas requieren joins complejos muy frecuentes.

### PostgreSQL Específico
PostgreSQL soporta tipos de datos avanzados como JSON, Arrays, y tipos personalizados que he usado para almacenar datos semi-estructurados sin perder las ventajas del modelo relacional.
Implemento funciones y procedimientos almacenados en PL/pgSQL para encapsular lógica de negocio compleja directamente en la base de datos.
Uso CTE (Common Table Expressions) con WITH para crear subconsultas nombradas que hacen consultas complejas más legibles y mantenibles.
Las funciones de ventana (Window Functions) me permiten calcular agregados sin agrupar filas, como ranking de productos o promedios móviles.

### MySQL Específico
MySQL uso InnoDB como motor de almacenamiento por su soporte de transacciones ACID y claves foráneas, reemplazando el antiguo MyISAM.
Implemento full-text search en columnas de texto para búsquedas eficientes de palabras clave sin necesidad de LIKE '%término%' que no usa índices.
AUTO_INCREMENT lo uso para generar IDs únicos automáticamente al insertar nuevos registros sin necesidad de gestionarlos manualmente.

## Bases de Datos NoSQL

### Conceptos Fundamentales
NoSQL (Not Only SQL) abarca bases de datos que no siguen el modelo relacional tabular, diseñadas para escalabilidad horizontal y flexibilidad de esquema.
Estas bases de datos sacrifican algunas garantías ACID en favor de disponibilidad y particionamiento según el teorema CAP (Consistency, Availability, Partition tolerance).
Los casos de uso donde prefiero NoSQL incluyen datos no estructurados, necesidad de escalamiento masivo, esquemas que cambian frecuentemente, o patrones de acceso de lectura intensiva.

### Tipos de Bases de Datos NoSQL
Document stores como MongoDB almacenan datos en documentos JSON-like con esquemas flexibles, ideales para datos semi-estructurados que varían entre registros.
Key-Value stores como Redis son las más simples, almacenando pares clave-valor, perfectas para cachés, sesiones de usuario o contadores de alta frecuencia.
Column-family stores como Cassandra organizan datos en columnas en lugar de filas, optimizadas para escrituras masivas y análisis de grandes volúmenes.
Graph databases como Neo4j modelan relaciones como ciudadanos de primera clase, ideales para redes sociales, recomendaciones o detección de fraude donde las conexiones son tan importantes como los datos.

### MongoDB
MongoDB almacena documentos BSON (Binary JSON) en colecciones sin requerir que todos los documentos tengan la misma estructura, proporcionando flexibilidad de esquema.
Implemento consultas con métodos como find(), findOne(), insertOne(), updateMany() usando un lenguaje de consulta basado en objetos JavaScript en lugar de SQL.
Uso aggregation pipeline para transformaciones complejas de datos encadenando operadores como $match, $group, $project, $sort similar a operaciones SQL complejas.
Los índices en MongoDB funcionan similar a bases relacionales, creándolos en campos frecuentemente consultados con createIndex() para mejorar rendimiento.
Implemento relaciones mediante referencias (almacenando ObjectId de otro documento) o embedding (anidando documentos completos), eligiendo según patrones de acceso.
La desnormalización es común en MongoDB, duplicando datos intencionalmente para optimizar lecturas y reducir joins, aceptando el costo de mantener consistencia en actualizaciones.

### Redis
Redis es una base de datos en memoria que uso principalmente como caché para reducir latencia de operaciones frecuentes que de otra forma consultarían bases de datos más lentas.
Implemento almacenamiento de sesiones de usuario en Redis con expiración automática usando SETEX, evitando la necesidad de limpiar sesiones expiradas manualmente.
Uso estructuras de datos avanzadas como Hashes para almacenar objetos, Lists para colas, Sets para colecciones únicas, y Sorted Sets para rankings o leaderboards.
Pub/Sub de Redis lo implemento para comunicación en tiempo real entre microservicios, donde servicios publican mensajes a canales y otros servicios suscritos los reciben instantáneamente.
Configuro persistencia con snapshots o AOF (Append Only File) cuando necesito que datos en memoria sobrevivan reinicios del servidor, aunque aceptando que es principalmente una base de datos en memoria.

### Comparación Relacional vs NoSQL
Elijo bases de datos relacionales cuando necesito transacciones ACID fuertes, consultas complejas con múltiples joins, o esquemas estrictos que no cambiarán frecuentemente.
Prefiero NoSQL para escalamiento horizontal masivo, esquemas flexibles que evolucionan rápidamente, o cuando los patrones de acceso son predecibles y permiten desnormalización.
En proyectos he implementado arquitecturas polyglot usando PostgreSQL para datos transaccionales críticos, MongoDB para catálogos de productos con atributos variables, y Redis para caché y sesiones.
La elección entre relacional y NoSQL no es binaria, muchas aplicaciones modernas usan ambas aprovechando las fortalezas de cada modelo según el caso de uso específico.

## Integración Angular con Bases de Datos

### Backend APIs
Las aplicaciones Angular no se conectan directamente a bases de datos sino a través de APIs REST o GraphQL que el backend expone y maneja las operaciones de base de datos.
Implemento servicios Angular que consumen endpoints HTTP del backend, enviando datos con POST/PUT y recibiendo respuestas que transformo a modelos TypeScript.
Uso HttpHeaders para enviar tokens de autenticación en cada petición que requiere acceso a datos protegidos en la base de datos.
Manejo estados de carga mostrando spinners mientras se obtienen datos del backend, y estados de error mostrando mensajes cuando las operaciones de base de datos fallan.

### Caché y Optimización
Implemento caché en servicios Angular usando BehaviorSubject para almacenar datos ya obtenidos y evitar peticiones repetidas al backend para la misma información.
Uso estrategias de polling con interval de RxJS para actualizar datos periódicamente cuando necesito mostrar información casi en tiempo real de la base de datos.
WebSockets los implemento cuando necesito actualizaciones en tiempo real verdadero, como notificaciones o dashboards que reflejan cambios de base de datos instantáneamente.

### Manejo de Estado
Para aplicaciones grandes con múltiples componentes compartiendo datos de base de datos, he implementado NgRx como store centralizado que sincroniza el estado del frontend con el backend.
El patrón de effects en NgRx me permite gestionar llamadas asíncronas al backend, disparando acciones cuando los datos se obtienen exitosamente o cuando ocurren errores de base de datos.

