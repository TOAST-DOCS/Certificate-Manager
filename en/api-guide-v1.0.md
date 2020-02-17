## Management > Certificate Manager > API v1.0 Guide

Certificate Manager provides APIs to upload or download certificates. Clients must register certificates and certificate files on console to use data via APIs. 

### Basic Information
#### EndPoint
```text
https://alpha-api-certmanager.cloud.toast.com
```

#### Available API Types 
| Method | URI | Description |
| ------ | --- | --- |
| POST | /certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files | Upload files to a registered certificate. If a file is already registered, it shall be replaced by a newly uploaded file. |
| GET | /certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files | Download certificate files that are registered. |

##### Path Variables of API Request

| Value | Type | Description |
| --- | --- | --- |
| appKey | String | Appkey of the TOAST project in which data is saved |
| certificateName | String | Name of data (certificate) to use |

##### Common Data Header of API Response

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

| Value | Type | Description |
| --- | --- | --- |
| resultCode | Number | Result code value of API call |
| resultMessage | String | Result message of API call |
| isSuccessful | Boolean | API call successful or not |

### Uploading Certificate Files 

Files can be uploaded to certificates registered at Certificate Manager. If a file is already registered, it shall be replaced by a newly uploaded file.  
Regarding supported certificate file formats (.pem), read '[Troubleshooting Guide > Converting Certificate File Formats](http://alpha-docs.toast.com/ko/Management/Certificate%20Manager/ko/troubleshooting-guide/#_1)'.

#### Request

```
POST /certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files
```

[Request Header]

```
Content-Type:multipart/form-data
```

[Request Body]

```
file: {file}
```

#### Response

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

### Downloading Certificate Files 

Certificate files registered at Certificate Manager can be downloaded. 

#### Request

```
GET /certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files
```

#### Response

[Response Header]

```
Content-Disposition:attachment; filename="{file name}"
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
#### For Command Line Interface (CLI) 

Download Certificate File API can be requested by using the `curl` command. 

```sh
#Write to File
curl 'https://alpha-api-certmanager.cloud.toast.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files' > cert.pem

#Specify File Name
curl -o cert.pem 'https://alpha-api-certmanager.cloud.toast.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files'

#Maintain Uploaded File Name
curl -OJ 'https://alpha-api-certmanager.cloud.toast.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files'
```
* See the link below on how to use curl command
  * curl command guide : [https://curl.haxx.se/docs/manpage.html](https://curl.haxx.se/docs/manpage.html)

### Response Codes

| isSuccessful | resultCode | resultMessage | Description |
| ------------ | ---------- | ------------- | --- |
| true | 0 | SUCCESS | Successful |
| false | 52000 | Certificate name does not exist. | Requested certificate name does not exist. |
| false | 52001 | Certificate file does not exist. | Requested certificate file does not exist. |
| false | 52002 | There are more than one certificate file. | More than two files are registered for requested certificate. |
| false | 52003 | The certificate file is not a pem file. | Requested certificate file is not pem file. |
| false | 52004 | The certificate name in the file is different from the requested certificate name. | Requested certificate name is different from registered name on certificate file. |
| false | 52005 | Certificate file has expired | Requested certificate file is expired. |
