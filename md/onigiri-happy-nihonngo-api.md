FORMAT: 1A

# Happy Nihongo Onigiri用API仕様書

# Group Onigiri

## POST /onigiri-tests

テストデータを取得します。
以下のパラメータをJSON形式で送信します。

+ genre (string, required) - ジャンル名。50文字以内
+ testId (int, required) - テストID。11文字以内

+ Request (application/json)
  {
    "genre": "IT",
    "testId": "2"
  }

+ Response 201 (application/json)
  + Body
        {
          "kanji": "認証",
          "answer": "authentication"
          "selectArray":[
            "authentication",
            "zero-day",
            "authorization",
            "WAP"
          ],
          "audio": "authentication.mp3"
        }

+ Response 400
  + Body
        {
          "message":"validation error",
          "errors":[
            {
              "field":"eng_name",
              "messages":[
                "cannot be empty",
                "maximum length is 50"
              ]
            },
            {
              "field":"testId",
              "messages":[
                "cannot be null",
                "maximum length is 11",
              ]
            }
          ]
        }

# Group Common

## 存在しないURIへのアクセス

Response `404`

```json
{
  "message": "resource not found"
}
```

## DBへの接続ができないなどのシステムエラー

Response `500`

```json
{
  "message": "system error"
}
```
