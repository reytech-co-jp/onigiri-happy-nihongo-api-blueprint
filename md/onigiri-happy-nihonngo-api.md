FORMAT: 1A

# Happy Nihongo Onigiri用API仕様書

# Group Onigiri

## GET /onigiri-tests{?genre,testId}

テストデータ（1テスト：10単語分）を取得します。
Responseは2単語分に省略して表示

+ Parameters
  + genre: IT (string, required) - ジャンル名。50文字以内
  + testId: 1 (int, required) - テストID。999以下

+ Response 200 (application/json)
  + Body
        {
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
            },
            {
               "kanji": "入力",
               "answer": "input",
               "selectArray":[
                 "input",
                 "output",
                 "push",
                 "pull"
               ],
               "audio": "input.mp3"
            }
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
                "maximum value is 999",
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
