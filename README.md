# Gestión de Congresos - Deploy

Repositorio encargado de levantar el entorno de desarrollo del proyecto **Gestión de Congresos** utilizando Docker Compose.

## Descripción

Este repositorio contiene la configuración necesaria para ejecutar los servicios del proyecto en contenedores Docker.

Actualmente se incluyen los siguientes servicios:

* Backend (Spring Boot)
* Base de datos MySQL 8.4

El objetivo es que cualquier integrante del equipo pueda clonar el repositorio y levantar el entorno completo con un único comando.

---

# Requisitos

Antes de comenzar es necesario tener instalado:

* Docker Desktop
* Git

Se recomienda verificar la instalación ejecutando:

```bash
docker --version
docker compose version
```

---

# Clonar el repositorio

```bash
git clone <URL_DEL_REPOSITORIO>
cd gestion-congresos-deploy
```

---

# Configuración

Crear un archivo llamado `.env` en la raíz del proyecto tomando como referencia el archivo `.env.example`.

Ejemplo:

```properties
MYSQL_DATABASE=gestion_congresos
MYSQL_USER=gestion_congresos_user
MYSQL_PASSWORD=tu_password
MYSQL_ROOT_PASSWORD=tu_root_password
```

---

# Levantar el entorno

Construir las imágenes e iniciar los contenedores:

```bash
docker compose up --build
```

Para ejecutar los contenedores en segundo plano:

```bash
docker compose up -d --build
```

---

# Detener el entorno

```bash
docker compose down
```

---

# Reconstruir las imágenes

Si se modifica el `Dockerfile` o el `docker-compose.yml`, volver a construir las imágenes:

```bash
docker compose up --build
```

---

# Acceso a los servicios

## Backend (Spring Boot)

URL:

```
http://localhost:8080
```

Ejemplo de endpoint de prueba:

```
http://localhost:8080/api/users/test
```

---

## Base de datos MySQL

Desde MySQL Workbench:

| Parámetro     | Valor                         |
| ------------- | ----------------------------- |
| Host          | localhost                     |
| Puerto        | 3307                          |
| Base de datos | gestion_congresos             |
| Usuario       | gestion_congresos_user        |
| Contraseña    | definida en el archivo `.env` |

> **Nota:** El puerto **3307** corresponde al equipo anfitrión (host) y se redirige al puerto **3306** del contenedor de MySQL.

---

# Comandos útiles

Ver los contenedores en ejecución:

```bash
docker ps
```

Ver los logs:

```bash
docker compose logs
```

Seguir los logs en tiempo real:

```bash
docker compose logs -f
```

Detener y eliminar los contenedores:

```bash
docker compose down
```

Eliminar también los volúmenes asociados:

```bash
docker compose down -v
```

Reconstruir las imágenes:

```bash
docker compose up --build
```

---

# Estructura del repositorio

```
gestion-congresos-deploy
│
├── docker-compose.yml
├── .env.example
├── .gitignore
└── README.md
```

---

# Tecnologías utilizadas

* Docker
* Docker Compose
* Spring Boot
* MySQL 8.4

---

# Notas

* El backend se expone en el puerto **8080**.
* MySQL se expone en el puerto **3307** del equipo anfitrión y utiliza el puerto **3306** dentro del contenedor.
* El backend no se comunica con MySQL mediante `localhost`, sino utilizando el nombre del servicio definido en `docker-compose.yml`.
* El archivo `.env` no debe subirse al repositorio. Cada integrante del equipo debe crear su propia copia a partir de `.env.example`.
