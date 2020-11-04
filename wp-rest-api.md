# Wordpress REST API
By [Travesy Media](https://www.youtube.com/watch?v=fFNXWinbgro)

### Required
* Docker for local dev
* Postman for get or post request

### Plugins
* JWT Authentication for WP-API
* Custom Post Type UI

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
