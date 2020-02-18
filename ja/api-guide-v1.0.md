## Management > Certificate Manager > API v1.0ガイド

Certificate Managerでは証明書のアップロード、ダウンロードを行うためのAPIを提供します。クライアントはコンソールで証明書と証明書ファイルを登録した後、APIを通してデータを使用できます。

### 基本情報
#### EndPoint
```text
https://alpha-api-certificate-manager.cloud.toast.com
```

#### 提供するAPI種類
| Method | URI | 説明 |
| ------ | --- | --- |
| POST | /certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files | 登録された証明書にファイルをアップロードします。ファイルが登録されている場合、アップロードしたファイルに更新されます。 |
| GET | /certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files | 登録された証明書ファイルをダウンロードします。 |

##### APIリクエストのパス変数

| 値 | タイプ | 説明 |
| --- | --- | --- |
| appKey | String | 使用するデータを保存しているTOASTプロジェクトのアプリキー |
| certificateName | String | 使用するデータ(証明書)の名前 |

##### APIレスポンスのデータ共通ヘッダ

``` json
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

### 証明書ファイルのアップロード

Certificate Managerに登録した証明書にファイルをアップロードする時に使用します。ファイルが登録されている場合、新たにアップロードしたファイルに更新されます。
サポートする証明書ファイル(.pem)の形式は[問題解決ガイド > 証明書ファイルフォーマット変換](http://alpha-docs.toast.com/ko/Management/Certificate%20Manager/ko/troubleshooting-guide/#_1)を参照してください。

#### リクエスト

```
POST https://alpha-api-certificate-manager.cloud.toast.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files
```

[Request Header]

```
Content-Type:multipart/form-data
```

[Request Body]

```
file: {ファイル}
```

#### レスポンス

[Response Header]

```
Content-Type:application/json
```

[Response Body]

``` json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    },
    "body": null
}
```

### 証明書ファイルのダウンロード

Certificate Managerに登録した証明書ファイルをダウンロードする時に使用します。

#### リクエスト

```
GET https://alpha-api-certificate-manager.cloud.toast.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files
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

```sh
#ファイルに書き込む
curl 'https://alpha-api-certificate-manager.cloud.toast.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files' > cert.pem

#ファイル名指定
curl -o cert.pem 'https://alpha-api-certificate-manager.cloud.toast.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files'

#アップロードしたファイル名を維持
curl -OJ 'https://alpha-api-certificate-manager.cloud.toast.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files'
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
| false | 52003 | The certificate file is not a pem file. | リクエストした証明書ファイルが.pemファイルではありません。 |
| false | 52004 | The certificate name in the file is different from the requested certificate name. | リクエストした証明書名と証明書ファイルに登録された名前が異なります。 |
| false | 52005 | Certificate file has expired | リクエストした証明書ファイルの有効期限が切れています。 |
