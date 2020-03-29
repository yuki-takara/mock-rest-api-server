# mock-rest-api-server

## 使い方

```bash
# clone & ライブラリインストール
$ git clone https://github.com/meganedogYuu/mock-rest-api-server.git
$ npm install

# RESTのモックサーバ起動
$ npm run sample
# => Resources
# => http://localhost:3000/movies
```

<img width="707" alt="スクリーンショット 2020-03-23 13 07 45" src="https://user-images.githubusercontent.com/10525280/77280304-4ea73100-6d07-11ea-8a76-77d29d6dd2a7.png">


### 認証付きサーバ

```bash
# 認証付きサーバを起動
$ npm run auth-server
```

トークンを取得

```bash
curl -X POST 'localhost:3000/auth/login' \
-H 'Content-Type: application/json' \
-d '{
  "email": "hoge@email.com",
  "password":"hoge"
}'
```

```
{
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImhvZ2VAZW1haWwuY29tIiwicGFzc3dvcmQiOiJob2dlIiwiaWF0IjoxNTg1NDU0NDM4LCJleHAiOjE1ODU0NTgwMzh9.0UbPNWNn3jEySnA2-mRpZ7pGQJv3i9vadIYRahNYBfo"
}
```

トークンを使ってアクセスする

```bash
curl -X GET 'localhost:3000/books' \
-H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImhvZ2VAZW1haWwuY29tIiwicGFzc3dvcmQiOiJob2dlIiwiaWF0IjoxNTg1NDU0NDM4LCJleHAiOjE1ODU0NTgwMzh9.0UbPNWNn3jEySnA2-mRpZ7pGQJv3i9vadIYRahNYBfo'
```

```
[
  {
    "id": 1,
    "title": "Math",
    "price": 1000
  },
  {
    "id": 2,
    "title": "Science",
    "price": 1200
  },
  {
    "id": 3,
    "title": "Chemical",
    "price": 1400
  }
]
```

tokenを使わなかった場合は以下のようになる

```
{
  "status": 401,
  "message": "Error in authorization format"
}
```

参考記事: [Node\.js APIで認証付きのMockREST APIサーバの導入 \- Qiita](https://qiita.com/oz4you/items/3f3223048bd2109de47b)
