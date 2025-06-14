# Documentación Completa - Diagramas C4 CRM Educativo

## 🎯 Nivel 1: Diagrama de Contexto

### Usuarios/Actores

| Actor | Tipo | Descripción | Relación con el sistema |
|-------|------|-------------|------------------------|
| Estudiante | Usuario externo | Usuario que se inscribe en cursos, consume contenido educativo y realiza pagos | Accede vía Web/Mobile App para cursos y pagos |
| Instructor | Usuario externo | Profesor que crea cursos, gestiona contenido y da clases en vivo | Utiliza Web App para crear y gestionar cursos |
| Administrador | Usuario interno | Administra usuarios, configura el sistema y gestiona operaciones | Accede vía Admin Dashboard para configuración |
| Marketing Manager | Usuario interno | Gestiona campañas de marketing, leads y estrategias de captación | Utiliza CRM Dashboard para campañas y leads |
| Sales Representative | Usuario interno | Gestiona clientes, oportunidades de venta y pipeline comercial | Accede vía CRM Dashboard para gestión de ventas |
| Soporte Técnico | Usuario interno | Brinda atención al cliente y resuelve problemas técnicos | Utiliza Support Dashboard para atención |
| Creador de Contenido | Usuario externo | Desarrolla material educativo y recursos de aprendizaje | Accede vía Content Management para crear material |
| Business Analyst | Usuario interno | Analiza métricas de negocio y genera reportes | Utiliza Analytics Dashboard para reportes |

### Sistemas Externos

| Sistema | Tipo | Descripción | Relación con el sistema |
|---------|------|-------------|------------------------|
| Stripe | Sistema externo | Procesamiento de pagos con tarjeta de crédito y débito | Integrado vía REST API para pagos |
| PayPal | Sistema externo | Procesamiento de pagos alternativos y billeteras digitales | Integrado vía REST API para pagos alternativos |
| SendGrid | Sistema externo | Servicio de envío masivo de emails y campañas de marketing | Integrado vía REST API para emails |
| WhatsApp Business API | Sistema externo | Mensajería empresarial y soporte via WhatsApp | Integrado vía Business API para mensajería |
| Firebase | Sistema externo | Push notifications para aplicaciones móviles | Integrado vía Firebase Admin SDK |
| Zoom | Sistema externo | Plataforma de videoconferencias para clases en vivo | Integrado vía Zoom API para clases |
| OpenAI GPT-4 | Sistema externo | Inteligencia artificial para chatbots y asistentes virtuales | Integrado vía OpenAI API para IA |
| Google Analytics | Sistema externo | Analytics web y seguimiento de comportamiento de usuarios | Integrado vía Measurement Protocol |
| AWS Cloud | Sistema externo | Infraestructura cloud para hosting, almacenamiento y servicios | Desplegado en AWS Services |
| Datadog | Sistema externo | Monitoreo de aplicaciones, logs e infraestructura | Integrado vía Agent/API para monitoreo |
| HashiCorp Vault | Sistema externo | Gestión segura de secretos y credenciales | Integrado vía Vault API para secretos |
| Snowflake | Sistema externo | Data warehouse en la nube para analytics avanzados | Integrado vía Snowflake Connector |

## 🧱 Nivel 2: Diagrama de Contenedores

