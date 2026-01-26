## CLOUD COMPUTING

**Introducción:** Modelo de entrega de recursos computacionales (servidores, almacenamiento, bases de datos, redes, software) a través de internet con pago por uso.

**Por qué se utiliza:** Eliminar inversión en infraestructura física, escalabilidad bajo demanda, reducir costos operativos, acceso global, alta disponibilidad.

**Ventajas:**
- Escalabilidad elástica (escalar arriba/abajo según demanda)
- Pago por uso (sin inversión inicial)
- Alta disponibilidad y redundancia
- Acceso global desde cualquier lugar
- Actualizaciones automáticas
- Recuperación ante desastres

**Desventajas:**
- Dependencia de conexión internet
- Costos pueden crecer sin control
- Seguridad y privacidad de datos
- Vendor lock-in (dependencia del proveedor)
- Latencia de red
- Menos control sobre infraestructura

### Fundamentos de cloud computing

**Qué trata:** Conceptos base de computación en la nube, modelos de servicio y despliegue.

**Modelos de servicio:**

**1. IaaS (Infrastructure as a Service):**

**Qué trata:** Proveedor ofrece infraestructura virtualizada (VMs, almacenamiento, redes).

**Características:**
- Control total sobre VMs
- Gestión de OS y aplicaciones
- Máxima flexibilidad

**Ejemplos:**
- Amazon EC2 (Elastic Compute Cloud)
- Google Compute Engine
- Azure Virtual Machines

**Responsabilidad del usuario:**
- Sistema operativo
- Middleware
- Runtime
- Aplicaciones
- Datos

**Ejemplo de uso:**
```bash
# Crear VM en AWS EC2
aws ec2 run-instances \
  --image-id ami-0c55b159cbfafe1f0 \
  --instance-type t2.micro \
  --key-name mi-key \
  --security-group-ids sg-903004f8 \
  --subnet-id subnet-6e7f829e
```

**2. PaaS (Platform as a Service):**

**Qué trata:** Plataforma para desarrollar, ejecutar y gestionar aplicaciones sin infraestructura.

**Características:**
- Enfoque en desarrollo
- Escalado automático
- Integración CI/CD

**Ejemplos:**
- Heroku
- Google App Engine
- Azure App Service
- AWS Elastic Beanstalk

**Responsabilidad del usuario:**
- Aplicaciones
- Datos

**Ejemplo de uso:**
```bash
# Deploy en Heroku
git push heroku main
heroku ps:scale web=3  # Escalar a 3 instancias
```

**3. SaaS (Software as a Service):**

**Qué trata:** Software completo entregado por internet, listo para usar.

**Características:**
- Sin instalación
- Acceso vía navegador
- Actualizaciones automáticas

**Ejemplos:**
- Gmail, Google Workspace
- Microsoft 365
- Salesforce
- Dropbox, Slack

**Responsabilidad del usuario:**
- Datos y configuración

**Modelos de despliegue:**

**1. Nube Pública:**
- Infraestructura compartida
- Propiedad del proveedor
- Ejemplos: AWS, Azure, GCP
- **Ventaja:** Bajo costo, sin mantenimiento
- **Desventaja:** Menos control, seguridad compartida

**2. Nube Privada:**
- Infraestructura dedicada a una organización
- On-premise o hosted
- Ejemplos: VMware vCloud, OpenStack
- **Ventaja:** Control total, mayor seguridad
- **Desventaja:** Costo alto, gestión compleja

**3. Nube Híbrida:**
- Combinación de pública y privada
- Datos sensibles en privada, workloads en pública
- **Ventaja:** Flexibilidad, optimización de costos
- **Desventaja:** Complejidad de gestión

**4. Multi-Cloud:**
- Uso de múltiples proveedores cloud
- Evita vendor lock-in
- **Ventaja:** Redundancia, mejores precios
- **Desventaja:** Gestión compleja

**Características clave de cloud:**

**1. On-demand self-service:**
Provisionar recursos automáticamente sin intervención humana

**2. Broad network access:**
Acceso desde cualquier dispositivo vía internet

**3. Resource pooling:**
Recursos compartidos entre múltiples usuarios

**4. Rapid elasticity:**
Escalar recursos rápidamente según demanda

**5. Measured service:**
Pago basado en uso medido (pay-as-you-go)

**Conceptos importantes:**

**Regiones y Zonas de disponibilidad:**
```
Región (us-east-1)
  ├── Zona de Disponibilidad A (us-east-1a) - Data Center 1
  ├── Zona de Disponibilidad B (us-east-1b) - Data Center 2
  └── Zona de Disponibilidad C (us-east-1c) - Data Center 3
```

**Alta disponibilidad:**
- Desplegar en múltiples zonas
- Load balancing
- Auto-scaling
- Backups automáticos

**Elasticidad:**
```
Carga baja:  2 instancias
Carga media: 5 instancias (escala arriba)
Carga alta:  10 instancias (escala arriba)
Carga baja:  2 instancias (escala abajo)
```

**Ejemplo de uso completo:** E-commerce con frontend en S3 + CloudFront (CDN), backend en EC2 con auto-scaling, base de datos en RDS (multi-AZ), archivos de productos en S3, cache en ElastiCache, deploy en múltiples regiones para baja latencia global.

### Fundamentos de la nube de AWS

**Qué trata:** Amazon Web Services - proveedor líder de servicios cloud con más de 200 servicios.

**Por qué se utiliza:** Mayor cuota de mercado, servicios maduros, documentación extensa, comunidad grande, certificaciones reconocidas.

**Servicios principales:**

**1. EC2 (Elastic Compute Cloud):**

**Qué trata:** Servidores virtuales escalables en la nube.

**Tipos de instancias:**
- **t2/t3:** Propósito general, burstable (desarrollo, sitios web pequeños)
- **m5/m6:** Propósito general balanceado (aplicaciones empresariales)
- **c5/c6:** Optimizadas para cómputo (procesamiento batch, gaming)
- **r5/r6:** Optimizadas para memoria (bases de datos, cache)
- **p3/p4:** GPU (machine learning, rendering)

**Crear instancia EC2:**

```bash
# Via AWS CLI
aws ec2 run-instances \
  --image-id ami-0c55b159cbfafe1f0 \
  --instance-type t2.micro \
  --key-name mi-keypair \
  --security-group-ids sg-903004f8 \
  --subnet-id subnet-6e7f829e \
  --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=MiServidor}]'

# Conectar por SSH
ssh -i mi-keypair.pem ec2-user@<IP-PUBLICA>
```

**Puertos comunes:**
- **22:** SSH (Linux)
- **3389:** RDP (Windows)
- **80:** HTTP
- **443:** HTTPS
- **3306:** MySQL
- **5432:** PostgreSQL
- **27017:** MongoDB

**Grupos de seguridad (Security Groups):**

```bash
# Crear grupo de seguridad
aws ec2 create-security-group \
  --group-name mi-web-sg \
  --description "Seguridad para servidor web"

# Permitir SSH (puerto 22)
aws ec2 authorize-security-group-ingress \
  --group-id sg-903004f8 \
  --protocol tcp \
  --port 22 \
  --cidr 0.0.0.0/0

# Permitir HTTP (puerto 80)
aws ec2 authorize-security-group-ingress \
  --group-id sg-903004f8 \
  --protocol tcp \
  --port 80 \
  --cidr 0.0.0.0/0

# Permitir HTTPS (puerto 443)
aws ec2 authorize-security-group-ingress \
  --group-id sg-903004f8 \
  --protocol tcp \
  --port 443 \
  --cidr 0.0.0.0/0

# Permitir rango de puertos (ej: 8000-9000)
aws ec2 authorize-security-group-ingress \
  --group-id sg-903004f8 \
  --protocol tcp \
  --port 8000-9000 \
  --cidr 10.0.0.0/16
```

**IPs en EC2:**
- **IP Privada:** 10.0.1.x, 172.31.x.x (solo dentro de VPC)
- **IP Pública:** Asignada automáticamente, cambia al reiniciar
- **Elastic IP:** IP pública estática que persiste

```bash
# Asignar Elastic IP
aws ec2 allocate-address --domain vpc
aws ec2 associate-address \
  --instance-id i-1234567890abcdef0 \
  --allocation-id eipalloc-64d5890a
```

**2. S3 (Simple Storage Service):**

**Qué trata:** Almacenamiento de objetos escalable, duradero y de bajo costo.

**Características:**
- Almacenamiento ilimitado
- Durabilidad 99.999999999% (11 nueves)
- Versionamiento
- Cifrado
- Control de acceso

**Crear bucket y subir archivos:**

