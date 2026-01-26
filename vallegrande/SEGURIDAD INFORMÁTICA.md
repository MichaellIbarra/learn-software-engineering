## SEGURIDAD INFORMÁTICA

**¿De qué trata?**
Disciplina que protege sistemas, redes y datos contra accesos no autorizados, modificaciones o destrucción.

**¿Por qué se utiliza?**
- Proteger información sensible y activos digitales
- Garantizar continuidad del negocio
- Cumplir normativas legales (GDPR, ISO 27001)
- Prevenir pérdidas económicas y reputacionales

**Ventajas/Beneficios:**
- Reducción de riesgos cibernéticos
- Confianza de clientes y usuarios
- Protección de propiedad intelectual
- Cumplimiento legal y regulatorio

**Desventajas:**
- Costos de implementación elevados
- Requiere actualización constante
- Puede afectar la usabilidad del sistema
- Necesita personal especializado

**Ciclo de vida:**
1. Identificación de activos
2. Evaluación de riesgos
3. Implementación de controles
4. Monitoreo continuo
5. Respuesta a incidentes
6. Mejora continua

---

### Pilares AAA, Triada CID, Eventos, Ataques e Incidentes

**¿De qué trata?**
Fundamentos esenciales de la seguridad informática que establecen los principios de protección y gestión de accesos.

**Pilares AAA:**
- **Autenticación (Authentication):** Verificar la identidad del usuario
- **Autorización (Authorization):** Determinar permisos y accesos
- **Auditoría (Accounting):** Registrar actividades para trazabilidad

**Triada CID:**
- **Confidencialidad:** Solo usuarios autorizados acceden a la información
- **Integridad:** Los datos no son alterados sin autorización
- **Disponibilidad:** Información accesible cuando se necesita

**¿Por qué se utiliza?**
- Establecer marco de trabajo en seguridad
- Garantizar control de accesos efectivo
- Mantener trazabilidad de operaciones

**Eventos, Ataques e Incidentes:**
- **Evento:** Cualquier acción observable en el sistema
- **Ataque:** Intento deliberado de comprometer la seguridad
- **Incidente:** Evento que afecta la seguridad del sistema

**Ejemplo de uso:**
- Login con usuario/contraseña (Autenticación)
- Verificar permisos de lectura/escritura (Autorización)
- Registrar accesos en logs (Auditoría)

**Ventajas:**
- Control granular de accesos
- Trazabilidad completa
- Detección temprana de amenazas

**Desventajas:**
- Complejidad en la implementación
- Overhead en rendimiento
- Requiere gestión continua de logs

---

### Criptografía, mecanismos de cifrado simétrico y asimétrico

**¿De qué trata?**
Ciencia de proteger información mediante transformación de datos en formato ilegible sin la clave correcta.

**Cifrado Simétrico:**
- Usa la **misma clave** para cifrar y descifrar
- Algoritmos: AES, DES, 3DES, Blowfish
- Rápido y eficiente para grandes volúmenes

**Cifrado Asimétrico:**
- Usa **par de claves**: pública y privada
- Algoritmos: RSA, ECC, DSA
- Más lento pero más seguro para intercambio de claves

**¿Por qué se utiliza?**
- Proteger datos en tránsito y en reposo
- Garantizar confidencialidad
- Firmar digitalmente documentos
- Autenticar usuarios y sistemas

**Ventajas:**
- **Simétrico:** Rápido, bajo consumo de recursos
- **Asimétrico:** No requiere intercambio previo de clave secreta, ideal para firma digital

**Desventajas:**
- **Simétrico:** Distribución segura de claves es complejo
- **Asimétrico:** Más lento, mayor consumo de recursos

**Ejemplo de uso:**
- **Simétrico:** Cifrar disco duro completo (BitLocker, AES-256)
- **Asimétrico:** HTTPS, SSL/TLS, firmas digitales
- **Híbrido:** TLS usa asimétrico para intercambiar clave simétrica

**Ciclo de ejecución (TLS):**
1. Cliente solicita conexión segura
2. Servidor envía certificado (clave pública)
3. Cliente genera clave simétrica y la cifra con clave pública
4. Servidor descifra con clave privada
5. Comunicación continúa con cifrado simétrico

---

### Tecnologías de Vulnerabilidades

**¿De qué trata?**
Herramientas y metodologías para identificar, evaluar y gestionar debilidades en sistemas de información.

