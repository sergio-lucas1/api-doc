---
tags: [Survey]
---

# Syncronization screen

![](../../assets/images/screens/sync.png)

### Actions:
- Try Again - перезапускает синхронизацию

### Data upload:
На этапе синхронизации отправлятся данные получение с устройства на сервер.
Синхронизацию можно разделить на несколько этапов:
 1. [Получения эндпоинта для загрузки файлов на амазон ](#receiving-data)
 2. [Загрузка файлов по эндпоинтам с ответа от сервера ](#upload-data)
 3. Уведомление о том что данные отправлены

Все файлы можно разделить на категории:
  - [Данные по калибровке](#calibration-data)
  - [Данные по записи экрана](#screen-data)
  - [Данные с камеры](#capture-data)

## Receiving data

### Calibration data
  - calibration_capture.mp4 - запись камеры в момент прохождения калибровки
  - [calibration_{create_timestamp}.json](../../examples/data/calibration/calibration.md) - данные по устройству в момент калибровки

  Request body:
<!--
type: tab
title: Schema
-->

```json json_schema
{
  "type": "object",
  "properties": {
    "questionid": {
      "type": "number",
    },
    "respondentid": {
      "type": "number"
    },
    "dataType": {
      "type": "string",
      "description": "Static value",
      "enum": ["responseData"]
    },
    "webEyeTracker": {
      "type": "boolean",
      "enum": [true]
    },
    "files": {
      "type": ["string", "array"]
    },
    "ignoreMimeType": {
      "type": "boolean",
      "enum": [false]
    }
  },
  "required": [
    "questionid",
    "respondentid",
    "webEyeTracker",
    "dataType",
    "files",
    "ignoreMimeType"
  ]
}
```

<!--
type: tab
title: Example
-->

```json
{
  "questionid": 238385457,
  "respondentid": 239086415,
  "dataType": "responseData",
  "webEyeTracker": true,
  "ignoreMimeType": false,
  "files": ["calibration_{create_timestamp}.json", "calibration_capture.mp4"]
}
```

<!-- type: tab-end -->

### Screen data
  - capture.mp4 - запись экрана в момент сбора данных
  - data.json - пока не ясно для чего данный файл. [Структура](../../examples/data/screen/data.md)
  - index.json - хранит массив с одним элементом типа "string" (["capture.mp4"]) - имя видеофайла

<!-- theme: danger -->
> После загрузки файла **index.json** необходимо [уведомить сервер]  что файлы доступны для анализа(#data-uploaded)

  Request body:
<!--
type: tab
title: Schema
-->

```json json_schema
{
  "type": "object",
  "properties": {
    "questionid": {
      "type": "number",
    },
    "respondentid": {
      "type": "number"
    },
    "dataType": {
      "type": "string",
      "description": "Static value",
      "enum": ["responseData"]
    },
    "screenShotTracker": {
      "type": "boolean",
      "enum": [true]
    },
    "files": {
      "type": ["string", "array"]
    },
    "ignoreMimeType": {
      "type": "boolean",
      "enum": [false]
    }
  },
  "required": [
    "questionid",
    "respondentid",
    "screenShotTracker",
    "dataType",
    "files",
    "ignoreMimeType"
  ]
}
```

<!--
type: tab
title: Example
-->

```json
{
  "questionid": 238385457,
  "respondentid": 239086415,
  "dataType": "responseData",
  "screenShotTracker": true,
  "ignoreMimeType": false,
  "files": ["data.json", "capture.mp4", "index.json"]
}
```

<!-- type: tab-end -->



### Capture data
  - capture.mp4 - запись камеры в момент сбора данных
  - tracking_{create_timestamp}.json - [данные в момент сбора](../../examples/data/camera/tracking.md)
  - data.json - [тачи, скролы в вебвью/прототипе](../../examples/data/camera/data.md)
  - index.json - хранит массив с одним элементом типа "string" (["capture.mp4"]) - имя видеофайла
  - wet-job-info.json - general file -[ хранит ссылки на файлы](../../examples/data/camera/wet-job-info.md)

<!-- theme: danger -->
> После загрузки файлов **index.json, wet-job-info.json** необходимо [уведомить сервер](#data-uploaded) что файлы доступны для анализа

  Request body:
<!--
type: tab
title: Schema
-->

```json json_schema
{
  "type": "object",
  "properties": {
    "questionid": {
      "type": "number",
    },
    "respondentid": {
      "type": "number"
    },
    "dataType": {
      "type": "string",
      "description": "Static value",
      "enum": ["responseData"]
    },
    "webcamTracker": {
      "type": "boolean",
      "enum": [true]
    },
    "files": {
      "type": ["string", "array"]
    },
    "ignoreMimeType": {
      "type": "boolean",
      "enum": [false]
    }
  },
  "required": [
    "questionid",
    "respondentid",
    "webEyeTracker",
    "dataType",
    "files",
    "ignoreMimeType"
  ]
}
```

<!--
type: tab
title: Example
-->

```json
{
  "questionid": 238385457,
  "respondentid": 239086415,
  "dataType": "responseData",
  "webcamTracker": true,
  "ignoreMimeType": false,
  "files": ["tracking_{create_timestamp}.json", "capture.mp4", "data.json", "index.json", "wet-job-info.json"]
}
```

<!-- type: tab-end -->



 ```yaml http
{
  "method": "post",
  "url": "https://test3.2futureresearch.com/GetUploadTokens.ashx"
}
```

<!--
type: tab
title: Schema
-->

```json json_schema
{
  "type": "object",
  "properties": {
    "questionid": {
      "type": "number",
    },
    "respondentid": {
      "type": "number"
    },
    "dataType": {
      "type": "string",
      "description": "Static value",
      "enum": ["responseData"]
    },
    "screenShotTracker": {
      "type": "boolean",
      "enum": [true]
    },
    "files": {
      "type": ["string", "array"]
    },
    "ignoreMimeType": {
      "type": "boolean",
      "enum": [false]
    }
  },
  "required": [
    "questionid",
    "respondentid",
    "screenShotTracker",
    "dataType",
    "files",
    "ignoreMimeType"
  ]
}
```

<!--
type: tab
title: application/json
-->

```json
{
  "res": "1",
  "files": [
    {
      "OriginalFileName": "[VID_20200226_093838.mp4",
      "UploadUrl": "https://s3.amazonaws.com/cooltool.static/ProjectContact/ProjectContact_239086446/WebEyeTracker/q_239080159/_VID_20200226_093838.mp4?AWSAccessKeyId=AKIAJK2OK5NFLD3C3BPQ&ContentType=video%2Fmp4&Expires=1585508220&Signature=PGRAwv8dEo7hRrL2UtcIBNSTmcU%3D"
    },
    {
      "OriginalFileName": "\r\n123.mp4",
      "UploadUrl": "https://s3.amazonaws.com/cooltool.static/ProjectContact/ProjectContact_239086446/WebEyeTracker/q_239080159/_123.mp4?AWSAccessKeyId=AKIAJK2OK5NFLD3C3BPQ&ContentType=video%2Fmp4&Expires=1585508220&Signature=CQejevlU3wC5RMNpNhuLum8P384%3D"
    },
    {
      "OriginalFileName": "\r\ntest.mp4]",
      "UploadUrl": "https://s3.amazonaws.com/cooltool.static/ProjectContact/ProjectContact_239086446/WebEyeTracker/q_239080159/_test.mp4%5D?AWSAccessKeyId=AKIAJK2OK5NFLD3C3BPQ&ContentType=application%2Foctet-stream&Expires=1585508220&Signature=mel06tEUiL7Lt1P8DsGtcOyij4Y%3D"
    }
  ]
}
```

<!-- type: tab-end -->

## Upload data

<!-- theme: danger -->
> На сервер выгружается blob для каждого файла


 ```yaml http
{
  "method": "put",
  "url": "https://s3.amazonaws.com/cooltool.static/ProjectContact/ProjectContact_239086446/WebEyeTracker/q_239080159/_test.mp4%5D?AWSAccessKeyId=AKIAJK2OK5NFLD3C3BPQ&ContentType=application%2Foctet-stream&Expires=1585508220&Signature=mel06tEUiL7Lt1P8DsGtcOyij4Y%3D"
}
```


## Data uploaded

Пометка файлов как "получен"


 ```yaml http
{
  "method": "post",
  "url": "http://test3.2futureresearch.com/DataUploaded.ashx"
}
```

  Request body:
<!--
type: tab
title: Schema
-->

```json json_schema
{
  "type": "object",
  "properties": {
    "dataType": {
      "type": "string",
    },
    "filePath": {
      "type": "string",
      "description": "Путь к файлу на амазоне"
    },
    "files": {
      "type": "string",
      "description": "Имя файла"
    },
    "questionid": {
      "type": "number",
    },
    "respondentid": {
      "type": "number"
    },
    "webEyeTracker": {
      "type": "boolean",
      "enum": [true]
    }
  },
  "required": [
    "questionid",
    "respondentid",
    "webEyeTracker",
    "dataType",
    "files",
    "filePath"
  ]
}
```

<!--
type: tab
title: Example
-->

```json
{
  dataType:"responseData"
  filePath:"https://s3.amazonaws.com/cooltool.static/ProjectContactAnswer/ProjectContactAnswer_239063406/WebCamCaptures/wet-job-info.json"
  files:"wet-job-info.json"
  questionid:238385457
  respondentid:"239063397"
  webEyeTracker:true
}
```

<!-- type: tab-end -->
