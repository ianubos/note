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
