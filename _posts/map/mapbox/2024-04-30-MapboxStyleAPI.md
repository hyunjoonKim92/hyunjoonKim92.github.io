---
layout: post
title: "[Mapbox] Styles API"
date: 2024-04-30
description: Mapbox Styles API
---

![Mapbox Image](/assets/img/map/mapbox_style_image.png)
<br>

#### Mapbox Styles API 란?
* 지리적 데이터 및 지도 스타일을 관리하고 조작하는데 사용되는 API
* 사용자 정의 지도 스타일을 생성하고 관리할 수 있음
* [Mapbox Styles API Doc](https://docs.mapbox.com/api/maps/styles/)
<br>

#### Mapbox Styles API 특징
* **Style 생성**
  * 사용자 정의 지도 스타일 생성 가능
  * 원하는대로 지도의 모양을 조정
* **Style 수정**
  * 이미 생성된 스타일 수정 가능
  * 지도 스타일을 계속 개선하고 조정
* **Style 공유**
  * 생성된 스타일을 공유하고 다른 사용자들과 협업 가능
  * 개발자나 디자이너 간 지도 스타일을 공유하고 함께 작업 가능
* **Style Version 관리**
  * 이전 버전을 관리하고 특정 시점으로 되돌릴 수 있음
  * 스타일 변경 사항의 이력을 추적하고, 필요할 때 이전 버전으로 롤백
* **Style 적용**
  * 생성된 스타일을 지도에 적용하여 사용자에게 제공
  * 지도를 사용하는 사용자들의 사용자 정의 스타일을 적용한 지도 확인 가능
<br>

Mapbox Styles API 는 RESTful API 로 제공되며, HTTP 요청을 통해 스타일을 관리하고 수정할 수 있음
JSON 형식의 데이터를 사용하여 스타일을 정의하고 전송
<br><br>

#### Mapbox Style Spec
* Root
  * Mapbox Style 사양 내 전반적인 모습과 동작을 정의하는데 기초를 제공
```json
    {
        "version": 8,
        "name": "Mapbox Streets",
        "sprite": "mapbox://sprites/mapbox/streets-v{{ref.$version}}",
        "glyphs": "mapbox://fonts/mapbox/{fontstack}/{range}.pbf",
        "sources": {...},
        "layers": [...]
    } 
```
  * layers (<span style="color: gray">Required array of layers</span>)
    * 스타일에서 정의된 레이어들의 그리기 순서를 결정
  * sources (<span style="color: gray">Required object with wource values</span>)
    * 스타일에서 사용되는 지리적 데이터를 정의하는데 사용
  * version (<span style="color: gray">Required enum</span>)
    * 스타일 사양의 버전
  * glyphs (<span style="color: gray">Optional string. Default to "mapbox://fonts/mapbox/{fontstack}/{range}.pbf"</span>)
    * 스타일에 적용되는 글꼴을 지정
  * name (<span style="color: gray">Optional string</span>)
    * 스타일의 고유한 이름을 지정
  * sprite (<span style="color: gray">Optional string</span>)
    * 스타일에 사용되는 image sprite sheet 의 위치를 지정
<br>

---
<span style="color:red">**NOTE**</span>
<span style="font-size:100%">
    image sprite sheet 란 여러 개의 작은 image 를 하나의 큰 image file 에 결합하여 관리하는 기술
</span>

---
<br>

#### Style Object

|Property|Type|Description|
|---|---|-----|
|version|number|현재 사용중인 스타일 사양의 버전|
|name|string|스타일에 대한 이름|
|metadata|object|스타일에 관련된 부가적인 정보를 포함|
|sources|object|지도에 표시될 데이터 정의|
|layers|array|레이어들의 생성 순서를 지정|
|created|string|스타일이 생성된 날짜와 시간|
|id|string|스타일을 식별하는 고유한 식별자|
|modified|string|스타일이 마지막으로 수정된 날짜와 시간|
|owner|string|스타일 소유자의 이름|
|visibility|string|스타일의 액세스 제어|
|protected|boolean|스타일을 관리하고 보호|
|draft|boolean|스타일의 상태 <br> * 현재 작업중 또는 완전히 공개되지 않았을 경우 사용|

```json
{
  "version": 8,
  "name": "{name}",
  "metadata": "{metadata}",
  "sources": "{sources}",
  "sprite": "mapbox://sprites/{username}/{style_id}",
  "glyphs": "mapbox://fonts/{username}/{fontstack}/{range}.pbf",
  "layers": ["{layers}"],
  "created": "2015-10-30T22:18:31.111Z",
  "id": "{style_id}",
  "modified": "2015-10-30T22:22:06.077Z",
  "owner": "{username}",
  "visibility": "private",
  "protected": false,
  "draft": true
}
```

* 유효한 JSON 이어야 함
* 가장 최근 버전의 Mapbox Style Spec 에 맞춰야 함
* 최대 15개의 Source 로 구성될 수 있음
* 스타일 내 본문에 나열된 Style Spec 에 없는 Key 를 포함해서는 안됌
* 소스 객체의 URL 속성은 유효한 Mapbox Tileset ID 이어야 함
* Raster 및 Vector Source 만 지원

<br>

#### Style API
[Mapbox Javascript SDK](https://github.com/mapbox/mapbox-sdk-js/blob/main/docs/services.md)

##### Retrieve a style - 특정 스타일 검색
```javascript
# GET
https://api.mapbox.com/styles/v1/{username}/{style_id}
```

|Required parameters|Type|Description|
|---|---|-----|
|username|string|스타일이 속한 계정의 사용자 이름|
|style_id|string|검색할 스타일의 ID|

```json
# Response Body
{
  "version": 8,
  "name": "Meteorites",
  "metadata": {
    "mapbox:origin": "basic-template-v1",
    "mapbox:autocomposite": true,
    "mapbox:type": "template",
    "mapbox:sdk-support": {
      "js": "0.45.0",
      "android": "6.0.0",
      "ios": "4.0.0"
    }
  },
  "center": [74.24426803763072, -2.2507114487818853],
  "zoom": 0.6851443156248076,
  "bearing": 0,
  "pitch": 0,
  "sources": {
    "composite": {
      "url": "mapbox://mapbox.mapbox-streets-v8,examples.0fr72zt8",
      "type": "vector"
    }
  },
  "sprite": "mapbox://sprites/examples/cjikt35x83t1z2rnxpdmjs7y7",
  "glyphs": "mapbox://fonts/{username}/{fontstack}/{range}.pbf",
  "layers": [
    {
      "id": "background",
      "type": "background",
      "layout": {},
      "paint": {
        "background-color": []
      }
    },
    {}
  ],
  "created": "2015-10-30T22:18:31.111Z",
  "id": "cjikt35x83t1z2rnxpdmjs7y7",
  "modified": "2015-10-30T22:22:06.077Z",
  "owner": "examples",
  "visibility": "public",
  "protected": true,
  "draft": false
}
```
<br>

##### List styles - 스타일 리스트 검색
```javascript
# GET
https://api.mapbox.com/styles/v1/{username}
```

|Required parameters|Type|Description|
|---|---|-----|
|username|string|스타일이 속한 계정의 사용자 이름|

|Optional parameters|Type|Description|
|---|---|-----|
|draft|boolean|임시 스타일 반환 true, 모든 스타일 반환 false <br> Default: false|
|limit|integer|반환할 스타일의 최대 수|
|start|string|리스트를 시작할 스타일의 ID|

```json
# Response Body
[
  {
    "version": 8,
    "name": "My Awesome Style",
    "created": "{timestamp}",
    "id": "cige81msw000acnm7tvsnxcp5",
    "modified": "{timestamp}",
    "owner": "{username}"
  },
  {
    "version": 8,
    "name": "My Cool Style",
    "created": "{timestamp}",
    "id": "cig9rvfe300009lj9kekr0tm2",
    "modified": "{timestamp}",
    "owner": "{username}"
  }
]
```