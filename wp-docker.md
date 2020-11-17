### docker image, use it with the aiz template docker image!
```docker
version: '3.6'
services:
    database:
        image: mysql:5.7
        command:
            - "--character-set-server=utf8"
            - "--collation-server=utf8_unicode_ci"
        ports:
            - "3306:3306"
        restart: on-failure:5
        container_name: "${PRODUCTION_NAME}_db"
        volumes:
            - db-data:/var/lib/mysql
        environment:
            MYSQL_USER: wordpress
            MYSQL_DATABASE: wordpress
            MYSQL_PASSWORD: wordpress
            MYSQL_ROOT_PASSWORD: wordpress
        networks:
            - back_bridge
    wordpress:
        depends_on:
            - database
        image: wordpress:latest
        container_name: "${PRODUCTION_NAME}_wordpress"
        restart: on-failure:5
        expose:
            - "80"
        volumes:
            - ./wordpress:/var/www/html
        env_file: .env
        environment:
            WORDPRESS_DB_HOST: database:3306
            WORDPRESS_DB_PASSWORD: wordpress
            VIRTUAL_HOST: "${PRODUCTION_NAME}.localhost"
            LETSENCRYPT_HOST: "${PRODUCTION_NAME}.localhost"
            LETSENCRYPT_EMAIL: info@localhost
        networks:
            - front_bridge
            - back_bridge
    webpack:
        image: aiz_webpack:1.1.9
        volumes:
            - ./wordpress/wp-content/themes/kisimo_v3/assets/webpack/src:/webpack/src
            - ./wordpress/wp-content/themes/kisimo_v3/assets/webpack/dist:/webpack/dist
volumes:
    db-data:
    wp-admin:
        driver: local
    wp-includes:
        driver: local

networks:
    front_bridge:
        external: true
    back_bridge:
        driver: bridge
```
