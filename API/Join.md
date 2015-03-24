## Travel

旅行への参加を表すモデル

- [構造](#struct)
- [API](#api)
	- **[GET /travel/:travelId/join](#api-post_travel_join_all)※**
		旅行への参加情報の一覧を取得する
	- **[GET /travel/:travelId/join/:userId](#api-post_travel_join)※**
		旅行への参加情報を取得する
	- **[POST /travel/:travelId/join/:userId](#api-post_travel_join)※**
		旅行へ参加する
	- **[DELETE /travel/:travelId/join/:userId](#api-delete_travel_join)※**
		旅行への参加を取り消す

**※太字は認証が必要なAPI**

## <a name="struct"></a>構造

```json
{
	"id": "872123946123",
	"created": "2015-03-24 18:10",
	"updated": "2015-03-24 18:10",
	"owner": <% User %>,	//作成者
	"travel": <% Travel %>	//旅行
}
```

## <a name="api"></a>API

### <a name="api-get_travel_join_all"></a> GET /travel/:travelId/join

`private`

旅行への参加情報の一覧を取得する

#### リクエスト

- URL
```
GET /travel/923495263452/join/123841292341
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

---

### <a name="api-get_travel_join"></a> GET /travel/:travelId/join/:userId

`private`

旅行への参加情報を取得する

#### リクエスト

- URL
```
GET /travel/923495263452/join/123841292341
```

#### レスポンス

- 参加済みの場合
	- body
	```json
	{
		"status": "OK",
		"result": {
			"id": "872123946123",
			"created": "2015-03-24 18:10",
			"updated": "2015-03-24 18:10",
			"owner": <% User %>,
			"travel": <% Travel %>
		}
	}
	```
- 未参加の場合
	- body
	```json
	{
		"status": "NG",
		"result": {
			"code": 1,
			"type": "NOT_FOUND",
			"detail": [ "join" ]
		}
	}
	```

---

### <a name="api-post_travel_join"></a> POST /travel/:travelId/join/:userId

`private`

旅行へ参加する。このAPIは参加するユーザー自身しか叩けない。

#### リクエスト

- URL
```
POST /travel/923495263452/join/123841292341
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
- すでに参加済みの場合
	- body
	```json
	{
		"status": "NG",
		"result": {
			"code": 4,
			"type": "ALREADY_CREATED",
			"detail": [ "join" ]
		}
	}
	```

---

### <a name="api-delete_travel_join"></a> DELETE /travel/:travelId/join/:userId

`private`

旅行への参加を取りやめる。このAPIは参加するユーザー自身しか叩けない。

> @NOTE
>
> userIDパラメータは現在は不要だが、
> 今後、ブロック機能とかつけるときのために残しておく。
> 要はRESTful性の確保

#### リクエスト

- URL
```
DELETE /travel/923495263452/join/123841292341
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
- 旅行にもとから参加していない場合
	- body
	```json
	{
		"status": "NG",
		"result": {
			"code": 3,
			"type": "INVALID_PARAMETER"
		}
	}
	```
