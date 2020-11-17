# Wordpress REST API
By [Travesy Media](https://www.youtube.com/watch?v=fFNXWinbgro)

### Required
* Docker for local dev
* Postman for get or post request

### Plugins
* JWT Authentication for WP-API
* Custom Post Type UI
* Advanced Custom Fields
* ACF to REST API   // Expose custom fields to REST API

## GET & POST with Postman
Get method
```
Method: GET
Content-Type: application/json
Url: http://restapi.localhost/wp-json/wp/v2/
```
Post method
```
Method: POST
Url: http://restapi.localhost/wp-json/wp/v2/posts
Content-Type: application/json
Authorization: Bearer <your token>
Body(raw): 
{
    "title": "Title here",
    "content": "What you want to put in the content here.",
    "status": "publish"
}
```
Get token method, using plugin jwt auth
```
Method: POST
Url: http://restapi.localhost/wp-json/jwt-auth/v1/token
Content-Type: application/json
Body(raw): 
{
    "username": "<your wordpress username>",
    "password": "<your wordpress password>"
}
```
## Get Custom Post
ex) Custom post type named Books
```
Method: Get
Content-Type: application/json
Url: http://restapi.localhost/wp-json/wp/v2/books  // Entire Books Object
Url: http://restapi.localhost/wp-json/wp/v2/books/9   //By id
Url: http://restapi.localhost/wp-json/wp/v2/books?per_page=1   //Just one book
-> same to set Params per_page: 1
```


## Set up React
Create React folder
```
npx create-react-app frontend
cd frontend
npm i axios react-router-dom
npm start
```

# Set Up with Docker
{project directory}
|-template-of-aiz_webpack
|-wordpress
|-.env
|-docker-compose.yml

### Firstly, prepare docker images
Clone aiz-web-pack and build and run the image
```
git clone https://github.com/yamanaka-aiz/template-of-aiz_webpack.git
cd template-of-aiz_webpack
docker build -t aiz_webpack:【バージョン】 --force-rm ./webpack
docker-compose up -d
```
Then @ {project directory}, make docker-composel.yml like this. 
```
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
And make .env file
```
PRODUCTION_NAME=kisimo
```
Then run docker image
```
docker network create front_bridge
docker-compose up -d
```


