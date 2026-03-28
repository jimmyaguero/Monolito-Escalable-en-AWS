Un buen README.md es la cara visible de tu repositorio y, para un Arquitecto Cloud, es la oportunidad de demostrar que sabes documentar infraestructura profesionalmente.

Aquí tienes una estructura sólida, técnica y lista para copiar.

Monolito Escalable en AWS - Módulo 6
Este proyecto forma parte de la evaluación del Módulo 6 de Alkemy / AWS Academy. Consiste en la migración de una aplicación monolítica on-premise hacia una arquitectura en la nube de AWS, garantizando Alta Disponibilidad, Escalabilidad Automática y Monitoreo.

Situación Inicial
La empresa presentaba caídas constantes en sus servicios debido a un servidor único con recursos limitados. La solución propuesta migra esta carga a AWS utilizando servicios gestionados para eliminar puntos únicos de fallo.

Arquitectura
La solución implementa los siguientes servicios de Amazon Web Services:

Amazon EC2: Servidor de cómputo para el monolito (Amazon Linux 2023).

Application Load Balancer (ALB): Punto de entrada único que distribuye el tráfico hacia las instancias saludables.

Auto Scaling Group (ASG): Gestión elástica de instancias (Mín: 1, Máx: 2) según la demanda.

Amazon CloudWatch: Sistema de alarmas basado en el uso de CPU para disparar el escalado.

Amazon DynamoDB: Capa de persistencia NoSQL para el registro de visitas.

Diagrama de Red (Mermaid)
Code snippet
graph TD
    Internet((Internet)) --> ALB[Application Load Balancer]
    subgraph VPC
        ALB --> ASG[Auto Scaling Group]
        subgraph Disponibilidad
            ASG --> EC2[EC2 Instance - Monolito]
        end
        EC2 <--> DDB[(Amazon DynamoDB)]
        EC2 -.-> CW[CloudWatch Alarms]
    end
Implementación Paso a Paso
Cómputo: Despliegue de instancia base con servidor Apache/Nginx mediante User Data.

Red y Seguridad: Configuración de Security Groups permitiendo tráfico HTTP (80), HTTPS (443) y SSH (22).

Alta Disponibilidad: Creación de un Target Group y un ALB para balancear el tráfico entre zonas de disponibilidad.

Elasticidad: Configuración de Launch Template y ASG para asegurar la disponibilidad del servicio.

Observabilidad: Creación de alarmas en CloudWatch con un umbral de CPU > 80% para escalado horizontal.

Lecciones Aprendidas
Troubleshooting: Resolución de errores 503 mediante el ajuste de Health Checks y alineación de Security Groups entre el ALB y las instancias.

Infraestructura como Valor: La importancia de separar la capa de datos (DynamoDB) del cómputo para facilitar el escalado sin pérdida de información.
