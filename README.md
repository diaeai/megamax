# Introduction
Megamax exposes its data via an Application Programming Interface (API), so developers can interact programmatically with the Megamax service. Our API has been adapted to match the specification of other services. However, there are slight differences.

### The Base-URL for all API calls:
```
https://api.megamax.me/api
```
All requests to the API shall be HTTP $\color{red}{GET}$ or $\color{red}{POST}$; most calls require $\color{red}{login}$ & $\color{red}{key}$, which can be found on your account settings.
### The Base-URL for all API calls:
```json
{
  "status": "string | `success` or `error`",
  "message": "string | `informational message. might vary, use the status in your code`",
  "result": "array or object or string | `result of the request`"
}
```
# File Management
### Get File
Get the file information
#### Request:
```
https://api.megamax.me/api/file/get/{hashid}?login={login}&key={key}
```
#### Parameters:
| Name  | Description | Example | Required
| ------------- | ------------- | ------------- |  ------------- |
| login | API Login	 | example@mail.com |  yes |
| key | API Key | IUPMWsMjrAHzdjTBoRyHCdeZ4F0mVI7d |  yes |
| hashid | File HashID | WeLMEmnAjkDgPvqK |  yes |
#### Response:
```json
{
  "status": "success",
  "message": "OK",
  "result": {
    "hashid": "VKfTySnLTOSLJ",
    "name": "MNCT EP 02 FHD",
    "type": "video",
    "size": 256365743,
    "views": 1,
    "poster": "lrWGphxAmdYo8.jpg",
    "status": "converted",
    "created_at": "2023-04-15T03:15:21.000000Z"
  }
}
```
### Get Files
Get the list information of your files
#### Request:
```
https://api.megamax.me/api/file/get?login={login}&key={key}&folder={folder}
```
#### Parameters:
| Name  | Description | Example | Required
| ------------- | ------------- | ------------- |  ------------- |
| login | API Login	 | example@mail.com |  yes |
| key | API Key | IUPMWsMjrAHzdjTBoRyHCdeZ4F0mVI7d |  yes |
| folder | Folder ID | 1 |  no |
| status | Get by status | onqueue, transferring, processing, converting, converted, failed	 |  no |
#### Response:
```json
{
  "status": "success",
  "message": "OK",
  "result": [
    {
      "hashid": "VKfTySnLTOSLJ",
      "name": "MNCT EP 02 FHD",
      "type": "video",
      "size": 256365743,
      "views": 1,
      "poster": "lrWGphxAmdYo8.jpg",
      "status": "converted",
      "created_at": "2023-04-15T03:15:21.000000Z"
    },
    {
      "hashid": "A0yEgf1z7NCha",
      "name": "Wataten!: An Angel Flew Down To Me - Ep 13",
      "type": "video",
      "size": 1380063437,
      "views": 0,
      "poster": "0YflPp787JDPG.jpg",
      "status": "converted",
      "created_at": "2023-04-14T07:16:19.000000Z"
    },
    {
      "hashid": "VMCXEq7gz4PUK",
      "name": "ORYNT EP 01 FHD",
      "type": "video",
      "size": 231966357,
      "views": 2,
      "poster": "dP2FhsByVGTka.jpg",
      "status": "converted",
      "created_at": "2023-04-13T22:46:29.000000Z"
    },
    {
      "hashid": "Bp5RI9krVCAEK",
      "name": "YGS EP 02 FHD",
      "type": "video",
      "size": 339038317,
      "views": 1,
      "poster": "1xxHWtNM7zr1Z.jpg",
      "status": "converted",
      "created_at": "2023-04-13T22:31:32.000000Z"
    }
  ]
}
```
## Upload File
Upload a video file. Before uploading a file. You need to generate an upload URL. And that returned URL should be requested with $\color{red}{POST}$ and must be $\color{red}{multipart/form-data}$
#### Request:
```
https://api.megamax.me/api/file/upload/generate?login={login}&key={key}
```
#### Parameters:
| Name  | Description | Example | Required
| ------------- | ------------- | ------------- |  ------------- |
| login | API Login	 | example@mail.com |  yes |
| key | API Key | IUPMWsMjrAHzdjTBoRyHCdeZ4F0mVI7d |  yes |
#### Response:
```json
{
  "status": "success",
  "message": "OK",
  "result": "https://endpoint.megamax.cloud/endpoint/file/upload/c76z9hu"
}
```
After you generated a new upload URL. You can use that result to upload your file.

