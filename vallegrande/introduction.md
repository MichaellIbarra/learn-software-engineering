# Temarío para estudiar Examen de Vallegrande


---


---

## FUNDAMENTOS DE PROGRAMACION

**Introducción:** Principios, paradigmas y tecnologías fundamentales para construir aplicaciones de software modernas, desde la programación orientada a objetos hasta frameworks web.

**Por qué se utiliza:** Establecer bases sólidas para desarrollo escalable, reutilizable y mantenible. Permite crear aplicaciones robustas con arquitecturas bien definidas.

**Ventajas:**
- Código reutilizable y organizado
- Facilita mantenimiento y escalabilidad
- Separación de responsabilidades
- Estándares de la industria
- Ecosistema de herramientas maduro

**Desventajas:**
- Curva de aprendizaje inicial
- Puede generar sobre-ingeniería
- Requiere conocimiento de múltiples tecnologías
- Abstracción puede complicar debugging
- Dependencia de frameworks y librerías

### Conceptos básicos y pilares POO

**Qué trata:** Programación Orientada a Objetos - paradigma que organiza el código en objetos que contienen datos (atributos) y comportamiento (métodos).

**Por qué se utiliza:** Modelar el mundo real en código, facilitar reutilización, mejorar mantenibilidad y organización del software.

**Los 4 Pilares de POO:**

**1. Encapsulamiento:**
- **Qué trata:** Ocultar detalles internos y exponer solo lo necesario
- **Ejemplo:**
```java
public class CuentaBancaria {
    private double saldo; // Privado, no accesible directamente
    
    public double getSaldo() { // Método público para acceder
        return saldo;
    }
    
    public void depositar(double monto) {
        if (monto > 0) {
            saldo += monto;
        }
    }
}
```
- **Beneficio:** Protege datos, controla acceso, reduce acoplamiento

**2. Abstracción:**
- **Qué trata:** Ocultar complejidad mostrando solo características esenciales
- **Ejemplo:**
```java
public abstract class Vehiculo {
    abstract void acelerar(); // Define qué hacer, no cómo
}

public class Auto extends Vehiculo {
    void acelerar() { // Implementación específica
        System.out.println("El auto acelera con gasolina");
    }
}
```
- **Beneficio:** Simplifica código, enfoca en lo importante, permite flexibilidad

**3. Herencia:**
- **Qué trata:** Crear clases nuevas basadas en clases existentes, heredando atributos y métodos
- **Ejemplo:**
```java
public class Empleado {
    protected String nombre;
    protected double salario;
    
    public void trabajar() {
        System.out.println(nombre + " está trabajando");
    }
}

public class Desarrollador extends Empleado {
    private String lenguaje;
    
    public void programar() {
        System.out.println(nombre + " programa en " + lenguaje);
    }
}
```
- **Beneficio:** Reutilización de código, jerarquías lógicas, DRY principle

**4. Polimorfismo:**
- **Qué trata:** Capacidad de objetos de diferentes clases de responder al mismo mensaje de forma diferente
- **Ejemplo:**
```java
public interface Forma {
    double calcularArea();
}

public class Circulo implements Forma {
    private double radio;
    public double calcularArea() {
        return Math.PI * radio * radio;
    }
}

public class Rectangulo implements Forma {
    private double base, altura;
    public double calcularArea() {
        return base * altura;
    }
}

// Uso polimórfico
List<Forma> formas = Arrays.asList(new Circulo(), new Rectangulo());
formas.forEach(f -> System.out.println(f.calcularArea()));
```
- **Beneficio:** Flexibilidad, extensibilidad, código más genérico

**Conceptos adicionales:**

**Clases y Objetos:**
```java
// Clase: Plantilla/molde
public class Persona {
    String nombre;
    int edad;
    
    void saludar() {
        System.out.println("Hola, soy " + nombre);
    }
}

// Objetos: Instancias de la clase
Persona juan = new Persona();
juan.nombre = "Juan";
juan.edad = 25;
juan.saludar();
```

**Constructores:**
```java
public class Producto {
    private String nombre;
    private double precio;
    
    // Constructor
    public Producto(String nombre, double precio) {
        this.nombre = nombre;
        this.precio = precio;
    }
}

Producto laptop = new Producto("Dell XPS", 1200.00);
```

**Interfaces:**
```java
public interface Pagable {
    void procesarPago(double monto);
}

public class TarjetaCredito implements Pagable {
    public void procesarPago(double monto) {
        System.out.println("Procesando $" + monto + " con tarjeta");
    }
}
```

**Ejemplo de uso completo:** Sistema de gestión de empleados con clase base `Empleado` y subclases `Desarrollador`, `Gerente`, `Diseñador`. Cada uno hereda atributos comunes (nombre, salario) pero implementa su propio método `calcularBono()` según su rol.

### Patrón MVC y DAO, Frameworks JSF, Primefaces y Persistencia de datos

**Qué trata:** Patrones arquitectónicos y frameworks para separar lógica de negocio, presentación y acceso a datos en aplicaciones Java EE.

**Patrón MVC (Model-View-Controller):**

**Qué trata:** Separar aplicación en tres componentes principales para mejorar organización y mantenibilidad.

**Componentes:**

**Model (Modelo):**
- **Qué trata:** Datos y lógica de negocio
- **Ejemplo:**
```java
public class Usuario {
    private int id;
    private String nombre;
    private String email;
    
    // Getters, setters, lógica de negocio
}
```

**View (Vista):**
- **Qué trata:** Interfaz de usuario, presentación
- **Ejemplo:** Archivos JSF/XHTML
```xhtml
<h:form>
    <h:inputText value="#{usuarioBean.nombre}" />
    <h:commandButton value="Guardar" action="#{usuarioBean.guardar}" />
</h:form>
```

**Controller (Controlador):**
- **Qué trata:** Maneja interacción usuario, actualiza modelo y vista
- **Ejemplo:**
```java
@ManagedBean
public class UsuarioBean {
    private Usuario usuario = new Usuario();
    private UsuarioDAO dao = new UsuarioDAO();
    
    public String guardar() {
        dao.guardar(usuario);
        return "exito";
    }
}
```

**Flujo MVC:**
1. Usuario interactúa con Vista (click botón)
2. Vista notifica al Controlador
3. Controlador actualiza Modelo
4. Modelo notifica cambios
5. Vista se actualiza con nuevos datos

**Patrón DAO (Data Access Object):**

**Qué trata:** Abstrae y encapsula acceso a fuente de datos, separando lógica de negocio de lógica de persistencia.

**Estructura:**
```java
// Interface DAO
public interface UsuarioDAO {
    void guardar(Usuario usuario);
    Usuario buscarPorId(int id);
    List<Usuario> listarTodos();
    void actualizar(Usuario usuario);
    void eliminar(int id);
}

// Implementación
public class UsuarioDAOImpl implements UsuarioDAO {
    private Connection conexion;
    
    public void guardar(Usuario usuario) {
        String sql = "INSERT INTO usuarios (nombre, email) VALUES (?, ?)";
        try (PreparedStatement stmt = conexion.prepareStatement(sql)) {
            stmt.setString(1, usuario.getNombre());
            stmt.setString(2, usuario.getEmail());
            stmt.executeUpdate();
        } catch (SQLException e) {
            throw new RuntimeException("Error al guardar", e);
        }
    }
    
    public Usuario buscarPorId(int id) {
        // Implementación de búsqueda
    }
}
```

**Ventajas DAO:**
- Separación de responsabilidades
- Fácil cambiar tecnología de persistencia
- Código más testeable
- Reutilización de lógica de acceso a datos

**JSF (JavaServer Faces):**

**Qué trata:** Framework Java para construir interfaces de usuario web basadas en componentes.

**Características:**
- Componentes reutilizables
- Binding bidireccional
- Validación automática
- Navegación declarativa
- Manejo de eventos

**Ejemplo:**
```xhtml
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:h="http://xmlns.jcp.org/jsf/html">
<h:head>
    <title>Registro Usuario</title>
</h:head>
<h:body>
    <h:form>
        <h:panelGrid columns="2">
            <h:outputLabel value="Nombre:" />
            <h:inputText value="#{usuarioBean.usuario.nombre}" required="true" />
            
            <h:outputLabel value="Email:" />
            <h:inputText value="#{usuarioBean.usuario.email}" 
                         validatorMessage="Email inválido">
                <f:validateRegex pattern=".+@.+\..+" />
            </h:inputText>
            
            <h:commandButton value="Registrar" action="#{usuarioBean.registrar}" />
        </h:panelGrid>
        <h:messages />
    </h:form>
</h:body>
</html>
```

**PrimeFaces:**

**Qué trata:** Librería de componentes UI rica para JSF con Ajax, temas y componentes avanzados.

**Componentes populares:**
```xhtml
<!-- DataTable con filtros y paginación -->
<p:dataTable value="#{usuarioBean.usuarios}" var="user" 
             paginator="true" rows="10" filterable="true">
    <p:column headerText="Nombre" sortBy="#{user.nombre}">
        <h:outputText value="#{user.nombre}" />
    </p:column>
    <p:column headerText="Email">
        <h:outputText value="#{user.email}" />
    </p:column>
    <p:column headerText="Acciones">
        <p:commandButton icon="pi pi-pencil" 
                         action="#{usuarioBean.editar(user)}" />
    </p:column>
</p:dataTable>

<!-- Dialog modal -->
<p:dialog header="Editar Usuario" widgetVar="dlgEditar">
    <h:form>
        <p:inputText value="#{usuarioBean.usuarioSeleccionado.nombre}" />
        <p:commandButton value="Guardar" 
                         action="#{usuarioBean.actualizar}" 
                         update="@form" />
    </h:form>
</p:dialog>
```

**Persistencia de datos con JPA:**

**Qué trata:** Java Persistence API - estándar para mapeo objeto-relacional (ORM).

**Entidades JPA:**
```java
@Entity
@Table(name = "usuarios")
public class Usuario {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false, length = 100)
    private String nombre;
    
    @Column(unique = true)
    private String email;
    
    @OneToMany(mappedBy = "usuario", cascade = CascadeType.ALL)
    private List<Pedido> pedidos;
    
    // Getters y setters
}
```

**EntityManager:**
```java
@Stateless
public class UsuarioService {
    @PersistenceContext
    private EntityManager em;
    
    public void guardar(Usuario usuario) {
        em.persist(usuario);
    }
    
    public Usuario buscar(Long id) {
        return em.find(Usuario.class, id);
    }
    
    public List<Usuario> listarTodos() {
        return em.createQuery("SELECT u FROM Usuario u", Usuario.class)
                 .getResultList();
    }
}
```

**persistence.xml:**
```xml
<persistence xmlns="http://xmlns.jcp.org/xml/ns/persistence" version="2.2">
    <persistence-unit name="miApp">
        <provider>org.hibernate.jpa.HibernatePersistenceProvider</provider>
        <properties>
            <property name="javax.persistence.jdbc.url" 
                      value="jdbc:mysql://localhost/midb"/>
            <property name="hibernate.hbm2ddl.auto" value="update"/>
            <property name="hibernate.show_sql" value="true"/>
        </properties>
    </persistence-unit>
</persistence>
```

**Ciclo de vida completo (MVC + DAO + JSF + JPA):**
1. Usuario envía formulario JSF (Vista)
2. ManagedBean procesa (Controlador)
3. Bean llama a Service/DAO
4. DAO usa EntityManager (JPA)
5. JPA persiste en base de datos
6. Respuesta regresa a Bean
7. Bean actualiza Vista
8. PrimeFaces renderiza componentes

**Ejemplo de uso:** Sistema de gestión de biblioteca web donde JSF con PrimeFaces muestra catálogo, usuarios buscan/reservan libros, ManagedBeans controlan flujo, DAO/JPA persisten reservas en MySQL.

### API, tipos de APIs y Servicio Rest

**Qué trata:** Interfaces de programación que permiten comunicación entre diferentes sistemas de software.

**API (Application Programming Interface):**

**Introducción:** Conjunto de definiciones y protocolos para construir e integrar software de aplicación. Contrato entre proveedor y consumidor.

**Por qué se utiliza:** Integrar sistemas, reutilizar funcionalidad, exponer servicios, separar frontend de backend, permitir terceros.

**Tipos de APIs:**

**1. APIs Web:**
- **REST (Representational State Transfer)**
- **SOAP (Simple Object Access Protocol)**
- **GraphQL**
- **WebSockets**

**2. APIs de Sistema:**
- **APIs de SO (Windows API, POSIX)**
- **APIs de hardware**

**3. APIs de Librerías:**
- **Java API, Python stdlib**
- **jQuery, Lodash**

**4. APIs de Base de Datos:**
- **JDBC, ODBC**
- **MongoDB Driver**

**Servicio REST:**

**Qué trata:** Arquitectura para servicios web que usa HTTP y principios RESTful para operaciones CRUD.

**Principios REST:**

**1. Recursos identificados por URI:**
```
GET /api/usuarios          - Listar usuarios
GET /api/usuarios/123      - Obtener usuario 123
POST /api/usuarios         - Crear usuario
PUT /api/usuarios/123      - Actualizar usuario 123
DELETE /api/usuarios/123   - Eliminar usuario 123
```

**2. Métodos HTTP estándar:**
- **GET:** Leer recursos (idempotente, seguro)
- **POST:** Crear recursos
- **PUT:** Actualizar completo (idempotente)
- **PATCH:** Actualización parcial
- **DELETE:** Eliminar recursos (idempotente)

**3. Representación de recursos (JSON/XML):**
```json
{
  "id": 123,
  "nombre": "Juan Pérez",
  "email": "juan@email.com",
  "activo": true
}
```

**4. Sin estado (Stateless):**
- Cada petición contiene toda la información necesaria
- No se mantiene sesión en servidor
- Escalabilidad mejorada

**5. HATEOAS (opcional):**
```json
{
  "id": 123,
  "nombre": "Juan",
  "links": [
    {"rel": "self", "href": "/api/usuarios/123"},
    {"rel": "pedidos", "href": "/api/usuarios/123/pedidos"}
  ]
}
```

**Implementación REST en Java (Spring Boot):**

**Controlador REST:**
```java
@RestController
@RequestMapping("/api/usuarios")
public class UsuarioController {
    
    @Autowired
    private UsuarioService service;
    
    // GET /api/usuarios
    @GetMapping
    public List<Usuario> listarTodos() {
        return service.listarTodos();
    }
    
    // GET /api/usuarios/123
    @GetMapping("/{id}")
    public ResponseEntity<Usuario> obtenerPorId(@PathVariable Long id) {
        Usuario usuario = service.buscarPorId(id);
        if (usuario == null) {
            return ResponseEntity.notFound().build();
        }
        return ResponseEntity.ok(usuario);
    }
    
    // POST /api/usuarios
    @PostMapping
    public ResponseEntity<Usuario> crear(@RequestBody Usuario usuario) {
        Usuario nuevo = service.guardar(usuario);
        return ResponseEntity.status(HttpStatus.CREATED).body(nuevo);
    }
    
    // PUT /api/usuarios/123
    @PutMapping("/{id}")
    public ResponseEntity<Usuario> actualizar(
            @PathVariable Long id, 
            @RequestBody Usuario usuario) {
        Usuario actualizado = service.actualizar(id, usuario);
        return ResponseEntity.ok(actualizado);
    }
    
    // DELETE /api/usuarios/123
    @DeleteMapping("/{id}")
    public ResponseEntity<Void> eliminar(@PathVariable Long id) {
        service.eliminar(id);
        return ResponseEntity.noContent().build();
    }
}
```

