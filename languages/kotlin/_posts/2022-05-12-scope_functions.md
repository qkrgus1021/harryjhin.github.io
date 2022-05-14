---
title: '[Kotlin] Scope Function(let, with, run, apply, also)'
excerpt: '코틀린의 범위 함수의 정의와 차이를 알아보자'
---

## 개요

코틀린에는 객체 내의 코드를 실행하는 것이 목적인 함수가 있습니다. 람다식으로 객체에서 이러한 함수를 호출할 때 임시 범위를 형성합니다. 이 임시 범위는 해당 객체의 이름을 사용하지 않고도 객체에 접근할 수 있게 합니다.

말로만 들으면 이해가 잘 안 되니 `Person` 클래스를 예로 들어보겠습니다.

```kotlin
data class Person(var name: String, var age: Int) {
    fun introduce() {
        println("안녕, 내 이름은 ${name}이고 ${age}살이야." )
    }
    fun increamentAge() {
        age++
    }
}
```

기존에 `Person` 객체를 사용하는 방법은 다음과 같습니다.

```kotlin
fun main() {
    val jjh = Person("jjh", "20")
    println(jjh) // Person(name=jjh, age=20)
    jjh.introduce() // 안녕, 내 이름은 jjh이고 20살이야.
    jjh.increamentAge()
    println(jjh) // Person(name=jjh, age=21)
}
```

객체를 사용할 때마다 객체의 이름을 반복해야 합니다.

범위 함수를 사용하면 다음과 같이 사용할 수 있습니다.

```kotlin
fun main() {
    Person("jjh", 20).let {
        println(it) // Person(name=jjh, age=20)
        it.introduce() // 안녕, 내 이름은 jjh이고 20살이야.
        it.incrementAge()
        println(it) // Person(name=jjh, age=21)
    }
}
```

`it` 키워드는 자기 자신을 가리킵니다.

이처럼 범위 함수는 코드를 간결하고, 가독성 좋게 만들 수 있습니다.

다만 범위 함수는 `let`만 있는 것이 아니고, 이들의 특성과 결과가 비슷해서 사용할 때 많이 헷갈립니다.

선택의 기준은 보통 의도, 프로젝트 사용의 일관성에 따르게 되나, 각 차이점에 대해 먼저 알아두는 것이 좋습니다.

## 범위 함수 선택

목적에 맞는 범위 함수를 고르는 데 도움이 될만한 표입니다.

| 함수    | 객체 참조 | 반환값        | 목적                                                      |
| ------- | --------- | ------------- | --------------------------------------------------------- |
| `let`   | `it`      | 람다식 결과   | `null`이 아닌 객체에서 람다 실행, 지역 변수로 표현식 소개 |
| `run`   | `this`    | 람다식 결과   | 객체 구성 및 결과를 계산                                  |
| `run`   |           | 람다식 결과   | 표현식이 필요한 실행문                                    |
| `with`  | `this`    | 람다식 결과   | 객체에 대한 그룹화 함수 호출                              |
| `apply` | `this`    | 컨텍스트 객체 | 객체 구성                                                 |
| `also`  | `it`      | 컨텍스트 객체 | 추가 효과                                                 |

## 구별

범위 함수는 매우 유사하기 때문에 차이점을 이해하는 것이 중요합니다. 각 범위 함수에는 두 가지 핵심적인 차이점이 존재합니다.

- 컨텍스트 객체를 참조하는 방법
- 반환 값

### 컨텍스트 객체: `this` 또는 `it`

범위 함수의 람다 내에서 컨텍스트 객체는 이름 대신 짧은 참조(`this`, `it`)를 사용할 수 있습니다. 각 범위 함수는 두 가지 방법 중 하나를 사용합니다.

`this`는 람다 수신기(receiver), `it`은 람다 인수(argument)입니다. 둘 다 기능은 동일하나 각각의 장단점을 알아보겠습니다.

#### `this`

`run`, `with`, `apply` 함수는 `this` 키워드로 컨텍스트 객체를 람다 수신기로 참조합니다. 따라서 람다에서 객체는 일반 클래스 함수에서와 같이 사용할 수 있습니다. 대부분의 경우 수신자 객체의 멤버에 접근할 때 객체의 이름을 생략하여 짧은 코드를 작성하게 만들어줍니다.

따라서 `this`를 사용하는 범위 함수는 주로 객체 멤버에 대해 접근하는 람다에 권장합니다(setter 같은 느낌으로 초기 선언 시 멤버 초기화에 적합).

```kotlin
val adam = Person("Adam").apply { 
    age = 20                       // 같은 효과: this.age = 20 또는 adam.age = 20
    city = "London"
}
println(adam)
```

#### `it`

`let`, `also` 함수는 `it` 키워드로 컨텍스트 객체를 람다 인수로 사용합니다. 인수 이름이 선언되지 않은 경우, 객체는 암시적으로 `it`이라는 키워드를 통해 접근할 수 있게 됩니다.

```kotlin

```

### 반환 값

---

## 참조 문서

- <https://kotlinlang.org/docs/scope-functions.html>