```bash
# Crear bucket
aws s3 mb s3://mi-bucket-unico-123

# Subir archivo
aws s3 cp archivo.txt s3://mi-bucket-unico-123/

# Subir carpeta recursivamente
aws s3 sync ./mi-carpeta s3://mi-bucket-unico-123/carpeta/

# Listar objetos
aws s3 ls s3://mi-bucket-unico-123/

# Descargar archivo
aws s3 cp s3://mi-bucket-unico-123/archivo.txt ./

# Hacer bucket público (website)
aws s3 website s3://mi-bucket-unico-123/ \
  --index-document index.html \
  --error-document error.html
```

**Clases de almacenamiento:**
- **S3 Standard:** Acceso frecuente
- **S3 Intelligent-Tiering:** Optimización automática
- **S3 Standard-IA:** Acceso infrecuente
- **S3 Glacier:** Archivado (retrieval en minutos/horas)
- **S3 Glacier Deep Archive:** Archivado largo plazo (retrieval en 12 horas)

**3. RDS (Relational Database Service):**

**Qué trata:** Bases de datos relacionales administradas.

**Motores soportados:**
- MySQL (puerto 3306)
- PostgreSQL (puerto 5432)
- MariaDB (puerto 3306)
- Oracle (puerto 1521)
- SQL Server (puerto 1433)
- Aurora (compatible MySQL/PostgreSQL)

**Crear base de datos RDS:**

```bash
# Crear instancia MySQL
aws rds create-db-instance \
  --db-instance-identifier mi-mysql \
  --db-instance-class db.t3.micro \
  --engine mysql \
  --engine-version 8.0.28 \
  --master-username admin \
  --master-user-password MiPassword123 \
  --allocated-storage 20 \
  --vpc-security-group-ids sg-12345678 \
  --availability-zone us-east-1a \
  --backup-retention-period 7 \
  --multi-az

# Obtener endpoint
aws rds describe-db-instances \
  --db-instance-identifier mi-mysql \
  --query 'DBInstances[0].Endpoint.Address' \
  --output text
```

**Conectar desde EC2:**

```bash
# Habilitar acceso en Security Group de RDS
# Permitir puerto 3306 desde Security Group de EC2

# Conectar
mysql -h mi-mysql.c9akciq32.us-east-1.rds.amazonaws.com \
      -P 3306 \
      -u admin \
      -p
```

**Multi-AZ vs Read Replicas:**
- **Multi-AZ:** Alta disponibilidad (failover automático)
- **Read Replicas:** Escalado de lectura (hasta 5 réplicas)

**4. VPC (Virtual Private Cloud):**

**Qué trata:** Red privada virtual aislada en AWS.

**Componentes:**
- **CIDR Block:** Rango de IPs (ej: 10.0.0.0/16)
- **Subnets:** Subredes públicas/privadas
- **Route Tables:** Tablas de enrutamiento
- **Internet Gateway:** Acceso a internet
- **NAT Gateway:** Salida a internet desde subnet privada
- **Security Groups:** Firewall a nivel de instancia
- **Network ACLs:** Firewall a nivel de subnet

**Crear VPC:**

```bash
# Crear VPC
aws ec2 create-vpc --cidr-block 10.0.0.0/16

# Crear subnet pública
aws ec2 create-subnet \
  --vpc-id vpc-12345678 \
  --cidr-block 10.0.1.0/24 \
  --availability-zone us-east-1a

# Crear subnet privada
aws ec2 create-subnet \
  --vpc-id vpc-12345678 \
  --cidr-block 10.0.2.0/24 \
  --availability-zone us-east-1a

# Crear Internet Gateway
aws ec2 create-internet-gateway
aws ec2 attach-internet-gateway \
  --vpc-id vpc-12345678 \
  --internet-gateway-id igw-12345678

# Crear tabla de rutas para subnet pública
aws ec2 create-route-table --vpc-id vpc-12345678
aws ec2 create-route \
  --route-table-id rtb-12345678 \
  --destination-cidr-block 0.0.0.0/0 \
  --gateway-id igw-12345678
```

**Arquitectura típica:**
```
VPC (10.0.0.0/16)
├── Subnet Pública (10.0.1.0/24)
│   ├── Internet Gateway
│   ├── Load Balancer
│   └── Bastion Host
└── Subnet Privada (10.0.2.0/24)
    ├── EC2 App Servers
    ├── RDS Database
    └── NAT Gateway (para salida a internet)
```

**5. ELB (Elastic Load Balancing):**

**Qué trata:** Distribuir tráfico entre múltiples instancias.

**Tipos:**
- **Application Load Balancer (ALB):** HTTP/HTTPS, Layer 7
- **Network Load Balancer (NLB):** TCP/UDP, Layer 4, ultra baja latencia
- **Classic Load Balancer (CLB):** Legacy

**Crear ALB:**

```bash
# Crear Application Load Balancer
aws elbv2 create-load-balancer \
  --name mi-alb \
  --subnets subnet-12345678 subnet-87654321 \
  --security-groups sg-12345678

# Crear Target Group
aws elbv2 create-target-group \
  --name mi-targets \
  --protocol HTTP \
  --port 80 \
  --vpc-id vpc-12345678 \
  --health-check-path /health

# Registrar instancias
aws elbv2 register-targets \
  --target-group-arn arn:aws:elasticloadbalancing:... \
  --targets Id=i-1234567890abcdef0 Id=i-0987654321fedcba0

# Crear Listener
aws elbv2 create-listener \
  --load-balancer-arn arn:aws:elasticloadbalancing:... \
  --protocol HTTP \
  --port 80 \
  --default-actions Type=forward,TargetGroupArn=arn:...
```

**Puertos comunes en ALB:**
- **80:** HTTP
- **443:** HTTPS
- **Health Check:** Configurable (ej: /health en puerto 80)

**6. Auto Scaling:**

**Qué trata:** Escalar automáticamente instancias EC2 según demanda.

```bash
# Crear Launch Template
aws ec2 create-launch-template \
  --launch-template-name mi-template \
  --version-description v1 \
  --launch-template-data '{
    "ImageId": "ami-0c55b159cbfafe1f0",
    "InstanceType": "t2.micro",
    "KeyName": "mi-key",
    "SecurityGroupIds": ["sg-903004f8"]
  }'

# Crear Auto Scaling Group
aws autoscaling create-auto-scaling-group \
  --auto-scaling-group-name mi-asg \
  --launch-template LaunchTemplateName=mi-template,Version='$Latest' \
  --min-size 2 \
  --max-size 10 \
  --desired-capacity 2 \
  --vpc-zone-identifier "subnet-12345,subnet-67890" \
  --target-group-arns arn:aws:elasticloadbalancing:...

# Crear política de escalado (basada en CPU)
aws autoscaling put-scaling-policy \
  --auto-scaling-group-name mi-asg \
  --policy-name scale-up \
  --policy-type TargetTrackingScaling \
  --target-tracking-configuration '{
    "PredefinedMetricSpecification": {
      "PredefinedMetricType": "ASGAverageCPUUtilization"
    },
    "TargetValue": 70.0
  }'
```

**7. Lambda:**

**Qué trata:** Ejecutar código sin provisionar servidores (serverless).

**Características:**
- Pago por ejecución (milisegundos)
- Escala automáticamente
- Soporta: Node.js, Python, Java, Go, C#, Ruby

```bash
# Crear función Lambda (Python)
# archivo: lambda_function.py
def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': 'Hola desde Lambda!'
    }

# Crear función
zip function.zip lambda_function.py

aws lambda create-function \
  --function-name mi-funcion \
  --runtime python3.9 \
  --role arn:aws:iam::123456789012:role/lambda-role \
  --handler lambda_function.lambda_handler \
  --zip-file fileb://function.zip

# Invocar función
aws lambda invoke \
  --function-name mi-funcion \
  --payload '{"key": "value"}' \
  output.txt
```

**Triggers comunes:**
- API Gateway (HTTP requests)
- S3 (nuevo objeto)
- DynamoDB Streams
- EventBridge (cron jobs)
- SQS/SNS (mensajes)

**8. IAM (Identity and Access Management):**

**Qué trata:** Gestión de acceso y permisos en AWS.

**Componentes:**
- **Users:** Usuarios individuales
- **Groups:** Conjunto de usuarios
- **Roles:** Permisos temporales para servicios
- **Policies:** Documentos JSON con permisos

```bash
# Crear usuario
aws iam create-user --user-name juan

# Crear grupo
aws iam create-group --group-name desarrolladores

# Agregar usuario a grupo
aws iam add-user-to-group \
  --user-name juan \
  --group-name desarrolladores

# Adjuntar política a grupo
aws iam attach-group-policy \
  --group-name desarrolladores \
  --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess

# Crear política personalizada
aws iam create-policy \
  --policy-name MiPolitica \
  --policy-document '{
    "Version": "2012-10-17",
    "Statement": [{
      "Effect": "Allow",
      "Action": ["s3:GetObject", "s3:PutObject"],
      "Resource": "arn:aws:s3:::mi-bucket/*"
    }]
  }'
```

