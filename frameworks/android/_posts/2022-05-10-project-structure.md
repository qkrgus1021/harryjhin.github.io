---
title: '[안드로이드] 프로젝트 구조'
excerpt: '안드로이드 프로젝트는 여러 파일로 구성되어 있습니다.'
---

## 개요

안드로이드 프로젝트를 다음과 같이 설정하고 생성합니다.

- Template: Empty Activity
- Name: com.example
- Language: Kotlin
- Minimum SDK: API 21

## 프로젝트 구조

```markdown
.
├─manifests
│   └─AndroidManifest.xml
├─java
│   ├─com.example.myapplication
│   │    └─MainActivity.kt
│   ├─com.example.myapplication (androidTest)
│   │    └─ExampleInstrumentedTest.kt
│   └─com.example.myapplication (test)
│        └─ExampleUnitTest.kt
├─res
│   ├─drawable  // 이미지 리소스 폴더
│   ├─layout    // 액티비티 레이아웃 폴더
│   │   └─activity_main.xml
│   ├─mipmap    // 앱의 아이콘 폴더
│   ├─values    // 리소스화 폴더 (문자열 다국어, 테마 등)
│   └─xml
├─build.gradle (project)
└─build.gradle (module)
```

- `AndroidManifest.xml`은 앱 구성을 기술한 파일입니다. 액티비티가 몇 개인지, 어느 액티비티가 시작 부분인지와 같은 정보가 들어 있습니다. 보통은 자동으로 작성되는데 특정 작업을 하기 위해 앱에 권한을 추가할 때는 직접 편집합니다. 앞으로 매니페스트라고 언습하면 이 파일을 가리키는 것입니다.
- `MainActivity.kt`는 코드를 착정하고 `activity_main.xml` 파일에는 화면 레이아웃을 작성합니다. 이 둘이 한 세트라고 생각하면 됩니다.
- `build.gradle`은 안드로이드의 빌드 구성 파일입니다. 빌드에 필요한 각종 설정 스크립트가 Groovy 언어로 작성되어 있습니다.
