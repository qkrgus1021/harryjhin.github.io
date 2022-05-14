---
title: '[Android] View Binding 활성화'
excerpt: 'findViewById() 함수를 사용하지 않고 XML에 선언된 뷰에 접근하기'
---

## 개요

액티비티에서 뷰에 접근하기 위해 `findViewById()` 함수를 사용해 왔습니다.

다만 뷰마다 사용하는 것은 매우 귀찮은 일이기에 손쉽게 접근할 수 있는 뷰 바인딩 개념이 생겼습니다.

**참고**: 옛날에는 butterknife 라이브러리를 사용했으니 뷰 바인딩은 간단한 설정만으로 손쉽게 이용할 수 있습니다.
{: notice--info}

## 뷰 바인딩 활성화

`build.gradle` 파일에 다음 설정을 추가합니다.

```groovy
android {
    // ...
    buildFeatures {
        viewBinding true
    }
}
```

`Sync now` 버튼을 클릭하면 활성화가 완료되었습니다.

## 바인딩 객체 선언

액티비티에서 사용하기 위해 다음과 같이 선언합니다.

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        // 바인딩 객체 얻기
        val binding = ActivityMainBinding.inflate(layoutflater)
        // 액티비티 화면 출력
        setContentView(binding.root)
    }
}
```

액티비티의 이름에 따라 자동으로 바인딩 클래스가 생성됩니다(예: activity_main.xml -> ActivityMainBinding).

자동으로 만들어진 바인딩 클래스의 `inflate()` 함수를 호출하면 바인딩 객체를 얻을 수 있습니다.

이 떄 인자로 `layoutInflater`를 전달합니다.

액티비티 연결 후 화면 출력을 위해 `setContentView()` 함수를 호출합니다.

이 때 인자로 `binding.root`를 전달합니다.

바인딩 객체의 `root` 프로퍼티에는 XML의 루트 태그가 자동으로 등록되어 있어 연결됩니다.

## 바인딩 객체로 뷰 접근

XML의 뷰 id 속성을 알면 접근할 수 있습니다.

```kotlin
binding.textView1.text.setText("Hello")
```