**9. CloudWatch:**

**Qué trata:** Monitoreo y observabilidad de recursos AWS.

```bash
# Ver métricas de EC2
aws cloudwatch get-metric-statistics \
  --namespace AWS/EC2 \
  --metric-name CPUUtilization \
  --dimensions Name=InstanceId,Value=i-1234567890abcdef0 \
  --start-time 2025-01-25T00:00:00Z \
  --end-time 2025-01-25T23:59:59Z \
  --period 3600 \
  --statistics Average

# Crear alarma
aws cloudwatch put-metric-alarm \
  --alarm-name cpu-alta \
  --alarm-description "CPU > 80%" \
  --metric-name CPUUtilization \
  --namespace AWS/EC2 \
  --statistic Average \
  --period 300 \
  --threshold 80 \
  --comparison-operator GreaterThanThreshold \
  --evaluation-periods 2

# Ver logs
aws logs tail /aws/lambda/mi-funcion --follow
```

**10. Route 53:**

**Qué trata:** Servicio de DNS escalable.

```bash
# Crear zona hospedada
aws route53 create-hosted-zone \
  --name ejemplo.com \
  --caller-reference $(date +%s)

# Crear registro A (apuntar a IP)
aws route53 change-resource-record-sets \
  --hosted-zone-id Z123456789 \
  --change-batch '{
    "Changes": [{
      "Action": "CREATE",
      "ResourceRecordSet": {
        "Name": "www.ejemplo.com",
        "Type": "A",
        "TTL": 300,
        "ResourceRecords": [{"Value": "54.123.45.67"}]
      }
    }]
  }'

# Crear alias a Load Balancer
# Type: A, Alias: true, Target: ALB DNS name
```

**Arquitectura completa en AWS:**

```
Usuario
  ↓
Route 53 (DNS)
  ↓
CloudFront (CDN)
  ↓
Application Load Balancer (ALB)
  ↓
Auto Scaling Group
  ├── EC2 (us-east-1a) - 10.0.1.10
  ├── EC2 (us-east-1b) - 10.0.2.10
  └── EC2 (us-east-1c) - 10.0.3.10
  ↓
RDS Multi-AZ (Primary: us-east-1a, Standby: us-east-1b)
  ↓
S3 (archivos estáticos)
ElastiCache (cache Redis)
CloudWatch (monitoreo)
Lambda (procesamiento async)
```

**Ejemplo de uso completo:** Aplicación web de comercio electrónico en AWS. Frontend en S3 + CloudFront, backend en EC2 con Auto Scaling detrás de ALB, base de datos RDS MySQL Multi-AZ, imágenes en S3, cache Redis en ElastiCache, Lambda para procesar pedidos asincrónicamente, CloudWatch para monitoreo, Route 53 para DNS, todo dentro de VPC con subnets públicas y privadas en múltiples AZs.

### Configuración de MV en Google Cloud Platform

**Qué trata:** Crear y gestionar máquinas virtuales en Google Cloud Platform (GCP).

**Por qué se utiliza:** Infraestructura de Google, innovación en Kubernetes, BigQuery, precios competitivos, red global privada de Google.

**Servicios principales de GCP:**

**1. Compute Engine (VMs):**

**Qué trata:** Máquinas virtuales escalables en infraestructura de Google.

**Tipos de máquinas:**
- **e2:** Económicas, uso general
- **n1/n2:** Propósito general
- **c2:** Optimizadas para cómputo
- **m1/m2:** Optimizadas para memoria
- **a2:** GPU para ML

**Crear VM con gcloud CLI:**

```bash
# Instalar gcloud CLI
curl https://sdk.cloud.google.com | bash
gcloud init

# Configurar proyecto
gcloud config set project mi-proyecto-123

# Listar zonas disponibles
gcloud compute zones list

# Crear VM
gcloud compute instances create mi-vm \
  --zone=us-central1-a \
  --machine-type=e2-medium \
  --image-family=debian-11 \
  --image-project=debian-cloud \
  --boot-disk-size=10GB \
  --tags=http-server,https-server

# Crear VM con script de inicio
gcloud compute instances create web-server \
  --zone=us-central1-a \
  --machine-type=e2-micro \
  --image-family=ubuntu-2004-lts \
  --image-project=ubuntu-os-cloud \
  --metadata=startup-script='#!/bin/bash
    apt-get update
    apt-get install -y nginx
    systemctl start nginx
    echo "Hola desde GCP" > /var/www/html/index.html'

# Listar VMs
gcloud compute instances list

# Ver detalles de VM
gcloud compute instances describe mi-vm --zone=us-central1-a

# SSH a la VM
gcloud compute ssh mi-vm --zone=us-central1-a

# Detener VM
gcloud compute instances stop mi-vm --zone=us-central1-a

# Iniciar VM
gcloud compute instances start mi-vm --zone=us-central1-a

# Eliminar VM
gcloud compute instances delete mi-vm --zone=us-central1-a
```

**IPs en GCP:**

```bash
# IP efímera (cambia al reiniciar)
# Asignada automáticamente

# Reservar IP estática (externa)
gcloud compute addresses create mi-ip-estatica --region=us-central1

# Listar IPs estáticas
gcloud compute addresses list

# Asignar IP estática a VM
gcloud compute instances delete-access-config mi-vm \
  --access-config-name="external-nat" \
  --zone=us-central1-a

gcloud compute instances add-access-config mi-vm \
  --access-config-name="external-nat" \
  --address=35.123.45.67 \
  --zone=us-central1-a

# IP interna: 10.128.0.x (automática en VPC)
```

**2. Firewall Rules (Reglas de firewall):**

**Qué trata:** Controlar tráfico de entrada/salida a VMs.

```bash
# Crear regla para permitir HTTP (puerto 80)
gcloud compute firewall-rules create allow-http \
  --allow=tcp:80 \
  --source-ranges=0.0.0.0/0 \
  --target-tags=http-server \
  --description="Permitir HTTP"

# Crear regla para permitir HTTPS (puerto 443)
gcloud compute firewall-rules create allow-https \
  --allow=tcp:443 \
  --source-ranges=0.0.0.0/0 \
  --target-tags=https-server

# Crear regla para permitir SSH (puerto 22)
gcloud compute firewall-rules create allow-ssh \
  --allow=tcp:22 \
  --source-ranges=0.0.0.0/0 \
  --description="Permitir SSH"

# Permitir rango de puertos
gcloud compute firewall-rules create allow-app-ports \
  --allow=tcp:8080-8090 \
  --source-ranges=10.0.0.0/8 \
  --target-tags=app-server

# Permitir ping (ICMP)
gcloud compute firewall-rules create allow-ping \
  --allow=icmp \
  --source-ranges=0.0.0.0/0

# Listar reglas
gcloud compute firewall-rules list

# Eliminar regla
gcloud compute firewall-rules delete allow-http
```

**Puertos comunes:**
- **22:** SSH
- **80:** HTTP
- **443:** HTTPS
- **3306:** MySQL
- **5432:** PostgreSQL
- **27017:** MongoDB
- **6379:** Redis
- **8080:** Aplicaciones web alternativas

**3. VPC (Virtual Private Cloud):**

```bash
# Crear VPC personalizada
gcloud compute networks create mi-vpc \
  --subnet-mode=custom

# Crear subnet
gcloud compute networks subnets create mi-subnet \
  --network=mi-vpc \
  --region=us-central1 \
  --range=10.0.0.0/24

# Crear VM en VPC personalizada
gcloud compute instances create vm-privada \
  --zone=us-central1-a \
  --machine-type=e2-micro \
  --network=mi-vpc \
  --subnet=mi-subnet \
  --no-address  # Sin IP externa

# Listar redes
gcloud compute networks list

# Listar subnets
gcloud compute networks subnets list
```

**4. Cloud Storage (equivalente a S3):**

```bash
# Crear bucket
gsutil mb gs://mi-bucket-unico-gcp-123/

# Subir archivo
gsutil cp archivo.txt gs://mi-bucket-unico-gcp-123/

# Subir carpeta
gsutil -m cp -r ./carpeta gs://mi-bucket-unico-gcp-123/

# Listar objetos
gsutil ls gs://mi-bucket-unico-gcp-123/

# Descargar archivo
gsutil cp gs://mi-bucket-unico-gcp-123/archivo.txt ./

# Hacer público
gsutil iam ch allUsers:objectViewer gs://mi-bucket-unico-gcp-123

# Sincronizar carpeta
gsutil rsync -r ./local gs://mi-bucket-unico-gcp-123/remote/

# Eliminar bucket
gsutil rm -r gs://mi-bucket-unico-gcp-123/
```

