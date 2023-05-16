## Management > Certificate Manager > API v1.0ガイド

Certificate Manager は、証明書リスト検索、証明書のアップロード、またはダウンロード用の API を提供します。クライアントはコンソールで証明書と証明書ファイルを登録した後、APIを通してデータを使用できます。

### 基本情報
#### EndPoint
```text
https://certmanager.api.gov-nhncloudservice.com
```

#### 提供するAPI種類
| Method | URI | 説明 |
| ------ | --- | --- |
| GET | /certmanager/v1.0/appkeys/{appKey}/certificates | 証明書のリストを検索します。 |
| GET | /certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files | 登録された証明書ファイルをダウンロードします。 |

##### APIリクエストのパス変数

| 値 | タイプ | 説明 |
| --- | --- | --- |
| appKey | String | 使用するデータを保存しているNHN Cloudプロジェクトのアプリキー |
| certificateName | String | 使用するデータ(証明書)の名前 |

##### APIレスポンスのデータ共通ヘッダ

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    },
    "body": {

    }
}
```

| 値 | タイプ | 説明 |
| --- | --- | --- |
| resultCode | Number | API呼び出し結果コード値 |
| resultMessage | String | API呼び出し結果メッセージ |
| isSuccessful | Boolean | API呼び出し成否 |

### 証明書の検索リスト

Certificate Manager に登録されている証明書のリストを照会するために使用されます。

#### リクエスト

```
GET https://certmanager.api.gov-nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates?pageSize={pageSize}&pageNum={pageNum}&all={all}&status={status}
```

| 値 | タイプ | 説明 | 入力可能 |
| --- | --- | --- | --- |
| pageSize | Number | ページサイズ | 10(default) |
| pageNum | Number | ページ番号 | 1(default) |
| all | Boolean | 完全検索 | true, false(default) |
| status | String | 証明書の有効期限ステータス | ALL, EXPIRED, UNEXPIRED(default) |

※ all、statusの値は大文字/小文字を区別せずに使用できます。

#### レスポンス

[Response Header]

```
Content-Type:application/json
```

[Response Body]

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    },
    "body": {
        "totalCount": 1,
        "totalPage": 1,
        "currentPage": 1,
        "pageSize": 10,
        "data": [
            {
                "certificateName": "test.nhn.com",
                "authority": "NHN",
                "signatureAlgorithm": "SHA256withRSA",
                "fileCreationDate": "2020-03-02",
                "expirationDate": "2021-03-25"
            }
        ]
    }
}
```

| 値 | タイプ | 説明 |
| --- | --- | --- |
| totalCount | Number | 証明書の合計数 |
| totalPage | Number | 合計ページ数 |
| currentPage | Number | 現在のページ |
| pageSize | Number | ページサイズ |
| certificateName | String | 名証明書 |
| authority | String | 権限 |
| signatureAlgorithm | String | シグニチャ アルゴリズム |
| fileCreationDate | String | 証明書ファイルの作成日 |
| expirationDate | String | 証明書ファイルの有効期限 |

### 証明書ファイルのダウンロード

Certificate Managerに登録した証明書ファイルをダウンロードする時に使用します。

#### リクエスト

```
GET https://certmanager.api.gov-nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files
```

#### レスポンス

[Response Header]

```
Content-Disposition:attachment; filename="{ファイル名}"
Content-Type:application/octet-stream
```

[Response Body]

```
-----BEGIN CERTIFICATE-----
...
-----END CERTIFICATE-----
...
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
```
#### Command Line Interface(CLI)使用時

証明書ファイルダウンロードAPIは`curl`コマンドを使用してリクエストできます。

```bash
#ファイルに書き込む
curl 'https://certmanager.api.gov-nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files' > cert.pem

#ファイル名指定
curl -o cert.pem 'https://certmanager.api.gov-nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files'

#アップロードしたファイル名を維持
curl -OJ 'https://certmanager.api.gov-nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files'
```
* その他curlコマンドの使用方法は下記のガイドを参照してください。
  * curl command guide : [https://curl.haxx.se/docs/manpage.html](https://curl.haxx.se/docs/manpage.html)

### レスポンスコード

| isSuccessful | resultCode | resultMessage | 説明 |
| ------------ | ---------- | ------------- | --- |
| true | 0 | SUCCESS | 成功 |
| false | 52000 | Certificate name does not exist. | リクエストした証明書名が存在しません。 |
| false | 52001 | Certificate file does not exist. | リクエストした証明書ファイルが存在しません。 |
| false | 52002 | There are more than one certificate file. | リクエストした証明書に登録されたファイルが2つ以上あります。 |
| false | 52003 | The certificate file is not a pem file. | リクエストした証明書ファイルがpemファイルではありません。 |
| false | 52004 | The certificate name in the file is different from the requested certificate name. | リクエストした証明書名と証明書ファイルに登録された名前が異なります。 |
| false | 52005 | Certificate file has expired | リクエストした証明書ファイルの有効期限が切れています。 |
| false | 52006 | The certificate has an invalid certificate authority name. | 要求された証明書ファイルの認証局情報が無効です。 |
| false | 52007 | Requested certificate file should be one. | 同時にアップロードできる証明書ファイルは1つだけです。 |
| false | 52008 | Maximum permitted size is {} bytes. But, requested {} bytes. | アップロードできる最大ファイルサイズは512KBです。 |
