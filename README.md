# WordPress Plugin Development Environment

A Docker-based WordPress development environment optimized for plugin development and testing.

## Overview

This project provides a complete WordPress development stack using Docker containers, including:
- WordPress with custom configuration
- MariaDB database
- phpMyAdmin for database management
- Custom PHP configuration for development

## Features

- **Multi-stage Docker build** for optimized WordPress container
- **Environment-based configuration** using `.env` files
- **Volume mounting** for live plugin/theme development
- **phpMyAdmin** for easy database management
- **Custom PHP settings** optimized for WordPress development
- **Debug-friendly** configuration with error reporting

## Prerequisites

- Docker Desktop installed and running
- Docker Compose v3.9 or higher
- Basic knowledge of WordPress plugin development

## Quick Start

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd wooplugin
   ```

2. **Create environment file**
   ```bash
   cp .env.example .env
   ```
   Edit the `.env` file with your preferred settings:
   ```env
   # Database Configuration
   MYSQL_ROOT_PASSWORD=your_root_password
   MYSQL_DATABASE=wordpress_db
   MYSQL_USER=wp_user
   MYSQL_PASSWORD=wp_password
   
   # WordPress Configuration
   WORDPRESS_DB_HOST=db:3306
   WORDPRESS_DB_USER=wp_user
   WORDPRESS_DB_PASSWORD=wp_password
   WORDPRESS_DB_NAME=wordpress_db
   
   # Port Configuration
   WORDPRESS_PORT=8080
   PHPMYADMIN_PORT=8081
   
   # Debug Settings
   WORDPRESS_DEBUG=true
   WORDPRESS_DEBUG_LOG=true
   WORDPRESS_DEBUG_DISPLAY=true
   ```

3. **Start the development environment**
   ```bash
   docker-compose up -d
   ```

4. **Access your WordPress site**
   - WordPress: http://localhost:8080
   - phpMyAdmin: http://localhost:8081

## Project Structure

```
wooplugin/
├── docker-compose.yml          # Main orchestration file
├── wordpress/                  # WordPress container context
│   ├── Dockerfile             # Multi-stage WordPress build
│   ├── php.ini               # Custom PHP configuration
│   ├── wp-config.php         # WordPress configuration
│   └── wp-content/           # WordPress content (plugins/themes)
│       ├── plugins/          # Custom plugins go here
│       └── themes/           # Custom themes go here
└── README.md                 # This file
```

## Development Workflow

### Plugin Development

1. **Create your plugin** in `wordpress/wp-content/plugins/your-plugin-name/`
2. **Edit plugin files** directly on your host machine
3. **Changes are reflected immediately** due to volume mounting
4. **Test and debug** using WordPress debug features

### Theme Development

1. **Create your theme** in `wordpress/wp-content/themes/your-theme-name/`
2. **Edit theme files** directly on your host machine
3. **Changes are reflected immediately** due to volume mounting

### Database Management

- Access phpMyAdmin at http://localhost:8081
- Use the credentials from your `.env` file
- Export/import databases as needed

## Docker Services

### WordPress Service (`woo_site`)
- **Base Image**: wordpress:latest
- **Port**: 8080 (configurable)
- **Features**:
  - Custom PHP configuration
  - Debug mode enabled
  - Volume-mounted wp-content for development
  - Environment-based configuration

### Database Service (`woo_db`)
- **Base Image**: mariadb:11
- **Features**:
  - Persistent data storage
  - Environment-based configuration
  - Optimized for WordPress

### phpMyAdmin Service (`woo_phpmyadmin`)
- **Base Image**: phpmyadmin/phpmyadmin
- **Port**: 8081 (configurable)
- **Features**:
  - Web-based database management
  - Direct connection to MariaDB

## Custom Configuration

### PHP Settings (`php.ini`)
- Upload limit: 64MB
- Post size limit: 64MB
- Execution time: 300 seconds
- Memory limit: 256MB
- Error reporting enabled for development

### WordPress Configuration (`wp-config.php`)
- Environment-based database settings
- Debug mode support
- Custom authentication keys
- Security hardening options

## Useful Commands

```bash
# Start services
docker-compose up -d

# Stop services
docker-compose down

# View logs
docker-compose logs -f wordpress

# Access WordPress container
docker-compose exec wordpress bash

# Reset database (WARNING: destroys all data)
docker-compose down -v
docker-compose up -d

# Update WordPress
docker-compose pull wordpress
docker-compose up -d --force-recreate wordpress


# Clean all volumes and image 
docker compose down --volumes --remove-orphans --rmi all
```

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `WORDPRESS_PORT` | WordPress access port | 8080 |
| `PHPMYADMIN_PORT` | phpMyAdmin access port | 8081 |
| `MYSQL_ROOT_PASSWORD` | MySQL root password | Required |
| `MYSQL_DATABASE` | WordPress database name | wordpress_db |
| `MYSQL_USER` | Database user | wp_user |
| `MYSQL_PASSWORD` | Database password | Required |
| `WORDPRESS_DEBUG` | Enable WordPress debug mode | false |
| `WORDPRESS_DEBUG_LOG` | Enable debug logging | false |
| `WORDPRESS_DEBUG_DISPLAY` | Display debug info | false |

## Troubleshooting

### Common Issues

1. **Port conflicts**: Change ports in `.env` file if 8080/8081 are in use
2. **Permission issues**: Ensure Docker has access to the project directory
3. **Database connection**: Verify database credentials in `.env` file
4. **Memory issues**: Increase Docker memory allocation if needed

### Debug Mode

Enable debug mode by setting these in your `.env` file:
```env
WORDPRESS_DEBUG=true
WORDPRESS_DEBUG_LOG=true
WORDPRESS_DEBUG_DISPLAY=true
```

Debug logs will be available in `wp-content/debug.log`

## Security Notes

- This setup is for **development only**
- Change all default passwords before production use
- Use proper authentication keys in production
- Review security settings in `wp-config.php`

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For issues and questions:
- Check the troubleshooting section
- Review Docker and WordPress documentation
- Open an issue in the repository
