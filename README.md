# Laravel Docker Application

A modern Laravel web application with PostgreSQL database, containerized using Docker with Nginx and PHP-FPM.

## 🚀 Features

- **Laravel Framework** - Latest Laravel installation
- **PostgreSQL Database** - Robust relational database
- **Docker Containerization** - Easy deployment and development
- **Nginx Web Server** - High-performance web server
- **PHP-FPM** - Fast PHP processor
- **Session Management** - Database-driven sessions
- **Queue System** - Background job processing
- **Cache System** - Database-based caching

## 📋 Prerequisites

Before running this application, ensure you have:

- Docker and Docker Compose installed
- Composer installed on your host machine
- Basic knowledge of Docker and Laravel
- Git installed (for cloning/deployment)

## 🛠️ Installation & Setup

### Local Development

1. **Clone the repository**
   ```bash
   git clone <your-repository-url>
   cd laravel
   ```

2. **Install PHP dependencies**
   ```bash
   composer install
   ```

3. **Environment Configuration**
   ```bash
   cp .env.example .env
   ```
   
   Update your [.env](.env) file with appropriate values:
   ```env
   APP_NAME=Laravel
   APP_ENV=local
   APP_DEBUG=true
   APP_URL=http://localhost
   
   DB_CONNECTION=pgsql
   DB_HOST=pgsql
   DB_PORT=5432
   DB_DATABASE=db
   DB_USERNAME=user
   DB_PASSWORD=password
   ```

4. **Start Docker containers**
   ```bash
   docker-compose up -d
   ```

5. **Run database migrations**
   ```bash
   docker exec -it app-php-fpm php artisan migrate
   ```

6. **Access the application**
   Visit `http://localhost` in your browser

## 🐳 Docker Services

The application uses the following Docker services:

- **app-php-fpm** - PHP-FPM container running Laravel
- **nginx** - Nginx web server (Alpine-based)
- **pgsql** - PostgreSQL 12.1 database (Alpine-based)

### Docker Commands

```bash
# Start all containers
docker-compose up -d

# Stop all containers
docker-compose down

# View running containers
docker ps

# Execute Laravel commands
docker exec -it app-php-fpm php artisan <command>

# Access container shell
docker exec -it app-php-fpm bash
```

## 📁 Project Structure

```
├── app/                    # Laravel application code
│   ├── Http/              # Controllers, middleware, requests
│   ├── Models/            # Eloquent models
│   └── Providers/         # Service providers
├── config/                # Configuration files
├── database/              # Migrations, seeders, factories
├── docker_s/              # Docker configuration files
├── public/                # Public web files
├── resources/             # Views, assets, lang files
├── routes/                # Route definitions
├── storage/               # Logs, cache, sessions
├── tests/                 # Test files
└── vendor/                # Composer dependencies
```

## 🔧 Configuration

### Environment Variables

Key environment variables in [.env](.env):

- `APP_*` - Application settings
- `DB_*` - Database connection settings
- `SESSION_DRIVER=database` - Session storage method
- `CACHE_STORE=database` - Cache storage method
- `QUEUE_CONNECTION=database` - Queue driver

### Database

The application uses PostgreSQL as the primary database. Connection details:
- **Host**: pgsql (container name)
- **Port**: 5432
- **Database**: db
- **Username**: user
- **Password**: password

## 🚀 Deployment

For production deployment, refer to the detailed instructions in [docker_s/README.md](docker_s/README.md).

### Quick Deployment Steps

1. **Server Setup**
   - Install Docker, Docker Compose, Nginx, Git
   - Create deployment user and configure Docker permissions

2. **Application Deployment**
   ```bash
   git clone <repository> project_folder
   cd project_folder
   cp .env.example .env
   # Configure .env for production
   composer install --no-dev --optimize-autoloader
   docker-compose up -d
   docker exec -it app-php-fpm php artisan migrate --force
   ```

3. **Nginx Configuration**
   - Configure reverse proxy to Docker container
   - Set up SSL certificates
   - Configure domain/DNS

## 🔍 Troubleshooting

### Common Issues

1. **Sessions table doesn't exist**
   ```bash
   docker exec -it app-php-fpm php artisan migrate
   ```

2. **Permission issues**
   ```bash
   sudo chown -R $USER:www-data storage bootstrap/cache
   chmod -R 775 storage bootstrap/cache
   ```

3. **Container restart after Dockerfile changes**
   ```bash
   docker-compose down
   docker system prune -f
   docker-compose up -d
   ```

### Database Access

Connect to PostgreSQL:
- **Host**: 127.0.0.1
- **Port**: 5432
- **Database**: db
- **Username**: user
- **Password**: password

## 📚 Additional Resources

- [Laravel Documentation](https://laravel.com/docs)
- [Docker Documentation](https://docs.docker.com/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
