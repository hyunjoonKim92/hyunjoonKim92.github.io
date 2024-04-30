---
layout: post
title: "[Mapbox] Styles API"
date: 2024-04-30
description: Mapbox Styles API
---

![제목](/assets/img/map/mapbox_style_image.png)
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
  * layers (Required array of layers)
    * 스타일에서 정의된 레이어들의 그리기 순서를 결정
  * sources (Required object with wource values)
    * 스타일에서 사용되는 지리적 데이터를 정의하는데 사용
  * version (Required enum)
    * 스타일 사양의 버전
  * glyphs (Optional string. Default to "mapbox://fonts/mapbox/{fontstack}/{range}.pbf")
    * 스타일에 적용되는 글꼴을 지정
  * name (Optional string)
    * 스타일의 고유한 이름을 지정
  * sprite (Optional string)
    * 스타일에 사용되는 image sprite sheet 의 위치를 지정
<br>

---
<span style="color:red">**NOTE**</span>

<span style="font-size:100%">
    image sprite sheet 란 여러 개의 작은 image 를 하나의 큰 image file 에 결합하여 관리하는 기술
</span>

---