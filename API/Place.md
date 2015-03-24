## Travel

場所を表すモデル

- [構造](#struct)
- [API](#api)
	- [GET /place/:placeId](#api-get_place)
		場所の情報を取得する

**※太字は認証が必要なAPI**

## <a name="struct"></a>構造

```json
{
	"id": "094310512912",
	"created": "2015-03-24 18:10",
	"updated": "2015-03-24 18:10",

	//以下、Google Maps API 準拠

	"address_components" : [
		 {
			"long_name" : "48",
			"short_name" : "48",
			"types" : [ "street_number" ]
		 },
		 {
			"long_name" : "Pirrama Road",
			"short_name" : "Pirrama Road",
			"types" : [ "route" ]
		 },
		 {
			"long_name" : "Pyrmont",
			"short_name" : "Pyrmont",
			"types" : [ "locality", "political" ]
		 },
		 {
			"long_name" : "NSW",
			"short_name" : "NSW",
			"types" : [ "administrative_area_level_1", "political" ]
		 },
		 {
			"long_name" : "AU",
			"short_name" : "AU",
			"types" : [ "country", "political" ]
		 },
		 {
			"long_name" : "2009",
			"short_name" : "2009",
			"types" : [ "postal_code" ]
		 }
	  ],
	  "events" : [
		{
		  "event_id" : "9lJ_jK1GfhX",
		  "start_time" : 1293865200,
		  "summary" : "<p>A visit from author John Doe, who will read from his latest book.</p>
					   <p>A limited number of signed copies will be available.</p>",
		  "url" : "http://www.example.com/john_doe_visit.html"
		}
	  ],
	  "formatted_address" : "48 Pirrama Road, Pyrmont NSW, Australia",
	  "formatted_phone_number" : "(02) 9374 4000",
	  "geometry" : {
		 "location" : {
		   "lat" : -33.8669710,
		   "lng" : 151.1958750
		 }
	  },
	  "icon" : "http://maps.gstatic.com/mapfiles/place_api/icons/generic_business-71.png",
	  "id" : "4f89212bf76dde31f092cfc14d7506555d85b5c7",
	  "international_phone_number" : "+61 2 9374 4000",
	  "name" : "Google Sydney",
	  "rating" : 4.70,
	  "reference" : "CnRsAAAA98C4wD-VFvzGq-KHVEFhlHuy1TD1W6UYZw7KjuvfVsKMRZkbCVBVDxXFOOCM108n9PuJMJxeAxix3WB6B16c1p2bY1ZQyOrcu1d9247xQhUmPgYjN37JMo5QBsWipTsnoIZA9yAzA-0pnxFM6yAcDhIQbU0z05f3xD3m9NQnhEDjvBoUw-BdcocVpXzKFcnMXUpf-nkyF1w",
	  "reviews" : [
		 {
			"aspects" : [
			   {
				  "rating" : 3,
				  "type" : "quality"
			   }
			],
			"author_name" : "Simon Bengtsson",
			"author_url" : "https://plus.google.com/104675092887960962573",
			"text" : "Just went inside to have a look at Google. Amazing.",
			"time" : 1338440552869
		 }
	  ],
	  "types" : [ "establishment" ],
	  "url" : "http://maps.google.com/maps/place?cid=10281119596374313554",
	  "vicinity" : "48 Pirrama Road, Pyrmont",
	  "website" : "http://www.google.com.au/"
}
```

## <a name="api"></a>API

### <a name="api-get_place"></a> GET /place/:placeId

場所の情報を取得する

#### リクエスト

- URL
```
GET /place/094310512912
```

#### レスポンス

- 成功時
	- body
	```json
	{
		"status": "OK",
		"result": <% Place %>
	}
	```

- 場所が存在しない場合
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