**5. Cloud SQL (bases de datos administradas):**

```bash
# Crear instancia MySQL
gcloud sql instances create mi-mysql \
  --database-version=MYSQL_8_0 \
  --tier=db-f1-micro \
  --region=us-central1 \
  --root-password=MiPassword123 \
  --availability-type=regional

# Crear base de datos
gcloud sql databases create midb --instance=mi-mysql

# Crear usuario
gcloud sql users create usuario1 \
  --instance=mi-mysql \
  --password=Password123

# Obtener IP de conexión
gcloud sql instances describe mi-mysql \
  --format="value(ipAddresses[0].ipAddress)"

# Permitir IP para conexión
gcloud sql instances patch mi-mysql \
  --authorized-networks=35.123.45.67/32

# Conectar con Cloud SQL Proxy
./cloud_sql_proxy -instances=mi-proyecto:us-central1:mi-mysql=tcp:3306

# Conectar desde otra terminal
mysql -h 127.0.0.1 -u root -p
```

**6. Load Balancing:**

```bash
# Crear Instance Group
gcloud compute instance-groups managed create mi-grupo \
  --base-instance-name=web \
  --size=2 \
  --template=mi-template \
  --zone=us-central1-a

# Crear health check
gcloud compute health-checks create http mi-health-check \
  --port=80 \
  --request-path=/health

# Crear backend service
gcloud compute backend-services create mi-backend \
  --protocol=HTTP \
  --health-checks=mi-health-check \
  --global

# Agregar backend
gcloud compute backend-services add-backend mi-backend \
  --instance-group=mi-grupo \
  --instance-group-zone=us-central1-a \
  --global

# Crear URL map
gcloud compute url-maps create mi-lb \
  --default-service=mi-backend

# Crear HTTP proxy
gcloud compute target-http-proxies create mi-http-proxy \
  --url-map=mi-lb

# Crear forwarding rule
gcloud compute forwarding-rules create mi-http-rule \
  --global \
  --target-http-proxy=mi-http-proxy \
  --ports=80
```

**7. Cloud Functions (serverless):**

```bash
# Crear función (Python)
# main.py
def hello_world(request):
    return 'Hola desde Cloud Functions!'

# Deploy
gcloud functions deploy hello \
  --runtime=python39 \
  --trigger-http \
  --allow-unauthenticated \
  --entry-point=hello_world

# Invocar
gcloud functions call hello

# Ver logs
gcloud functions logs read hello
```

**8. Google Kubernetes Engine (GKE):**

```bash
# Crear cluster
gcloud container clusters create mi-cluster \
  --zone=us-central1-a \
  --num-nodes=3 \
  --machine-type=e2-medium

# Obtener credenciales
gcloud container clusters get-credentials mi-cluster \
  --zone=us-central1-a

# Ahora kubectl está configurado
kubectl get nodes
```

**9. Monitoring (Cloud Monitoring):**

```bash
# Instalar agente en VM
curl -sSO https://dl.google.com/cloudagents/add-monitoring-agent-repo.sh
sudo bash add-monitoring-agent-repo.sh
sudo apt-get update
sudo apt-get install -y stackdriver-agent
sudo service stackdriver-agent start

# Ver métricas via gcloud
gcloud monitoring time-series list \
  --filter='metric.type="compute.googleapis.com/instance/cpu/utilization"'
```

**10. IAM (Identity and Access Management):**

```bash
# Crear cuenta de servicio
gcloud iam service-accounts create mi-sa \
  --display-name="Mi Service Account"

# Otorgar rol
gcloud projects add-iam-policy-binding mi-proyecto-123 \
  --member="serviceAccount:mi-sa@mi-proyecto-123.iam.gserviceaccount.com" \
  --role="roles/compute.instanceAdmin.v1"

# Generar key
gcloud iam service-accounts keys create key.json \
  --iam-account=mi-sa@mi-proyecto-123.iam.gserviceaccount.com

# Usar key
export GOOGLE_APPLICATION_CREDENTIALS="./key.json"
```

**Regiones y zonas en GCP:**

```
Región us-central1 (Iowa, USA)
  ├── us-central1-a
  ├── us-central1-b
  ├── us-central1-c
  └── us-central1-f

Región europe-west1 (Bélgica)
  ├── europe-west1-b
  ├── europe-west1-c
  └── europe-west1-d

Región asia-east1 (Taiwán)
  ├── asia-east1-a
  ├── asia-east1-b
  └── asia-east1-c
```

**Ciclo de vida completo:**

1. **Crear proyecto:** `gcloud projects create mi-proyecto`
2. **Habilitar APIs:** `gcloud services enable compute.googleapis.com`
3. **Crear VPC y subnets**
4. **Configurar firewall rules**
5. **Crear VMs** con tags apropiados
6. **Configurar Load Balancer** (si multi-instancia)
7. **Configurar Cloud SQL** para base de datos
8. **Configurar Cloud Storage** para archivos
9. **Configurar monitoring y alertas**
10. **Configurar backups y snapshots**

**Ejemplo de uso completo:** Aplicación web en GCP con frontend servido desde Cloud Storage + Cloud CDN, backend en Compute Engine con Managed Instance Group detrás de Load Balancer, base de datos Cloud SQL PostgreSQL en alta disponibilidad, archivos de usuarios en Cloud Storage, funciones serverless en Cloud Functions para procesamiento de imágenes, todo monitoreado con Cloud Monitoring.

### Microservicios, Observabilidad y sistemas escalables

**Qué trata:** Principios y herramientas para construir, monitorear y escalar sistemas distribuidos basados en microservicios.

**Observabilidad:**

**Qué trata:** Capacidad de entender el estado interno del sistema examinando sus salidas (logs, métricas, traces).

**Los 3 pilares de observabilidad:**

**1. Logs (Registros):**

**Qué trata:** Eventos discretos con timestamp que ocurren en el sistema.

**Herramientas:**
- **ELK Stack:** Elasticsearch + Logstash + Kibana
- **Loki:** Logging de Grafana
- **CloudWatch Logs:** AWS
- **Cloud Logging:** GCP

**Implementación con ELK:**

```bash
# Docker Compose para ELK
version: '3.8'
services:
  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:8.11.0
    environment:
      - discovery.type=single-node
      - xpack.security.enabled=false
    ports:
      - "9200:9200"
    volumes:
      - elastic-data:/usr/share/elasticsearch/data
  
  logstash:
    image: docker.elastic.co/logstash/logstash:8.11.0
    ports:
      - "5000:5000"
      - "9600:9600"
    volumes:
      - ./logstash.conf:/usr/share/logstash/pipeline/logstash.conf
    depends_on:
      - elasticsearch
  
  kibana:
    image: docker.elastic.co/kibana/kibana:8.11.0
    ports:
      - "5601:5601"
    environment:
      - ELASTICSEARCH_HOSTS=http://elasticsearch:9200
    depends_on:
      - elasticsearch

volumes:
  elastic-data:
```

**Logging en aplicación:**

```java
// Spring Boot con SLF4J
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.slf4j.MDC;

@Service
public class PedidoService {
    private static final Logger log = LoggerFactory.getLogger(PedidoService.class);
    
    public Pedido crear(PedidoDTO dto) {
        MDC.put("usuarioId", dto.getUsuarioId().toString());
        MDC.put("traceId", UUID.randomUUID().toString());
        
        log.info("Iniciando creación de pedido");
        
        try {
            Pedido pedido = pedidoRepository.save(new Pedido(dto));
            log.info("Pedido creado: pedidoId={}, total={}", 
                     pedido.getId(), pedido.getTotal());
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

**2. Métricas:**

**Qué trata:** Valores numéricos agregados sobre el tiempo (contadores, gauges, histogramas).

**Herramientas:**
- **Prometheus + Grafana**
- **CloudWatch Metrics**
- **Datadog**
- **New Relic**

**Prometheus setup:**

```yaml
# docker-compose.yml
version: '3.8'
services:
  prometheus:
    image: prom/prometheus:latest
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus-data:/prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
  
  grafana:
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin
    volumes:
      - grafana-data:/var/lib/grafana
    depends_on:
      - prometheus

volumes:
  prometheus-data:
  grafana-data:
```

```yaml
# prometheus.yml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'spring-boot-app'
    metrics_path: '/actuator/prometheus'
    static_configs:
      - targets: ['app:8080']
  
  - job_name: 'node-exporter'
    static_configs:
      - targets: ['node-exporter:9100']
```

**Exponer métricas en Spring Boot:**

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
<dependency>
    <groupId>io.micrometer</groupId>
    <artifactId>micrometer-registry-prometheus</artifactId>
</dependency>
```

```yaml
# application.yml
management:
  endpoints:
    web:
      exposure:
        include: health,info,prometheus,metrics
  metrics:
    export:
      prometheus:
        enabled: true
```