| Contenedor | Tecnología | Descripción / Responsabilidad | Conexiones / Relación |
|------------|------------|------------------------------|----------------------|
| Web Pública | Next.js 14 + TypeScript, Tailwind CSS | Aplicación web pública para estudiantes, instructores y creadores | Consume Kong Gateway y GraphQL Gateway |
| Admin Dashboard | Angular 17 + NgRx, Material UI | Panel de administración para usuarios internos (admin, marketing, sales, soporte, analysts) | Conecta con Kong Gateway y GraphQL Gateway |
| Mobile App | Flutter 3.x + Dart, GetX/Riverpod | Aplicación móvil para estudiantes e instructores | Consume Kong Gateway y GraphQL Gateway |
| PWA | Service Workers, IndexedDB | Aplicación web progresiva con capacidades offline | Conecta con Kong Gateway |
| Kong Gateway | Kong + Rate Limiting + Load Balancing | API Gateway principal para enrutamiento y control | Distribuye requests a Traefik y servicios |
| Traefik | Reverse Proxy + SSL Termination | Proxy reverso con terminación SSL | Enruta a todos los microservicios |
| GraphQL Federation | Apollo Federation + Schema Stitching | Gateway GraphQL federado | Conecta con Auth, User, Course, CRM services |
| Keycloak | OAuth 2.0/OIDC + JWT + SSO | Servicio de autenticación centralizado | Integra con Auth Service |
| Auth Service | Spring Boot 3 + Spring Security + JWT | Contexto de identidad y acceso | Conecta con PostgreSQL, Redis, Vault |
| User Service | Node.js + Express + TypeScript + Prisma | Contexto de gestión de usuarios | Conecta con PostgreSQL, Redis, Elasticsearch |
| Course Service | Python + FastAPI + SQLAlchemy + Celery | Contexto de aprendizaje y cursos | Conecta con PostgreSQL, Redis, S3, Elasticsearch |
| Payment Service | Java + Spring Boot + Stripe SDK + Event Sourcing | Contexto de pagos con Event Sourcing | Conecta con PostgreSQL, Redis, Stripe, PayPal |
| CRM Core | C# + .NET 8 + Entity Framework + MediatR CQRS | Contexto CRM con patrón CQRS | Conecta con PostgreSQL, ClickHouse, Redis |
| Analytics Service | Python + Django + Pandas + Apache Airflow | Contexto de analytics con ETL pipelines | Conecta con ClickHouse, PostgreSQL, Airflow |
| Notification Service | Node.js + NestJS + Bull Queue + WebSocket | Contexto de comunicación tiempo real | Conecta con PostgreSQL, Redis, SendGrid, Firebase |
| AI & ML Service | Python + FastAPI + LangChain + Hugging Face | Contexto de inteligencia artificial | Conecta con PostgreSQL, Redis, OpenAI |
| PostgreSQL 15 | OLTP Database + Connection Pooling + Read Replicas | Base de datos principal transaccional | Usada por todos los servicios core |
| ClickHouse | OLAP Warehouse + Columnar Storage + Real-time Analytics | Data warehouse para analytics | Usada por CRM y Analytics services |
| Redis Cluster | Cache Layer + Session Store + Rate Limiting | Caché distribuido y gestión de sesiones | Usada por todos los servicios |
| Elasticsearch | Search Engine + Full-text Search + ML Features | Motor de búsqueda y ML | Usada por User, Course, AI services |
| Apache Kafka | Message Broker + Event Streaming + CQRS Events | Bus de eventos para arquitectura event-driven | Conecta todos los servicios |
| AWS S3 + CloudFront | File Storage + CDN + MediaConvert + Video Streaming | Almacenamiento y distribución de contenido | Usada por Course Service y frontend apps |
| Apache Superset | Dashboards + Data Visualization | Dashboards empresariales | Conecta con ClickHouse |
| Metabase | Self-service BI + Reporting | Reportes autoservicio | Conecta con PostgreSQL y ClickHouse |
| Apache Airflow | ETL/ELT Pipelines + Data Orchestration | Orquestación de pipelines de datos | Conecta con PostgreSQL, ClickHouse, S3 |

## ⚙️ Nivel 3: Diagrama de Componentes

### Auth Service (Spring Boot 3)

| Componente | Contenedor | Descripción | Tecnología | Se comunica con |
|------------|------------|-------------|------------|-----------------|
| Auth Controller | Auth Service | Endpoints de autenticación y login | Spring MVC | JWT Filter, Auth Service Impl |
| User Controller | Auth Service | Gestión CRUD de usuarios | Spring MVC | User Service Impl, Validation |
| JWT Filter | Auth Service | Filtro de validación de tokens JWT | Spring Security | Security Config, JWT Provider |
| Auth Service Impl | Auth Service | Lógica de negocio de autenticación | Spring Service | User Aggregate, Password Encoder |
| User Aggregate | Auth Service | Agregado de dominio Usuario con reglas | Domain Entity | User Repository, Auth Domain Service |
| User Repository | Auth Service | Repositorio de persistencia de usuarios | Spring Data JPA | PostgreSQL Database |
| JWT Provider | Auth Service | Generación y validación de tokens | JJWT Library | HashiCorp Vault, Redis Cache |
| Password Encoder | Auth Service | Codificación segura de contraseñas | BCrypt | HashiCorp Vault para salts |
| Event Publisher | Auth Service | Publicación de eventos de dominio | Spring Events + Kafka | Apache Kafka |

