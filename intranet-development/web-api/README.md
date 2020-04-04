## APIサーバ構成図

![](https://github.com/GrahamSolution/documents/blob/master/intranet-development/web-api/img/api-server-structure.png)

## Swagger.yamlからhtml生成方法

 ```bash
 npm install -g redoc
 npm install -g redoc-cli
 npx redoc-cli bundle api-reference.yaml -o index.html
 ```