```java
// Métricas personalizadas
@Service
public class PedidoService {
    
    private final Counter pedidosCreados;
    private final Timer pedidoTimer;
    
    public PedidoService(MeterRegistry registry) {
        this.pedidosCreados = Counter.builder("pedidos.creados")
            .description("Total de pedidos creados")
            .tag("servicio", "pedido-service")
            .register(registry);
        
        this.pedidoTimer = Timer.builder("pedido.crear.duracion")
            .description("Duración de creación de pedido")
            .register(registry);
    }
    
    public Pedido crear(PedidoDTO dto) {
        return pedidoTimer.record(() -> {
            Pedido pedido = pedidoRepository.save(new Pedido(dto));
            pedidosCreados.increment();
            return pedido;
        });
    }
}
```

**Acceso a métricas:**
- Prometheus UI: `http://localhost:9090`
- Grafana: `http://localhost:3000` (admin/admin)
- Métricas de app: `http://localhost:8080/actuator/prometheus`

**3. Traces (Trazas distribuidas):**

**Qué trata:** Rastrear petición a través de múltiples servicios.

**Herramientas:**
- **Jaeger**
- **Zipkin**
- **AWS X-Ray**
- **Google Cloud Trace**

**Jaeger setup:**

```yaml
# docker-compose.yml
version: '3.8'
services:
  jaeger:
    image: jaegertracing/all-in-one:latest
    ports:
      - "5775:5775/udp"     # zipkin.thrift compact
      - "6831:6831/udp"     # jaeger.thrift compact
      - "6832:6832/udp"     # jaeger.thrift binary
      - "5778:5778"         # serve configs
      - "16686:16686"       # UI
      - "14268:14268"       # jaeger.thrift
      - "14250:14250"       # gRPC
      - "9411:9411"         # Zipkin compatible
    environment:
      - COLLECTOR_ZIPKIN_HOST_PORT=:9411
```

**Instrumentación con Spring Cloud Sleuth:**

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-sleuth</artifactId>
</dependency>
<dependency>
    <groupId>io.opentracing.contrib</groupId>
    <artifactId>opentracing-spring-jaeger-web-starter</artifactId>
    <version>3.3.1</version>
</dependency>
```

```yaml
# application.yml
opentracing:
  jaeger:
    udp-sender:
      host: localhost
      port: 6831
    probabilistic-sampler:
      sampling-rate: 1.0  # 100% sampling
```

**Logs con Trace ID:**
```
2025-01-25 10:30:15 [pedido-service,abc123,def456] INFO - Creando pedido
2025-01-25 10:30:15 [inventario-service,abc123,ghi789] INFO - Reservando inventario
2025-01-25 10:30:16 [pago-service,abc123,jkl012] INFO - Procesando pago
```

**Acceso a Jaeger UI:** `http://localhost:16686`

**Health Checks:**

**Qué trata:** Endpoints para verificar estado de servicio.

```java
@RestController
@RequestMapping("/actuator")
public class HealthController {
    
    @Autowired
    private DataSource dataSource;
    
    @Autowired
    private RestTemplate restTemplate;
    
    @GetMapping("/health")
    public HealthResponse health() {
        HealthResponse response = new HealthResponse();
        response.setStatus("UP");
        
        // Check database
        try {
            dataSource.getConnection().close();
            response.setDatabase("UP");
        } catch (Exception e) {
            response.setDatabase("DOWN");
            response.setStatus("DOWN");
        }
        
        // Check dependent services
        try {
            restTemplate.getForObject("http://inventario-service/actuator/health", 
                                      String.class);
            response.setInventarioService("UP");
        } catch (Exception e) {
            response.setInventarioService("DOWN");
        }
        
        return response;
    }
}
```

**Kubernetes Liveness y Readiness probes:**

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pedido-service
spec:
  containers:
  - name: app
    image: pedido-service:1.0
    ports:
    - containerPort: 8080
    
    # Liveness: ¿Está vivo? (reiniciar si falla)
    livenessProbe:
      httpGet:
        path: /actuator/health/liveness
        port: 8080
      initialDelaySeconds: 30
      periodSeconds: 10
      timeoutSeconds: 5
      failureThreshold: 3
    
    # Readiness: ¿Listo para tráfico? (no enviar si falla)
    readinessProbe:
      httpGet:
        path: /actuator/health/readiness
        port: 8080
      initialDelaySeconds: 10
      periodSeconds: 5
      timeoutSeconds: 3
      failureThreshold: 2
```

**Sistemas escalables:**

**Escalado Horizontal (Scale Out):**
- Agregar más instancias
- Load balancer distribuye tráfico
- Stateless services

```bash
# Kubernetes horizontal pod autoscaler
kubectl autoscale deployment pedido-service \
  --cpu-percent=70 \
  --min=2 \
  --max=10
```

**Escalado Vertical (Scale Up):**
- Incrementar recursos de instancia
- Más CPU/RAM
- Límite físico del servidor

**Patrones de escalabilidad:**

**1. Caching:**

```java
// Redis para cache
@Service
public class ProductoService {
    
    @Autowired
    private RedisTemplate<String, Producto> redisTemplate;
    
    @Cacheable(value = "productos", key = "#id")
    public Producto getProducto(Long id) {
        return productoRepository.findById(id)
            .orElseThrow(() -> new NotFoundException());
    }
    
    @CacheEvict(value = "productos", key = "#producto.id")
    public Producto actualizar(Producto producto) {
        return productoRepository.save(producto);
    }
}
```

**2. CDN (Content Delivery Network):**
- Distribuir contenido estático globalmente
- CloudFront (AWS), Cloud CDN (GCP)
- Reduce latencia

**3. Database Replication:**

```
Master (Write)
  ├── Read Replica 1
  ├── Read Replica 2
  └── Read Replica 3
```

**4. Message Queues:**

```java
// RabbitMQ para desacoplar
@Service
public class PedidoService {
    
    @Autowired
    private RabbitTemplate rabbitTemplate;
    
    public Pedido crear(PedidoDTO dto) {
        Pedido pedido = pedidoRepository.save(new Pedido(dto));
        
        // Async: enviar a cola para procesamiento
        rabbitTemplate.convertAndSend("pedidos.queue", pedido);
        
        return pedido;
    }
}
```

**Puertos comunes en observabilidad:**
- **9090:** Prometheus
- **3000:** Grafana
- **16686:** Jaeger UI
- **5601:** Kibana
- **9200:** Elasticsearch
- **5000:** Logstash
- **9411:** Zipkin

**Ejemplo de uso completo:** Sistema de e-commerce con microservicios instrumentados con Spring Cloud Sleuth enviando traces a Jaeger, logs centralizados en ELK Stack, métricas expuestas a Prometheus y visualizadas en Grafana. Health checks en cada servicio monitoreados por Kubernetes. Auto-scaling basado en métricas CPU y custom (pedidos/segundo). Cache Redis para productos populares, CDN para imágenes, Read Replicas en base de datos.

### Conocimiento e implementación de la tecnología Docker

**Qué trata:** Plataforma para desarrollar, empaquetar y ejecutar aplicaciones en contenedores portátiles y aislados.

**Por qué se utiliza:** Consistencia entre entornos (dev/test/prod), portabilidad, aislamiento, eficiencia de recursos, despliegue rápido.

**Ventajas:**
- Mismo comportamiento en dev y producción
- Inicio rápido (segundos vs minutos de VMs)
- Uso eficiente de recursos (comparte kernel)
- Versionamiento de imágenes
- Ecosistema maduro (Docker Hub)
- Integración con CI/CD

**Desventajas:**
- Curva de aprendizaje inicial
- Seguridad requiere configuración adecuada
- Persistencia de datos requiere volúmenes
- Networking puede ser complejo
- No aislamiento completo del kernel

**Conceptos fundamentales:**

**1. Imagen vs Contenedor:**
- **Imagen:** Plantilla read-only (blueprint)
- **Contenedor:** Instancia en ejecución de una imagen

```
Imagen (ubuntu:20.04)
  ├── Contenedor 1 (web-server)
  ├── Contenedor 2 (db-server)
  └── Contenedor 3 (cache-server)
```

**2. Instalación de Docker:**

```bash
# Ubuntu/Debian
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# Agregar usuario a grupo docker
sudo usermod -aG docker $USER

# Verificar instalación
docker --version
docker run hello-world
```

**3. Comandos básicos:**

```bash
# Buscar imágenes en Docker Hub
docker search nginx

# Descargar imagen
docker pull nginx:latest
docker pull mysql:8.0
docker pull node:18-alpine

# Listar imágenes locales
docker images

# Ejecutar contenedor
docker run nginx

# Ejecutar en background (-d detached)
docker run -d nginx

