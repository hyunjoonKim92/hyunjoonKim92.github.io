---
layout: post
title: "[TypeScript] tsconfig"
date: 2024-04-29
description: tsconfig
---


```javascript
// tsconfig.js

{
    "compilerOptions": {
        "outDir": "./dist/", // compile 된 js 파일 저장 경로
        "sourceMap": true, // 
        "noImplicityAny": true, // any type 추론할 경우 error 처리
        "module": "es6",
        "target": "es5", // typescript code 가 javascript code 로 compile 될 때 지정될 언어
        "allowJs": true
    }
}
```