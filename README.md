# Redis Docker Service

Este repositorio contiene la configuración para desplegar un servicio de Redis junto con Redis Commander utilizando Docker Compose.

## Contenido

- `docker-compose.yml`: Archivo de configuración de Docker Compose para desplegar Redis y Redis Commander.
- `init-redis.sh`: Script de inicialización para crear datos de ejemplo en Redis.
- `.env.prod`: Archivo de variables de entorno para Redis Commander.

## Servicios

### Redis

- **Imagen**: `redis:latest`
- **Contenedor**: `redis-dev`
- **Puertos**: `6379:6379`
- **Volúmenes**: `redis-data:/data`
- **Red**: `caddy_network`

### Redis Commander

- **Imagen**: `rediscommander/redis-commander:latest`
- **Contenedor**: `redis-commander`
- **Puertos**: `8082:8081`
- **Red**: `caddy_network`
- **Autenticación**: Configurada mediante variables de entorno en `.env.prod`

## Uso

### Prerrequisitos

- Docker
- Docker Compose

### Pasos

1. Clona este repositorio:

    ```sh
    git clone <URL_DEL_REPOSITORIO>
    cd redis-docker-service
    ```

2. Asegúrate de que el script `init-redis.sh` tenga permisos de ejecución:

    ```sh
    chmod +x init-redis.sh
    ```

3. Inicia los servicios con Docker Compose:

    ```sh
    docker compose -f "docker-compose.yml" up -d --build
    ```

4. Accede a Redis Commander en `http://<TU_IP>:8082` con las credenciales configuradas en .

## Variables de Entorno

Configura las siguientes variables en el archivo :

- `HTTP_USER`: Nombre de usuario para Redis Commander.
- `HTTP_PASSWORD`: Contraseña para Redis Commander.

## Datos de Ejemplo

El script `init-redis.sh` crea los siguientes datos de ejemplo en Redis:

- Clave-valor: `example_key` con valor `example_value`
- Hash: `example_hash` con campos `field1` y `field2`
- Lista: `example_list` con valores `value1`, `value2`, `value3`
- Conjunto: `example_set` con miembros `member1`, `member2`, `member3`
- Conjunto ordenado: `example_zset` con miembros `member1`, `member2`, `member3` y puntuaciones `1`, `2`, `3`

## Licencia

Este proyecto está licenciado bajo la MIT License