# Ejecutar con nombre personalizado
docker run -d --name mi-nginx nginx

# Ejecutar con puerto mapeado
docker run -d -p 8080:80 nginx
# Host:Container (8080 local → 80 contenedor)

# Ejecutar con variables de entorno
docker run -d \
  -e MYSQL_ROOT_PASSWORD=password123 \
  -e MYSQL_DATABASE=midb \
  mysql:8.0

# Ejecutar con volumen
docker run -d \
  -v /host/data:/var/lib/mysql \
  mysql:8.0

# Ejecutar interactivamente con terminal
docker run -it ubuntu:20.04 /bin/bash

# Listar contenedores en ejecución
docker ps

# Listar todos (incluidos detenidos)
docker ps -a

# Ver logs de contenedor
docker logs mi-nginx
docker logs -f mi-nginx  # Seguir logs (tail -f)

# Ejecutar comando en contenedor en ejecución
docker exec mi-nginx ls /etc/nginx
docker exec -it mi-nginx /bin/bash  # Shell interactivo

# Detener contenedor
docker stop mi-nginx

# Iniciar contenedor detenido
docker start mi-nginx

# Reiniciar contenedor
docker restart mi-nginx

# Eliminar contenedor
docker rm mi-nginx

# Forzar eliminación de contenedor en ejecución
docker rm -f mi-nginx

# Eliminar imagen
docker rmi nginx:latest

# Ver uso de recursos
docker stats

# Inspeccionar contenedor (JSON)
docker inspect mi-nginx

# Ver procesos en contenedor
docker top mi-nginx
```

**4. Dockerfile - Crear imágenes personalizadas:**

**Qué trata:** Archivo de texto con instrucciones para construir imagen Docker.

**Ejemplo Node.js:**

```dockerfile
# Imagen base
FROM node:18-alpine

# Metadata
LABEL maintainer="tu@email.com"
LABEL version="1.0"

# Directorio de trabajo
WORKDIR /app

# Copiar package.json y package-lock.json
COPY package*.json ./

# Instalar dependencias
RUN npm install --production

# Copiar código fuente
COPY . .

# Exponer puerto
EXPOSE 3000

# Variable de entorno
ENV NODE_ENV=production

# Usuario no-root (seguridad)
RUN addgroup -g 1001 -S nodejs
RUN adduser -S nodejs -u 1001
USER nodejs

# Comando de inicio
CMD ["node", "server.js"]
```

**Ejemplo Java Spring Boot:**

```dockerfile
# Multi-stage build
# Stage 1: Build
FROM maven:3.8-openjdk-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# Stage 2: Runtime
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY --from=build /app/target/mi-app-1.0.0.jar app.jar

EXPOSE 8080

ENV JAVA_OPTS="-Xmx512m"

ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS -jar app.jar"]
```

**Ejemplo Python Flask:**

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

ENV FLASK_APP=app.py
ENV FLASK_ENV=production

CMD ["flask", "run", "--host=0.0.0.0"]
```

**Construir imagen:**

```bash
# Construir desde Dockerfile
docker build -t mi-app:1.0 .

# Construir con nombre y etiqueta
docker build -t usuario/mi-app:latest .

# Construir sin cache
docker build --no-cache -t mi-app:1.0 .

# Construir con argumento
docker build --build-arg VERSION=1.2.3 -t mi-app:1.2.3 .
```

**5. Docker Compose - Múltiples contenedores:**

**Qué trata:** Herramienta para definir y ejecutar aplicaciones multi-contenedor con YAML.

**docker-compose.yml completo:**

```yaml
version: '3.8'

services:
  # Base de datos
  db:
    image: mysql:8.0
    container_name: mysql-db
    restart: always
    ports:
      - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: midb
      MYSQL_USER: usuario
      MYSQL_PASSWORD: password
    volumes:
      - db-data:/var/lib/mysql
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql
    networks:
      - app-network
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost"]
      interval: 10s
      timeout: 5s
      retries: 3
  
  # Cache Redis
  redis:
    image: redis:7-alpine
    container_name: redis-cache
    restart: always
    ports:
      - "6379:6379"
    networks:
      - app-network
    command: redis-server --appendonly yes
    volumes:
      - redis-data:/data
  
  # Backend
  backend:
    build:
      context: ./backend
      dockerfile: Dockerfile
    container_name: app-backend
    restart: always
    ports:
      - "8080:8080"
    environment:
      SPRING_DATASOURCE_URL: jdbc:mysql://db:3306/midb
      SPRING_DATASOURCE_USERNAME: usuario
      SPRING_DATASOURCE_PASSWORD: password
      SPRING_REDIS_HOST: redis
      SPRING_REDIS_PORT: 6379
    depends_on:
      db:
        condition: service_healthy
      redis:
        condition: service_started
    networks:
      - app-network
    volumes:
      - ./backend/logs:/app/logs
  
  # Frontend
  frontend:
    build:
      context: ./frontend
      dockerfile: Dockerfile
    container_name: app-frontend
    restart: always
    ports:
      - "80:80"
    depends_on:
      - backend
    networks:
      - app-network
  
  # Nginx reverse proxy
  nginx:
    image: nginx:alpine
    container_name: nginx-proxy
    restart: always
    ports:
      - "443:443"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro
      - ./nginx/ssl:/etc/nginx/ssl:ro
    depends_on:
      - frontend
      - backend
    networks:
      - app-network

volumes:
  db-data:
  redis-data:

networks:
  app-network:
    driver: bridge
```

**Comandos Docker Compose:**

```bash
# Iniciar todos los servicios
docker-compose up

# Iniciar en background
docker-compose up -d

# Construir imágenes y iniciar
docker-compose up --build

# Ver logs de todos los servicios
docker-compose logs

# Ver logs de servicio específico
docker-compose logs backend

# Seguir logs
docker-compose logs -f

# Listar servicios en ejecución
docker-compose ps

# Detener servicios
docker-compose stop

# Detener y eliminar contenedores
docker-compose down

# Detener, eliminar contenedores y volúmenes
docker-compose down -v

# Escalar servicio
docker-compose up -d --scale backend=3

# Reiniciar servicio específico
docker-compose restart backend

# Ejecutar comando en servicio
docker-compose exec backend /bin/bash
```

**6. Volúmenes - Persistencia de datos:**

```bash
# Crear volumen
docker volume create mi-volumen

# Listar volúmenes
docker volume ls

# Inspeccionar volumen
docker volume inspect mi-volumen

# Usar volumen
docker run -d -v mi-volumen:/data nginx

# Bind mount (mapear carpeta host)
docker run -d -v /host/path:/container/path nginx

# Volume de solo lectura
docker run -d -v mi-volumen:/data:ro nginx

# Eliminar volumen
docker volume rm mi-volumen

# Eliminar volúmenes no utilizados
docker volume prune
```

**7. Networking:**

```bash
# Listar redes
docker network ls

# Crear red
docker network create mi-red

# Conectar contenedor a red
docker network connect mi-red mi-contenedor

# Crear contenedor en red específica
docker run -d --network mi-red nginx

# Inspeccionar red
docker network inspect mi-red

# Desconectar contenedor de red
docker network disconnect mi-red mi-contenedor
```

**Tipos de redes:**
- **bridge:** Red por defecto, contenedores en mismo host
- **host:** Usa red del host directamente
- **none:** Sin red
- **overlay:** Multi-host (Swarm/Kubernetes)

**8. Docker Registry - Compartir imágenes:**

```bash
# Login a Docker Hub
docker login

# Etiquetar imagen
docker tag mi-app:1.0 usuario/mi-app:1.0

# Push a Docker Hub
docker push usuario/mi-app:1.0

# Pull de Docker Hub
docker pull usuario/mi-app:1.0

# Registro privado
docker run -d -p 5000:5000 --name registry registry:2

# Push a registro privado
docker tag mi-app localhost:5000/mi-app:1.0
docker push localhost:5000/mi-app:1.0
```

**9. Optimización de imágenes:**

```dockerfile
# ✅ Buenas prácticas

# 1. Usar imágenes base pequeñas
FROM node:18-alpine  # Alpine es más pequeña

# 2. Multi-stage builds (separar build de runtime)
FROM maven:3.8-openjdk-17 AS build
# ... build ...
FROM openjdk:17-jdk-slim  # Imagen final más pequeña
COPY --from=build /app/target/app.jar .

# 3. Minimizar capas (combinar RUN)
RUN apt-get update && \
    apt-get install -y curl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# 4. Copiar solo lo necesario
COPY package*.json ./
RUN npm install
COPY . .

# 5. .dockerignore para excluir archivos
# .dockerignore:
# node_modules
# .git
# *.log

# 6. No ejecutar como root
USER nodejs

# 7. Especificar versiones exactas
FROM node:18.16.0-alpine
```

