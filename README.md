# 🛒 Infraestructura en AWS - E-Commerce Escalable  

Este repositorio contiene los **templates de AWS CloudFormation** y configuraciones relacionadas con la **infraestructura del e-commerce**, incluyendo red, seguridad, cómputo, CI/CD y monitoreo.  

El diseño sigue principios de **escalabilidad, alta disponibilidad, seguridad y optimización de costos**, utilizando **Infraestructura como Código (IaC)** para garantizar despliegues reproducibles, automatizados y fáciles de mantener.  

---

## 📌 Estructura del Proyecto  
```
infra/
├── templates/
│ ├── vpc.yml # Red VPC, subnets públicas/privadas, ruteo
│ ├── infra-app.yml # Seguridad, SGs, roles
│ └── ecs-ecr-iam.yml # ECS Cluster, repositorios ECR, roles IAM
└── README_infra.md # Guía detallada de despliegue
```

---

## 📌 Despliegue de Stacks  

- ***Comandos para ejecutar la infraestructura (CloudFormation) manualmente desde local***

1. Desplegar la **VPC**  
```
   aws cloudformation deploy \
     --stack-name ecommerce-stack-vpc \
     --template-file templates/vpc.yml \
     --capabilities CAPABILITY_NAMED_IAM \
     --region us-east-2
Desplegar la Seguridad (SGs, roles básicos)

aws cloudformation deploy \
  --stack-name ecommerce-stack-security \
  --template-file templates/infra-app.yml \
  --capabilities CAPABILITY_NAMED_IAM \
  --region us-east-2
Desplegar ECS, ECR e IAM

aws cloudformation deploy \
  --stack-name ecommerce-stack-ecs-ecr-iam \
  --template-file templates/ecs-ecr-iam.yml \
  --capabilities CAPABILITY_NAMED_IAM \
  --region us-east-2
```

🔄 CI/CD (Integración y Despliegue Continuo)
- Pipelines definidos en GitHub Actions / Jenkins para:
- Construcción de imágenes Docker.
- Publicación de imágenes en Amazon ECR.
- Despliegue automático en Amazon ECS (Fargate).
- Despliegue de infraestructura con CloudFormation.
- Uso de Infrastructure as Code (IaC) para entornos dev, qa y prod.

📊 Monitoreo y Observabilidad
- Amazon CloudWatch
- Logs centralizados (ECS, Lambdas, balanceadores).
- Métricas personalizadas de CPU, memoria, latencia y throughput.
- Alarmas configuradas para alta latencia, errores 5xx y baja disponibilidad.
- Trazabilidad de peticiones entre microservicios.
- Dashboards en CloudWatch para métricas clave:
  - Estado de ECS Services y tareas.
  - Salud de instancias detrás del Load Balancer.
  - Consumo de base de datos.

🔒 Seguridad
- Gestión de accesos con IAM
- Roles y Policies bajo principio de privilegio mínimo.
- Separación de roles por servicio (ECS, ECR, RDS, CI/CD).
- AWS Secrets Manager
- Manejo de contraseñas y secretos de forma centralizada y cifrada.

Network Security
- Subnets públicas/privadas para aislar componentes.
- Security Groups segmentados (frontend, backend, base de datos).
- Cifrado en tránsito (HTTPS con TLS).
- AWS WAF + Shield
- Protección contra ataques comunes (SQL Injection, XSS, DDoS).

✅ Requisitos Previos
AWS CLI configurado con credenciales.

Permisos para crear recursos (IAM, VPC, ECS, ECR, CloudWatch).

Región: us-east-2.

