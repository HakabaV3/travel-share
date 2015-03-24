## Travel

旅行を表すモデル

- [構造](#struct)
- [API](#api)
	- [GET /travel/:travelId](#api-get_travel)
		旅行の情報を取得する
	- **[POST /travel](#api-post_travel)※**
		旅行を作成する
	- **[PATCH /travel/:travelId](#api-patch_travel)※**
		旅行の情報を変更する

**※太字は認証が必要なAPI、ただし`GET /travel/:travelId`は認証することで情報量が増える**

## <a name="struct"></a>構造

```json
{
	"id": "923495263452",
	"created": "2015-03-24 18:10",
	"updated": "2015-03-24 18:10",
	"name": "温泉旅行",	//名前
	"members": [ <% User %> ],	//メンバー一覧
	"places": [ <% Place %> ],	//行き先一覧
}
```

## <a name="api"></a>API

### <a name="api-get_travel"></a> GET /travel/:travelId

旅行の情報を取得する。認証していない場合、取得できる情報は`Travel#name`のみ。

#### リクエスト

- URL
```
GET /travel/923495263452
```

#### レスポンス

- 成功時(未認証)
	- body
	```json
	{
		"status": "OK",
		"result": {
			"id": "923495263452",
			"created": "2015-03-24 18:10",
			"updated": "2015-03-24 18:10",
			"name": "温泉旅行",
			"members": [],
			"places": []
		}
	}
	```
- 成功時(認証済み)
	- body
	```json
	{
		"status": "OK",
		"result": {
			"id": "923495263452",
			"created": "2015-03-24 18:10",
			"updated": "2015-03-24 18:10",
			"name": "温泉旅行",
			"members": [{
				"id": "123841292341",
				"created": "2015-03-24 18:10",
				"updated": "2015-03-24 18:10",
				"userId": "kikurage",
				"name": "きくらげ"
			}, {
				"id": "123841292342",
				"created": "2015-03-24 18:10",
				"updated": "2015-03-24 18:10",
				"userId": "stogu",
				"name": "stogu"
			}, {
				"id": "123841292341",
				"created": "2015-03-24 18:10",
				"updated": "2015-03-24 18:10",
				"userId": "jinssk",
				"name": "jinssk"
			}],
			"places": [				//@TODO //行き先一覧
				"094310512912",		//行き先のPlaceのID
				"094310512913",
				"094310512914"
			]
		}
	}
	```
- 旅行が存在しない場合
	- body
	```json
	{
		"status": "NG",
		"result": {
			"code": 1,
			"type": "NOT_FOUND",
			"detail": [ "travel" ]
		}
	}
	```

---

### <a name="api-post_travel"></a> POST /travel

`private`

旅行を作成する

#### リクエスト

- URL
```
POST /travel
```
- body
```json
{
	"name": "温泉旅行"
}
```

#### レスポンス

- 成功時
	- body
	```json
	{
		"status": "OK",
		"result": <% Travel %>
	}
	```
- パラメータのうち、nameを送信しなかった場合
	- body
	```json
	{
		"status": "NG",
		"result": {
			"code": 3,
			"type": "INVALID_PARAMETER",
			"detail": ["name"]
		}
	}
	```

---

### <a name="api-patch_travel"></a> PATCH /travel/:travelId

`private`

旅行の情報を変更する。旅行メンバー以外がこのAPIを叩いた場合`PERMISSION_DENIED`となる。

#### リクエスト

- URL
```
PATCH /travel/923495263452
```
- body
```json
{
	"name": "温泉旅行(edited)"
}
```

#### レスポンス

- 成功時
	- body
	```json
	{
		"status": "OK",
		"result": <% Travel %>
	}
	```
