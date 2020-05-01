# MariaDB on Raspberry Pi / ARM (other archs should work too)

Slightly modified from https://github.com/Tob1asDocker/rpi-mariadb (Thank you!)

# What is MariaDB?

MariaDB is a community-developed fork of the MySQL relational database management system intended to remain free under the GNU GPL. Being a fork of a leading open source software system, it is notable for being led by the original developers of MySQL, who forked it due to concerns over its acquisition by Oracle. Contributors are required to share their copyright with the MariaDB Foundation.

The intent is also to maintain high compatibility with MySQL, ensuring a "drop-in" replacement capability with library binary equivalency and exact matching with MySQL APIs and commands. It includes the XtraDB storage engine for replacing InnoDB, as well as a new storage engine, Aria, that intends to be both a transactional and non-transactional engine perhaps even included in future versions of MySQL.

> [wikipedia.org/wiki/MariaDB](https://en.wikipedia.org/wiki/MariaDB)

![logo](https://raw.githubusercontent.com/docker-library/docs/master/mariadb/logo.png)

### About these images:
* a port of the official [MariaDB](https://hub.docker.com/_/mariadb)-Image.
* based on official Image: [debian](https://hub.docker.com/_/debian)

#### Docker-Compose

```yaml
version: '2.4'
services:
  mariadb:
    build:
      context: https://github.com/lalexdotcom/docker-mariadb.git
    container_name: mariadb
    image: lalexdotcom/mariadb
    volumes:
      - ./data/mariadb:/var/lib/mysql
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro
    environment:
      MYSQL_DATABASE: exampledb
      MYSQL_USER: exampleuser
      MYSQL_PASSWORD: examplepass
      MYSQL_ROOT_PASSWORD: rootpassword
     #MYSQL_RANDOM_ROOT_PASSWORD: "yes"
    restart: unless-stopped
    ports:
      - 3306:3306
    healthcheck:
      test:  mysqladmin ping -h 127.0.0.1 -u $$MYSQL_USER --password=$$MYSQL_PASSWORD || exit 1
      #start_period: 60s
      interval: 30s
      timeout: 5s
      retries: 5
```

### This Image on
* [GitHub](https://github.com/lalexdotcom/docker-mariadb)
