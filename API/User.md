# User

ユーザーを表すモデル

- [構造](#struct)
- [API](#api)
	- [GET /user/:id](#api-get_user)
		ユーザーを取得する
	- [POST /user](#api-post_user)
		ユーザーを作成する
	- **[PATCH /user/:id](#api-patch_user)※**
		ユーザー情報を変更する
	- **[DELETE /user/:id](#api-delete_user)※**
		ユーザーを削除する
	- **[GET /user/:userId/invited](#api-get_user_invited)※**
		指定されたユーザー宛ての招待一覧を取得する
	- **[GET /user/:userId/joined](#api-get_user_joined)※**
		指定されたユーザーの参加済み旅行の一覧を取得する

**※太字は認証が必要なAPI**

## <a name="struct"></a>構造

```json
{
	"id": "123841292341",
	"created": "2015-03-24 18:10",
	"updated": "2015-03-24 18:10",
	"userId": "kikurage",	//ユーザー内でのみユニーク
	"name": "きくらげ"	//実際に表示される名前　ユニークでなくとも良い
}
```

## <a name="api"></a>API


### <a name="api-get_user"></a> GET /user/:id

ユーザーを取得する

#### リクエスト

- URL
```
GET /user/123841292341
```

#### レスポンス

- 成功時
	- body
	```json
	{
		"status": "OK",
		"result": <% User %>
	}
	```
- ユーザーが存在しない場合
	- body
	```json
	{
		"status": "NG",
		"result": {
			"code": 1,
			"type": "NOT_FOUND",
			"detail": [ "user" ]
		}
	}
	```

---

### <a name="api-post_user"></a> POST /user

ユーザーを作成する

#### リクエスト

- URL
```
POST /user/:userId
```
- body
```json
{
	"name": "きくらげ"
}
```

#### レスポンス

- 成功時
	- body
	```json
	{
		"status": "OK",
		"result": <% User %>
	}
	```
- パラメータのうち、userIdを送信しなかった場合
	- body
	```json
	{
		"status": "NG",
		"result": {
			"code": 3,
			"type": "INVALID_PARAMETER",
			"detail": [ "userId" ]
		}
	}
	```
- userIdがすでに使用されていた場合
	- body
	```json
	{
		"status": "NG",
		"result": {
			"code": 4,
			"type": "ALREADY_CREATED",
			"detail": [ "userId" ]
		}
	}
	```

---

### <a name="api-patch_user"></a> PATCH /user/:id

`private`

ユーザー情報を変更する

#### リクエスト

- URL
```
PATCH /user/123841292341
```
- body
```json
{
	"name": "きくらげ(edited)"
}
```

#### レスポンス

- 成功時
	- body
	```json
	{
		"status": "OK",
		"result": <% User %>
	}
	```
- 認証に失敗した場合
	- body
	```json
	{
		"status": "NG",
		"result": {
			"code": 2,
			"type": "PERMISSION_DENIED",
			"detail": {}
		}
	}
	```

---

### <a name="api-delete_user"></a> DELETE /user/:id

`private`

ユーザーを削除する

#### リクエスト

- URL
```
DELETE /user/123841292341
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

---

### <a name="api-get_user_invitated"></a> GET /user/:userId/invitated

`private`

指定されたユーザー宛ての招待一覧を取得する

#### リクエスト

- URL
```
GET /user/123841292344/invited
```

#### レスポンス

- 成功時
	- body
	```json
	{
		"status": "OK",
		"result": [ <% Invitation %> ]
	}
	```
- 成功時(招待が1件もない場合)
	- body
	```json
	{
		"status": "OK",
		"result": []
	}
	```
---

### <a name="api-get_user_joined"></a> GET /user/:userId/joined

`private`

指定されたユーザーの参加済み旅行の一覧を取得する

#### リクエスト

- URL
```
GET /user/123841292341/joined
```

#### レスポンス

- 成功時
	- body
	```json
	{
		"status": "OK",
		"result": [ <% Join %> ]
	}
	```
