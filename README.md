# LAMP for Docker
Complete LAMP setup with Docker Compose for development environment. Start developing in less than 5 minutes.
Development stack is based on PHP 8.0 + Apache 2.4 and MySQL 5.7 containers. 

##### Table of Contents  
- [Prerequisites](https://github.com/danieltoader/lamp-docker#prerequisites)  
- [What is included?](https://github.com/danieltoader/lamp-docker#what-is-included)
- [Quick Start](https://github.com/danieltoader/lamp-docker#quick-start)
- [Configuration](https://github.com/danieltoader/lamp-docker#fast-configuration)
- [Others](https://github.com/danieltoader/lamp-docker#others)

## Prerequisites

You'll need to have the following prerequisites **installed** on your workstation:

 * [Git](http://git-scm.com/)
 * [Docker](https://docs.docker.com/install/)
 * [Docker Compose](https://docs.docker.com/compose/install/)

## What is included?
 * **Apache 2.4**
 * **MySQL 5.7**
 * **PHP 8.0**
 * **PhpMyAdmin**

## Quick Start

### Using the archive
Click the download button or this [link](https://github.com/danieltoader/lamp-docker/archive/master.zip) or use the script below.
Extract the files in the path that you will use for your project.
```bash
$ wget https://github.com/danieltoader/lamp-docker/archive/master.zip
$ unzip ./master.zip -d /path/to/project/root/directory
$ cd /path/to/project/root/directory
$ cp ./.env.example ./.env
$ docker-compose up -d
```

### Using git
```bash
$ git clone https://github.com/danieltoader/lamp-docker.git /path/to/project/root/directory
$ cd /path/to/project/root/directory
$ cp ./.env.example ./.env
$ docker-compose up -d
```

Once the process is finished you can place your application in the ```www``` folder and access it using the exposed ports.

For quick access, check the links below:
- phpmyadmin: http://localhost:8800
- app: http://localhost:8080
- mysql: 127.0.0.1:3306

## Configuration

For fast configuration you can copy ``.env.example`` into ``.env`` file and modify the defined variables.

```
CONTAINER_PREFIX=lamp-docker

# If you already has the port 8800 in use, you can change it
HOST_MACHINE_PHPMYADMIN_PORT=8800

# If you already has the port 8080 in use, you can change it (for example if you have Apache)
HOST_MACHINE_UNSECURE_HOST_PORT=8080
HOST_MACHINE_SECURE_HOST_PORT=8443

# If you already has the port 3306 in use, you can change it (for example if you have MySQL)
HOST_MACHINE_MYSQL_PORT=3306

# MySQL root user password
MYSQL_ROOT_PASSWORD=root

# Database settings: username, password and database name
MYSQL_USER=lamp
MYSQL_PASSWORD=lamp
MYSQL_DATABASE=lamp
```

## Others

##### Connect to mysql
```php
$servername = "mysql";
$username = "lamp";
$password = "lamp";

try {
    $conn = new PDO("mysql:host=$servername;dbname=lamp", $username, $password);
    // set the PDO error mode to exception
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    echo "Connected successfully";
}
catch(PDOException $e)
{
    echo "Connection failed: " . $e->getMessage();
}
```

##### Notice
You must understand that this setup is meant to be disposable, it is not supposed to be persistent. Any persistent data **should remain on your host computer**, do not apply changes to the VM nor store data or documents that you don't want to lose. 

As a consequence, you may mess up with this setup, do heavy testing, install new apps to evaluate them and even crash it. If you need to rollback, just destroy it and recreate it as pure as the driven snow but with all your data (sources, databases and configuration intact). It is as simple as a `docker-compose rm -fsv && docker-compose up -d --force-recreate`.

Have Fun!