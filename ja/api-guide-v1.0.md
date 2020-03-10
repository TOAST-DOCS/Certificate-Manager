## Management > Certificate Manager > API v1.0 가이드

Certificate Manager는 인증서 업로드, 다운로드를 위한 API를 제공합니다. 클라이언트는 콘솔에서 인증서와 인증서 파일을 등록한 후 API를 통해 데이터를 사용할 수 있습니다.

### 기본 정보
#### EndPoint
```text
https://api-certificate-manager.cloud.toast.com
```

#### 제공하는 API 종류
| Method | URI | 설명 |
| ------ | --- | --- |
| POST | /certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files | 등록되어있는 인증서에 파일을 업로드합니다. 파일이 등록되어 있는 경우, 업로드하는 파일로 교체됩니다. |
| GET | /certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files | 등록되어있는 인증서 파일을 다운로드합니다. |

##### API 요청의 경로 변수

| 값 | 타입 | 설명 |
| --- | --- | --- |
| appKey | String | 사용하려는 데이터를 저장하고 있는 TOAST 프로젝트의 앱 키 |
| certificateName | String | 사용하려는 데이터(인증서)의 이름 |

##### API 응답의 데이터 공통 헤더

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

| 값 | 타입 | 설명 |
| --- | --- | --- |
| resultCode | Number | API 호출 결과 코드값 |
| resultMessage | String | API 호출 결과 메시지 |
| isSuccessful | Boolean | API 호출 성공 여부 |

### 인증서 파일 업로드

Certificate Manager에 등록한 인증서에 파일을 업로드 할 때 사용합니다. 파일이 등록되어 있다면, 새로 업로드하는 파일로 교체됩니다.
지원하는 인증서 파일(.pem) 형식은 '[문제 해결 가이드 > 인증서 파일 포맷 변환](http://docs.toast.com/ko/Management/Certificate%20Manager/ko/troubleshooting-guide/#_1)' 참고 부탁드립니다.

#### 요청

```
POST https://api-certificate-manager.cloud.toast.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files
```

[Request Header]

```
Content-Type:multipart/form-data
```

[Request Body]

```
file: {파일}
```

#### 응답

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

### 인증서 파일 다운로드

Certificate Manager에 등록한 인증서 파일을 다운로드 할 때 사용합니다.

#### 요청

```
GET https://api-certificate-manager.cloud.toast.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files
```

#### 응답

[Response Header]

```
Content-Disposition:attachment; filename="{파일명}"
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
#### Command Line Interface(CLI) 사용 시

인증서 파일 다운로드 API는 `curl` 명령어를 사용하여 요청하실 수 있습니다.

```sh
#파일에 쓰기
curl 'https://api-certificate-manager.cloud.toast.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files' > cert.pem

#파일명 지정
curl -o cert.pem 'https://api-certificate-manager.cloud.toast.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files'

#업로드한 파일명 유지
curl -OJ 'https://api-certificate-manager.cloud.toast.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files'
```
* 기타 curl 명령어 사용 방법은 아래 링크 참고 부탁드립니다.
  * curl command guide : [https://curl.haxx.se/docs/manpage.html](https://curl.haxx.se/docs/manpage.html)

### 응답 코드

| isSuccessful | resultCode | resultMessage | 설명 |
| ------------ | ---------- | ------------- | --- |
| true | 0 | SUCCESS | 成功 |
| false | 52000 | Certificate name does not exist. | リクエストした証明書名が存在しません。 |
| false | 52001 | Certificate file does not exist. | リクエストした証明書ファイルが存在しません。 |
| false | 52002 | There are more than one certificate file. | リクエストした証明書に登録されたファイルが2つ以上あります。 |
| false | 52003 | The certificate file is not a pem file. | リクエストした証明書ファイルが.pemファイルではありません。 |
| false | 52004 | The certificate name in the file is different from the requested certificate name. | リクエストした証明書名と証明書ファイルに登録された名前が異なります。 |
| false | 52005 | Certificate file has expired | リクエストした証明書ファイルの有効期限が切れています。 |
| false | 52006 | The certificate has an invalid certificate authority name. | 要求された証明書ファイルの認証局情報が無効です。 |
| false | 52007 | Requested certificate file should be one. | 同時にアップロードできる証明書ファイルは1つだけです。 |
| false | 52008 | Maximum permitted size is {} bytes. But, requested {} bytes. | アップロードできる最大ファイルサイズは512KBです。 |