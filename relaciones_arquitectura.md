# Tabla de Relaciones - Arquitectura CRM Educativo

## 📋 Relaciones completas para dibujar en Miro

| # | Origen | Destino | Tipo de Relación | Protocolo/Tecnología | Descripción |
|---|--------|---------|------------------|---------------------|-------------|
| **FRONTEND → GATEWAY** |
| 1 | Admin Dashboard | Kong Gateway | API REST | HTTPS/REST | Panel administrativo consume API |
| 2 | Web Pública | Kong Gateway | API REST | HTTPS/REST | Web pública consume API |
| 3 | Mobile App | Kong Gateway | API REST | HTTPS/REST | App móvil consume API |
| 4 | PWA | Kong Gateway | API REST | HTTPS/REST | PWA consume API |
| 5 | Admin Dashboard | GraphQL Federation | API GraphQL | GraphQL | Panel admin usa GraphQL |
| 6 | Web Pública | GraphQL Federation | API GraphQL | GraphQL | Web pública usa GraphQL |
| 7 | Mobile App | GraphQL Federation | API GraphQL | GraphQL | App móvil usa GraphQL |
| **GATEWAY → MICROSERVICIOS** |
| 8 | Kong Gateway | Traefik | Load Balancing | Load Balance | Kong distribuye carga a Traefik |
| 9 | Traefik | Auth Service | Enrutamiento | Route | Traefik enruta a Auth Service |
| 10 | Traefik | User Service | Enrutamiento | Route | Traefik enruta a User Service |
| 11 | Traefik | Course Service | Enrutamiento | Route | Traefik enruta a Course Service |
| 12 | Traefik | Payment Service | Enrutamiento | Route | Traefik enruta a Payment Service |
| 13 | Traefik | CRM Service | Enrutamiento | Route | Traefik enruta a CRM Service |
| 14 | Traefik | Analytics Service | Enrutamiento | Route | Traefik enruta a Analytics Service |
| 15 | Traefik | Notification Service | Enrutamiento | Route | Traefik enruta a Notification Service |
| 16 | Traefik | AI Service | Enrutamiento | Route | Traefik enruta a AI Service |
| 17 | Keycloak | Auth Service | Autenticación | OAuth2/JWT | Keycloak integra con Auth Service |
| 18 | GraphQL Federation | Auth Service | Schema Federation | Federation | GraphQL federa Auth Service |
| 19 | GraphQL Federation | User Service | Schema Federation | Federation | GraphQL federa User Service |
| 20 | GraphQL Federation | Course Service | Schema Federation | Federation | GraphQL federa Course Service |
| 21 | GraphQL Federation | CRM Service | Schema Federation | Federation | GraphQL federa CRM Service |
| **MICROSERVICIOS → DATOS** |
| 22 | Auth Service | PostgreSQL | Persistencia | User Auth Data | Auth Service almacena datos de usuarios |
| 23 | Auth Service | Redis | Cache | Session Cache | Auth Service cachea sesiones |
| 24 | User Service | PostgreSQL | Persistencia | User Profile | User Service almacena perfiles |
| 25 | User Service | Redis | Cache | Cache | User Service usa caché |
| 26 | User Service | Elasticsearch | Búsqueda | Search Index | User Service indexa búsquedas |
| 27 | Course Service | PostgreSQL | Persistencia | Course Data | Course Service almacena cursos |
| 28 | Course Service | AWS S3 | Almacenamiento | Video Storage | Course Service almacena videos |
| 29 | Course Service | Redis | Cache | Cache | Course Service usa caché |
| 30 | Course Service | Elasticsearch | Búsqueda | Course Search | Course Service indexa búsquedas |
| 31 | Payment Service | PostgreSQL | Persistencia | Transactions | Payment Service almacena transacciones |
| 32 | Payment Service | Apache Kafka | Eventos | Payment Events | Payment Service publica eventos |
| 33 | Payment Service | Redis | Cache | Cache | Payment Service usa caché |
| 34 | CRM Service | PostgreSQL | Persistencia | CRM Data | CRM Service almacena datos CRM |
| 35 | CRM Service | ClickHouse | Analytics | Analytics Data | CRM Service almacena analytics |
| 36 | CRM Service | Apache Kafka | Eventos | CRM Events | CRM Service publica eventos |
| 37 | CRM Service | Redis | Cache | Cache | CRM Service usa caché |
| 38 | Analytics Service | ClickHouse | Lectura | Read Analytics | Analytics Service lee analytics |
| 39 | Analytics Service | PostgreSQL | Metadatos | Meta Data | Analytics Service almacena metadatos |
| 40 | Analytics Service | Apache Kafka | Eventos | Consume Events | Analytics Service consume eventos |
| 41 | Notification Service | Redis | Cola | Queue Management | Notification Service gestiona colas |
| 42 | Notification Service | Apache Kafka | Eventos | Event Consumption | Notification Service consume eventos |
| 43 | Notification Service | PostgreSQL | Log | Notification Log | Notification Service registra logs |
| 44 | AI Service | PostgreSQL | Persistencia | AI Model Data | AI Service almacena modelos |
| 45 | AI Service | Redis | Cache | ML Cache | AI Service cachea ML |
| 46 | AI Service | Elasticsearch | Búsqueda | Vector Search | AI Service busca vectores |
| **SERVICIOS EXTERNOS** |
| 47 | AI Service | OpenAI | API Externa | API Calls | AI Service llama a OpenAI |
| 48 | Notification Service | SendGrid | Email | Email Sending | Notification Service envía emails |
| 49 | Notification Service | WhatsApp Business API | Mensajería | WhatsApp API | Notification Service envía WhatsApp |
| 50 | Notification Service | Firebase | Push | Push Notifications | Notification Service envía push |
| 51 | Payment Service | Stripe/PayPal | Pagos | Payment Processing | Payment Service procesa pagos |
| 52 | Course Service | Zoom/WebRTC | Video | Live Classes | Course Service integra clases en vivo |
| **INFRAESTRUCTURA** |
| 53 | Microservicios | Kubernetes | Despliegue | Deployed on | Microservicios desplegados en K8s |
| 54 | Kubernetes | Prometheus + Grafana | Monitoreo | Metrics | K8s envía métricas |
| 55 | Kubernetes | ELK Stack | Logging | Logs | K8s envía logs |
| 56 | Kubernetes | Jaeger | Tracing | Traces | K8s envía trazas |
| 57 | Kubernetes | HashiCorp Vault | Secretos | Secrets | K8s obtiene secretos |
| 58 | GitHub Actions | Kubernetes | CI/CD | Deploy | CI/CD despliega en K8s |
| 59 | Prometheus + Grafana | Apache Kafka | Eventos | Metrics Events | Monitoring publica eventos |
| 60 | ELK Stack | Apache Kafka | Eventos | Log Events | Logging publica eventos |
| **BUSINESS INTELLIGENCE** |
| 61 | Apache Superset | ClickHouse | Consultas | Analytics Queries | Superset consulta ClickHouse |
| 62 | Metabase | PostgreSQL | Datos | Operational Data | Metabase consulta PostgreSQL |
| 63 | Metabase | ClickHouse | Analytics | Analytics Data | Metabase consulta ClickHouse |
| 64 | Apache Airflow | PostgreSQL | ETL | ETL Source | Airflow extrae de PostgreSQL |
| 65 | Apache Airflow | ClickHouse | ETL | ETL Target | Airflow carga en ClickHouse |
| 66 | Apache Airflow | AWS S3 | Data Lake | Data Lake | Airflow gestiona Data Lake |
| **COMUNICACIÓN ENTRE MICROSERVICIOS** |
| 67 | User Service | Apache Kafka | Eventos | User Events | User Service publica eventos |
| 68 | Course Service | Apache Kafka | Eventos | Course Events | Course Service publica eventos |
| 69 | Payment Service | Apache Kafka | Eventos | Payment Events | Payment Service publica eventos |
| 70 | CRM Service | Apache Kafka | Eventos | CRM Events | CRM Service publica eventos |
| 71 | CRM Service | User Service | API Bidireccional | API Calls | CRM Service llama a User Service |
| 72 | User Service | CRM Service | API Bidireccional | API Calls | User Service responde a CRM |
| 73 | CRM Service | Course Service | API Bidireccional | API Calls | CRM Service llama a Course Service |
| 74 | Course Service | CRM Service | API Bidireccional | API Calls | Course Service responde a CRM |
| 75 | CRM Service | Payment Service | API Bidireccional | API Calls | CRM Service llama a Payment Service |
| 76 | Payment Service | CRM Service | API Bidireccional | API Calls | Payment Service responde a CRM |
| 77 | AI Service | User Service | API Bidireccional | User Data | AI Service obtiene datos de usuarios |
| 78 | User Service | AI Service | API Bidireccional | User Data | User Service envía datos a AI |
| 79 | AI Service | Course Service | API Bidireccional | Course Recommendations | AI Service envía recomendaciones |
| 80 | Course Service | AI Service | API Bidireccional | Course Recommendations | Course Service recibe recomendaciones |
| 81 | Notification Service | CRM Service | API Bidireccional | Campaign Triggers | Notification Service recibe triggers |
| 82 | CRM Service | Notification Service | API Bidireccional | Campaign Triggers | CRM Service envía triggers |

## 🎨 Consejos para dibujar en Miro:

### **Organización por Capas:**
1. **Frontend** (arriba) → Gateway → Microservicios → Datos (abajo)
2. **Servicios Externos** (izquierda)
3. **Infraestructura** (derecha)
4. **BI** (esquina inferior derecha)

### **Tipos de Líneas:**
- **Líneas sólidas** → Comunicación directa
- **Líneas punteadas** → Comunicación asíncrona (Kafka)
- **Líneas bidireccionales** → API calls bidireccionales
- **Colores diferentes** → Por tipo de protocolo (REST, GraphQL, Kafka, etc.)

### **Agrupación:**
- Agrupa los microservicios por contexto DDD
- Usa contenedores/frames para las capas principales
- Coloca las bases de datos cerca de sus servicios principales