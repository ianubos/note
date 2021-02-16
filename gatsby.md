
## dependencies
 - sass
 - [source-filesysmtem](https://www.gatsbyjs.com/plugins/gatsby-source-filesystem/?=gatsby-source-)
 - transformer-remark
 - [cross-env](https://www.gatsbyjs.com/docs/using-graphql-playground/)
    how to use graphql
 

## errors
 - error ```eperm operation not permitted```
   [see this answer on stackoverflow](https://stackoverflow.com/questions/34600932/npm-eperm-operation-not-permitted-on-windows)
   delete node_modules folder and reinstall by `npm install`
   npm audit fix is working!
   ```
   npm audit fix
   ```
   
