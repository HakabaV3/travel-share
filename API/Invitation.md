## Invitation

旅行への招待を表すモデル。

- [構造](#struct)
- [API](#api)
	- **[GET /travel/:travelId/invitation](#api-get_travel_inivitation_all)※**
		すでに出されている招待の一覧を取得する
	- **[GET /travel/:travelId/invitation/:userId](#api-get_travel_inivitation)※**
		招待の詳細を取得する
	- **[POST /travel/:travelId/invitation/:userId](#api-post_travel_inivitation)※**
		招待をだす
	- **[DELETE /travel/:travelId/invitation/:userId](#api-delete_travel_inivitation)※**
		招待を削除する

**※太字は認証が必要なAPI**

## <a name="struct"></a>構造

```json
{
	"id": "872123948123",
	"created": "2015-03-24 18:10",
	"updated": "2015-03-24 18:10",
	"owner": <% User %>,	//作成者(=招待した人)
	"target": <% User %>,	//招待された人
	"travel": <% Travel %>	//旅行
}
```

## <a name="api"></a>API

### <a name="api-get_travel_inivitation_all"></a> GET /travel/:travelId/invitation

`private`

すでに出されている招待の一覧を取得する。このAPIは、当該旅行のメンバーであれば自分以外のメンバーが出した招待の状況も確認できる。

#### リクエスト

- URL
```
GET /travel/923495263452/invitation
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

---

### <a name="api-get_travel_inivitation"></a> GET /travel/:travelId/invitation/:userId

`private`

招待の詳細を取得する。このAPIは、当該旅行のメンバーであれば自分以外のメンバーが出した招待の状況も確認できる。

#### リクエスト

- URL
```
GET /travel/923495263452/invitation/123841292344
```

#### レスポンス

- 成功時
	- body
	```json
	{
		"status": "OK",
		"result": <% Invitation %>
	}
	```
- 招待が存在しない場合
	- body
	```json
	{
		"status": "NG",
		"result": {
			"code": 1,
			"type": "NOT_FOUND",
			"detail": [ "invitation" ]
		}
	}
	```

---

### <a name="api-post_travel_inivitation"></a> POST /travel/:travelId/invitation/:userId

`private`

ユーザーを旅行へ招待する。

#### リクエスト

- URL
```
POST /travel/923495263452/invitation/123841292344
```

#### レスポンス

- 成功時
	- body
	```json
	{
		"status": "OK",
		"result": <% Invitation %>
	}
	```
- 招待がすでに送られている場合
	- body
	```json
	{
		"status": "NG",
		"result": {
			"code": 4,
			"type": "ALREADY_CREATED",
			"detail": [ "invitation" ]
		}
	}
	```

---

### <a name="api-delete_travel_inivitation"></a> DELETE /travel/:travelId/invitation/:userId

`private`

招待を削除する。このAPIは、当該旅行のメンバーであれば自分以外のメンバーが出した招待も取りやめられる。

#### リクエスト

- URL
```
DELETE /travel/923495263452/invitation/123841292344
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