Here's an example curl command:
```shell
curl -k -F file=@/path/to/sample.mp4 -F login={login} -F key={key} -F folder={folder} https://endpoint.megamax.cloud/endpoint/file/upload/c76z9hu
```
#### Response:
```json
{
  "status": "success",
  "message": "OK",
  "result": {
    "hashid": "9mOEbPDayyD3M1kN",
    "folder": null,
    "name": "sample.mp4",
    "ext": "mp4",
    "mimeType": "video/mp4",
    "size": 4073348,
    "status": "converting",
    "uploaded_at": "2023-01-09T21:32:11.000000Z"
  }
}
```
## Get Mirrors 'Iframes' and 'Downloads' URL
Get direct Mirrors URL of iframes video or download.
#### Request:
```
https://api.megamax.me/api/mirror/get/{hashid}?login={login}&key={key}
```
#### Parameters:
| Name  | Description | Example | Required
| ------------- | ------------- | ------------- |  ------------- |
| login | API Login	 | example@mail.com |  yes |
| key | API Key | IUPMWsMjrAHzdjTBoRyHCdeZ4F0mVI7d |  yes |
| hashid | File HashID | WeLMEmnAjkDgPvqK |  yes |
#### Response:
```json
{
  "status": "success",
  "message": "OK",
  "result": [
    {
      "title": "source",
      "size": 231966357,
      "mirrors": [
        {
          "driver": "ok",
          "iframe": "//ok.ru/videoembed/5937251879654",
          "link": null,
          "uploaded_at": "2023-04-13 22:46:37",
          "checked_at": null
        },
        {
          "driver": "uptobox",
          "iframe": "//uptostream.com/iframe/1w261fc75gme",
          "link": "https://uptobox.com/1w261fc75gme",
          "uploaded_at": "2023-04-13 22:46:38",
          "checked_at": null
        },
        {
          "driver": "streamlare",
          "iframe": "//streamlare.com/e/gLXEDVM03L9nQY74",
          "link": "//streamlare.com/v/gLXEDVM03L9nQY74",
          "uploaded_at": "2023-04-13 22:46:41",
          "checked_at": null
        }
      ]
    }
  ]
}
```
## Get Direct 'Streams' and 'Downloads' URL
Get direct URL of streams file or download. Make sure you have enough available premium plan. Check our premium plans
#### Request:
```
https://api.megamax.me/api/file/get/{hashid}/direct?login={login}&key={key}
```
#### Parameters:
| Name  | Description | Example | Required
| ------------- | ------------- | ------------- |  ------------- |
| login | API Login	 | example@mail.com |  yes |
| key | API Key | IUPMWsMjrAHzdjTBoRyHCdeZ4F0mVI7d |  yes |
| hashid | File HashID | WeLMEmnAjkDgPvqK |  yes |
#### Response:
```json
{
  "status": "success",
  "message": "OK",
  "result": [
    {
      "label": "source",
      "size": 733297168,
      "stream": "https://cdn1.megamax.cloud/attach/1/1681874106/UeyDOobUnWCKp/MNCT_EP_02_.mp4?signature=8c532269ebd6fc781407a837e221a19e37e4bdefcbc72b9ce1be4a0e2de0094a",
      "download": "https://cdn1.megamax.cloud/attach/1/1681874106/UeyDOobUnWCKp/MNCT_EP_02_.mp4?dl=1&signature=268a08ed0d7d75b52e27b60729a671a055f974d5597c1473f66b30784a7303bb",
      "expires_at": "2023-04-19T03:15:06.669931Z"
    }
  ]
}
```




