🛒 Infraestructura en AWS - E-Commerce Escalable

Este repositorio contiene los templates de AWS CloudFormation para desplegar la infraestructura de una aplicación e-commerce de tres capas (Frontend, Backend y Datos).

El diseño sigue principios de escalabilidad, alta disponibilidad, seguridad y optimización de costos, utilizando Infraestructura como Código (IaC) para garantizar que los despliegues sean reproducibles, automatizados y fáciles de mantener.

📌 Estructura del Proyecto
infra/
 ├── templates/
 │    ├── vpc.yml              # Red VPC, subnets públicas/privadas, ruteo
 │    ├── infra-app.yml        # Seguridad, SGs, roles
 │    └── ecs-ecr-iam.yml      # ECS Cluster, repositorios ECR, roles IAM
 └── README_infra.md           # Guía detallada de despliegue

📌 Despliegue de Stacks

Los templates se deben desplegar manualmente desde local con AWS CLI:

1️⃣ VPC
aws cloudformation deploy \
  --stack-name ecommerce-stack-vpc \
  --template-file templates/vpc.yml \
  --capabilities CAPABILITY_NAMED_IAM \
  --region us-east-2

2️⃣ Seguridad (SGs, roles básicos)
aws cloudformation deploy \
  --stack-name ecommerce-stack-security \
  --template-file templates/infra-app.yml \
  --capabilities CAPABILITY_NAMED_IAM \
  --region us-east-2

3️⃣ ECS, ECR e IAM
aws cloudformation deploy \
  --stack-name ecommerce-stack-ecs-ecr-iam \
  --template-file templates/ecs-ecr-iam.yml \
  --capabilities CAPABILITY_NAMED_IAM \
  --region us-east-2

📌 Características Clave

Arquitectura escalable y altamente disponible

Balanceadores de carga y ECS para manejar tráfico variable.

Auto Scaling integrado para responder a picos de demanda.

Seguridad incorporada

IAM Roles y Policies siguiendo privilegio mínimo.

Security Groups segmentando frontend, backend y base de datos.

Infraestructura modular

Templates separados para red, seguridad y cómputo.

Fácil reutilización en otros entornos (dev, qa, prod).

100% IaC

Control de versiones en GitHub.

Despliegue automatizado vía AWS CLI y adaptable a pipelines (GitHub Actions, Jenkins, etc.).

📌 Requisitos Previos

AWS CLI configurado con credenciales.

Permisos para crear recursos (IAM, VPC, ECS, ECR).

Región: us-east-2.
