# Módulo 4: Dashboard de Estadísticas - Acortador de URLs

Este repositorio contiene el código fuente y la infraestructura como código (IaC) para el *Módulo 4: Dashboard de Estadísticas*. Este componente representa la interfaz gráfica (Frontend) mediante la cual los usuarios pueden monitorear el rendimiento y tráfico de sus enlaces acortados.

##  Objetivo del Módulo
Proveer una aplicación web estática y responsiva que actúe como el panel de control analítico del sistema. Este módulo se encarga de consumir la API REST de estadísticas (Módulo 3), procesar el JSON de respuesta y renderizar de forma visual el total de clics y la gráfica histórica de visitas por fecha.

### Características Clave:
* *Consumo de API:* Integración directa vía fetch al endpoint del Módulo 3 (GET /stats/{codigo}).
* *Visualización de Datos:* Renderizado de gráficos dinámicos (usando librerías como Chart.js) para mostrar el mapa de analytics proveniente de DynamoDB.
* *Alojamiento Serverless:* Hosting estático de alta disponibilidad utilizando Amazon S3.
* *Distribución Global:* Despliegue a través de la CDN Amazon CloudFront para garantizar baja latencia y acceso seguro mediante HTTPS.

## Tecnologías Utilizadas
* *Frontend:* HTML5, CSS3, JavaScript (Vanilla).
* *AWS S3:* Almacenamiento y hosting de los archivos estáticos del sitio web.
* *AWS CloudFront:* Red de entrega de contenido (CDN) para exponer la interfaz de usuario de manera segura.
* *Terraform:* Aprovisionamiento automatizado de los buckets, políticas de acceso y distribuciones.

## Estructura del Proyecto
```text
acortador-modulo4/
├── frontend/
│   ├── index.html        # Estructura principal del Dashboard
├── terraform/
│   ├── main.tf           # Declaración de recursos S3 y CloudFront
│   ├── variables.tf      # Variables de configuración
│   └── outputs.tf        # URL pública de la distribución de CloudFront
└── README.md             # Documentación formal del módulo
 Instrucciones de Despliegue
1. Despliegue de la Infraestructura (AWS)
Navega al directorio de Terraform:

Bash
cd terraform
Inicializa el entorno y aplica los cambios:

Bash
terraform init
terraform apply --auto-approve
Anota la URL de CloudFront o del Bucket S3 generada en los Outputs de la terminal.

2. Configuración e Integración (Frontend)
Abre el archivo frontend/app.js (o donde se encuentre la lógica de consumo).

Reemplaza la variable de la URL base con el Invoke URL del Módulo 3:

JavaScript
const API_STATS_URL = "[https://tu-api-modulo3.execute-api.us-east-1.amazonaws.com/prod/](https://tu-api-modulo3.execute-api.us-east-1.amazonaws.com/prod/)";
Sube los archivos de la carpeta frontend/ al bucket de S3 recién creado. Puedes hacerlo vía la consola de AWS o con el siguiente comando de AWS CLI:

Bash
aws s3 sync ./frontend s3://nombre-de-tu-bucket-modulo4
 Consideraciones de Seguridad y CORS
Para que este Dashboard pueda renderizar los datos correctamente, el Módulo 3 debe tener habilitadas las políticas de CORS (Cross-Origin Resource Sharing). Si el navegador bloquea la petición al consultar un código, asegúrese de verificar que el API Gateway de estadísticas permite el método GET y posee el encabezado Access-Control-Allow-Origin.

 Autoría
Desarrollador Responsable: Angely Julieth Ortega Ospino
