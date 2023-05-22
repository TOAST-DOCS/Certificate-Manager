## Management > Certificate Manager > API v1.0 Guide

Certificate Manager provides APIs for certificate list lookup, uploading or downloading certificates. Clients must register certificates and certificate files on console to use data via APIs. 

### Basic Information
#### EndPoint
```text
https://certmanager.api.nhncloudservice.com
```

#### Available API Types 
| Method | URI | Description |
| ------ | --- | --- |
| GET | /certmanager/v1.0/appkeys/{appKey}/certificates | Look up the list of certificates. |
| GET | /certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files | Download certificate files that are registered. |

##### Path Variables of API Request

| Value | Type | Description |
| --- | --- | --- |
| appKey | String | Appkey of the NHN Cloud project in which data is saved |
| certificateName | String | Name of data (certificate) to use |

##### Common Data Header of API Response

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

| Value | Type | Description |
| --- | --- | --- |
| resultCode | Number | Result code value of API call |
| resultMessage | String | Result message of API call |
| isSuccessful | Boolean | API call successful or not |

### Lookup certificate list

Used to query the list of certificates registered with Certificate Manager.

#### Request

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates?pageSize={pageSize}&pageNum={pageNum}&all={all}&status={status}
```

| Value | Type | Description | Available |
| --- | --- | --- | --- |
| pageSize | Number | Page size | 10(default) |
| pageNum | Number | Page number | 1(default) |
| all | Boolean | Full lookup | true, false(default) |
| status | String | Certificate expiration status | ALL, EXPIRED, UNEXPIRED(default) | 

※ The values for all and status are case insensitive.

#### Response

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

| Value | Type | Description |
| --- | --- | --- |
| totalCount | Number | Total certificates |
| totalPage | Number | Total pages |
| currentPage | Number | Current page |
| pageSize | Number | Page size |
| certificateName | String | Certificate name |
| authority | String | Authority |
| signatureAlgorithm | String | Signature algorithm |
| fileCreationDate | String | Certificate file creation date |
| expirationDate | String | Certificate file expiration date |

### Downloading Certificate Files 

Certificate files registered at Certificate Manager can be downloaded. 

#### Request

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files
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

```bash
#Write to File
curl 'https://certmanager.api.nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files' > cert.pem

#Specify File Name
curl -o cert.pem 'https://certmanager.api.nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files'

#Maintain Uploaded File Name
curl -OJ 'https://certmanager.api.nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files'
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
| false | 52006 | The certificate has an invalid certificate authority name. | The certificate authority information in the requested certificate file is invalid. |
| false | 52007 | Requested certificate file should be one. | Only one certificate file can be uploaded at the same time. |
| false | 52008 | Maximum permitted size is {} bytes. But, requested {} bytes. | The maximum file size that can be uploaded is 512KB. |