**Códigos de estado HTTP:**
- **200 OK:** Éxito general
- **201 Created:** Recurso creado
- **204 No Content:** Éxito sin contenido (DELETE)
- **400 Bad Request:** Error en petición
- **401 Unauthorized:** No autenticado
- **403 Forbidden:** Sin permisos
- **404 Not Found:** Recurso no existe
- **500 Internal Server Error:** Error servidor

**Manejo de errores:**
```java
@ExceptionHandler(UsuarioNotFoundException.class)
public ResponseEntity<ErrorResponse> manejarUsuarioNoEncontrado(
        UsuarioNotFoundException ex) {
    ErrorResponse error = new ErrorResponse(
        "USUARIO_NO_ENCONTRADO",
        ex.getMessage(),
        LocalDateTime.now()
    );
    return ResponseEntity.status(HttpStatus.NOT_FOUND).body(error);
}
```

**Autenticación REST:**

**JWT (JSON Web Token):**
```java
@PostMapping("/login")
public ResponseEntity<TokenResponse> login(@RequestBody LoginRequest request) {
    // Validar credenciales
    Authentication auth = authenticationManager.authenticate(
        new UsernamePasswordAuthenticationToken(
            request.getUsername(), 
            request.getPassword()
        )
    );
    
    // Generar token
    String token = jwtTokenProvider.createToken(auth.getName());
    return ResponseEntity.ok(new TokenResponse(token));
}

// Uso del token
// Header: Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

**CORS (Cross-Origin Resource Sharing):**
```java
@Configuration
public class CorsConfig {
    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/api/**")
                        .allowedOrigins("http://localhost:4200")
                        .allowedMethods("GET", "POST", "PUT", "DELETE")
                        .allowedHeaders("*")
                        .allowCredentials(true);
            }
        };
    }
}
```

**Paginación y filtrado:**
```java
@GetMapping
public Page<Usuario> listar(
        @RequestParam(defaultValue = "0") int page,
        @RequestParam(defaultValue = "10") int size,
        @RequestParam(required = false) String nombre) {
    
    Pageable pageable = PageRequest.of(page, size, Sort.by("nombre"));
    
    if (nombre != null) {
        return service.buscarPorNombre(nombre, pageable);
    }
    return service.listarTodos(pageable);
}

// GET /api/usuarios?page=0&size=10&nombre=Juan
```

**Consumir API REST (Cliente):**

**JavaScript (Fetch):**
```javascript
// GET
fetch('http://localhost:8080/api/usuarios')
    .then(response => response.json())
    .then(data => console.log(data));

// POST
fetch('http://localhost:8080/api/usuarios', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer ' + token
    },
    body: JSON.stringify({
        nombre: 'Juan',
        email: 'juan@email.com'
    })
})
.then(response => response.json())
.then(data => console.log(data));
```

**Java (RestTemplate):**
```java
RestTemplate restTemplate = new RestTemplate();

// GET
Usuario usuario = restTemplate.getForObject(
    "http://localhost:8080/api/usuarios/123", 
    Usuario.class
);

// POST
Usuario nuevo = new Usuario("Juan", "juan@email.com");
Usuario creado = restTemplate.postForObject(
    "http://localhost:8080/api/usuarios",
    nuevo,
    Usuario.class
);
```

**Versionamiento de API:**
```java
// Por URI
@GetMapping("/api/v1/usuarios")
@GetMapping("/api/v2/usuarios")

// Por header
@GetMapping(value = "/api/usuarios", headers = "API-Version=1")

// Por parámetro
@GetMapping(value = "/api/usuarios", params = "version=1")
```

**Ejemplo de uso completo:** Aplicación móvil de e-commerce consume API REST del backend. Frontend hace GET para mostrar productos, POST para agregar al carrito, autenticación con JWT, backend Spring Boot expone endpoints RESTful que interactúan con base de datos.

### Fundamentos del DOM, NodeJS y TypeScript

**DOM (Document Object Model):**

**Qué trata:** Representación en árbol de documento HTML/XML que permite manipular estructura, estilo y contenido mediante JavaScript.

**Estructura del DOM:**
```html
<!DOCTYPE html>
<html>
    <head>
        <title>Mi Página</title>
    </head>
    <body>
        <div id="contenedor">
            <h1 class="titulo">Hola Mundo</h1>
            <p>Contenido</p>
        </div>
    </body>
</html>
```

**Árbol DOM:**
```
Document
  └─ html
      ├─ head
      │   └─ title
      │       └─ "Mi Página"
      └─ body
          └─ div#contenedor
              ├─ h1.titulo
              │   └─ "Hola Mundo"
              └─ p
                  └─ "Contenido"
```

**Manipulación del DOM:**

**Selección de elementos:**
```javascript
// Por ID
const contenedor = document.getElementById('contenedor');

// Por clase
const titulos = document.getElementsByClassName('titulo');

// Por selector CSS
const titulo = document.querySelector('.titulo');
const todosP = document.querySelectorAll('p');

// Por tag
const divs = document.getElementsByTagName('div');
```

**Modificación de contenido:**
```javascript
// Cambiar texto
titulo.textContent = 'Nuevo Título';
titulo.innerHTML = '<strong>Título en Negrita</strong>';

// Cambiar atributos
const img = document.querySelector('img');
img.src = 'nueva-imagen.jpg';
img.setAttribute('alt', 'Descripción');

// Cambiar estilos
titulo.style.color = 'blue';
titulo.style.fontSize = '24px';
titulo.classList.add('destacado');
titulo.classList.remove('viejo');
titulo.classList.toggle('activo');
```

**Creación y eliminación:**
```javascript
// Crear elemento
const nuevoDiv = document.createElement('div');
nuevoDiv.textContent = 'Nuevo contenido';
nuevoDiv.className = 'nuevo';

// Agregar al DOM
contenedor.appendChild(nuevoDiv);
contenedor.insertBefore(nuevoDiv, contenedor.firstChild);

// Eliminar
contenedor.removeChild(nuevoDiv);
nuevoDiv.remove(); // Más moderno
```

**Eventos:**
```javascript
// Click
const boton = document.getElementById('miBoton');
boton.addEventListener('click', function(event) {
    console.log('Botón clickeado');
    event.preventDefault(); // Prevenir acción por defecto
});

// Input
const input = document.querySelector('input');
input.addEventListener('input', (e) => {
    console.log('Valor actual:', e.target.value);
});

// Submit form
const form = document.querySelector('form');
form.addEventListener('submit', (e) => {
    e.preventDefault();
    const formData = new FormData(form);
    console.log(Object.fromEntries(formData));
});

// Delegación de eventos
document.body.addEventListener('click', (e) => {
    if (e.target.matches('.boton-eliminar')) {
        e.target.parentElement.remove();
    }
});
```

**Ejemplo práctico DOM:**
```javascript
// Lista de tareas dinámica
const lista = document.getElementById('lista-tareas');
const input = document.getElementById('nueva-tarea');
const btnAgregar = document.getElementById('btn-agregar');

btnAgregar.addEventListener('click', () => {
    const texto = input.value.trim();
    if (texto) {
        const li = document.createElement('li');
        li.innerHTML = `
            <span>${texto}</span>
            <button class="eliminar">X</button>
        `;
        lista.appendChild(li);
        input.value = '';
    }
});

lista.addEventListener('click', (e) => {
    if (e.target.classList.contains('eliminar')) {
        e.target.parentElement.remove();
    }
});
```

**Node.js:**

**Qué trata:** Entorno de ejecución JavaScript del lado del servidor basado en motor V8 de Chrome.

**Por qué se utiliza:** Construir aplicaciones backend escalables, APIs, herramientas CLI, aplicaciones en tiempo real.

**Características:**
- **Asíncrono y basado en eventos**
- **Single-threaded con event loop**
- **NPM (Node Package Manager)** - gestor de paquetes
- **Non-blocking I/O**
- **Gran ecosistema de módulos**

**Módulos en Node.js:**

**Módulos nativos:**
```javascript
// File System
const fs = require('fs');

// Lectura síncrona
const contenido = fs.readFileSync('archivo.txt', 'utf8');
console.log(contenido);

// Lectura asíncrona
fs.readFile('archivo.txt', 'utf8', (err, data) => {
    if (err) throw err;
    console.log(data);
});

// Escritura
fs.writeFile('nuevo.txt', 'Contenido', (err) => {
    if (err) throw err;
    console.log('Archivo creado');
});

// HTTP
const http = require('http');

const servidor = http.createServer((req, res) => {
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end('Hola desde Node.js');
});

servidor.listen(3000, () => {
    console.log('Servidor en http://localhost:3000');
});

// Path
const path = require('path');
const rutaCompleta = path.join(__dirname, 'archivos', 'datos.json');
const extension = path.extname('archivo.txt'); // .txt
```

**Módulos personalizados:**
```javascript
// matematicas.js
function sumar(a, b) {
    return a + b;
}

function restar(a, b) {
    return a - b;
}

module.exports = { sumar, restar };

// app.js
const { sumar, restar } = require('./matematicas');
console.log(sumar(5, 3)); // 8
```

**NPM - Gestor de paquetes:**
```bash
# Inicializar proyecto
npm init -y

# Instalar paquetes
npm install express
npm install --save-dev nodemon

# package.json
{
  "name": "mi-app",
  "version": "1.0.0",
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js"
  },
  "dependencies": {
    "express": "^4.18.0"
  }
}
```

**Express.js - Framework web:**
```javascript
const express = require('express');
const app = express();

// Middleware
app.use(express.json());

// Rutas
app.get('/', (req, res) => {
    res.send('Hola desde Express');
});

app.get('/api/usuarios', (req, res) => {
    res.json([
        { id: 1, nombre: 'Juan' },
        { id: 2, nombre: 'María' }
    ]);
});

app.post('/api/usuarios', (req, res) => {
    const usuario = req.body;
    // Guardar en BD
    res.status(201).json(usuario);
});

app.listen(3000, () => {
    console.log('Servidor Express en puerto 3000');
});
```

**Promesas y Async/Await:**
```javascript
// Promesas
function leerArchivo(ruta) {
    return new Promise((resolve, reject) => {
        fs.readFile(ruta, 'utf8', (err, data) => {
            if (err) reject(err);
            else resolve(data);
        });
    });
}

leerArchivo('datos.txt')
    .then(data => console.log(data))
    .catch(err => console.error(err));

// Async/Await
async function procesarDatos() {
    try {
        const data = await leerArchivo('datos.txt');
        console.log(data);
    } catch (err) {
        console.error(err);
    }
}
```

**TypeScript:**

**Qué trata:** Superset de JavaScript que añade tipado estático opcional y características avanzadas.

**Por qué se utiliza:** Detectar errores en tiempo de compilación, mejor autocompletado IDE, código más mantenible, refactoring seguro.

**Tipos básicos:**
```typescript
// Primitivos
let nombre: string = 'Juan';
let edad: number = 25;
let activo: boolean = true;
let nulo: null = null;
let indefinido: undefined = undefined;

// Arrays
let numeros: number[] = [1, 2, 3];
let nombres: Array<string> = ['Ana', 'Luis'];

// Tuplas
let persona: [string, number] = ['Juan', 25];

// Enum
enum Color {
    Rojo,
    Verde,
    Azul
}
let colorFavorito: Color = Color.Rojo;

// Any (evitar cuando sea posible)
let variable: any = 'puede ser cualquier cosa';

// Union types
let id: number | string = 123;
id = 'ABC123'; // Válido

// Literal types
let direccion: 'norte' | 'sur' | 'este' | 'oeste' = 'norte';
```

**Interfaces y Types:**
```typescript
// Interface
interface Usuario {
    id: number;
    nombre: string;
    email: string;
    edad?: number; // Opcional
    readonly fechaCreacion: Date; // Solo lectura
}

const usuario: Usuario = {
    id: 1,
    nombre: 'Juan',
    email: 'juan@email.com',
    fechaCreacion: new Date()
};

// Type alias
type Punto = {
    x: number;
    y: number;
};

type ID = number | string;

// Extending interfaces
interface Empleado extends Usuario {
    salario: number;
    cargo: string;
}
```

**Funciones:**
```typescript
// Tipado de funciones
function sumar(a: number, b: number): number {
    return a + b;
}

// Función arrow
const multiplicar = (a: number, b: number): number => a * b;

// Parámetros opcionales
function saludar(nombre: string, apellido?: string): string {
    return apellido ? `Hola ${nombre} ${apellido}` : `Hola ${nombre}`;
}

// Parámetros por defecto
function crearUsuario(nombre: string, rol: string = 'usuario'): Usuario {
    return { id: 1, nombre, email: '', fechaCreacion: new Date() };
}

// Rest parameters
function sumarTodos(...numeros: number[]): number {
    return numeros.reduce((acc, n) => acc + n, 0);
}
```

**Clases:**
```typescript
class Persona {
    // Propiedades
    private id: number;
    public nombre: string;
    protected edad: number;
    
    // Constructor
    constructor(id: number, nombre: string, edad: number) {
        this.id = id;
        this.nombre = nombre;
        this.edad = edad;
    }
    
    // Métodos
    public saludar(): string {
        return `Hola, soy ${this.nombre}`;
    }
    
    // Getter
    get obtenerEdad(): number {
        return this.edad;
    }
    
    // Setter
    set establecerEdad(edad: number) {
        if (edad > 0) {
            this.edad = edad;
        }
    }
}

class Empleado extends Persona {
    constructor(
        id: number, 
        nombre: string, 
        edad: number, 
        public salario: number
    ) {
        super(id, nombre, edad);
    }
    
    public calcularBono(): number {
        return this.salario * 0.1;
    }
}
```

**Generics:**
```typescript
// Función genérica
function identidad<T>(valor: T): T {
    return valor;
}

let num = identidad<number>(123);
let str = identidad<string>('hola');

// Clase genérica
class Caja<T> {
    private contenido: T;
    
    constructor(contenido: T) {
        this.contenido = contenido;
    }
    
    obtener(): T {
        return this.contenido;
    }
}

let cajaNumero = new Caja<number>(123);
let cajaString = new Caja<string>('texto');

// Interface genérica
interface Respuesta<T> {
    datos: T;
    mensaje: string;
    codigo: number;
}

const respuesta: Respuesta<Usuario[]> = {
    datos: [{ id: 1, nombre: 'Juan', email: 'juan@email.com', fechaCreacion: new Date() }],
    mensaje: 'Éxito',
    codigo: 200
};
```

**Compilación TypeScript:**
```bash
# Instalar TypeScript
npm install -g typescript

# Inicializar configuración
tsc --init

# Compilar archivo
tsc archivo.ts

# Watch mode
tsc --watch
```

**tsconfig.json:**
```json
{
  "compilerOptions": {
    "target": "ES6",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true,
    "outDir": "./dist",
    "rootDir": "./src",
    "sourceMap": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```

**Ejemplo de uso completo:** API REST con Node.js + Express + TypeScript que maneja usuarios. TypeScript provee tipado para modelos, controladores y servicios. Express maneja rutas HTTP. Frontend vanilla JS manipula DOM para mostrar/crear usuarios consumiendo la API.

### Fundamentos de aplicaciones web SPA con Angular

**Qué trata:** Framework TypeScript para construir Single Page Applications (SPA) - aplicaciones web dinámicas que cargan una sola página HTML y actualizan contenido dinámicamente.

**Por qué se utiliza Angular:**
- Estructura clara y opinionada
- TypeScript nativo
- Two-way data binding
- Dependency injection
- Herramientas completas (router, HTTP, forms)
- Respaldado por Google

**Ventajas:**
- Aplicación completa (full-featured)
- Rendimiento optimizado
- Testeable y mantenible
- CLI poderosa
- Gran comunidad

**Desventajas:**
- Curva de aprendizaje pronunciada
- Verboso comparado con alternativas
- Tamaño del bundle inicial
- Requiere TypeScript
- Actualizaciones frecuentes pueden romper compatibilidad

**Conceptos fundamentales:**

**1. Componentes:**

**Qué trata:** Bloques de construcción básicos de una aplicación Angular. Encapsulan template, estilos y lógica.

**Estructura:**
```typescript
// usuario.component.ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-usuario',
  templateUrl: './usuario.component.html',
  styleUrls: ['./usuario.component.css']
})
export class UsuarioComponent implements OnInit {
  // Propiedades
  nombre: string = 'Juan';
  edad: number = 25;
  usuarios: string[] = ['Ana', 'Luis', 'María'];
  
  // Constructor
  constructor() { }
  
  // Lifecycle hook
  ngOnInit(): void {
    console.log('Componente inicializado');
  }
  
  // Métodos
  saludar(): void {
    alert(`Hola ${this.nombre}`);
  }
  
  agregarUsuario(nombre: string): void {
    this.usuarios.push(nombre);
  }
}
```

**Template:**
```html
<!-- usuario.component.html -->
<div class="usuario-container">
    <h2>{{ nombre }}</h2>
    <p>Edad: {{ edad }}</p>
    
    <!-- Event binding -->
    <button (click)="saludar()">Saludar</button>
    
    <!-- Property binding -->
    <input [value]="nombre" />
    
    <!-- Two-way binding -->
    <input [(ngModel)]="nombre" />
    
    <!-- Lista -->
    <ul>
        <li *ngFor="let usuario of usuarios">
            {{ usuario }}
        </li>
    </ul>
    
    <!-- Condicional -->
    <div *ngIf="edad >= 18">
        <p>Mayor de edad</p>
    </div>
    
    <div *ngIf="edad < 18; else menorTemplate">
        <p>Menor de edad</p>
    </div>
    <ng-template #menorTemplate>
        <p>Adulto</p>
    </ng-template>
</div>
```

**2. Módulos:**

**Qué trata:** Contenedores que agrupan componentes, servicios, directivas relacionados.

```typescript
// app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';
import { HttpClientModule } from '@angular/common/http';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { UsuarioComponent } from './usuario/usuario.component';
import { UsuarioService } from './services/usuario.service';

@NgModule({
  declarations: [
    AppComponent,
    UsuarioComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpClientModule,
    AppRoutingModule
  ],
  providers: [UsuarioService],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

**3. Servicios e Inyección de Dependencias:**

**Qué trata:** Clases que encapsulan lógica de negocio, llamadas HTTP, estado compartido. Se inyectan en componentes.

```typescript
// usuario.service.ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

interface Usuario {
  id: number;
  nombre: string;
  email: string;
}

@Injectable({
  providedIn: 'root'
})
export class UsuarioService {
  private apiUrl = 'http://localhost:3000/api/usuarios';
  
  constructor(private http: HttpClient) { }
  
  obtenerTodos(): Observable<Usuario[]> {
    return this.http.get<Usuario[]>(this.apiUrl);
  }
  
  obtenerPorId(id: number): Observable<Usuario> {
    return this.http.get<Usuario>(`${this.apiUrl}/${id}`);
  }
  
  crear(usuario: Usuario): Observable<Usuario> {
    return this.http.post<Usuario>(this.apiUrl, usuario);
  }
  
  actualizar(id: number, usuario: Usuario): Observable<Usuario> {
    return this.http.put<Usuario>(`${this.apiUrl}/${id}`, usuario);
  }
  
  eliminar(id: number): Observable<void> {
    return this.http.delete<void>(`${this.apiUrl}/${id}`);
  }
}
```

**Uso en componente:**
```typescript
export class ListaUsuariosComponent implements OnInit {
  usuarios: Usuario[] = [];
  
  constructor(private usuarioService: UsuarioService) { }
  
  ngOnInit(): void {
    this.cargarUsuarios();
  }
  
  cargarUsuarios(): void {
    this.usuarioService.obtenerTodos()
      .subscribe(
        data => this.usuarios = data,
        error => console.error('Error:', error)
      );
  }
  
  eliminarUsuario(id: number): void {
    this.usuarioService.eliminar(id)
      .subscribe(() => {
        this.usuarios = this.usuarios.filter(u => u.id !== id);
      });
  }
}
```

**4. Routing (Enrutamiento):**

**Qué trata:** Navegación entre vistas/componentes sin recargar página.

```typescript
// app-routing.module.ts
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { ListaUsuariosComponent } from './lista-usuarios/lista-usuarios.component';
import { DetalleUsuarioComponent } from './detalle-usuario/detalle-usuario.component';
import { LoginComponent } from './login/login.component';
import { AuthGuard } from './guards/auth.guard';

const routes: Routes = [
  { path: '', redirectTo: '/home', pathMatch: 'full' },
  { path: 'home', component: HomeComponent },
  { path: 'login', component: LoginComponent },
  { 
    path: 'usuarios', 
    component: ListaUsuariosComponent,
    canActivate: [AuthGuard]
  },
  { 
    path: 'usuarios/:id', 
    component: DetalleUsuarioComponent 
  },
  { path: '**', redirectTo: '/home' }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

**Template con router:**
```html
<!-- app.component.html -->
<nav>
  <a routerLink="/home" routerLinkActive="active">Home</a>
  <a routerLink="/usuarios" routerLinkActive="active">Usuarios</a>
</nav>

<router-outlet></router-outlet>
```

**Navegación programática:**
```typescript
export class LoginComponent {
  constructor(private router: Router) { }
  
  login(): void {
    // Lógica de autenticación
    this.router.navigate(['/usuarios']);
  }
  
  verDetalle(id: number): void {
    this.router.navigate(['/usuarios', id]);
  }
}
```

**Parámetros de ruta:**
```typescript
export class DetalleUsuarioComponent implements OnInit {
  usuario: Usuario;
  
  constructor(
    private route: ActivatedRoute,
    private usuarioService: UsuarioService
  ) { }
  
  ngOnInit(): void {
    const id = Number(this.route.snapshot.paramMap.get('id'));
    this.usuarioService.obtenerPorId(id)
      .subscribe(data => this.usuario = data);
  }
}
```

**5. Formularios:**

**Template-driven forms:**
```html
<form #formulario="ngForm" (ngSubmit)="guardar(formulario)">
  <input 
    type="text" 
    name="nombre" 
    [(ngModel)]="usuario.nombre" 
    required 
    minlength="3"
    #nombre="ngModel"
  />
  <div *ngIf="nombre.invalid && nombre.touched">
    <span *ngIf="nombre.errors?.['required']">Nombre requerido</span>
    <span *ngIf="nombre.errors?.['minlength']">Mínimo 3 caracteres</span>
  </div>
  
  <button [disabled]="formulario.invalid">Guardar</button>
</form>
```

**Reactive forms:**
```typescript
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

export class FormularioUsuarioComponent implements OnInit {
  formulario: FormGroup;
  
  constructor(private fb: FormBuilder) { }
  
  ngOnInit(): void {
    this.formulario = this.fb.group({
      nombre: ['', [Validators.required, Validators.minLength(3)]],
      email: ['', [Validators.required, Validators.email]],
      edad: [0, [Validators.required, Validators.min(18)]]
    });
  }
  
  guardar(): void {
    if (this.formulario.valid) {
      console.log(this.formulario.value);
    }
  }
  
  get nombre() {
    return this.formulario.get('nombre');
  }
}
```

```html
<form [formGroup]="formulario" (ngSubmit)="guardar()">
  <input formControlName="nombre" />
  <div *ngIf="nombre?.invalid && nombre?.touched">
    <span *ngIf="nombre?.errors?.['required']">Requerido</span>
  </div>
  
  <input formControlName="email" type="email" />
  <input formControlName="edad" type="number" />
  
  <button [disabled]="formulario.invalid">Guardar</button>
</form>
```

**6. Pipes:**

**Qué trata:** Transforman datos en templates.

```html
<!-- Pipes incorporados -->
<p>{{ nombre | uppercase }}</p>
<p>{{ precio | currency:'USD' }}</p>
<p>{{ fecha | date:'dd/MM/yyyy' }}</p>
<p>{{ porcentaje | percent }}</p>
<p>{{ objeto | json }}</p>

<!-- Pipe personalizado -->
```

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'resaltar'
})
export class ResaltarPipe implements PipeTransform {
  transform(texto: string, buscar: string): string {
    if (!buscar) return texto;
    const regex = new RegExp(buscar, 'gi');
    return texto.replace(regex, `<mark>$&</mark>`);
  }
}

// Uso: <p [innerHTML]="texto | resaltar:'angular'"></p>
```

**7. Directivas:**

**Directivas estructurales (modifican DOM):**
- `*ngIf`: Condicional
- `*ngFor`: Iteración
- `*ngSwitch`: Switch-case

**Directivas de atributo:**
```html
<!-- ngClass -->
<div [ngClass]="{'activo': isActivo, 'error': hasError}"></div>

<!-- ngStyle -->
<div [ngStyle]="{'color': color, 'font-size': size + 'px'}"></div>
```

**Directiva personalizada:**
```typescript
import { Directive, ElementRef, HostListener } from '@angular/core';

@Directive({
  selector: '[appResaltar]'
})
export class ResaltarDirective {
  constructor(private el: ElementRef) { }
  
  @HostListener('mouseenter') onMouseEnter() {
    this.el.nativeElement.style.backgroundColor = 'yellow';
  }
  
  @HostListener('mouseleave') onMouseLeave() {
    this.el.nativeElement.style.backgroundColor = '';
  }
}

// Uso: <p appResaltar>Texto que se resalta al pasar mouse</p>
```

**8. Observables (RxJS):**

**Qué trata:** Manejo de operaciones asíncronas y streams de datos.

```typescript
import { Observable, of, from } from 'rxjs';
import { map, filter, catchError } from 'rxjs/operators';

// Observable simple
const numeros$ = of(1, 2, 3, 4, 5);

numeros$.pipe(
  filter(n => n % 2 === 0),
  map(n => n * 2)
).subscribe(
  valor => console.log(valor),
  error => console.error(error),
  () => console.log('Completado')
);

// En servicio
obtenerUsuarios(): Observable<Usuario[]> {
  return this.http.get<Usuario[]>(this.apiUrl)
    .pipe(
      map(usuarios => usuarios.filter(u => u.activo)),
      catchError(error => {
        console.error('Error:', error);
        return of([]);
      })
    );
}
```

**CLI Angular:**

```bash
# Instalar CLI
npm install -g @angular/cli

# Crear proyecto
ng new mi-app
cd mi-app

# Servir aplicación
ng serve
# Abre http://localhost:4200

# Generar componente
ng generate component usuarios/lista-usuarios
ng g c usuarios/lista-usuarios

# Generar servicio
ng generate service services/usuario
ng g s services/usuario

# Generar módulo
ng generate module usuarios --routing

# Build para producción
ng build --prod
```

**Ciclo de vida de componente:**

```typescript
export class MiComponente implements OnInit, OnDestroy {
  // 1. Constructor
  constructor() {
    console.log('Constructor');
  }
  
  // 2. ngOnInit - Inicialización
  ngOnInit(): void {
    console.log('ngOnInit - Componente inicializado');
    // Cargar datos, suscripciones
  }
  
  // 3. ngOnChanges - Cuando cambian inputs
  ngOnChanges(changes: SimpleChanges): void {
    console.log('ngOnChanges', changes);
  }
  
  // 4. ngAfterViewInit - Después de inicializar vista
  ngAfterViewInit(): void {
    console.log('Vista inicializada');
  }
  
  // 5. ngOnDestroy - Antes de destruir componente
  ngOnDestroy(): void {
    console.log('ngOnDestroy - Limpieza');
    // Cancelar suscripciones, timers
  }
}
```

**Comunicación entre componentes:**

**Padre a hijo (@Input):**
```typescript
// Hijo
export class HijoComponent {
  @Input() nombre: string;
  @Input() edad: number;
}

// Padre template
<app-hijo [nombre]="'Juan'" [edad]="25"></app-hijo>
```

**Hijo a padre (@Output):**
```typescript
// Hijo
export class HijoComponent {
  @Output() usuarioSeleccionado = new EventEmitter<Usuario>();
  
  seleccionar(usuario: Usuario): void {
    this.usuarioSeleccionado.emit(usuario);
  }
}

// Padre template
<app-hijo (usuarioSeleccionado)="onUsuarioSeleccionado($event)"></app-hijo>

// Padre component
onUsuarioSeleccionado(usuario: Usuario): void {
  console.log('Usuario seleccionado:', usuario);
}
```

**Ejemplo completo de aplicación:**

```typescript
// Estructura de proyecto
src/
  app/
    components/
      usuarios/
        lista-usuarios/
        detalle-usuario/
        formulario-usuario/
    services/
      usuario.service.ts
      auth.service.ts
    models/
      usuario.model.ts
    guards/
      auth.guard.ts
    app.module.ts
    app-routing.module.ts
    app.component.ts
```

**Ejemplo de uso real:** Aplicación de gestión de tareas SPA con Angular. Lista de tareas, crear/editar/eliminar, filtros, búsqueda. Frontend Angular consume API REST backend. Routing para navegación, servicios para HTTP, formularios reactivos, componentes reutilizables, guards para proteger rutas autenticadas.

### Framework para aplicaciones web back-end (SpringBoot)

**Qué trata:** Framework Java para construir aplicaciones empresariales, microservicios y APIs REST de forma rápida con configuración mínima (convención sobre configuración).

**Por qué se utiliza:** Elimina configuración XML compleja, autoconfiguración inteligente, servidor embebido, producción lista con métricas y health checks, ecosistema maduro.

**Ventajas:**
- Configuración automática (auto-configuration)
- Servidor embebido (Tomcat, Jetty, Undertow)
- Starter dependencies (gestión simplificada)
- Spring Boot Actuator (monitoreo)
- Desarrollo rápido y productivo
- Amplia comunidad y documentación

**Desventajas:**
- Curva de aprendizaje inicial
- "Magia" de autoconfiguración puede confundir
- Tamaño del JAR puede ser grande
- Overhead para aplicaciones muy simples
- Actualizaciones pueden romper compatibilidad

**Conceptos fundamentales:**

**1. Estructura básica de proyecto:**

```
mi-app/
  src/
    main/
      java/
        com/ejemplo/miapp/
          MiAppApplication.java      # Clase principal
          controller/
            UsuarioController.java
          service/
            UsuarioService.java
          repository/
            UsuarioRepository.java
          model/
            Usuario.java
          dto/
            UsuarioDTO.java
          config/
            SecurityConfig.java
      resources/
        application.properties       # Configuración
        application.yml
        static/                      # Archivos estáticos
        templates/                   # Templates (Thymeleaf)
  pom.xml                           # Maven
```

**2. Clase principal (@SpringBootApplication):**

```java
package com.ejemplo.miapp;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
// Combina: @Configuration + @EnableAutoConfiguration + @ComponentScan
public class MiAppApplication {
    public static void main(String[] args) {
        SpringApplication.run(MiAppApplication.class, args);
    }
}
```

**3. Entidad JPA:**

```java
package com.ejemplo.miapp.model;

import javax.persistence.*;
import lombok.Data;
import lombok.NoArgsConstructor;
import lombok.AllArgsConstructor;

@Entity
@Table(name = "usuarios")
@Data  // Lombok: genera getters, setters, toString, equals, hashCode
@NoArgsConstructor
@AllArgsConstructor
public class Usuario {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false, length = 100)
    private String nombre;
    
    @Column(unique = true, nullable = false)
    private String email;
    
    @Column(nullable = false)
    private String password;
    
    @Enumerated(EnumType.STRING)
    private Role role;
    
    @CreatedDate
    @Column(nullable = false, updatable = false)
    private LocalDateTime createdAt;
    
    @OneToMany(mappedBy = "usuario", cascade = CascadeType.ALL)
    private List<Pedido> pedidos;
}
```

**4. Repository (Spring Data JPA):**

```java
package com.ejemplo.miapp.repository;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;
import org.springframework.stereotype.Repository;
import java.util.Optional;
import java.util.List;

@Repository
public interface UsuarioRepository extends JpaRepository<Usuario, Long> {
    
    // Métodos automáticos por convención de nombres
    Optional<Usuario> findByEmail(String email);
    List<Usuario> findByNombreContaining(String nombre);
    List<Usuario> findByRole(Role role);
    boolean existsByEmail(String email);
    void deleteByEmail(String email);
    
    // Consultas personalizadas con @Query
    @Query("SELECT u FROM Usuario u WHERE u.activo = true")
    List<Usuario> findAllActivos();
    
    @Query(value = "SELECT * FROM usuarios WHERE created_at > ?1", 
           nativeQuery = true)
    List<Usuario> findRecentUsers(LocalDateTime fecha);
    
    // Paginación automática
    Page<Usuario> findAll(Pageable pageable);
}
```

**5. Service (Lógica de negocio):**

```java
package com.ejemplo.miapp.service;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;
import lombok.RequiredArgsConstructor;

@Service
@RequiredArgsConstructor  // Lombok: constructor con final fields
public class UsuarioService {
    
    private final UsuarioRepository usuarioRepository;
    private final PasswordEncoder passwordEncoder;
    
    @Transactional(readOnly = true)
    public List<Usuario> obtenerTodos() {
        return usuarioRepository.findAll();
    }
    
    @Transactional(readOnly = true)
    public Usuario obtenerPorId(Long id) {
        return usuarioRepository.findById(id)
            .orElseThrow(() -> new ResourceNotFoundException("Usuario no encontrado"));
    }
    
    @Transactional
    public Usuario crear(UsuarioDTO dto) {
        // Validar email único
        if (usuarioRepository.existsByEmail(dto.getEmail())) {
            throw new DuplicateException("Email ya existe");
        }
        
        Usuario usuario = new Usuario();
        usuario.setNombre(dto.getNombre());
        usuario.setEmail(dto.getEmail());
        usuario.setPassword(passwordEncoder.encode(dto.getPassword()));
        usuario.setRole(Role.USER);
        
        return usuarioRepository.save(usuario);
    }
    
    @Transactional
    public Usuario actualizar(Long id, UsuarioDTO dto) {
        Usuario usuario = obtenerPorId(id);
        usuario.setNombre(dto.getNombre());
        usuario.setEmail(dto.getEmail());
        return usuarioRepository.save(usuario);
    }
    
    @Transactional
    public void eliminar(Long id) {
        if (!usuarioRepository.existsById(id)) {
            throw new ResourceNotFoundException("Usuario no encontrado");
        }
        usuarioRepository.deleteById(id);
    }
}
```

**6. Controller REST:**

```java
package com.ejemplo.miapp.controller;

import org.springframework.web.bind.annotation.*;
import org.springframework.http.ResponseEntity;
import org.springframework.http.HttpStatus;
import org.springframework.validation.annotation.Validated;
import lombok.RequiredArgsConstructor;
import javax.validation.Valid;

@RestController
@RequestMapping("/api/usuarios")
@RequiredArgsConstructor
@Validated
public class UsuarioController {
    
    private final UsuarioService usuarioService;
    
    @GetMapping
    public ResponseEntity<List<Usuario>> listarTodos() {
        return ResponseEntity.ok(usuarioService.obtenerTodos());
    }
    
    @GetMapping("/{id}")
    public ResponseEntity<Usuario> obtenerPorId(@PathVariable Long id) {
        return ResponseEntity.ok(usuarioService.obtenerPorId(id));
    }
    
    @PostMapping
    public ResponseEntity<Usuario> crear(@Valid @RequestBody UsuarioDTO dto) {
        Usuario usuario = usuarioService.crear(dto);
        return ResponseEntity.status(HttpStatus.CREATED).body(usuario);
    }
    
    @PutMapping("/{id}")
    public ResponseEntity<Usuario> actualizar(
            @PathVariable Long id,
            @Valid @RequestBody UsuarioDTO dto) {
        return ResponseEntity.ok(usuarioService.actualizar(id, dto));
    }
    
    @DeleteMapping("/{id}")
    public ResponseEntity<Void> eliminar(@PathVariable Long id) {
        usuarioService.eliminar(id);
        return ResponseEntity.noContent().build();
    }
    
    // Paginación
    @GetMapping("/page")
    public ResponseEntity<Page<Usuario>> listarPaginado(
            @RequestParam(defaultValue = "0") int page,
            @RequestParam(defaultValue = "10") int size,
            @RequestParam(defaultValue = "id") String sortBy) {
        
        Pageable pageable = PageRequest.of(page, size, Sort.by(sortBy));
        return ResponseEntity.ok(usuarioService.obtenerPaginado(pageable));
    }
}
```

**7. DTO (Data Transfer Object):**

```java
package com.ejemplo.miapp.dto;

import javax.validation.constraints.*;
import lombok.Data;

@Data
public class UsuarioDTO {
    
    @NotBlank(message = "Nombre es requerido")
    @Size(min = 3, max = 100, message = "Nombre entre 3 y 100 caracteres")
    private String nombre;
    
    @NotBlank(message = "Email es requerido")
    @Email(message = "Email inválido")
    private String email;
    
    @NotBlank(message = "Password es requerido")
    @Size(min = 6, message = "Password mínimo 6 caracteres")
    @Pattern(regexp = "^(?=.*[A-Z])(?=.*[0-9]).*$", 
             message = "Password debe tener mayúscula y número")
    private String password;
}
```

**8. Manejo de excepciones global:**

```java
package com.ejemplo.miapp.exception;

import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestControllerAdvice;
import org.springframework.http.ResponseEntity;
import org.springframework.http.HttpStatus;
import org.springframework.validation.FieldError;
import org.springframework.web.bind.MethodArgumentNotValidException;

@RestControllerAdvice
public class GlobalExceptionHandler {
    
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleResourceNotFound(
            ResourceNotFoundException ex) {
        ErrorResponse error = new ErrorResponse(
            "NOT_FOUND",
            ex.getMessage(),
            LocalDateTime.now()
        );
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(error);
    }
    
    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<ValidationErrorResponse> handleValidation(
            MethodArgumentNotValidException ex) {
        
        Map<String, String> errors = new HashMap<>();
        ex.getBindingResult().getAllErrors().forEach(error -> {
            String fieldName = ((FieldError) error).getField();
            String message = error.getDefaultMessage();
            errors.put(fieldName, message);
        });
        
        ValidationErrorResponse response = new ValidationErrorResponse(
            "VALIDATION_ERROR",
            errors,
            LocalDateTime.now()
        );
        return ResponseEntity.badRequest().body(response);
    }
    
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleGeneric(Exception ex) {
        ErrorResponse error = new ErrorResponse(
            "INTERNAL_ERROR",
            "Error interno del servidor",
            LocalDateTime.now()
        );
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)
                             .body(error);
    }
}
```

**9. Configuración (application.yml):**

```yaml
spring:
  application:
    name: mi-app
  
  datasource:
    url: jdbc:mysql://localhost:3306/midb
    username: root
    password: password
    driver-class-name: com.mysql.cj.jdbc.Driver
  
  jpa:
    hibernate:
      ddl-auto: update  # create, create-drop, validate, update, none
    show-sql: true
    properties:
      hibernate:
        format_sql: true
        dialect: org.hibernate.dialect.MySQL8Dialect
  
  # Perfiles
  profiles:
    active: dev

server:
  port: 8080
  servlet:
    context-path: /api

logging:
  level:
    root: INFO
    com.ejemplo.miapp: DEBUG
    org.hibernate.SQL: DEBUG

---
# Perfil de desarrollo
spring:
  config:
    activate:
      on-profile: dev
  datasource:
    url: jdbc:h2:mem:testdb
server:
  port: 8081

---
# Perfil de producción
spring:
  config:
    activate:
      on-profile: prod
  datasource:
    url: jdbc:mysql://prod-server:3306/midb
server:
  port: 80
```

**10. Seguridad con Spring Security:**

```java
package com.ejemplo.miapp.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.http.SessionCreationPolicy;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.web.SecurityFilterChain;

@Configuration
@EnableWebSecurity
public class SecurityConfig {
    
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .csrf().disable()
            .authorizeHttpRequests(auth -> auth
                .antMatchers("/api/auth/**").permitAll()
                .antMatchers("/api/admin/**").hasRole("ADMIN")
                .antMatchers("/api/usuarios/**").hasAnyRole("USER", "ADMIN")
                .anyRequest().authenticated()
            )
            .sessionManagement()
                .sessionCreationPolicy(SessionCreationPolicy.STATELESS)
            .and()
            .httpBasic();
        
        return http.build();
    }
    
    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
}
```

**11. Actuator (Monitoreo):**

```yaml
management:
  endpoints:
    web:
      exposure:
        include: health,info,metrics,prometheus
  endpoint:
    health:
      show-details: always
  metrics:
    export:
      prometheus:
        enabled: true
```

**Acceder a:**
- `http://localhost:8080/actuator/health` - Estado de salud
- `http://localhost:8080/actuator/metrics` - Métricas
- `http://localhost:8080/actuator/info` - Información de la app

**12. Testing:**

```java
package com.ejemplo.miapp.controller;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.test.web.servlet.MockMvc;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.*;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;
import static org.mockito.Mockito.*;

@WebMvcTest(UsuarioController.class)
class UsuarioControllerTest {
    
    @Autowired
    private MockMvc mockMvc;
    
    @MockBean
    private UsuarioService usuarioService;
    
    @Test
    void deberiaListarUsuarios() throws Exception {
        List<Usuario> usuarios = Arrays.asList(
            new Usuario(1L, "Juan", "juan@email.com"),
            new Usuario(2L, "Ana", "ana@email.com")
        );
        
        when(usuarioService.obtenerTodos()).thenReturn(usuarios);
        
        mockMvc.perform(get("/api/usuarios"))
            .andExpect(status().isOk())
            .andExpect(jsonPath("$").isArray())
            .andExpect(jsonPath("$.length()").value(2))
            .andExpect(jsonPath("$[0].nombre").value("Juan"));
    }
    
    @Test
    void deberiaCrearUsuario() throws Exception {
        UsuarioDTO dto = new UsuarioDTO("Juan", "juan@email.com", "Pass123");
        Usuario usuario = new Usuario(1L, "Juan", "juan@email.com");
        
        when(usuarioService.crear(any())).thenReturn(usuario);
        
        mockMvc.perform(post("/api/usuarios")
            .contentType(MediaType.APPLICATION_JSON)
            .content("{\"nombre\":\"Juan\",\"email\":\"juan@email.com\",\"password\":\"Pass123\"}"))
            .andExpect(status().isCreated())
            .andExpect(jsonPath("$.id").value(1))
            .andExpect(jsonPath("$.nombre").value("Juan"));
    }
}
```

**pom.xml (Maven dependencies):**

```xml
<dependencies>
    <!-- Spring Boot Starter Web -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    
    <!-- Spring Boot Starter Data JPA -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    
    <!-- Spring Boot Starter Validation -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-validation</artifactId>
    </dependency>
    
    <!-- Spring Boot Starter Security -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-security</artifactId>
    </dependency>
    
    <!-- MySQL Driver -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <scope>runtime</scope>
    </dependency>
    
    <!-- Lombok -->
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <optional>true</optional>
    </dependency>
    
    <!-- Spring Boot Actuator -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
    
    <!-- Spring Boot DevTools (auto-reload) -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <scope>runtime</scope>
    </dependency>
    
    <!-- Testing -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```

**Ciclo de vida de ejecución:**
1. `mvn clean install` - Compilar y crear JAR
2. `java -jar target/mi-app-1.0.0.jar` - Ejecutar aplicación
3. Spring Boot inicia servidor embebido Tomcat
4. Autoconfigura conexión BD, JPA, Security
5. Escanea componentes (@Component, @Service, @Repository)
6. Expone endpoints REST
7. Aplicación lista en `http://localhost:8080`

**Comandos útiles:**

```bash
# Ejecutar en modo desarrollo
mvn spring-boot:run

# Ejecutar con perfil específico
mvn spring-boot:run -Dspring-boot.run.profiles=dev

# Crear JAR ejecutable
mvn clean package

# Ejecutar JAR con perfil
java -jar target/app.jar --spring.profiles.active=prod

# Ejecutar con propiedades override
java -jar app.jar --server.port=9090 --spring.datasource.url=jdbc:mysql://localhost:3306/otherdb
```

**Ejemplo de uso completo:** API REST de e-commerce con Spring Boot. Gestiona usuarios, productos, pedidos. Autenticación JWT con Spring Security, persistencia con JPA/MySQL, validación de datos, manejo de excepciones global, paginación, Actuator para monitoreo. Frontend Angular consume los endpoints.

### Frameworks para aplicaciones web front-end (Boostrap, Angular Material y Prime NG)

**Qué trata:** Librerías de componentes UI pre-diseñados que aceleran desarrollo de interfaces web responsivas y atractivas.

**Por qué se utiliza:** Evitar diseñar desde cero, consistencia visual, responsive design integrado, componentes probados, cross-browser compatibility.

**Bootstrap:**

**Qué trata:** Framework CSS más popular para desarrollo web responsive con sistema de grillas y componentes pre-diseñados.

**Características:**
- Sistema de grillas flexbox de 12 columnas
- Componentes listos (navbar, cards, modals, forms)
- Utilidades CSS (spacing, colors, typography)
- JavaScript plugins (carousel, tooltips, modals)
- Mobile-first approach

**Ventajas:**
- Fácil de aprender
- Ampliamente adoptado
- Documentación excelente
- Temas y templates disponibles
- Compatible con todos los navegadores

**Desventajas:**
- Sitios pueden verse similares
- Clases CSS verbosas
- Peso del framework completo
- Personalización puede ser difícil
- jQuery dependency (Bootstrap 4, eliminado en v5)

**Instalación:**

```bash
# Via CDN
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

# Via NPM
npm install bootstrap

# En Angular
npm install bootstrap
# angular.json
"styles": [
  "node_modules/bootstrap/dist/css/bootstrap.min.css",
  "src/styles.css"
]
```

**Sistema de grillas:**

```html
<div class="container">
  <!-- Fila con columnas responsive -->
  <div class="row">
    <!-- En móvil 12 columnas, tablet 6, desktop 4 -->
    <div class="col-12 col-md-6 col-lg-4">
      <div class="card">
        <img src="producto.jpg" class="card-img-top" alt="Producto">
        <div class="card-body">
          <h5 class="card-title">Producto</h5>
          <p class="card-text">Descripción del producto</p>
          <a href="#" class="btn btn-primary">Comprar</a>
        </div>
      </div>
    </div>
    <div class="col-12 col-md-6 col-lg-4">
      <!-- Otro producto -->
    </div>
    <div class="col-12 col-md-6 col-lg-4">
      <!-- Otro producto -->
    </div>
  </div>
</div>
```

**Componentes populares:**

```html
<!-- Navbar -->
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">Mi App</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" 
            data-bs-target="#navbarNav">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link active" href="#">Inicio</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Productos</a>
        </li>
      </ul>
    </div>
  </div>
</nav>

<!-- Card -->
<div class="card" style="width: 18rem;">
  <img src="..." class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Título</h5>
    <p class="card-text">Contenido de la tarjeta</p>
    <a href="#" class="btn btn-primary">Acción</a>
  </div>
</div>

<!-- Modal -->
<button type="button" class="btn btn-primary" data-bs-toggle="modal" 
        data-bs-target="#miModal">
  Abrir Modal
</button>

<div class="modal fade" id="miModal" tabindex="-1">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Título del Modal</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">
        <p>Contenido del modal</p>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cerrar</button>
        <button type="button" class="btn btn-primary">Guardar</button>
      </div>
    </div>
  </div>
</div>

<!-- Formulario -->
<form>
  <div class="mb-3">
    <label for="email" class="form-label">Email</label>
    <input type="email" class="form-control" id="email" placeholder="nombre@ejemplo.com">
  </div>
  <div class="mb-3">
    <label for="password" class="form-label">Password</label>
    <input type="password" class="form-control" id="password">
  </div>
  <div class="mb-3 form-check">
    <input type="checkbox" class="form-check-input" id="remember">
    <label class="form-check-label" for="remember">Recordarme</label>
  </div>
  <button type="submit" class="btn btn-primary">Enviar</button>
</form>

<!-- Alert -->
<div class="alert alert-success alert-dismissible fade show" role="alert">
  <strong>¡Éxito!</strong> Operación completada correctamente.
  <button type="button" class="btn-close" data-bs-dismiss="alert"></button>
</div>
```

**Utilidades CSS:**

```html
<!-- Spacing (margin/padding) -->
<div class="mt-3 mb-5 p-4">  
  <!-- mt-3 = margin-top: 1rem, mb-5 = margin-bottom: 3rem, p-4 = padding: 1.5rem -->
</div>

<!-- Colores -->
<button class="btn btn-primary">Primario</button>
<button class="btn btn-success">Éxito</button>
<button class="btn btn-danger">Peligro</button>

<p class="text-primary">Texto azul</p>
<div class="bg-warning">Fondo amarillo</div>

<!-- Display -->
<div class="d-none d-md-block">Visible solo en tablet+</div>
<div class="d-flex justify-content-center align-items-center">
  Flexbox centrado
</div>

<!-- Texto -->
<p class="text-center">Centrado</p>
<p class="text-uppercase">Mayúsculas</p>
<p class="fw-bold">Negrita</p>
<p class="fs-1">Tamaño grande</p>
```

**Angular Material:**

**Qué trata:** Librería de componentes UI para Angular basada en Material Design de Google.

**Características:**
- Diseño Material Design
- Componentes Angular nativos
- Animaciones integradas
- Accesibilidad (a11y)
- Theming personalizable
- RTL support

**Ventajas:**
- Integración perfecta con Angular
- Componentes complejos (datepicker, autocomplete)
- TypeScript nativo
- Estilo moderno y profesional
- Mantenido por Google

**Desventajas:**
- Curva de aprendizaje
- Bundle size considerable
- Estilo Material puede no adaptarse a todos
- Personalización limitada
- Requiere configuración inicial

**Instalación:**

```bash
# Instalar Angular Material
ng add @angular/material

# Seleccionar tema
# - Indigo/Pink
# - Deep Purple/Amber
# - Pink/Blue Grey
# - Purple/Green
# - Custom

# Configurar animaciones (sí)
# Configurar tipografía global (sí)
```

**Importar módulos:**

```typescript
// app.module.ts
import { MatButtonModule } from '@angular/material/button';
import { MatCardModule } from '@angular/material/card';
import { MatInputModule } from '@angular/material/input';
import { MatTableModule } from '@angular/material/table';
import { MatPaginatorModule } from '@angular/material/paginator';
import { MatDialogModule } from '@angular/material/dialog';
import { MatDatepickerModule } from '@angular/material/datepicker';
import { MatNativeDateModule } from '@angular/material/core';

@NgModule({
  imports: [
    MatButtonModule,
    MatCardModule,
    MatInputModule,
    MatTableModule,
    MatPaginatorModule,
    MatDialogModule,
    MatDatepickerModule,
    MatNativeDateModule
  ]
})
export class AppModule { }
```

**Componentes comunes:**

```html
<!-- Botones -->
<button mat-button>Basic</button>
<button mat-raised-button color="primary">Raised</button>
<button mat-fab color="accent">
  <mat-icon>add</mat-icon>
</button>

<!-- Card -->
<mat-card>
  <mat-card-header>
    <mat-card-title>Título</mat-card-title>
    <mat-card-subtitle>Subtítulo</mat-card-subtitle>
  </mat-card-header>
  <mat-card-content>
    <p>Contenido de la tarjeta</p>
  </mat-card-content>
  <mat-card-actions>
    <button mat-button>ACCIÓN</button>
  </mat-card-actions>
</mat-card>

<!-- Formularios -->
<mat-form-field appearance="fill">
  <mat-label>Email</mat-label>
  <input matInput type="email" [(ngModel)]="email" required>
  <mat-error *ngIf="emailInvalid">Email inválido</mat-error>
</mat-form-field>

<mat-form-field appearance="outline">
  <mat-label>Seleccionar</mat-label>
  <mat-select [(ngModel)]="seleccion">
    <mat-option value="opcion1">Opción 1</mat-option>
    <mat-option value="opcion2">Opción 2</mat-option>
  </mat-select>
</mat-form-field>

<!-- Datepicker -->
<mat-form-field>
  <mat-label>Fecha</mat-label>
  <input matInput [matDatepicker]="picker" [(ngModel)]="fecha">
  <mat-datepicker-toggle matSuffix [for]="picker"></mat-datepicker-toggle>
  <mat-datepicker #picker></mat-datepicker>
</mat-form-field>

<!-- Tabla con paginación -->
<table mat-table [dataSource]="dataSource" class="mat-elevation-z8">
  <!-- Columna nombre -->
  <ng-container matColumnDef="nombre">
    <th mat-header-cell *matHeaderCellDef>Nombre</th>
    <td mat-cell *matCellDef="let usuario">{{ usuario.nombre }}</td>
  </ng-container>
  
  <!-- Columna email -->
  <ng-container matColumnDef="email">
    <th mat-header-cell *matHeaderCellDef>Email</th>
    <td mat-cell *matCellDef="let usuario">{{ usuario.email }}</td>
  </ng-container>
  
  <!-- Columna acciones -->
  <ng-container matColumnDef="acciones">
    <th mat-header-cell *matHeaderCellDef>Acciones</th>
    <td mat-cell *matCellDef="let usuario">
      <button mat-icon-button (click)="editar(usuario)">
        <mat-icon>edit</mat-icon>
      </button>
      <button mat-icon-button (click)="eliminar(usuario)">
        <mat-icon>delete</mat-icon>
      </button>
    </td>
  </ng-container>
  
  <tr mat-header-row *matHeaderRowDef="displayedColumns"></tr>
  <tr mat-row *matRowDef="let row; columns: displayedColumns;"></tr>
</table>
<mat-paginator [pageSizeOptions]="[5, 10, 20]" showFirstLastButtons></mat-paginator>

<!-- Dialog -->
<button mat-raised-button (click)="openDialog()">Abrir Dialog</button>
```

**Dialog component:**

```typescript
// dialog.component.ts
import { Component, Inject } from '@angular/core';
import { MAT_DIALOG_DATA, MatDialogRef } from '@angular/material/dialog';

@Component({
  selector: 'app-dialog',
  template: `
    <h2 mat-dialog-title>{{ data.title }}</h2>
    <mat-dialog-content>
      <p>{{ data.message }}</p>
    </mat-dialog-content>
    <mat-dialog-actions align="end">
      <button mat-button (click)="onCancel()">Cancelar</button>
      <button mat-raised-button color="primary" (click)="onConfirm()">Confirmar</button>
    </mat-dialog-actions>
  `
})
export class DialogComponent {
  constructor(
    public dialogRef: MatDialogRef<DialogComponent>,
    @Inject(MAT_DIALOG_DATA) public data: any
  ) {}
  
  onCancel(): void {
    this.dialogRef.close(false);
  }
  
  onConfirm(): void {
    this.dialogRef.close(true);
  }
}

// Uso en componente
import { MatDialog } from '@angular/material/dialog';

export class AppComponent {
  constructor(private dialog: MatDialog) {}
  
  openDialog(): void {
    const dialogRef = this.dialog.open(DialogComponent, {
      width: '400px',
      data: { title: 'Confirmar', message: '¿Está seguro?' }
    });
    
    dialogRef.afterClosed().subscribe(result => {
      if (result) {
        console.log('Confirmado');
      }
    });
  }
}
```

**Theming personalizado:**

```scss
// styles.scss
@use '@angular/material' as mat;
@include mat.core();

// Define paleta personalizada
$mi-primary: mat.define-palette(mat.$indigo-palette);
$mi-accent: mat.define-palette(mat.$pink-palette, A200, A100, A400);
$mi-warn: mat.define-palette(mat.$red-palette);

// Crear tema
$mi-theme: mat.define-light-theme((
  color: (
    primary: $mi-primary,
    accent: $mi-accent,
    warn: $mi-warn,
  )
));

// Aplicar tema
@include mat.all-component-themes($mi-theme);
```

**PrimeNG:**

**Qué trata:** Suite completa de componentes UI ricos para Angular con temas personalizables.

**Características:**
- 90+ componentes
- Múltiples temas prediseñados
- Componentes complejos (TreeTable, Chart, FileUpload)
- Gratis y open source (versión community)
- Internacionalización

**Ventajas:**
- Componentes muy completos
- Fácil personalización con temas
- Excelente documentación
- Templates flexibles
- Sin dependencias externas

**Desventajas:**
- Bundle size grande si usas muchos componentes
- Estilos pueden entrar en conflicto
- Curva de aprendizaje para componentes avanzados
- Versión Pro de pago para soporte premium

**Instalación:**

```bash
# Instalar PrimeNG
npm install primeng primeicons

# angular.json
"styles": [
  "node_modules/primeng/resources/themes/lara-light-blue/theme.css",
  "node_modules/primeng/resources/primeng.min.css",
  "node_modules/primeicons/primeicons.css",
  "src/styles.css"
]
```

**Importar módulos:**

```typescript
// app.module.ts
import { ButtonModule } from 'primeng/button';
import { TableModule } from 'primeng/table';
import { CardModule } from 'primeng/card';
import { DialogModule } from 'primeng/dialog';
import { InputTextModule } from 'primeng/inputtext';
import { DropdownModule } from 'primeng/dropdown';
import { CalendarModule } from 'primeng/calendar';
import { ToastModule } from 'primeng/toast';
import { ConfirmDialogModule } from 'primeng/confirmdialog';

@NgModule({
  imports: [
    ButtonModule,
    TableModule,
    CardModule,
    DialogModule,
    InputTextModule,
    DropdownModule,
    CalendarModule,
    ToastModule,
    ConfirmDialogModule
  ]
})
export class AppModule { }
```

**Componentes comunes:**

```html
<!-- Botones -->
<p-button label="Click" icon="pi pi-check"></p-button>
<p-button label="Primario" styleClass="p-button-primary"></p-button>
<p-button label="Éxito" styleClass="p-button-success"></p-button>
<p-button icon="pi pi-trash" styleClass="p-button-rounded p-button-danger"></p-button>

<!-- Card -->
<p-card header="Título" subheader="Subtítulo">
  <ng-template pTemplate="header">
    <img src="card-image.jpg" alt="Header Image">
  </ng-template>
  <p>Contenido de la tarjeta</p>
  <ng-template pTemplate="footer">
    <p-button label="Guardar" icon="pi pi-check"></p-button>
    <p-button label="Cancelar" icon="pi pi-times" styleClass="p-button-secondary"></p-button>
  </ng-template>
</p-card>

<!-- Tabla avanzada -->
<p-table [value]="usuarios" [paginator]="true" [rows]="10" 
         [showCurrentPageReport]="true" [rowsPerPageOptions]="[10,25,50]"
         [loading]="loading" [globalFilterFields]="['nombre','email']"
         [(selection)]="selectedUsuarios" dataKey="id">
  
  <ng-template pTemplate="caption">
    <div class="flex">
      <span class="p-input-icon-left ml-auto">
        <i class="pi pi-search"></i>
        <input pInputText type="text" (input)="dt.filterGlobal($event.target.value, 'contains')" 
               placeholder="Buscar..." />
      </span>
    </div>
  </ng-template>
  
  <ng-template pTemplate="header">
    <tr>
      <th style="width: 3rem">
        <p-tableHeaderCheckbox></p-tableHeaderCheckbox>
      </th>
      <th pSortableColumn="nombre">Nombre <p-sortIcon field="nombre"></p-sortIcon></th>
      <th pSortableColumn="email">Email <p-sortIcon field="email"></p-sortIcon></th>
      <th>Acciones</th>
    </tr>
  </ng-template>
  
  <ng-template pTemplate="body" let-usuario>
    <tr>
      <td>
        <p-tableCheckbox [value]="usuario"></p-tableCheckbox>
      </td>
      <td>{{ usuario.nombre }}</td>
      <td>{{ usuario.email }}</td>
      <td>
        <p-button icon="pi pi-pencil" styleClass="p-button-rounded p-button-success mr-2"
                  (click)="editarUsuario(usuario)"></p-button>
        <p-button icon="pi pi-trash" styleClass="p-button-rounded p-button-danger"
                  (click)="eliminarUsuario(usuario)"></p-button>
      </td>
    </tr>
  </ng-template>
  
  <ng-template pTemplate="emptymessage">
    <tr>
      <td colspan="4">No se encontraron usuarios.</td>
    </tr>
  </ng-template>
</p-table>

<!-- Dialog -->
<p-dialog header="Editar Usuario" [(visible)]="displayDialog" [modal]="true" 
          [style]="{width: '450px'}" [baseZIndex]="10000">
  <div class="p-fluid">
    <div class="p-field">
      <label for="nombre">Nombre</label>
      <input id="nombre" type="text" pInputText [(ngModel)]="usuario.nombre" required />
    </div>
    <div class="p-field">
      <label for="email">Email</label>
      <input id="email" type="email" pInputText [(ngModel)]="usuario.email" required />
    </div>
  </div>
  <ng-template pTemplate="footer">
    <p-button icon="pi pi-times" label="Cancelar" styleClass="p-button-text"
              (click)="displayDialog=false"></p-button>
    <p-button icon="pi pi-check" label="Guardar" 
              (click)="guardarUsuario()"></p-button>
  </ng-template>
</p-dialog>

<!-- Dropdown -->
<p-dropdown [options]="ciudades" [(ngModel)]="ciudadSeleccionada" 
            placeholder="Seleccionar ciudad" optionLabel="nombre" 
            [showClear]="true"></p-dropdown>

<!-- Calendar -->
<p-calendar [(ngModel)]="fecha" [showIcon]="true" dateFormat="dd/mm/yy"></p-calendar>

<!-- Toast (notificaciones) -->
<p-toast></p-toast>

<!-- Uso en component -->
```

```typescript
import { MessageService } from 'primeng/api';

export class AppComponent {
  constructor(private messageService: MessageService) {}
  
  mostrarExito() {
    this.messageService.add({
      severity: 'success', 
      summary: 'Éxito', 
      detail: 'Operación completada'
    });
  }
  
  mostrarError() {
    this.messageService.add({
      severity: 'error', 
      summary: 'Error', 
      detail: 'Ocurrió un error'
    });
  }
}
```

**ConfirmDialog:**

```html
<p-confirmDialog header="Confirmación" icon="pi pi-exclamation-triangle"></p-confirmDialog>
```

```typescript
import { ConfirmationService } from 'primeng/api';

export class AppComponent {
  constructor(private confirmationService: ConfirmationService) {}
  
  confirmarEliminacion() {
    this.confirmationService.confirm({
      message: '¿Está seguro de eliminar este usuario?',
      accept: () => {
        // Lógica de eliminación
        this.messageService.add({severity:'info', summary:'Confirmado', detail:'Usuario eliminado'});
      }
    });
  }
}
```

**Temas disponibles:**
- lara-light-blue, lara-dark-blue
- saga-blue, saga-green, saga-orange
- arya-blue, arya-green, arya-orange
- vela-blue, vela-green, vela-orange

**Comparación de frameworks:**

| Característica | Bootstrap | Angular Material | PrimeNG |
|---|---|---|---|
| **Tipo** | CSS + JS | Angular Components | Angular Components |
| **Curva aprendizaje** | Baja | Media | Media |
| **Componentes** | Básicos | Intermedios | Avanzados |
| **Diseño** | Personalizable | Material Design | Múltiples temas |
| **Bundle size** | Pequeño | Medio | Grande |
| **Mejor para** | Sitios rápidos | Apps empresariales | Dashboards complejos |

**Ejemplo de uso combinado:** Dashboard administrativo Angular con PrimeNG para tablas complejas y gráficos, Angular Material para formularios y diálogos, Bootstrap para layout responsive y utilidades CSS.

### Fundamentos de microserivicios y sus características

**Qué trata:** Arquitectura que estructura aplicación como colección de servicios pequeños, independientes y desplegables separadamente, cada uno ejecutando procesos propios y comunicándose vía APIs.

**Por qué se utiliza:** Escalabilidad independiente, desarrollo paralelo por equipos, tecnologías heterogéneas, despliegue continuo, tolerancia a fallos aislados.

**Ventajas:**
- **Escalabilidad granular:** Escalar solo servicios necesarios
- **Agilidad de desarrollo:** Equipos independientes
- **Resiliencia:** Fallo de un servicio no afecta todo el sistema
- **Flexibilidad tecnológica:** Cada servicio puede usar stack diferente
- **Despliegue independiente:** CI/CD por servicio
- **Mantenibilidad:** Servicios pequeños más fáciles de entender

**Desventajas:**
- **Complejidad distribuida:** Debugging más difícil
- **Overhead de comunicación:** Latencia de red
- **Gestión de datos:** Transacciones distribuidas complejas
- **Consistencia eventual:** No ACID tradicional
- **DevOps intensivo:** Requiere infraestructura robusta
- **Monitoreo complejo:** Múltiples servicios que rastrear

**Características fundamentales:**

**1. Servicios independientes:**

Cada microservicio:
- Corre en proceso propio
- Tiene base de datos propia (database per service)
- Se despliega independientemente
- Comunica solo vía APIs

**Ejemplo estructura:**

```
ecommerce/
  ├── usuario-service/          # Gestión de usuarios
  │   ├── src/
  │   ├── Dockerfile
  │   └── pom.xml
  ├── producto-service/         # Catálogo de productos
  │   ├── src/
  │   ├── Dockerfile
  │   └── pom.xml
  ├── pedido-service/           # Gestión de pedidos
  │   ├── src/
  │   ├── Dockerfile
  │   └── pom.xml
  ├── pago-service/             # Procesamiento de pagos
  │   ├── src/
  │   ├── Dockerfile
  │   └── pom.xml
  └── notificacion-service/     # Envío de notificaciones
      ├── src/
      ├── Dockerfile
      └── pom.xml
```

**2. Base de datos por servicio:**

```
Usuario-Service  → PostgreSQL (usuarios, autenticación)
Producto-Service → MongoDB (catálogo flexible)
Pedido-Service   → MySQL (transacciones ACID)
Pago-Service     → PostgreSQL (datos financieros)
Notificación-Service → Redis (cola de mensajes)
```

**3. Comunicación entre servicios:**

**REST/HTTP:**
```java
// Pedido-Service llama a Producto-Service
@Service
public class PedidoService {
    
    @Autowired
    private RestTemplate restTemplate;
    
    public Pedido crearPedido(PedidoDTO dto) {
        // Obtener info del producto
        String url = "http://producto-service/api/productos/" + dto.getProductoId();
        Producto producto = restTemplate.getForObject(url, Producto.class);
        
        if (producto.getStock() < dto.getCantidad()) {
            throw new InsufficientStockException();
        }
        
        // Crear pedido
        Pedido pedido = new Pedido();
        pedido.setProductoId(producto.getId());
        pedido.setPrecio(producto.getPrecio());
        pedido.setCantidad(dto.getCantidad());
        
        return pedidoRepository.save(pedido);
    }
}
```

**Mensajería asíncrona (RabbitMQ/Kafka):**
```java
// Pedido-Service publica evento
@Service
public class PedidoService {
    
    @Autowired
    private RabbitTemplate rabbitTemplate;
    
    public Pedido crearPedido(PedidoDTO dto) {
        Pedido pedido = pedidoRepository.save(new Pedido(dto));
        
        // Publicar evento
        PedidoCreatedEvent evento = new PedidoCreatedEvent(
            pedido.getId(),
            pedido.getUsuarioId(),
            pedido.getTotal()
        );
        rabbitTemplate.convertAndSend("pedidos.exchange", "pedido.created", evento);
        
        return pedido;
    }
}

// Notificacion-Service escucha evento
@Service
public class NotificacionListener {
    
    @RabbitListener(queues = "notificacion.queue")
    public void handlePedidoCreated(PedidoCreatedEvent evento) {
        // Enviar email de confirmación
        emailService.enviarConfirmacion(evento.getUsuarioId(), evento.getPedidoId());
    }
}
```

**4. API Gateway:**

**Qué trata:** Punto de entrada único que enruta peticiones a microservicios apropiados.

```java
// Spring Cloud Gateway
@Configuration
public class GatewayConfig {
    
    @Bean
    public RouteLocator customRouteLocator(RouteLocatorBuilder builder) {
        return builder.routes()
            .route("usuario-service", r -> r
                .path("/api/usuarios/**")
                .uri("lb://USUARIO-SERVICE"))
            .route("producto-service", r -> r
                .path("/api/productos/**")
                .uri("lb://PRODUCTO-SERVICE"))
            .route("pedido-service", r -> r
                .path("/api/pedidos/**")
                .uri("lb://PEDIDO-SERVICE"))
            .build();
    }
}
```

**Cliente accede:**
```
https://api.miapp.com/api/usuarios/123    → Usuario-Service
https://api.miapp.com/api/productos/456   → Producto-Service
https://api.miapp.com/api/pedidos/789     → Pedido-Service
```

**5. Service Discovery:**

**Qué trata:** Registro y descubrimiento automático de servicios (Eureka, Consul).

```java
// Eureka Server
@SpringBootApplication
@EnableEurekaServer
public class EurekaServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(EurekaServerApplication.class, args);
    }
}

// Microservicio se registra
@SpringBootApplication
@EnableEurekaClient
public class UsuarioServiceApplication {
    public static void main(String[] args) {
        SpringApplication.run(UsuarioServiceApplication.class, args);
    }
}

// application.yml
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
  instance:
    prefer-ip-address: true
spring:
  application:
    name: usuario-service
```

**6. Circuit Breaker:**

**Qué trata:** Patrón que previene cascada de fallos cuando servicio no responde (Resilience4j, Hystrix).

```java
@Service
public class PedidoService {
    
    @Autowired
    private RestTemplate restTemplate;
    
    @CircuitBreaker(name = "productoService", fallbackMethod = "getProductoFallback")
    public Producto getProducto(Long id) {
        return restTemplate.getForObject(
            "http://producto-service/api/productos/" + id, 
            Producto.class
        );
    }
    
    // Método de respaldo si servicio falla
    private Producto getProductoFallback(Long id, Exception ex) {
        // Retornar datos en caché o respuesta por defecto
        return new Producto(id, "Producto no disponible", 0.0);
    }
}

// application.yml
resilience4j:
  circuitbreaker:
    instances:
      productoService:
        failure-rate-threshold: 50
        wait-duration-in-open-state: 10000
        sliding-window-size: 10
```

**7. Distributed Tracing:**

**Qué trata:** Rastreo de peticiones a través de múltiples servicios (Sleuth + Zipkin).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-sleuth</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-sleuth-zipkin</artifactId>
</dependency>
```

```yaml
# application.yml
spring:
  sleuth:
    sampler:
      probability: 1.0  # 100% de trazas
  zipkin:
    base-url: http://localhost:9411
```

**Logs con Trace ID:**
```
[usuario-service,abc123,xyz789] Usuario creado: juan@email.com
[pedido-service,abc123,def456] Pedido creado: 12345
[pago-service,abc123,ghi789] Pago procesado: $100.00
```

**8. Configuración centralizada:**

**Qué trata:** Config Server para gestionar configuración de todos los servicios.

```java
// Config Server
@SpringBootApplication
@EnableConfigServer
public class ConfigServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(ConfigServerApplication.class, args);
    }
}

// application.yml del Config Server
spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/miapp/config-repo
          default-label: main
```

**Repositorio Git:**
```
config-repo/
  ├── usuario-service.yml
  ├── producto-service.yml
  ├── pedido-service.yml
  └── application.yml  # Configuración compartida
```

**Microservicio consume config:**
```yaml
# bootstrap.yml
spring:
  application:
    name: usuario-service
  cloud:
    config:
      uri: http://localhost:8888
      fail-fast: true
```

**9. Containerización con Docker:**

```dockerfile
# Dockerfile para cada microservicio
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY target/usuario-service-1.0.0.jar app.jar
EXPOSE 8081
ENTRYPOINT ["java", "-jar", "app.jar"]
```

**Docker Compose:**
```yaml
version: '3.8'
services:
  eureka-server:
    build: ./eureka-server
    ports:
      - "8761:8761"
  
  config-server:
    build: ./config-server
    ports:
      - "8888:8888"
    depends_on:
      - eureka-server
  
  usuario-service:
    build: ./usuario-service
    ports:
      - "8081:8081"
    environment:
      - EUREKA_CLIENT_SERVICEURL_DEFAULTZONE=http://eureka-server:8761/eureka/
    depends_on:
      - eureka-server
      - config-server
  
  producto-service:
    build: ./producto-service
    ports:
      - "8082:8082"
    depends_on:
      - eureka-server
  
  pedido-service:
    build: ./pedido-service
    ports:
      - "8083:8083"
    depends_on:
      - eureka-server
      - rabbitmq
  
  rabbitmq:
    image: rabbitmq:3-management
    ports:
      - "5672:5672"
      - "15672:15672"
  
  zipkin:
    image: openzipkin/zipkin
    ports:
      - "9411:9411"
```

**10. Principios de diseño:**

**Single Responsibility:** Cada servicio hace una cosa
- Usuario-Service: Solo autenticación y perfil
- Pedido-Service: Solo gestión de pedidos

**Bounded Context (DDD):** Límites claros
```
Contexto Usuario: Usuario, Perfil, Autenticación
Contexto Producto: Producto, Categoría, Inventario
Contexto Pedido: Pedido, LineaPedido, Estado
```

**Database per Service:** Base de datos independiente
- Evita acoplamiento a nivel de datos
- Permite escalar BD independientemente

**Smart endpoints, dumb pipes:** Lógica en servicios, no en middleware
- REST/HTTP simple
- Mensajería sin lógica de negocio

**Ciclo de vida en microservicios:**

1. **Desarrollo:** Equipos independientes por servicio
2. **Build:** CI pipeline por servicio
3. **Test:** Unitarios, integración, contract testing
4. **Containerización:** Docker image por servicio
5. **Deploy:** Kubernetes/Docker Swarm
6. **Discovery:** Servicio se registra en Eureka
7. **Ejecución:** Procesos independientes
8. **Comunicación:** REST síncrano o mensajería asíncrona
9. **Monitoreo:** Logs agregados, métricas, tracing
10. **Actualización:** Deploy de un servicio sin afectar otros

**Ejemplo de uso completo:** Plataforma de e-commerce con microservicios: Usuario-Service (autenticación JWT), Producto-Service (catálogo), Carrito-Service (sesión), Pedido-Service (checkout), Pago-Service (Stripe), Inventario-Service (stock), Notificación-Service (emails/SMS). API Gateway enruta peticiones, Eureka para discovery, RabbitMQ para eventos, Zipkin para tracing, Kubernetes para orquestación.

### Patrones de diseño y arquitectura de microservicio

**Qué trata:** Soluciones probadas para problemas comunes en arquitecturas de microservicios.

**Patrones de descomposición:**

**1. Decompose by Business Capability:**

**Qué trata:** Dividir sistema según capacidades de negocio.

```
E-commerce:
├── Gestión de Usuarios (usuarios, autenticación)
├── Catálogo de Productos (productos, categorías, búsqueda)
├── Gestión de Pedidos (carritos, pedidos, checkout)
├── Pagos (procesamiento, validación)
├── Envíos (logística, tracking)
└── Notificaciones (email, SMS, push)
```

**2. Decompose by Subdomain (DDD):**

**Qué trata:** Usar Domain-Driven Design para identificar bounded contexts.

```
Banking:
├── Core Domain: Cuentas y Transacciones
├── Supporting: Autenticación, Notificaciones
└── Generic: Logging, Auditoría
```

**Patrones de datos:**

**1. Database per Service:**

```java
// Cada servicio tiene su propia BD
Usuario-Service → usuarios_db (PostgreSQL)
Pedido-Service  → pedidos_db (MySQL)
Producto-Service → productos_db (MongoDB)
```

**Problema:** Consultas que requieren datos de múltiples servicios

**Solución:** CQRS, API Composition, Event Sourcing

**2. Shared Database (Anti-pattern):**

**Qué es:** Múltiples servicios acceden misma BD
**Por qué evitar:** Acoplamiento fuerte, no escalable independientemente

**3. Saga Pattern:**

**Qué trata:** Gestionar transacciones distribuidas como secuencia de transacciones locales.

**Ejemplo - Crear pedido:**

```java
// Orchestration-based Saga
@Service
public class CrearPedidoSaga {
    
    public void ejecutar(PedidoDTO dto) {
        try {
            // 1. Reservar inventario
            inventarioService.reservar(dto.getProductoId(), dto.getCantidad());
            
            // 2. Procesar pago
            pagoService.procesarPago(dto.getPagoInfo());
            
            // 3. Crear pedido
            Pedido pedido = pedidoService.crear(dto);
            
            // 4. Enviar notificación
            notificacionService.enviarConfirmacion(pedido.getId());
            
        } catch (Exception e) {
            // Compensación: revertir cambios
            inventarioService.liberarReserva(dto.getProductoId(), dto.getCantidad());
            pagoService.reembolsar(dto.getPagoInfo());
            throw new SagaFailedException(e);
        }
    }
}
```

**Choreography-based Saga (eventos):**

```java
// Pedido-Service publica evento
@Service
public class PedidoService {
    
    @Transactional
    public Pedido crear(PedidoDTO dto) {
        Pedido pedido = pedidoRepository.save(new Pedido(dto));
        eventPublisher.publish(new PedidoCreatedEvent(pedido));
        return pedido;
    }
}

// Inventario-Service escucha y responde
@Service
public class InventarioEventListener {
    
    @EventListener
    public void onPedidoCreated(PedidoCreatedEvent evento) {
        try {
            inventarioRepository.reservar(evento.getProductoId(), evento.getCantidad());
            eventPublisher.publish(new InventarioReservadoEvent(evento.getPedidoId()));
        } catch (StockInsuficienteException e) {
            eventPublisher.publish(new InventarioReservaFallidaEvent(evento.getPedidoId()));
        }
    }
}

// Pedido-Service escucha resultado
@Service
public class PedidoEventListener {
    
    @EventListener
    public void onInventarioReservaFallida(InventarioReservaFallidaEvent evento) {
        // Cancelar pedido
        pedidoRepository.cancelar(evento.getPedidoId());
    }
}
```

**4. CQRS (Command Query Responsibility Segregation):**

**Qué trata:** Separar modelo de lectura (queries) del modelo de escritura (commands).

```java
// Command Side - Escritura
@Service
public class PedidoCommandService {
    
    @Autowired
    private PedidoWriteRepository writeRepo;
    
    @Autowired
    private EventPublisher eventPublisher;
    
    public void crearPedido(CreatePedidoCommand command) {
        Pedido pedido = new Pedido(command);
        writeRepo.save(pedido);
        eventPublisher.publish(new PedidoCreatedEvent(pedido));
    }
}

// Query Side - Lectura optimizada
@Service
public class PedidoQueryService {
    
    @Autowired
    private PedidoReadRepository readRepo;  // BD desnormalizada
    
    public PedidoView getPedido(Long id) {
        return readRepo.findPedidoView(id);  // Vista optimizada
    }
    
    public List<PedidoView> buscarPedidos(PedidoFilter filter) {
        return readRepo.findByFilter(filter);  // Índices optimizados
    }
}

// Event Handler actualiza vista de lectura
@Service
public class PedidoEventHandler {
    
    @Autowired
    private PedidoReadRepository readRepo;
    
    @EventListener
    public void onPedidoCreated(PedidoCreatedEvent evento) {
        PedidoView view = crearVista(evento);
        readRepo.save(view);
    }
}
```

**5. Event Sourcing:**

**Qué trata:** Almacenar cambios de estado como secuencia de eventos en lugar del estado actual.

```java
// Eventos
public class PedidoCreatedEvent {
    private Long pedidoId;
    private Long usuarioId;
    private List<LineaPedido> lineas;
    private LocalDateTime timestamp;
}

public class PedidoConfirmadoEvent {
    private Long pedidoId;
    private LocalDateTime timestamp;
}

public class PedidoEnviadoEvent {
    private Long pedidoId;
    private String trackingNumber;
    private LocalDateTime timestamp;
}

// Event Store
@Service
public class EventStore {
    
    @Autowired
    private EventRepository eventRepo;
    
    public void guardarEvento(DomainEvent evento) {
        eventRepo.save(evento);
    }
    
    public List<DomainEvent> getEventos(Long aggregateId) {
        return eventRepo.findByAggregateId(aggregateId);
    }
}

// Reconstruir estado desde eventos
@Service
public class PedidoService {
    
    public Pedido reconstruir(Long pedidoId) {
        List<DomainEvent> eventos = eventStore.getEventos(pedidoId);
        
        Pedido pedido = new Pedido();
        for (DomainEvent evento : eventos) {
            pedido.apply(evento);  // Aplicar cada evento
        }
        return pedido;
    }
}
```

**Patrones de integración:**

**1. API Gateway:**

**Qué trata:** Punto de entrada único para clientes.

**Responsabilidades:**
- Routing
- Autenticación/Autorización
- Rate limiting
- Caching
- Request/Response transformation
- Load balancing

```java
// Spring Cloud Gateway
@Configuration
public class GatewayConfig {
    
    @Bean
    public RouteLocator routes(RouteLocatorBuilder builder) {
        return builder.routes()
            // Autenticación requerida
            .route("usuarios", r -> r
                .path("/api/usuarios/**")
                .filters(f -> f
                    .filter(authFilter)
                    .retry(3)
                    .circuitBreaker(config -> config
                        .setName("usuariosCB")
                        .setFallbackUri("/fallback/usuarios")))
                .uri("lb://USUARIO-SERVICE"))
            
            // Rate limiting
            .route("productos", r -> r
                .path("/api/productos/**")
                .filters(f -> f
                    .requestRateLimiter(config -> config
                        .setRateLimiter(redisRateLimiter())
                        .setKeyResolver(userKeyResolver())))
                .uri("lb://PRODUCTO-SERVICE"))
            
            .build();
    }
}
```

**2. Backend for Frontend (BFF):**

**Qué trata:** API Gateway específico por tipo de cliente.

```
Mobile App  → Mobile BFF → Microservicios
Web App     → Web BFF    → Microservicios
Smart TV    → TV BFF     → Microservicios
```

**Ejemplo:**
```java
// Mobile BFF - respuestas ligeras
@RestController
@RequestMapping("/mobile/api")
public class MobileBFFController {
    
    @GetMapping("/home")
    public MobileHomeResponse getHome() {
        // Agregación de múltiples servicios
        Usuario usuario = usuarioService.getUsuario();
        List<Producto> destacados = productoService.getDestacados(5);  // Solo 5
        List<Pedido> recientes = pedidoService.getRecientes(3);
        
        return new MobileHomeResponse(usuario, destacados, recientes);
    }
}

// Web BFF - respuestas completas
@RestController
@RequestMapping("/web/api")
public class WebBFFController {
    
    @GetMapping("/home")
    public WebHomeResponse getHome() {
        Usuario usuario = usuarioService.getUsuario();
        List<Producto> destacados = productoService.getDestacados(20);  // Más productos
        List<Pedido> recientes = pedidoService.getRecientes(10);
        List<Recomendacion> recomendaciones = recomendacionService.get();
        
        return new WebHomeResponse(usuario, destacados, recientes, recomendaciones);
    }
}
```

**3. Service Mesh (Istio, Linkerd):**

**Qué trata:** Capa de infraestructura para gestionar comunicación entre servicios.

**Características:**
- Service discovery automático
- Load balancing
- Circuit breaking
- Retry logic
- Métricas y tracing
- Seguridad (mTLS)

**Patrones de resiliencia:**

**1. Circuit Breaker:**

```java
@Service
public class ProductoService {
    
    @CircuitBreaker(
        name = "inventarioService",
        fallbackMethod = "getInventarioFallback"
    )
    @Retry(name = "inventarioService", fallbackMethod = "getInventarioFallback")
    public Inventario getInventario(Long productoId) {
        return restTemplate.getForObject(
            "http://inventario-service/api/inventario/" + productoId,
            Inventario.class
        );
    }
    
    private Inventario getInventarioFallback(Long productoId, Exception ex) {
        // Retornar datos en caché
        return cacheService.getInventario(productoId)
            .orElse(new Inventario(productoId, 0, false));
    }
}
```

**2. Bulkhead:**

**Qué trata:** Aislar recursos para prevenir cascada de fallos.

```java
@Configuration
public class ThreadPoolConfig {
    
    @Bean(name = "usuarioThreadPool")
    public Executor usuarioThreadPool() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setCorePoolSize(10);
        executor.setMaxPoolSize(20);
        executor.setQueueCapacity(100);
        return executor;
    }
    
    @Bean(name = "productoThreadPool")
    public Executor productoThreadPool() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setCorePoolSize(20);
        executor.setMaxPoolSize(50);
        executor.setQueueCapacity(200);
        return executor;
    }
}

@Service
public class AggregationService {
    
    @Async("usuarioThreadPool")
    public CompletableFuture<Usuario> getUsuario(Long id) {
        return CompletableFuture.completedFuture(usuarioService.get(id));
    }
    
    @Async("productoThreadPool")
    public CompletableFuture<List<Producto>> getProductos() {
        return CompletableFuture.completedFuture(productoService.getAll());
    }
}
```

**3. Rate Limiting:**

```java
@Configuration
public class RateLimitConfig {
    
    @Bean
    public RedisRateLimiter redisRateLimiter() {
        return new RedisRateLimiter(
            10,   // replenishRate: tokens por segundo
            20    // burstCapacity: máximo de tokens
        );
    }
}
```

**Patrones de observabilidad:**

**1. Log Aggregation:**

**Herramientas:** ELK Stack (Elasticsearch, Logstash, Kibana)

```java
// Structured Logging
@Service
public class PedidoService {
    
    private static final Logger log = LoggerFactory.getLogger(PedidoService.class);
    
    public Pedido crear(PedidoDTO dto) {
        MDC.put("usuarioId", dto.getUsuarioId().toString());
        MDC.put("accion", "crear_pedido");
        
        log.info("Creando pedido para usuario {}", dto.getUsuarioId());
        
        try {
            Pedido pedido = pedidoRepository.save(new Pedido(dto));
            log.info("Pedido creado exitosamente: {}", pedido.getId());
            return pedido;
        } catch (Exception e) {
            log.error("Error al crear pedido", e);
            throw e;
        } finally {
            MDC.clear();
        }
    }
}
```

**2. Distributed Tracing:**

```yaml
# Spring Cloud Sleuth + Zipkin
spring:
  sleuth:
    sampler:
      probability: 1.0
  zipkin:
    base-url: http://zipkin:9411
```

**3. Health Check API:**

```java
@RestController
@RequestMapping("/actuator")
public class HealthController {
    
    @GetMapping("/health")
    public HealthStatus health() {
        return HealthStatus.builder()
            .status("UP")
            .database(checkDatabase())
            .externalServices(checkExternalServices())
            .build();
    }
}
```

**Patrones de deployment:**

**1. Blue-Green Deployment:**

```
Blue (v1.0)  ← 100% tráfico
Green (v1.1) ← 0% tráfico

Deploy completado y probado:
Blue (v1.0)  ← 0% tráfico
Green (v1.1) ← 100% tráfico (switch instantáneo)
```

**2. Canary Deployment:**

```
v1.0 ← 90% tráfico
v1.1 ← 10% tráfico (usuarios beta)

Si v1.1 OK:
v1.0 ← 50% tráfico
v1.1 ← 50% tráfico

Finalmente:
v1.1 ← 100% tráfico
```

**3. Rolling Deployment:**

```
Instancias: A, B, C, D (todas v1.0)

1. A → v1.1, B,C,D → v1.0
2. A,B → v1.1, C,D → v1.0
3. A,B,C → v1.1, D → v1.0
4. A,B,C,D → v1.1
```

**Ejemplo de uso completo:** Marketplace con Usuario-Service (autenticación), Vendedor-Service (gestión vendedores), Producto-Service (catálogo), Búsqueda-Service (Elasticsearch), Pedido-Service (orders), Pago-Service, Envío-Service. Usa Saga para crear pedido (reservar producto, procesar pago, crear envío). CQRS para búsquedas optimizadas. API Gateway para routing. Event Sourcing para auditoría. Circuit Breaker para resiliencia.

### Mecanismo de comunicación de microservicios (Orquestación y Coreografía)

**Qué trata:** Patrones para coordinar interacciones entre múltiples microservicios en procesos de negocio complejos.

**Orquestación (Orchestration):**

**Qué trata:** Controlador central (orchestrator) que coordina y gestiona todas las llamadas entre servicios.

**Características:**
- Control centralizado
- Flujo explícito y predecible
- Fácil de entender y debuggear
- Orchestrator conoce todo el proceso

**Ventajas:**
- Lógica de negocio centralizada
- Fácil seguimiento del flujo
- Debugging simplificado
- Control de errores centralizado
- Versionamiento de procesos más fácil

**Desventajas:**
- Punto único de fallo (orchestrator)
- Acoplamiento al orchestrator
- Orchestrator puede volverse complejo
- Latencia adicional (hub-and-spoke)

**Implementación con Spring:**

```java
// Orchestrator para proceso de crear pedido
@Service
@Slf4j
public class CrearPedidoOrchestrator {
    
    @Autowired
    private UsuarioServiceClient usuarioService;
    
    @Autowired
    private ProductoServiceClient productoService;
    
    @Autowired
    private InventarioServiceClient inventarioService;
    
    @Autowired
    private PagoServiceClient pagoService;
    
    @Autowired
    private PedidoRepository pedidoRepository;
    
    @Autowired
    private EnvioServiceClient envioService;
    
    @Autowired
    private NotificacionServiceClient notificacionService;
    
    @Transactional
    public PedidoResponse crearPedido(CrearPedidoRequest request) {
        log.info("Iniciando orquestación de pedido para usuario: {}", request.getUsuarioId());
        
        try {
            // Paso 1: Validar usuario
            log.info("Paso 1: Validando usuario");
            Usuario usuario = usuarioService.obtenerUsuario(request.getUsuarioId());
            if (!usuario.isActivo()) {
                throw new UsuarioInactivoException();
            }
            
            // Paso 2: Validar productos y obtener precios
            log.info("Paso 2: Validando productos");
            List<Producto> productos = new ArrayList<>();
            double total = 0.0;
            
            for (LineaPedidoRequest linea : request.getLineas()) {
                Producto producto = productoService.obtenerProducto(linea.getProductoId());
                if (!producto.isActivo()) {
                    throw new ProductoNoDisponibleException(producto.getId());
                }
                productos.add(producto);
                total += producto.getPrecio() * linea.getCantidad();
            }
            
            // Paso 3: Verificar y reservar inventario
            log.info("Paso 3: Reservando inventario");
            ReservaInventarioRequest reservaRequest = new ReservaInventarioRequest(request.getLineas());
            ReservaInventarioResponse reserva = inventarioService.reservar(reservaRequest);
            
            if (!reserva.isExitoso()) {
                throw new InventarioInsuficienteException(reserva.getProductosAgotados());
            }
            
            try {
                // Paso 4: Procesar pago
                log.info("Paso 4: Procesando pago de ${}", total);
                ProcesarPagoRequest pagoRequest = new ProcesarPagoRequest(
                    usuario.getId(),
                    request.getMetodoPago(),
                    total
                );
                PagoResponse pago = pagoService.procesar(pagoRequest);
                
                if (!pago.isAprobado()) {
                    // Compensación: liberar inventario
                    inventarioService.liberar(reserva.getReservaId());
                    throw new PagoRechazadoException(pago.getMotivoRechazo());
                }
                
                try {
                    // Paso 5: Crear pedido en BD
                    log.info("Paso 5: Guardando pedido");
                    Pedido pedido = new Pedido();
                    pedido.setUsuarioId(usuario.getId());
                    pedido.setTotal(total);
                    pedido.setPagoId(pago.getPagoId());
                    pedido.setEstado(EstadoPedido.CONFIRMADO);
                    pedido.setLineas(mapearLineas(request.getLineas(), productos));
                    
                    Pedido pedidoGuardado = pedidoRepository.save(pedido);
                    
                    // Paso 6: Crear envío (async, no crítico)
                    log.info("Paso 6: Creando envío");
                    try {
                        CrearEnvioRequest envioRequest = new CrearEnvioRequest(
                            pedidoGuardado.getId(),
                            usuario.getDireccion()
                        );
                        EnvioResponse envio = envioService.crear(envioRequest);
                        pedidoGuardado.setEnvioId(envio.getEnvioId());
                        pedidoRepository.save(pedidoGuardado);
                    } catch (Exception e) {
                        log.warn("Error al crear envío, se procesará después", e);
                        // No falla todo el proceso
                    }
                    
                    // Paso 7: Enviar notificaciones (async, fire-and-forget)
                    log.info("Paso 7: Enviando notificaciones");
                    CompletableFuture.runAsync(() -> {
                        try {
                            notificacionService.enviarConfirmacionPedido(
                                usuario.getEmail(),
                                pedidoGuardado.getId()
                            );
                        } catch (Exception e) {
                            log.error("Error al enviar notificación", e);
                        }
                    });
                    
                    log.info("Pedido creado exitosamente: {}", pedidoGuardado.getId());
                    
                    return PedidoResponse.builder()
                        .pedidoId(pedidoGuardado.getId())
                        .estado(pedidoGuardado.getEstado())
                        .total(pedidoGuardado.getTotal())
                        .build();
                    
                } catch (Exception e) {
                    // Compensación: reembolsar pago y liberar inventario
                    log.error("Error al guardar pedido, iniciando compensación", e);
                    pagoService.reembolsar(pago.getPagoId());
                    inventarioService.liberar(reserva.getReservaId());
                    throw e;
                }
                
            } catch (PagoException e) {
                // Compensación: liberar inventario
                log.error("Error en pago, liberando inventario", e);
                inventarioService.liberar(reserva.getReservaId());
                throw e;
            }
            
        } catch (Exception e) {
            log.error("Error en orquestación de pedido", e);
            throw new CrearPedidoException("Error al crear pedido: " + e.getMessage(), e);
        }
    }
}
```

**Feign Clients para comunicación:**

```java
@FeignClient(name = "usuario-service")
public interface UsuarioServiceClient {
    
    @GetMapping("/api/usuarios/{id}")
    Usuario obtenerUsuario(@PathVariable Long id);
}

@FeignClient(name = "inventario-service")
public interface InventarioServiceClient {
    
    @PostMapping("/api/inventario/reservar")
    ReservaInventarioResponse reservar(@RequestBody ReservaInventarioRequest request);
    
    @PostMapping("/api/inventario/liberar/{reservaId}")
    void liberar(@PathVariable String reservaId);
}

@FeignClient(name = "pago-service")
public interface PagoServiceClient {
    
    @PostMapping("/api/pagos/procesar")
    PagoResponse procesar(@RequestBody ProcesarPagoRequest request);
    
    @PostMapping("/api/pagos/reembolsar/{pagoId}")
    void reembolsar(@PathVariable String pagoId);
}
```

**Coreografía (Choreography):**

**Qué trata:** Servicios reaccionan a eventos publicados por otros servicios sin controlador central.

**Características:**
- Descentralizado
- Basado en eventos
- Servicios autónomos
- Acoplamiento débil

**Ventajas:**
- No hay punto único de fallo
- Bajo acoplamiento entre servicios
- Servicios independientes
- Escalabilidad mejorada
- Flexibilidad para agregar servicios

**Desventajas:**
- Flujo difícil de entender
- Debugging complejo
- No hay vista global del proceso
- Riesgo de ciclos de eventos
- Monitoreo más complejo

**Implementación con RabbitMQ:**

```java
// 1. Pedido-Service: Inicia el proceso publicando evento
@Service
@Slf4j
public class PedidoService {
    
    @Autowired
    private RabbitTemplate rabbitTemplate;
    
    @Autowired
    private PedidoRepository pedidoRepository;
    
    public Pedido iniciarPedido(CrearPedidoRequest request) {
        log.info("Iniciando creación de pedido");
        
        // Crear pedido en estado PENDING
        Pedido pedido = new Pedido();
        pedido.setUsuarioId(request.getUsuarioId());
        pedido.setLineas(request.getLineas());
        pedido.setEstado(EstadoPedido.PENDING);
        pedido.setTotal(calcularTotal(request.getLineas()));
        
        Pedido pedidoGuardado = pedidoRepository.save(pedido);
        
        // Publicar evento
        PedidoIniciadoEvent evento = PedidoIniciadoEvent.builder()
            .pedidoId(pedidoGuardado.getId())
            .usuarioId(request.getUsuarioId())
            .lineas(request.getLineas())
            .total(pedidoGuardado.getTotal())
            .timestamp(LocalDateTime.now())
            .build();
        
        rabbitTemplate.convertAndSend(
            "pedidos.exchange",
            "pedido.iniciado",
            evento
        );
        
        log.info("Evento PedidoIniciado publicado para pedido: {}", pedidoGuardado.getId());
        
        return pedidoGuardado;
    }
    
    // Listener: Reacciona a eventos de inventario
    @RabbitListener(queues = "pedido.inventario.queue")
    public void handleInventarioReservado(InventarioReservadoEvent evento) {
        log.info("Inventario reservado para pedido: {}", evento.getPedidoId());
        
        Pedido pedido = pedidoRepository.findById(evento.getPedidoId())
            .orElseThrow(() -> new PedidoNotFoundException(evento.getPedidoId()));
        
        pedido.setEstado(EstadoPedido.INVENTARIO_RESERVADO);
        pedido.setReservaId(evento.getReservaId());
        pedidoRepository.save(pedido);
        
        // Publicar siguiente evento
        InventarioConfirmadoEvent siguienteEvento = InventarioConfirmadoEvent.builder()
            .pedidoId(pedido.getId())
            .usuarioId(pedido.getUsuarioId())
            .total(pedido.getTotal())
            .build();
        
        rabbitTemplate.convertAndSend(
            "pedidos.exchange",
            "inventario.confirmado",
            siguienteEvento
        );
    }
    
    @RabbitListener(queues = "pedido.inventario.fallido.queue")
    public void handleInventarioFallido(InventarioFallidoEvent evento) {
        log.error("Inventario insuficiente para pedido: {}", evento.getPedidoId());
        
        Pedido pedido = pedidoRepository.findById(evento.getPedidoId())
            .orElseThrow(() -> new PedidoNotFoundException(evento.getPedidoId()));
        
        pedido.setEstado(EstadoPedido.CANCELADO);
        pedido.setMotivoCancel("Inventario insuficiente: " + evento.getProductosAgotados());
        pedidoRepository.save(pedido);
        
        // Publicar evento de cancelación
        PedidoCanceladoEvent cancelEvent = new PedidoCanceladoEvent(
            pedido.getId(),
            "Inventario insuficiente"
        );
        
        rabbitTemplate.convertAndSend(
            "pedidos.exchange",
            "pedido.cancelado",
            cancelEvent
        );
    }
    
    @RabbitListener(queues = "pedido.pago.queue")
    public void handlePagoCompletado(PagoCompletadoEvent evento) {
        log.info("Pago completado para pedido: {}", evento.getPedidoId());
        
        Pedido pedido = pedidoRepository.findById(evento.getPedidoId())
            .orElseThrow(() -> new PedidoNotFoundException(evento.getPedidoId()));
        
        pedido.setEstado(EstadoPedido.CONFIRMADO);
        pedido.setPagoId(evento.getPagoId());
        pedidoRepository.save(pedido);
        
        // Publicar evento de confirmación
        PedidoConfirmadoEvent confirmEvent = new PedidoConfirmadoEvent(
            pedido.getId(),
            pedido.getUsuarioId(),
            pedido.getLineas()
        );
        
        rabbitTemplate.convertAndSend(
            "pedidos.exchange",
            "pedido.confirmado",
            confirmEvent
        );
    }
    
    @RabbitListener(queues = "pedido.pago.fallido.queue")
    public void handlePagoFallido(PagoFallidoEvent evento) {
        log.error("Pago fallido para pedido: {}", evento.getPedidoId());
        
        Pedido pedido = pedidoRepository.findById(evento.getPedidoId())
            .orElseThrow(() -> new PedidoNotFoundException(evento.getPedidoId()));
        
        // Liberar inventario reservado
        LiberarInventarioEvent liberarEvent = new LiberarInventarioEvent(
            pedido.getReservaId()
        );
        
        rabbitTemplate.convertAndSend(
            "inventario.exchange",
            "inventario.liberar",
            liberarEvent
        );
        
        pedido.setEstado(EstadoPedido.CANCELADO);
        pedido.setMotivoCancel("Pago rechazado: " + evento.getMotivo());
        pedidoRepository.save(pedido);
    }
}

// 2. Inventario-Service: Reacciona a eventos de pedido
@Service
@Slf4j
public class InventarioEventListener {
    
    @Autowired
    private InventarioService inventarioService;
    
    @Autowired
    private RabbitTemplate rabbitTemplate;
    
    @RabbitListener(queues = "inventario.pedido.queue")
    public void handlePedidoIniciado(PedidoIniciadoEvent evento) {
        log.info("Procesando reserva de inventario para pedido: {}", evento.getPedidoId());
        
        try {
            // Intentar reservar inventario
            String reservaId = inventarioService.reservar(evento.getLineas());
            
            // Publicar éxito
            InventarioReservadoEvent successEvent = InventarioReservadoEvent.builder()
                .pedidoId(evento.getPedidoId())
                .reservaId(reservaId)
                .timestamp(LocalDateTime.now())
                .build();
            
            rabbitTemplate.convertAndSend(
                "inventario.exchange",
                "inventario.reservado",
                successEvent
            );
            
            log.info("Inventario reservado exitosamente: {}", reservaId);
            
        } catch (InventarioInsuficienteException e) {
            // Publicar fallo
            InventarioFallidoEvent failEvent = InventarioFallidoEvent.builder()
                .pedidoId(evento.getPedidoId())
                .productosAgotados(e.getProductosAgotados())
                .timestamp(LocalDateTime.now())
                .build();
            
            rabbitTemplate.convertAndSend(
                "inventario.exchange",
                "inventario.fallido",
                failEvent
            );
            
            log.error("Inventario insuficiente para pedido: {}", evento.getPedidoId());
        }
    }
    
    @RabbitListener(queues = "inventario.liberar.queue")
    public void handleLiberarInventario(LiberarInventarioEvent evento) {
        log.info("Liberando reserva de inventario: {}", evento.getReservaId());
        inventarioService.liberar(evento.getReservaId());
    }
}

// 3. Pago-Service: Reacciona a confirmación de inventario
@Service
@Slf4j
public class PagoEventListener {
    
    @Autowired
    private PagoService pagoService;
    
    @Autowired
    private RabbitTemplate rabbitTemplate;
    
    @RabbitListener(queues = "pago.pedido.queue")
    public void handleInventarioConfirmado(InventarioConfirmadoEvent evento) {
        log.info("Procesando pago para pedido: {}", evento.getPedidoId());
        
        try {
            // Procesar pago
            String pagoId = pagoService.procesar(
                evento.getUsuarioId(),
                evento.getTotal()
            );
            
            // Publicar éxito
            PagoCompletadoEvent successEvent = PagoCompletadoEvent.builder()
                .pedidoId(evento.getPedidoId())
                .pagoId(pagoId)
                .monto(evento.getTotal())
                .timestamp(LocalDateTime.now())
                .build();
            
            rabbitTemplate.convertAndSend(
                "pago.exchange",
                "pago.completado",
                successEvent
            );
            
            log.info("Pago procesado exitosamente: {}", pagoId);
            
        } catch (PagoRechazadoException e) {
            // Publicar fallo
            PagoFallidoEvent failEvent = PagoFallidoEvent.builder()
                .pedidoId(evento.getPedidoId())
                .motivo(e.getMessage())
                .timestamp(LocalDateTime.now())
                .build();
            
            rabbitTemplate.convertAndSend(
                "pago.exchange",
                "pago.fallido",
                failEvent
            );
            
            log.error("Pago rechazado para pedido: {}", evento.getPedidoId());
        }
    }
}

// 4. Envio-Service: Reacciona a pedido confirmado
@Service
@Slf4j
public class EnvioEventListener {
    
    @Autowired
    private EnvioService envioService;
    
    @RabbitListener(queues = "envio.pedido.queue")
    public void handlePedidoConfirmado(PedidoConfirmadoEvent evento) {
        log.info("Creando envío para pedido: {}", evento.getPedidoId());
        
        try {
            String envioId = envioService.crear(
                evento.getPedidoId(),
                evento.getLineas()
            );
            
            log.info("Envío creado: {}", envioId);
            
        } catch (Exception e) {
            log.error("Error al crear envío para pedido: {}", evento.getPedidoId(), e);
            // No publica evento de fallo, se reintentará
        }
    }
}

// 5. Notificacion-Service: Reacciona a pedido confirmado y cancelado
@Service
@Slf4j
public class NotificacionEventListener {
    
    @Autowired
    private NotificacionService notificacionService;
    
    @RabbitListener(queues = "notificacion.confirmado.queue")
    public void handlePedidoConfirmado(PedidoConfirmadoEvent evento) {
        log.info("Enviando notificación de confirmación para pedido: {}", evento.getPedidoId());
        notificacionService.enviarConfirmacion(evento.getUsuarioId(), evento.getPedidoId());
    }
    
    @RabbitListener(queues = "notificacion.cancelado.queue")
    public void handlePedidoCancelado(PedidoCanceladoEvent evento) {
        log.info("Enviando notificación de cancelación para pedido: {}", evento.getPedidoId());
        notificacionService.enviarCancelacion(evento.getPedidoId(), evento.getMotivo());
    }
}
```

**Configuración RabbitMQ:**

```java
@Configuration
public class RabbitMQConfig {
    
    // Exchanges
    @Bean
    public TopicExchange pedidosExchange() {
        return new TopicExchange("pedidos.exchange");
    }
    
    @Bean
    public TopicExchange inventarioExchange() {
        return new TopicExchange("inventario.exchange");
    }
    
    @Bean
    public TopicExchange pagoExchange() {
        return new TopicExchange("pago.exchange");
    }
    
    // Queues
    @Bean
    public Queue inventarioPedidoQueue() {
        return new Queue("inventario.pedido.queue", true);
    }
    
    @Bean
    public Queue pedidoInventarioQueue() {
        return new Queue("pedido.inventario.queue", true);
    }
    
    @Bean
    public Queue pagoPedidoQueue() {
        return new Queue("pago.pedido.queue", true);
    }
    
    // Bindings
    @Bean
    public Binding inventarioPedidoBinding() {
        return BindingBuilder
            .bind(inventarioPedidoQueue())
            .to(pedidosExchange())
            .with("pedido.iniciado");
    }
    
    @Bean
    public Binding pedidoInventarioBinding() {
        return BindingBuilder
            .bind(pedidoInventarioQueue())
            .to(inventarioExchange())
            .with("inventario.reservado");
    }
}
```

**Comparación Orquestación vs Coreografía:**

| Aspecto | Orquestación | Coreografía |
|---|---|---|
| **Control** | Centralizado | Descentralizado |
| **Complejidad** | Simple de entender | Complejo de trazar |
| **Acoplamiento** | Alto (al orchestrator) | Bajo (eventos) |
| **Punto de fallo** | Orchestrator | Distribuido |
| **Debugging** | Fácil | Difícil |
| **Escalabilidad** | Limitada por orchestrator | Alta |
| **Visibilidad** | Clara | Requiere herramientas |
| **Modificación** | Centralizada | Distribuida |
| **Mejor para** | Procesos críticos con pasos claros | Procesos flexibles y evolutivos |

**Ejemplo híbrido (recomendado):**

```java
// Orquestación para flujo crítico principal
@Service
public class PedidoOrchestrator {
    
    public PedidoResponse crearPedido(CrearPedidoRequest request) {
        // Orquestación sincrónica de pasos críticos
        validarUsuario(request.getUsuarioId());
        reservarInventario(request.getLineas());
        procesarPago(request.getPago());
        Pedido pedido = guardarPedido(request);
        
        // Coreografía para procesos secundarios
        publicarEventoPedidoCreado(pedido);  // Dispara envío, notificaciones, analytics
        
        return mapToResponse(pedido);
    }
}
```

**Ejemplo de uso completo:** Plataforma de viajes con reserva de vuelo+hotel. **Orquestación** para proceso crítico de reserva (verificar disponibilidad, procesar pago, confirmar reserva) con compensación automática si falla. **Coreografía** para procesos secundarios (enviar confirmación email, agregar puntos lealtad, generar factura, actualizar analytics) que reaccionan al evento `ReservaConfirmada` sin bloquear flujo principal.