### User Service (Node.js + Express)

| Componente | Contenedor | Descripción | Tecnología | Se comunica con |
|------------|------------|-------------|------------|-----------------|
| User Controller | User Service | API REST para gestión de usuarios | Express Router | User Application Service |
| Profile Controller | User Service | API REST para gestión de perfiles | Express Router | Profile Service |
| Auth Middleware | User Service | Middleware de autenticación JWT | Express Middleware | Auth Service |
| User Application Service | User Service | Orquestación de casos de uso | TypeScript Class | User Aggregate, User Factory |
| User Aggregate | User Service | Agregado Usuario con invariantes de negocio | Domain Entity | User Repository Interface |
| User Repository Impl | User Service | Implementación de repositorio | Prisma ORM | PostgreSQL Database |
| Search Repository | User Service | Repositorio de búsqueda de usuarios | Elasticsearch Client | Elasticsearch |
| Cache Service | User Service | Servicio de caché de usuarios | Redis Client | Redis Cluster |
| Event Publisher | User Service | Publicador de eventos de usuario | Kafka Producer | Apache Kafka |

### Course Service (Python + FastAPI)

| Componente | Contenedor | Descripción | Tecnología | Se comunica con |
|------------|------------|-------------|------------|-----------------|
| Course Router | Course Service | API REST para gestión de cursos | FastAPI Router | Course Application Service |
| Lesson Router | Course Service | API REST para gestión de lecciones | FastAPI Router | Lesson Application Service |
| Auth Middleware | Course Service | Middleware de autenticación | FastAPI Middleware | Auth Service |
| Course Application Service | Course Service | Casos de uso de cursos | Python Class | Course Aggregate, Domain Service |
| Course Aggregate | Course Service | Agregado Curso con reglas de negocio | Domain Entity | Course Repository Interface |
| Course Repository Impl | Course Service | Implementación repositorio cursos | SQLAlchemy ORM | PostgreSQL Database |
| Video Processing Service | Course Service | Procesamiento de videos educativos | FFmpeg + Celery | AWS S3, Celery Workers |
| Search Repository | Course Service | Repositorio de búsqueda de cursos | Elasticsearch Client | Elasticsearch |
| File Storage Service | Course Service | Servicio de almacenamiento de archivos | AWS S3 Client | AWS S3 + CloudFront |
| Event Publisher | Course Service | Publicador de eventos de cursos | Kafka Producer | Apache Kafka |

### Payment Service (Java + Spring Boot)

| Componente | Contenedor | Descripción | Tecnología | Se comunica con |
|------------|------------|-------------|------------|-----------------|
| Payment Controller | Payment Service | API REST para procesamiento de pagos | Spring MVC | Payment Application Service |
| Webhook Controller | Payment Service | Recepción de webhooks de gateways | Spring MVC | Payment Application Service |
| Payment Security Filter | Payment Service | Filtro de seguridad para transacciones | Spring Security | Security Config |
| Payment Application Service | Payment Service | Casos de uso de pagos | Spring Service | Payment Aggregate, Fraud Detection |
| Payment Aggregate | Payment Service | Agregado Pago con Event Sourcing | Domain Entity | Event Store, Money VO |
| Event Store | Payment Service | Almacén de eventos para Event Sourcing | Custom Implementation | PostgreSQL Database |
| Stripe Gateway | Payment Service | Gateway de integración con Stripe | Stripe Java SDK | Stripe API |
| PayPal Gateway | Payment Service | Gateway de integración con PayPal | PayPal Java SDK | PayPal API |
| Fraud Detection Service | Payment Service | Servicio de detección de fraudes | Spring Service | Cache Service, ML Models |
| Event Publisher | Payment Service | Publicador de eventos de pagos | Spring Kafka | Apache Kafka |

### CRM Service (C# + .NET 8)

