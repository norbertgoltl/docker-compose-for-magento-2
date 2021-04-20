## Docker Configuration for Magento 2.4

<img src="https://img.shields.io/badge/magento-2.X-brightgreen.svg?logo=magento&longCache=true&style=flat-square" alt="Supported Magento Versions" />
<img src="https://img.shields.io/badge/macOS-ready-brightgreen?style=flat-square" alt="Supported Magento Versions" />

## Versions

Nginx: 1.19

PHP: 7.4

MySQL: 8.0.22

Redis: 6.0.6

Elasticsearch: 7.6.2

## Quick Start

**Setup your Docker engine** (You can configure Docker resources from the [Docker Desktop](https://docs.docker.com/desktop/#configure-docker-desktop))**:**

- CPUs: 2
- Memory: 6.00 GB
- Swap: 1.00 GB

**After clone this repository:**

1. Add your Magento Connect public and private authentication key in this file ([how to get](https://devdocs.magento.com/guides/v2.3/install-gde/prereq/connect-auth.html)): `.docker/php/7.4/.composer/auth.json`


2. Start by creating the working directory and within this folder, create the following directories:
    ```
    mkdir -p src/magento src/nginx_log src/phpfpm_log src/sock_data src/mysql_data src/mysql_log src/redis_data src/es_data src/es_log
    ```

3. Build and start all containers:
    ```
    docker-compose build && docker-compose up -d
    ```

4. Create a new Composer project using the Magento Open Source:
    ```
    docker-compose exec phpfpm composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition .
    ```

5. Install Magento:
    ```
    docker-compose exec -T phpfpm bin/magento setup:install \
    --base-url=http://localhost/ \
    --db-host=db \
    --db-name=magento \
    --db-user=magento \
    --db-password=magento \
    --admin-firstname=admin \
    --admin-lastname=admin \
    --admin-email=admin@admin.com \
    --admin-user=admin \
    --admin-password=admin123 \
    --language=en_US \
    --currency=USD \
    --timezone=America/Chicago \
    --use-rewrites=1 \
    --search-engine=elasticsearch7 \
    --elasticsearch-host=elasticsearch \
    --elasticsearch-port=9200 \
    --elasticsearch-index-prefix=magento
    ```

6. Stop containers:
    ```
    docker-compose stop
    ```

7. Uncomment `.docker/nginx/1.19/default.conf` line 10.


8. Build and start all containers again:
    ```
    docker-compose build && docker-compose up -d
    ```


After above completes running, you should be able to access your site at http://localhost