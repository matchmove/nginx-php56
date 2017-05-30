# nginx-php56
A Nginx + PHP 5.6 (FPM) base container. Builds upon on the excellent [phusion/baseimage-docker](https://github.com/phusion/baseimage-docker) container. You can find the docker automated build [here](https://registry.hub.docker.com/u/mstrazds/nginx-php56/).

### Services
All services are defined and managed using the phusion/baseimage methodology. Logs are output using syslog and can be accessed using ``docker logs {container}``.

* Nginx
* PHP-FPM (5.6)

### Default Settings
The container sets up a www root folder in the following location:

``/var/www/public``

As a final task a demo index.php is copied to this location.

### Web Root
The following folder is specified as the default root web folder:

``/var/www/public``

Note that the ``/var/www/public`` is the root folder for serving PHP files for your web server. The following ports are exposed:

* 80 (HTTP)
* 443 (HTTPS/SSL)

### SSL Self Signed Certificate
The image generates a self-signed certificate for each container within the folder:

``/etc/nginx/certs.d/``

During build the ``build/default`` file is used to copy and configure nginx default settings. This includes a cipher suite for legacy browser (IE8+) support. See: [https://cipherli.st/](https://cipherli.st/)

``docker run --name nginx -e NR_APP_NAME="nginx-test" -p 80:80 -p 443:443 -d mstrazds/nginx-php56:latest``

### Build Folder (within repo)
Contains nginx config files as well as php-fpm settings. Also include setup.sh file that offloads tasks from the Dockerfile to reduce layers.

### Databases
This image supports mysql and postgres.

### Notes
Note that PHP-FPM has been configured to pass through environment variables when starting the container using the ``clear_env = no`` flag within the ``/etc/php5/fpm/pool.d/www.conf`` file.
