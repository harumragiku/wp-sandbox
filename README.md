# WordPress Docker Compose Stack

This project provides a local WordPress development environment using Docker Compose, Nginx, PHP-FPM, MySQL, and Adminer.

## Services
- **wordpress**: WordPress running on PHP-FPM (`wordpress:php8.2-fpm`)
- **db**: MySQL 5.7 database
- **nginx**: Nginx web server, reverse proxying to WordPress FPM
- **adminer**: Database management tool (Adminer)

## Usage
1. **Start the stack:**
   ```sh
   docker compose up -d
   ```
2. **Access WordPress:**
   - [http://localhost:8080](http://localhost:8080)
3. **Access Adminer:**
   - [http://localhost:8081](http://localhost:8081)
   - System: MySQL
   - Server: db
   - Username: wordpress
   - Password: wordpress
   - Database: wordpress

## File Structure
- `docker-compose.yml`: Service definitions
- `nginx/conf.d/default.conf`: Nginx configuration for WordPress FPM
- `wordpress/`: WordPress files (ignored by git, see `.gitignore`)

## Notes
- The `wordpress` directory is mounted into both the WordPress and Nginx containers.
- Nginx serves static files and proxies PHP requests to the WordPress FPM container.
- The `wordpress` directory is listed in `.gitignore` and will not be tracked by git.

## Stopping the stack
```sh
docker compose down
```

## Troubleshooting
- If you see only HTML and no CSS, ensure the Nginx service has the volume mapping for `./wordpress:/var/www/html:ro`.
- If you need to reset the database, remove the `db_data` volume:
  ```sh
  docker compose down -v
  ```