| Componente | Contenedor | Descripción | Tecnología | Se comunica con |
|------------|------------|-------------|------------|-----------------|
| Lead Controller | CRM Service | API REST para gestión de leads | ASP.NET Core MVC | Lead Command/Query Handlers |
| Customer Controller | CRM Service | API REST para gestión de clientes | ASP.NET Core MVC | Customer Command/Query Handlers |
| Lead Command Handler | CRM Service | Manejador de comandos CQRS para leads | MediatR Handler | Lead Aggregate, Lead Repository |
| Lead Query Handler | CRM Service | Manejador de consultas CQRS para leads | MediatR Handler | Lead Repository, CRM Domain Service |
| Lead Aggregate | CRM Service | Agregado Lead con reglas de negocio | Domain Entity | Lead Repository Interface |
| Customer Aggregate | CRM Service | Agregado Customer con reglas CRM | Domain Entity | Customer Repository Interface |
| Lead Repository Impl | CRM Service | Implementación repositorio leads | Entity Framework Core | PostgreSQL Database |
| Analytics Repository | CRM Service | Repositorio de analytics CRM | ClickHouse Client | ClickHouse Database |
| Cache Service | CRM Service | Servicio de caché CRM | IMemoryCache + Redis | Redis Cluster |
| Event Publisher | CRM Service | Publicador de eventos CRM | MediatR + Kafka | Apache Kafka |

### Analytics Service (Python + Django)

| Componente | Contenedor | Descripción | Tecnología | Se comunica con |
|------------|------------|-------------|------------|-----------------|
| Metrics View | Analytics Service | API REST para métricas de negocio | Django REST API | Metrics Service |
| Reports View | Analytics Service | API REST para generación de reportes | Django REST API | Reports Service |
| Dashboards View | Analytics Service | API REST para gestión de dashboards | Django REST API | Dashboard Service |
| Metrics Service | Analytics Service | Servicio de cálculo de métricas | Django Service | Metric Aggregate, OLAP Repository |
| Reports Service | Analytics Service | Servicio de generación de reportes | Django Service | Report Aggregate, Reports Repository |
| Data Processing Service | Analytics Service | Procesamiento de datos con Pandas | Pandas + NumPy | Data Quality Policy, Search Repository |
| OLAP Repository | Analytics Service | Repositorio para consultas analíticas | ClickHouse Client | ClickHouse Database |
| Data Ingestion DAG | Analytics Service | DAG de ingesta de datos ETL | Airflow DAG | Kafka, PostgreSQL, ClickHouse |
| ML Pipeline DAG | Analytics Service | DAG de pipeline de Machine Learning | Airflow DAG | ClickHouse, ML Models |
| Metrics Worker | Analytics Service | Worker de procesamiento de métricas | Celery Worker | ClickHouse, Monitoring |

### Notification Service (Node.js + NestJS)

| Componente | Contenedor | Descripción | Tecnología | Se comunica con |
|------------|------------|-------------|------------|-----------------|
| Notification Controller | Notification Service | API REST para gestión de notificaciones | NestJS Controller | Notification Service Impl |
| Template Controller | Notification Service | API REST para plantillas de mensajes | NestJS Controller | Template Service |
| WebSocket Gateway | Notification Service | Gateway para notificaciones tiempo real | NestJS WebSocket | Notification Service Impl |
| Auth Guard | Notification Service | Guard de autenticación NestJS | NestJS Guard | Auth Service |
| Notification Service Impl | Notification Service | Servicio principal de notificaciones | NestJS Service | Notification Aggregate, Queue Service |
| Template Service | Notification Service | Servicio de gestión de plantillas | NestJS Service | Template Aggregate, Template Repository |
| Delivery Service | Notification Service | Servicio de entrega de notificaciones | NestJS Service | Delivery Policy, Providers |
| Notification Aggregate | Notification Service | Agregado Notificación con reglas | Domain Entity | Message VO, Delivery Status VO |
| Email Provider | Notification Service | Proveedor de servicios de email | SendGrid SDK | SendGrid API |
| SMS Provider | Notification Service | Proveedor de servicios de SMS | Twilio SDK | Twilio API |
| Push Provider | Notification Service | Proveedor de push notifications | Firebase Admin SDK | Firebase API |
| Queue Service | Notification Service | Servicio de colas de notificaciones | Bull Queue + Redis | Email/SMS/Push Processors |
| Event Publisher | Notification Service | Publicador de eventos de notificación | Kafka Producer | Apache Kafka |