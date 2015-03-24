## Invitation

認証状態を表すモデル。

- [構造](#struct)
- [API](#api)
	- **[GET /auth](#api-get_auth)※**
		認証済みユーザーを確認する
	- [POST /auth/:userId](#api-post_auth)
		認証を行う
	- **[DELETE /auth/:userId](#api-delete_auth)※**
		認証情報を削除する

**※太字は認証が必要なAPI**

## <a name="struct"></a>構造

```json
{
	"id": "872123948123",
	"created": "2015-03-24 18:10",
	"updated": "2015-03-24 18:10",
	"user": <% User %>,	//認証されたユーザー
	"token": "10349819519047591832074123" //トークン
}
```

## <a name="api"></a>API

### <a name="api-get_auth"></a> GET /auth

`private`

認証済みユーザーを確認する。

#### リクエスト

- URL
```
GET /auth
```

#### レスポンス

- 成功時
	- body
	```json
	{
		"status": "OK",
		"result": <% Auth %>
	}
	```
- 未認証時
	- body
	```json
	{
		"status": "NG",
		"result": {
			"code": 1,
			"type": "NOT_FOUND",
			"detail": [ "auth" ]
		}
	}
	```

---

### <a name="api-post_auth"></a> POST /auth/:userId

認証を行う

#### リクエスト

- URL
```
POST /auth/123841292344
```
- body
```json
{
	"password": "hirakegoma"
}
```
#### レスポンス

- 成功時
	- body
	```json
	{
		"status": "OK",
		"result": <% Auth %>
	}
	```
- パスワードまたはユーザー名が違う場合
	- body
	```json
	{
		"status": "NG",
		"result": {
			"code": 3,
			"type": "INVALID_PARAMETER",
			"detail": [ "userId", "password" ]
		}
	}
	```

---

### <a name="api-delet_auth"></a> DELETE /auth

`private`

認証情報を削除する

#### リクエスト

- URL
```
DELETE /auth/123841292341
```

#### レスポンス

- 成功時
	- body
	```json
	{
		"status": "OK",
		"result": {}
	}
	```
