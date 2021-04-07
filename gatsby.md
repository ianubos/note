
## resources
 - [gatsby-node.js](https://www.gatsbyjs.com/docs/reference/config-files/gatsby-node/)
 - [create pages](https://www.gatsbyjs.com/docs/creating-and-modifying-pages/)

## dependencies
 - sass
 - [source-filesysmtem](https://www.gatsbyjs.com/plugins/gatsby-source-filesystem/?=gatsby-source-)
 - transformer-remark
 - [cross-env](https://www.gatsbyjs.com/docs/using-graphql-playground/)
    how to use graphql
 - [plugin-sharp](https://www.gatsbyjs.com/plugins/gatsby-plugin-sharp/?=sharp), [remark-images](https://www.gatsbyjs.com/plugins/gatsby-remark-images/?=remark-image), [remark-relative-images](https://www.gatsbyjs.com/plugins/gatsby-remark-relative-images/?=remark-relative)

## errors
 - error ```eperm operation not permitted```  
   please try to change folder -> property -> security -> full control
   [see this answer on stackoverflow](https://stackoverflow.com/questions/34600932/npm-eperm-operation-not-permitted-on-windows)  
   delete node_modules folder and reinstall by `npm install`  
 - do not use ```npm audit fix```
   
## tailwind
 - vscode tells you problems,
 ```unknown at rule @tailwind```  
 create .vscode/css_custom_data.json and add these lines.
 ```json
 {
  "atDirectives": [
    {
      "name": "@tailwind",
      "description": "Use the @tailwind directive to insert Tailwind’s `base`, `components`, `utilities`, and `screens` styles into your CSS.",
      "references": [
        {
          "name": "Tailwind’s “Functions & Directives” documentation",
          "url": "https://tailwindcss.com/docs/functions-and-directives/#tailwind"
        }
      ]
    }
  ]
}
```
 [stackoverflow](https://stackoverflow.com/questions/47607602/how-to-add-a-tailwind-css-rule-to-css-checker)