**10. Debugging y troubleshooting:**

```bash
# Ver logs detallados
docker logs --tail 100 mi-contenedor

# Ver uso de recursos en tiempo real
docker stats

# Inspeccionar configuración
docker inspect mi-contenedor | jq '.[0].NetworkSettings'

# Shell en contenedor
docker exec -it mi-contenedor /bin/sh

# Copiar archivos desde/hacia contenedor
docker cp mi-contenedor:/app/logs/error.log ./
docker cp ./config.yml mi-contenedor:/app/

# Ver cambios en filesystem del contenedor
docker diff mi-contenedor

# Ver procesos
docker top mi-contenedor

# Guardar contenedor como imagen
docker commit mi-contenedor mi-imagen-nueva:1.0

# Exportar/importar imágenes
docker save mi-app:1.0 > mi-app.tar
docker load < mi-app.tar
```

**Puertos comunes en contenedores:**
- **3000:** Node.js/React/Next.js
- **8080:** Spring Boot/Tomcat
- **5000:** Flask/Python
- **80/443:** Nginx/Apache
- **3306:** MySQL
- **5432:** PostgreSQL
- **27017:** MongoDB
- **6379:** Redis
- **5672/15672:** RabbitMQ
- **9092:** Kafka

**Ciclo de vida completo:**

1. **Desarrollo:** Crear Dockerfile
2. **Build:** `docker build -t mi-app:1.0 .`
3. **Test local:** `docker run -p 8080:8080 mi-app:1.0`
4. **Tag:** `docker tag mi-app:1.0 usuario/mi-app:1.0`
5. **Push:** `docker push usuario/mi-app:1.0`
6. **Deploy:** Pull y run en servidor
7. **Monitor:** `docker logs` y `docker stats`
8. **Update:** Build nueva versión, tag, push, re-deploy

**Ejemplo de uso completo:** Aplicación full-stack con Docker Compose: Frontend React en Nginx (puerto 80), Backend Spring Boot (puerto 8080), Base de datos MySQL (puerto 3306), Redis cache (puerto 6379), todo en red Docker privada. Volúmenes para persistir datos de MySQL y Redis. Nginx como reverse proxy para enrutar /api al backend. CI/CD con GitHub Actions que construye imágenes, las sube a Docker Hub, y despliega en servidor con `docker-compose pull && docker-compose up -d`.

### Conocimiento e implementación de la tecnología Kubernetes

**Qué trata:** Sistema de orquestación de contenedores para automatizar despliegue, escalado y gestión de aplicaciones containerizadas.

**Por qué se utiliza:** Gestionar contenedores a escala, auto-scaling, auto-healing, despliegues sin downtime, balanceo de carga, gestión de configuración y secretos.

**Ventajas:**
- Orquestación automática de contenedores
- Auto-scaling horizontal
- Auto-healing (reinicia contenedores fallidos)
- Rolling updates sin downtime
- Service discovery integrado
- Gestión de secretos y configuración
- Multi-cloud y on-premise
- Ecosistema extenso (Helm, Operators)

**Desventajas:**
- Complejidad alta (curva de aprendizaje pronunciada)
- Overhead de recursos para cluster
- Configuración inicial compleja
- Debugging más difícil
- Requiere monitoreo robusto
- Puede ser overkill para apps pequeñas

**Arquitectura de Kubernetes:**

```
Cluster
├── Control Plane (Master)
│   ├── API Server (puerto 6443) - Punto de entrada
│   ├── etcd (puerto 2379-2380) - Key-value store
│   ├── Scheduler - Asigna pods a nodes
│   └── Controller Manager - Mantiene estado deseado
└── Worker Nodes
    ├── Kubelet (puerto 10250) - Agente en cada node
    ├── Kube-proxy - Networking
    └── Container Runtime (Docker/containerd)
```

**Conceptos fundamentales:**

**1. Pod:**

**Qué trata:** Unidad más pequeña desplegable, contiene uno o más contenedores.

```yaml
# pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.21
    ports:
    - containerPort: 80
    resources:
      requests:
        memory: "64Mi"
        CPU: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
```

```bash
# Crear pod
kubectl apply -f pod.yaml

# Listar pods
kubectl get pods

# Ver detalles de pod
kubectl describe pod nginx-pod

# Ver logs
kubectl logs nginx-pod

# Ejecutar comando en pod
kubectl exec nginx-pod -- ls /etc/nginx
kubectl exec -it nginx-pod -- /bin/bash

# Eliminar pod
kubectl delete pod nginx-pod
```

**2. Deployment:**

**Qué trata:** Gestiona ReplicaSets y provee actualizaciones declarativas para Pods.

```yaml
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3  # 3 pods
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.21
        ports:
        - containerPort: 80
        livenessProbe:
          httpGet:
            path: /
            port: 80
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /
            port: 80
          initialDelaySeconds: 5
          periodSeconds: 5
```

```bash
# Crear deployment
kubectl apply -f deployment.yaml

# Ver deployments
kubectl get deployments

# Ver pods creados por deployment
kubectl get pods -l app=nginx

# Escalar deployment
kubectl scale deployment nginx-deployment --replicas=5

# Actualizar imagen (rolling update)
kubectl set image deployment/nginx-deployment nginx=nginx:1.22

# Ver historial de rollouts
kubectl rollout history deployment/nginx-deployment

# Rollback a versión anterior
kubectl rollout undo deployment/nginx-deployment

# Ver estado de rollout
kubectl rollout status deployment/nginx-deployment

# Eliminar deployment
kubectl delete deployment nginx-deployment
```

**3. Service:**

**Qué trata:** Abstracción para exponer aplicación que se ejecuta en conjunto de Pods.

**Tipos de Services:**

**ClusterIP (por defecto):**
- Accesible solo dentro del cluster
- IP interna del cluster

```yaml
# service-clusterip.yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: ClusterIP
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 80        # Puerto del servicio
    targetPort: 80  # Puerto del contenedor
```

**NodePort:**
- Expone servicio en puerto específico de cada Node
- Accesible externamente: `<NodeIP>:<NodePort>`

```yaml
# service-nodeport.yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-nodeport
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
    nodePort: 30080  # Puerto 30000-32767
```

**LoadBalancer:**
- Crea balanceador de carga externo (cloud providers)

```yaml
# service-loadbalancer.yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-lb
spec:
  type: LoadBalancer
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
```

```bash
# Crear service
kubectl apply -f service.yaml

# Listar services
kubectl get svc

# Ver detalles
kubectl describe svc nginx-service

# Obtener endpoint
kubectl get endpoints nginx-service
```

**4. ConfigMap y Secrets:**

**ConfigMap:** Datos de configuración no sensibles

```yaml
# configmap.yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  database_url: "mysql://db:3306/midb"
  log_level: "info"
  app.properties: |
    server.port=8080
    spring.datasource.url=jdbc:mysql://db:3306/midb
```

```bash
# Crear desde archivo
kubectl create configmap app-config --from-file=app.properties

# Crear desde literal
kubectl create configmap app-config \
  --from-literal=database_url=mysql://db:3306/midb

# Ver configmap
kubectl get configmap
kubectl describe configmap app-config
```

**Usar ConfigMap en Pod:**

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: app-pod
spec:
  containers:
  - name: app
    image: mi-app:1.0
    env:
    # Variable de entorno desde ConfigMap
    - name: DATABASE_URL
      valueFrom:
        configMapKeyRef:
          name: app-config
          key: database_url
    # Montar ConfigMap como archivo
    volumeMounts:
    - name: config
      mountPath: /etc/config
  volumes:
  - name: config
    configMap:
      name: app-config
```

**Secret:** Datos sensibles (passwords, tokens, keys)

```yaml
# secret.yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  # Valores deben estar en base64
  username: YWRtaW4=        # admin
  password: cGFzczEyMzQ1    # pass12345
```

```bash
# Crear secret
kubectl create secret generic db-secret \
  --from-literal=username=admin \
  --from-literal=password=pass12345

# Ver secrets (valores ocultos)
kubectl get secrets

# Ver contenido (base64)
kubectl get secret db-secret -o yaml
```

**Usar Secret en Pod:**

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: db-pod
spec:
  containers:
  - name: mysql
    image: mysql:8.0
    env:
    - name: MYSQL_ROOT_PASSWORD
      valueFrom:
        secretKeyRef:
          name: db-secret
          key: password
```

**5. Volumes - Persistencia:**

```yaml
# deployment-with-volume.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - name: mysql
        image: mysql:8.0
        ports:
        - containerPort: 3306
        env:
        - name: MYSQL_ROOT_PASSWORD
          value: "password"
        volumeMounts:
        - name: mysql-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-storage
        persistentVolumeClaim:
          claimName: mysql-pvc
```

**PersistentVolumeClaim:**

