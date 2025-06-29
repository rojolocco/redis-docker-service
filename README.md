# Redis Docker Service

A containerized Redis service using Docker and Docker Compose, configured for both development and production environments.

## Overview

This repository provides a ready-to-use Redis 8.0 instance running in Docker. Redis is an open-source, in-memory data structure store that can be used as a database, cache, message broker, and more.

## Features

- Redis 8.0 in a Docker container
- Persistent data storage using Docker volumes
- Separate configurations for development and production
- Health checks for production environment
- Integration with external network (caddy_network)
- Environment variable configuration

## Prerequisites

- Docker and Docker Compose installed on your system
- External Docker network named `caddy_network` (must be created before running this service)

## Setup

1. Clone this repository:

   ```bash
   git clone <repository-url>
   cd redis-docker-service
   ```

2. Create the required environment file:

   ```bash
   # For development
   cp .env.example .env.dev
   
   # For production
   cp .env.example .env
   ```

3. Configure the environment variables in the `.env` or `.env.dev` file:

   ```env
   REDIS_HOST=redis
   REDIS_PASSWORD=your_secure_password
   ```

## Usage

### Development Environment

To start Redis in development mode:

```bash
docker-compose -f docker-compose.dev.yaml up -d
```

### Production Environment

To start Redis in production mode:

```bash
docker-compose up -d
```

### Connecting to Redis

You can connect to the Redis instance using the Redis CLI:

```bash
docker exec -it redis redis-cli
```

If you've set a password in the environment file:

```bash
docker exec -it redis redis-cli -a your_secure_password
```

## Configuration

### Environment Variables

- `REDIS_HOST`: The hostname for Redis (default: redis)
- `REDIS_PASSWORD`: Password for Redis authentication (recommended for production)

### Docker Compose Configuration

The service is configured with:

- Container name: `redis`
- Image: `redis:8.0`
- Restart policy: `always`
- Volume: `data-redis` mounted to `/data` for persistence
- Network: Connected to the external `caddy_network`
- Health check (production only): Verifies Redis is responding correctly

## Data Persistence

Redis data is persisted using a Docker volume named `data-redis`. This ensures your data survives container restarts and updates.

## About Redis

Redis is an open-source, in-memory data structure store that can be used as a:

- Database
- Cache
- Message broker
- Streaming engine

### Key Features of Redis

- In-memory data storage with optional persistence
- Support for various data structures (strings, hashes, lists, sets, sorted sets)
- Built-in replication and automatic partitioning with Redis Cluster
- Lua scripting
- Transactions
- Pub/Sub messaging
- High availability via Redis Sentinel

### Common Use Cases

- Caching
- Session management
- Real-time analytics
- Leaderboards/counting
- Message queuing
- Rate limiting

## License

See the [LICENSE](LICENSE) file for details.
