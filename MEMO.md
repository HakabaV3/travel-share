# マイルストーン1

- [ ]メンバー集め
	- [ ]メンバー招待

# 機能

- [ ]メンバー集め
	- [ ]メンバー招待
- [ ]日程決め
	- [ ]グループ内の日程調整
		- [ ]目的地の天気・休館日などの情報
- [ ]目的地選定
	- [ ]フリーワードでスポット検索
		- [ ]開館時間・休館日・料金などの情報
		- [ ]ルート検索・交通費計算
- [ ]ホテル手配
	- [ ]他サイト横断検索
	- [ ]予約
- [ ]レンタカー手配
- [ ]お会計機能
	- [ ]諸々の費用を簡単に計算
	- [ ]貸し借り機能
- [ ]コミュニケーション機能
	- [ ]写真・動画共有
	- [ ]アンケート機能
	- [ ]チャット
		- [ ]グループチャット
		- [ ]個別チャット

# エンティティとURI

- [ ] 認証状態
	- /auth
- [x] ユーザー
 	- /user/`:userId`
- [x] 旅行
 	- /travel/`:travelId`
- [x] 旅行への参加状況
 	- /travel/`:travelId`/join/`:userId`
- [x] 旅行への招待
 	- /travel/`:travelId`/invitation/`:userId`
- [x] 場所
 	- /place/`:placeId`
- [ ] メッセージ
	- /message/`:messageId`

## Message

チャットのメッセージを表すモデル

```json
{
	"id": "748323948123",
	"created": "2015-03-24 18:10",
	"updated": "2015-03-24 18:10",
	"target": "129851234723",		//投稿先
	"owner": "12384192341",			//投稿したUserのID
	"created": "2015-03-24 18:10",	//投稿日時
	"text": "Hello World!"			//本文
}
```

## Question

アンケートを表すモデル

```json
{
	"id": "091283021231",
	"created": "2015-03-24 18:10",
	"updated": "2015-03-24 18:10",
	"group": "129851723",		//該当するGroupのID
	"owner": "12384192341",		//作成したUserのID
	"text": "どこに行く?",		//本文
	"options": [				//選択肢一覧
		"10351231234",			//QuestionOptionのID
		"10351231235",
		"10351231236"
	]
}
```

## QuestionOption

アンケートに対する回答選択肢を表すモデル

```json
{
	"id": "127859283452",
	"created": "2015-03-24 18:10",
	"updated": "2015-03-24 18:10",
	"question": "0912830121231",	//該当するQuestionのID
	"text": "草津温泉"				//本文
}
```

## QuestionAnswer

アンケートに対する回答を表すモデル

```json
{
	"id": "136458112347",
	"created": "2015-03-24 18:10",
	"updated": "2015-03-24 18:10",
	"owner": "12384192341",			//回答したUserのID
	"question": "0912830121231",	//QuestionのID
	"questionOption": "27859283452"	//QuestionOptionのID
}
```

## GalleryItem

グループ内で共有した写真・動画などを表すモデル

```json
{
	"id": "871359813123",
	"created": "2015-03-24 18:10",
	"updated": "2015-03-24 18:10",
	"name": "写真 001",			//アイテムの名前
	"owner": "12384192341",		//投稿したUserのID
	"group": "0912830121231",	//投稿先GroupのID
	"file_url": "http://~~~~"	//実ファイルのURL
}
```