```yaml
# pvc.yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
  storageClassName: standard
```

**6. Ingress - Enrutamiento HTTP/HTTPS:**

**Qué trata:** Exponer rutas HTTP/HTTPS desde fuera del cluster a servicios internos.

```yaml
# ingress.yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: mi-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: miapp.ejemplo.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: frontend-service
            port:
              number: 80
      - path: /api
        pathType: Prefix
        backend:
          service:
            name: backend-service
            port:
              number: 8080
  tls:
  - hosts:
    - miapp.ejemplo.com
    secretName: tls-secret
```

**Instalar Ingress Controller (Nginx):**

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.8.1/deploy/static/provider/cloud/deploy.yaml
```

**7. Namespace - Aislamiento:**

```bash
# Crear namespace
kubectl create namespace desarrollo
kubectl create namespace produccion

# Listar namespaces
kubectl get namespaces

# Crear recurso en namespace específico
kubectl apply -f deployment.yaml -n desarrollo

# Listar pods en namespace
kubectl get pods -n desarrollo

# Cambiar contexto a namespace
kubectl config set-context --current --namespace=desarrollo

# Ver todos los pods de todos los namespaces
kubectl get pods --all-namespaces
kubectl get pods -A
```

**8. HorizontalPodAutoscaler (HPA):**

**Qué trata:** Escalar automáticamente número de pods basándose en métricas.

```yaml
# hpa.yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: nginx-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: nginx-deployment
  minReplicas: 2
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70  # 70% CPU
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageUtilization: 80  # 80% memoria
```

```bash
# Crear HPA via comando
kubectl autoscale deployment nginx-deployment \
  --cpu-percent=70 \
  --min=2 \
  --max=10

# Ver HPA
kubectl get hpa

# Ver detalles
kubectl describe hpa nginx-hpa
```

**9. Kubectl - Comandos esenciales:**

```bash
# Información del cluster
kubectl cluster-info
kubectl get nodes
kubectl describe node <node-name>

# Trabajar con recursos
kubectl get pods
kubectl get deployments
kubectl get services
kubectl get all  # Todos los recursos

# Formato de salida
kubectl get pods -o wide  # Más información
kubectl get pods -o yaml  # YAML
kubectl get pods -o json  # JSON

# Filtrar por label
kubectl get pods -l app=nginx
kubectl get pods --selector=app=nginx,tier=frontend

# Watch (actualización continua)
kubectl get pods --watch

# Debugging
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl logs -f <pod-name>  # Follow logs
kubectl logs <pod-name> -c <container-name>  # Multi-container pod

# Port forwarding (acceso local)
kubectl port-forward pod/nginx-pod 8080:80
# Ahora: http://localhost:8080

# Copiar archivos
kubectl cp <pod-name>:/path/to/file ./local-file
kubectl cp ./local-file <pod-name>:/path/to/file

# Contextos (múltiples clusters)
kubectl config get-contexts
kubectl config use-context <context-name>

# Aplicar configuración
kubectl apply -f deployment.yaml
kubectl apply -f ./directory/  # Todos los archivos

# Eliminar recursos
kubectl delete pod <pod-name>
kubectl delete -f deployment.yaml
kubectl delete all --all  # Eliminar todo (¡cuidado!)

# Eventos del cluster
kubectl get events --sort-by=.metadata.creationTimestamp

# Top (uso de recursos)
kubectl top nodes
kubectl top pods
```

**10. Helm - Package Manager:**

**Qué trata:** Gestor de paquetes para Kubernetes, facilita instalación de aplicaciones complejas.

```bash
# Instalar Helm
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

# Agregar repositorio
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update

# Buscar charts
helm search repo mysql

# Instalar chart
helm install mi-mysql bitnami/mysql \
  --set auth.rootPassword=password123 \
  --set primary.persistence.size=10Gi

# Listar releases
helm list

# Ver estado
helm status mi-mysql

# Actualizar
helm upgrade mi-mysql bitnami/mysql \
  --set auth.rootPassword=newpassword

# Rollback
helm rollback mi-mysql 1

# Desinstalar
helm uninstall mi-mysql

# Crear chart propio
helm create mi-app
```

**11. Ejemplo completo - Aplicación full-stack:**

```yaml
# namespace.yaml
apiVersion: v1
kind: Namespace
metadata:
  name: mi-app

---
# mysql-secret.yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysql-secret
  namespace: mi-app
type: Opaque
data:
  password: cGFzc3dvcmQxMjM=  # password123

---
# mysql-pvc.yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pvc
  namespace: mi-app
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi

---
# mysql-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql
  namespace: mi-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - name: mysql
        image: mysql:8.0
        ports:
        - containerPort: 3306
        env:
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-secret
              key: password
        - name: MYSQL_DATABASE
          value: "midb"
        volumeMounts:
        - name: mysql-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-storage
        persistentVolumeClaim:
          claimName: mysql-pvc

---
# mysql-service.yaml
apiVersion: v1
kind: Service
metadata:
  name: mysql
  namespace: mi-app
spec:
  type: ClusterIP
  selector:
    app: mysql
  ports:
  - port: 3306
    targetPort: 3306

---
# backend-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend
  namespace: mi-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: backend
  template:
    metadata:
      labels:
        app: backend
    spec:
      containers:
      - name: backend
        image: usuario/mi-backend:1.0
        ports:
        - containerPort: 8080
        env:
        - name: SPRING_DATASOURCE_URL
          value: "jdbc:mysql://mysql:3306/midb"
        - name: SPRING_DATASOURCE_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-secret
              key: password
        livenessProbe:
          httpGet:
            path: /actuator/health/liveness
            port: 8080
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /actuator/health/readiness
            port: 8080
          initialDelaySeconds: 10
          periodSeconds: 5
        resources:
          requests:
            memory: "256Mi"
            cpu: "250m"
          limits:
            memory: "512Mi"
            cpu: "500m"

---
# backend-service.yaml
apiVersion: v1
kind: Service
metadata:
  name: backend
  namespace: mi-app
spec:
  type: ClusterIP
  selector:
    app: backend
  ports:
  - port: 8080
    targetPort: 8080

---
# backend-hpa.yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: backend-hpa
  namespace: mi-app
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: backend
  minReplicas: 3
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70

---
# frontend-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend
  namespace: mi-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: frontend
  template:
    metadata:
      labels:
        app: frontend
    spec:
      containers:
      - name: frontend
        image: usuario/mi-frontend:1.0
        ports:
        - containerPort: 80

---
# frontend-service.yaml
apiVersion: v1
kind: Service
metadata:
  name: frontend
  namespace: mi-app
spec:
  type: ClusterIP
  selector:
    app: frontend
  ports:
  - port: 80
    targetPort: 80

---
# ingress.yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: mi-app-ingress
  namespace: mi-app
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: miapp.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: frontend
            port:
              number: 80
      - path: /api
        pathType: Prefix
        backend:
          service:
            name: backend
            port:
              number: 8080
```

**Desplegar todo:**

```bash
# Aplicar todos los manifiestos
kubectl apply -f .

# Verificar despliegue
kubectl get all -n mi-app

# Ver pods
kubectl get pods -n mi-app

# Ver services
kubectl get svc -n mi-app

# Ver ingress
kubectl get ingress -n mi-app
```

**Puertos comunes en Kubernetes:**
- **6443:** API Server
- **2379-2380:** etcd
- **10250:** Kubelet
- **10251:** kube-scheduler
- **10252:** kube-controller-manager
- **30000-32767:** NodePort range

**Ciclo de vida de aplicación en Kubernetes:**

1. **Desarrollo:** Crear Dockerfiles
2. **Build:** Construir imágenes Docker
3. **Push:** Subir a registry (Docker Hub, GCR, ECR)
4. **Manifiestos:** Crear YAML files (Deployment, Service, etc)
5. **Deploy:** `kubectl apply -f manifests/`
6. **Verificar:** `kubectl get pods`, `kubectl logs`
7. **Exponer:** Service + Ingress
8. **Monitorear:** Prometheus + Grafana
9. **Escalar:** HPA automático o manual
10. **Actualizar:** Rolling update con nueva imagen
11. **Rollback:** Si hay problemas

**Ejemplo de uso completo:** E-commerce cloud-native en Kubernetes (GKE/EKS): Frontend React (3 réplicas) + Backend Spring Boot (HPA 3-10 réplicas basado en CPU) + MySQL StatefulSet (persistente) + Redis para cache + RabbitMQ para mensajería. Ingress con SSL para dominio. ConfigMaps para configuración, Secrets para passwords. Prometheus + Grafana para monitoreo. CI/CD con GitHub Actions que construye imágenes, las sube a registry, y actualiza deployments con `kubectl set image`. Todo en namespace dedicado con ResourceQuotas y LimitRanges.