**Conceptos clave:**
- **Vulnerabilidad:** Debilidad explotable en el sistema
- **Exploit:** Código que aprovecha una vulnerabilidad
- **CVE:** Common Vulnerabilities and Exposures (registro público)
- **CVSS:** Sistema de puntuación de severidad (0-10)

**¿Por qué se utiliza?**
- Identificar puntos débiles antes que los atacantes
- Priorizar remediaciónes según criticidad
- Cumplir con políticas de seguridad
- Reducir superficie de ataque

**Herramientas principales:**
- **Escaners:** Nessus, OpenVAS, Qualys
- **Pentesting:** Metasploit, Burp Suite, OWASP ZAP
- **SAST:** Análisis estático (SonarQube, Checkmarx)
- **DAST:** Análisis dinámico (Acunetix, Veracode)

**Ventajas:**
- Detección proactiva de vulnerabilidades
- Reportes detallados y priorizados
- Automatización de escaneos
- Base de datos actualizada (CVE)

**Desventajas:**
- Falsos positivos frecuentes
- Requiere interpretación experta
- Puede afectar rendimiento en producción
- Licencias costosas

**Ciclo de vida:**
1. **Descubrimiento:** Escaneo de activos
2. **Análisis:** Validación de vulnerabilidades
3. **Priorización:** Según CVSS y contexto
4. **Remediación:** Parcheo o mitigación
5. **Verificación:** Re-escaneo
6. **Monitoreo:** Vigilancia continua

**Ejemplo de uso:**
- Escaneo semanal con Nessus en servidores web
- Identificación de Apache con CVE-2021-44228 (Log4Shell)
- Priorización: CVSS 10.0 (Crítico)
- Remediación: Actualizar a versión parcheada
- Verificación: Re-escaneo confirma corrección

---

### Securización de Microservicios, estándares, buenas prácticas y herramientas

**¿De qué trata?**
Estrategias y tecnologías para proteger arquitecturas distribuidas basadas en microservicios.

**¿Por qué se utiliza?**
- Arquitecturas modernas son más complejas
- Mayor superficie de ataque (múltiples servicios)
- Comunicación entre servicios requiere protección
- Cumplir con Zero Trust Architecture

**Estándares y protocolos:**
- **OAuth 2.0:** Autorización delegada
- **OpenID Connect:** Autenticación sobre OAuth
- **JWT (JSON Web Tokens):** Tokens de sesión
- **mTLS (Mutual TLS):** Autenticación bidireccional
- **API Gateway:** Punto único de entrada

**Buenas prácticas:**
1. **Autenticación/Autorización:** Implementar en cada servicio
2. **Principio de mínimo privilegio:** Solo permisos necesarios
3. **Cifrado en tránsito:** TLS 1.3 para todas las comunicaciones
4. **Secrets Management:** Vault, AWS Secrets Manager
5. **Rate Limiting:** Prevenir DDoS y abuso
6. **Logging centralizado:** ELK Stack, Splunk
7. **Service Mesh:** Istio, Linkerd para seguridad en capa de red
8. **Container Security:** Escaneo de imágenes, políticas de ejecución

**Herramientas:**
- **API Gateway:** Kong, AWS API Gateway, Nginx
- **Service Mesh:** Istio, Linkerd, Consul
- **Secrets:** HashiCorp Vault, AWS Secrets Manager
- **Monitoreo:** Prometheus, Grafana, Jaeger
- **Container Security:** Aqua Security, Twistlock, Clair

**Ventajas:**
- Aislamiento de fallos de seguridad
- Escalabilidad de políticas
- Visibilidad completa del tráfico
- Automatización de seguridad

**Desventajas:**
- Complejidad operacional aumentada
- Latencia adicional (service mesh)
- Curva de aprendizaje pronunciada
- Costos de infraestructura

**Ejemplo de uso (E-commerce):**
```
1. Cliente → API Gateway (autenticación JWT)
2. API Gateway → Servicio Catálogo (mTLS)
3. Servicio Catálogo → Base de Datos (cifrado)
4. Logs → Sistema Centralizado (SIEM)
```

**Ciclo de ejecución (OAuth + JWT):**
1. Usuario inicia sesión en Auth Service
2. Auth Service valida credenciales
3. Genera JWT firmado (expiración 15 min)
4. Cliente envía JWT en cada petición
5. API Gateway valida firma y expiración
6. Autoriza acceso según claims del token
7. Servicio procesa solicitud
8. Refresh token para renovar sesión