# Backend - Gestión de Tareas

Backend API construido con Node.js, Express, TypeScript y TypeORM, desplegado en AWS Lambda con API Gateway.

## 🚀 Tecnologías

- **Node.js 20.x**
- **Express.js** - Framework web
- **TypeScript** - Tipado estático
- **TypeORM** - ORM para PostgreSQL
- **AWS Lambda** - Funciones serverless
- **API Gateway** - Gestión de APIs
- **RDS PostgreSQL** - Base de datos
- **Terraform** - Infraestructura como código

## 📋 Requisitos Previos

- Node.js 20.x o superior
- PostgreSQL (para desarrollo local)
- AWS CLI configurado
- Terraform 1.6.0 o superior
- Cuenta de AWS

## 🛠️ Configuración Local

### 1. Instalar dependencias

```bash
npm install 
```

### 2. Configurar variables de entorno

Crea un archivo `.env` basado en `.env.example`:

```env
# Database
DB_HOST=localhost
DB_PORT=5432
DB_USER=postgres
DB_PASSWORD=tu_password
DB_NAME=gestion_tareas
DB_SSL=false

# Server
SERVER_PORT=3000

# JWT
JWT_SECRET=tu_secret_key_super_seguro
```

### 3. Ejecutar en modo desarrollo

```bash
npm run dev
```

La API estará disponible en `http://localhost:3000`

## 🏗️ Build y Deploy

### Build local

```bash
npm run build
```

### Deploy a AWS

El deploy se ejecuta automáticamente mediante GitHub Actions cuando haces push a la rama `main`.

## 🔐 Secrets de GitHub

Configura los siguientes secrets en tu repositorio de GitHub:

### AWS Credentials
- `AWS_ACCESS_KEY_ID` - Access Key ID de AWS
- `AWS_SECRET_ACCESS_KEY` - Secret Access Key de AWS

### Variables de Terraform
- `TF_VAR_JWT_SECRET` - Secret para JWT
- `TF_VAR_DB_USERNAME` - Usuario de la base de datos RDS
- `TF_VAR_DB_PASSWORD` - Contraseña de la base de datos RDS

## 📁 Estructura del Proyecto

```
backend/
├── src/
│   ├── entities/          # Entidades de TypeORM
│   ├── middleware/        # Middlewares de Express
│   ├── modules/
│   │   ├── auth/         # Módulo de autenticación
│   │   └── tasks/        # Módulo de tareas
│   ├── routes/           # Definición de rutas
│   ├── utils/            # Utilidades
│   ├── ormconfig.ts      # Configuración de TypeORM
│   └── server.ts         # Punto de entrada
├── terraform/            # Infraestructura como código
│   ├── lambda.tf         # Funciones Lambda
│   ├── api_gateway.tf    # API Gateway
│   ├── rds.tf            # Base de datos RDS
│   └── ...
└── .github/
    └── workflows/
        └── deploy.yml    # Pipeline CI/CD
```

## 🔌 Endpoints de la API

### Autenticación
- `POST /api/auth/register` - Registrar usuario
- `POST /api/auth/login` - Iniciar sesión
- `POST /api/auth/refresh-token` - Refrescar token

### Tareas (requiere autenticación)
- `GET /api/tasks` - Listar tareas
- `POST /api/tasks` - Crear tarea
- `PUT /api/tasks/:id` - Actualizar tarea
- `DELETE /api/tasks/:id` - Eliminar tarea

## 🧪 Testing

```bash
npm test
```

## 📦 Infraestructura AWS

La infraestructura incluye:

- **2 Funciones Lambda**: auth y tasks
- **API Gateway HTTP**: Para enrutamiento
- **RDS PostgreSQL**: Base de datos
- **VPC**: Red privada con subnets públicas y privadas
- **Security Groups**: Configuración de firewall
- **CloudWatch Logs**: Logs de las funciones Lambda

## 🔄 CI/CD Pipeline

El pipeline de GitHub Actions:

1. Instala dependencias
2. Compila TypeScript
3. Empaqueta funciones Lambda
4. Despliega infraestructura con Terraform
5. Muestra la URL del API Gateway

## 📝 Notas Importantes

- La base de datos RDS se crea automáticamente con Terraform
- El estado de Terraform se guarda en S3: `gestion-tareas-terraform-state-90968`
- Los logs de Lambda se retienen por 7 días en CloudWatch
- SSL está deshabilitado para desarrollo local, habilitado en producción

## 🤝 Contribuir

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📄 Licencia

ISC
