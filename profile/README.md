# 🏭 Tecda Maniquí Factory - Tercer Año TECDA

¡Bienvenido a la organización oficial de desarrollo de **Tecda Maniquí Factory**! 

Este espacio de trabajo unifica el diseño, la implementación y la analítica del sistema de producción, inventario y ventas de la fábrica de maniquíes **Tecda**, abarcando las materias de **Gestión de Bases de Datos** y **Prácticas Profesionalizantes** de la tecnicatura.

---

## 🏗️ Arquitectura Desacoplada (3 Capas)

El ecosistema completo se divide en tres componentes totalmente desacoplados e independientes para garantizar modularidad, alta disponibilidad y un flujo de trabajo profesional:

```mermaid
graph TD
    subgraph Frontend_App [Capa de Presentación]
        A["🎨 Cliente Web (Vite + React)"]
    end
    subgraph Service_App [Capa de Lógica]
        B["🔌 Servidor API (Node.js + Express)"]
        C["📖 Swagger UI (/api-docs)"]
    end
    subgraph Database_App [Capa de Datos]
        D["🗃️ Base de Datos (MariaDB / MySQL)"]
    end

    A -- "Consume REST JSON (Puerto 8082)" --> B
    B -- "Conexión Resiliente (Puerto 3307)" --> D
    C -- "Mapeo de Endpoints" --> B
```

---

## 📂 Repositorios y Componentes del Proyecto

La solución está organizada de forma simétrica en **tres repositorios independientes** dentro de esta organización. Haz clic en cada uno para acceder a su código fuente e instrucciones específicas:

### 1. 🗃️ [tp-maniqui-db](https://github.com/tecda-maniqui-factory/tp-maniqui-db)
* **Responsabilidad:** Capa de Datos (DDL, triggers, stored procedures, vistas analíticas de producción y entornos rápidos con Docker Compose).
* **Puerto local:** `3307` *(exponiendo MariaDB o MySQL)*.
* **Documentación destacada:**
  * [docs/README.md](https://github.com/tecda-maniqui-factory/tp-maniqui-db/blob/main/docs/README.md) *(Manual de base de datos y scripts)*.
  * [docs/DATABASE_LOGIC.md](https://github.com/tecda-maniqui-factory/tp-maniqui-db/blob/main/docs/DATABASE_LOGIC.md) *(Lógica programable, SPs y automatizaciones)*.
  * [docs/tp-maniqui-docker.md](https://github.com/tecda-maniqui-factory/tp-maniqui-db/blob/main/docs/tp-maniqui-docker.md) *(Despliegue y volúmenes con Docker)*.

### 2. 🔌 [tp-maniqui-backend](https://github.com/tecda-maniqui-factory/tp-maniqui-backend)
* **Responsabilidad:** Capa de Negocio y Servicios (API REST de Express, controladores modulares y especificación formal de endpoints).
* **Puerto local:** `8082` *(para evitar colisión con el puente local de WhatsApp)*.
* **Documentación destacada:**
  * [openapi.yaml](https://github.com/tecda-maniqui-factory/tp-maniqui-backend/blob/main/openapi.yaml) *(Especificación OpenAPI 3.0 de la API)*.
  * [tests/integration/api_tests.http](https://github.com/tecda-maniqui-factory/tp-maniqui-backend/blob/main/tests/integration/api_tests.http) *(Suite interactiva REST Client para pruebas)*.

### 3. 🎨 [tp-maniqui-frontend](https://github.com/tecda-maniqui-factory/tp-maniqui-frontend)
* **Responsabilidad:** Capa de Presentación (Dashboard de control administrativo responsivo Bento Box con estética Obsidian Glassmorphism).
* **Puerto local:** `5173`.
* **Documentación destacada:**
  * [docs/README.md](https://github.com/tecda-maniqui-factory/tp-maniqui-frontend/blob/main/docs/README.md) *(Manual de diseño visual y componentes)*.
  * [docs/ROLES_Y_OPERACIONES.md](https://github.com/tecda-maniqui-factory/tp-maniqui-frontend/blob/main/docs/ROLES_Y_OPERACIONES.md) *(Manual de operaciones y perfiles RBAC)*.
  * [docs/ARCHITECTURE.md](https://github.com/tecda-maniqui-factory/tp-maniqui-frontend/blob/main/docs/ARCHITECTURE.md) *(Detalles de la arquitectura modular)*.

---

## ⚡ Guía de Inicio Rápido (Clonado y Despliegue Local)

Sigue esta secuencia ordenada paso a paso para clonar y levantar el ecosistema completo de forma local en tu máquina:

### Paso 1: Clonar y Levantar la Base de Datos (MariaDB/MySQL)
Clona el repositorio del módulo de base de datos, navega a la carpeta de configuración de Docker y levanta el contenedor expuesto por defecto en el puerto **`3307`**:
```bash
# 1. Clonar el repositorio de base de datos
git clone https://github.com/tecda-maniqui-factory/tp-maniqui-db.git
cd tp-maniqui-db/docker/mariadb

# 2. Iniciar el contenedor de MariaDB
docker compose up -d
```
*Nota: La base de datos se inicializará y cargará de forma automatizada toda la estructura de tablas y datos semilla de prueba (seeds).*

### Paso 2: Clonar, Configurar y Levantar el Servidor Backend (API)
Abre otra terminal, clona el repositorio del backend, copia el archivo de variables de entorno para inicializar la configuración preestablecida, instala las dependencias mediante `pnpm` y levanta el servidor Express en el puerto **`8082`**:
```bash
# 1. Clonar el repositorio del backend
git clone https://github.com/tecda-maniqui-factory/tp-maniqui-backend.git
cd tp-maniqui-backend

# 2. Crear archivo de entorno a partir de la plantilla preconfigurada
cp .env.example .env
# (Configurado por defecto para apuntar al puerto de la API 8082 y a la DB en el 3307)

# 3. Instalar dependencias e iniciar el servidor en modo desarrollo
pnpm install
pnpm dev
```

### Paso 3: Clonar, Configurar y Levantar el Cliente Frontend (React)
Abre una tercera terminal, clona el repositorio del frontend, crea su archivo de variables de entorno para enlazarse con la API, instala las dependencias e inicia el servidor de desarrollo de Vite:
```bash
# 1. Clonar el repositorio del frontend
git clone https://github.com/tecda-maniqui-factory/tp-maniqui-frontend.git
cd tp-maniqui-frontend

# 2. Crear archivo de entorno para apuntar a la API
cp .env.example .env
# (Configurado por defecto para apuntar a VITE_API_URL=http://localhost:8082)

# 3. Instalar dependencias e iniciar la aplicación web
pnpm install
pnpm dev
```

---

## 🔑 Credenciales de Prueba para el Evaluador

El sistema viene preconfigurado en la base de datos con usuarios de prueba que poseen diferentes niveles de acceso (RBAC):

| Rol / Nivel de Acceso | Usuario | Contraseña | Permisos Destacados |
| :--- | :--- | :--- | :--- |
| **Gerente de Producción** (Admin) | `gerente` | `gerente` | Acceso completo de administrador, creación de modelos, reportes analíticos de rentabilidad y stock. |
| **Vendedor** | `vendedor` | `vendedor` | Registrar ventas y consultas generales de catálogo. |
| **Operario** | `operario` | `operario` | Consulta básica y operaciones de planta. |

---
> [!TIP]
> **Gestión de dependencias:** Todos los subproyectos de Node en esta organización tienen como estándar mandatorio y exclusivo el uso de **`pnpm`** para garantizar instalaciones veloces y optimización de caché en disco.
