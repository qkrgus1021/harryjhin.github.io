---
title: '[Kotlin] 함수 타입'
excerpt: '함수 타입은 함수를 선언할 때 매개변수와 반환 타입을 의미합니다.'
---

일반적인 함수의 선언은 다음과 같습니다.

```kotlin
fun temp(x: Int, y: Int): Int {...}
```

여기서 `(x: Int, y: Int): Int`를 `(Int, Int) -> Int`로 표현할 수 있습니다.

```kotlin
val temp: (Int, Int) -> Int = {x: Int, y: Int -> ...}
```

- `(x: Int, y: Int): Int`는 함수 타입에 해당됩니다.
- `{x: Int, y: Int -> ...}`는 람다 함수에 해당됩니다.
