## Management > Certificate Manager > API v1.2 Guide

Certificate Manager provides an API for viewing and downloading certificate lists. Clients can register certificates and certificate files in the console and then access the data through the API.

### Basic information
#### EndPoint
```text
https://certmanager.api.nhncloudservice.com
```

#### APIs Provided
| Method | URI                                                                     | Description |
| ------ |-------------------------------------------------------------------------| --- |
| GET | /certmanager/v1.2/appkeys/{appKey}/certificates                         | Retrieve the certificate list. |
| GET | /certmanager/v1.2/appkeys/{appKey}/certificates/{certificateName}/files | Download the registered certificate file. |

##### API Request Path Variable

| Value | Type | Description |
| --- | --- | --- |
| appKey | String | Appkey of the NHN Cloud project storing the data to be used |
| certificateName | String | Name of the data (certificate) to be used |

##### API Response Data Common Headers

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
| resultCode | Number | API call result code |
| resultMessage | String | API call result message |
| isSuccessful | Boolean | Whether the API call was successful |

### Retrieve Certificate List

Use the function to retrieve a list of certificates registered in the Certificate Manager.

#### Request

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.2/appkeys/{appKey}/certificates?pageSize={pageSize}&pageNum={pageNum}&all={all}&status={status}
```

| Value | Type | Description | Input |
| --- | --- | --- | --- |
| pageSize | Number | Page size | 10 (default) |
| pageNum | Number | Page number | 1 (default) |
| all | Boolean | Full query | true, false (default) |
| status | String | Certificate status | ALL, EXPIRED, UNEXPIRED (default) |

※ The values ​​for "all" and "status" are case-insensitive.

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
                "certificateName": "nhncloudservice.com",
                "authority": "NHN",
                "domains": [
                  "nhncloudservice.com",
                  "*.nhncloudservice.com"
                ],
                "signatureAlgorithm": "SHA256withRSA",
                "fileCreationDate": "2025-03-02",
                "expirationDate": "2026-03-25"
            }
        ]
    }
}
```

| Value | Type | Description |
| --- | --- | --- |
| totalCount | Number | Total number of certificates |
| totalPage | Number | Total number of pages |
| currentPage | Number | Current page |
| pageSize | Number | Page size |
| certificateName | String | Certificate name |
| authority | String | Certificate authority |
| signatureAlgorithm | String | Signature method |
| fileCreationDate | String | Certificate file creation date |
| expirationDate | String | Certificate file expiration date |


### Download Certificate File

Use the feature to download the certificate file registered on the Certificate Manager.

#### Request

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.2/appkeys/{appKey}/certificates/{certificateName}/files
```

#### Success Response

[Response Header]

```
Content-Disposition:attachment; filename="{filenmae}"
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

#### Failure Response
[Response Header]
```
Content-Type:application/json
```
[Response Body]

```
{
    "header": {
        "resultCode": 52000,
        "resultMessage": "Certificate name does not exist.",
        "isSuccessful": false
    },
    "body": {}
}
```


#### When Using Command Line Interface(CLI)

The certificate file download API can be requested using the `curl` command.

```bash
#Write to a File
curl 'https://certmanager.api.nhncloudservice.com/certmanager/v1.2/appkeys/{appKey}/certificates/{certificateName}/files' > cert.pem

#Specify a file name
curl -o cert.pem 'https://certmanager.api.nhncloudservice.com/certmanager/v1.2/appkeys/{appKey}/certificates/{certificateName}/files'

#Keep the uploaded file name
curl -OJ 'https://certmanager.api.nhncloudservice.com/certmanager/v1.2/appkeys/{appKey}/certificates/{certificateName}/files'
```
* For how to use other curl commands, refer to the guide below:
  * curl command guide : [https://curl.haxx.se/docs/manpage.html](https://curl.haxx.se/docs/manpage.html)

### Response Code

| isSuccessful | resultCode | resultMessage | Description |
| ------------ | ---------- | ------------- | --- |
| true | 0 | SUCCESS | Success |
| false | 52000 | Certificate name does not exist. | The requested certificate name does not exist. |
| false | 52001 | Certificate file does not exist. | The requested certificate file does not exist. |
| false | 52002 | There are more than one certificate file. | There are more than one certificate file registered to the requested certificate. |
| false | 52003 | The certificate file is not a pem file. | The requested certificate file is not a pem file. |
| false | 52004 | The certificate name in the file is different from the requested certificate name. | The requested certificate name and the name registered in the certificate file are different. |
| false | 52005 | Certificate file has expired. | The requested certificate file has expired. |
| false | 52006 | The certificate has an invalid certificate authority name. | The certificate authority information in the requested certificate file is invalid. |
| false | 52007 | The requested certificate file should be one. | Only one certificate file can be uploaded at a time. |
| false | 52008 | The maximum permitted size is {} bytes. However, the requested {} bytes. | The maximum file size that can be uploaded is 512KB. |
