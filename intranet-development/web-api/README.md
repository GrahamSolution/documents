## APIサーバ構成図

![](https://github.com/GrahamSolution/documents/blob/master/intranet-development/web-api/img/api-server-structure.png)

## SpringBoot × JPA プロジェクト雛形パッケージ構成
```
├─ src/main/java
│   └─ com.example
│        ├─ interfaces                       ... アプリケーションのインターフェースを格納するパッケージ
│        │   ├─ request                      ... RequestBodyがここで定義したJavaオブジェクトに変換される
│        │   │   └─ JwtRequestForm.java
│        │   └─ response                     ... ResponseBodyがここで定義したJavaオブジェクトからJSONに変換される
│        │       └─ JwtResponseForm.java    
│        ├─ domain                           ... ドメイン層のパッケージ（DB周り）
│        │   ├─ model                        ... DBから取得してくるデータを列挙するEntity
│        │   │   └─ StaffEntity.java
│        │   └─ Repository                   ... DBアクセスを担うinterface
│        │       └─ StaffRepository.java
│        ├─ common                           ... プロジェクト共通で使うクラスを格納するパッケージ（現状ゴミ箱化してる）
│        │   └─ GrahamHttpStatus.java
│        ├─ config                           ... プロジェクトの共通設定を定義するパッケージ
│        │   └─ WebSecurityConfig.java
│        ├─ controllers                      ... 各APIのリクエストをハンドルするコントローラを格納するパッケージ
│        │   └─ StaffController.java
│        ├─ exception                        ... 例外処理クラスを格納するパッケージ
│        │   └─ GrahamException.java
│        ├─ security                         ... 認証・認可周りの機能を格納するパッケージ
│        │   └─ JwtTokenProvider.java
│        ├─ service                          ... ビジネスロジックを格納するパッケージ
│        │   └─ StaffService.java
│        └─ GsStartupProjectApplication.java ... SpringBootApplicationアノテーションを付与したクラス
│ 
└─ src/main/resources
     │   
     └─ application.yaml                     ... DB接続情報などアプリケーション固有の情報定義
```

## Swagger.yamlからhtml生成方法

 ```bash
 npm install -g redoc
 npm install -g redoc-cli
 npx redoc-cli bundle api-reference.yaml -o index.html
 ```
