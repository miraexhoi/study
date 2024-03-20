# 변수

변동이 심한, 가변적인, 변할 수 있는 숫자를 말합니다. 프로그래밍에서 말하고 싶은 변수의 뜻은 가변할 수 있는 값을 지정할 수 있는 저장공간입니다.  프로그램을 만드는 주재료가 됩니다.

## 변수 선언 기본 형태

`var/val 변수명: 변수타입 = 초기화값`

ex)

```kotlin
fun main() {
var name: String = " "
        val age: Int = 10
    val alive: Boolean = true
}
```

### **var/val**

**val(Immutable)**

- val 로 선언된 함수는 초기에 값을 할당하면 더이상 값을 변경할 수 없습니다.
- 읽기만 가능한 변수입니다.

**var(Mutable)**

- `var` 로 선언된 값의 변경이 가능합니다.
- 그러나, 다른 타입의 값을 넣을 수는 없습니다.
- 읽기/쓰기가 가능한 변수입니다.

## 변수명

- 변수명은 본인 목적에 맞게 마음대로 설정 가능
- 가끔 이미 코틀린에서 사용되고 있는 예약어(ex. `val`, `in` 등)를 변수에 사용해야 될 경우가 있습니다. 변수명을 변경할 수도 있지만 반드시 사용해야되는 경우 ```을 양쪽에 위치시키면 됩니다.

```kotlin
fun main() {
    val in: Int = 0 // 컴파일 에러
    val `in`: Int = 0 // 정상 동작
}
```

**컴파일 에러**
`Kotlin: Expecting property name or receiver type`

- 숫자로 시작할 수 없습니다.

```kotlin
fun main() {
    var 1st: Int // 컴파일 에러
    var first1: Int // 정상 동작
}
```

## 변수 초기화

- 변수에 초기화 값을 넣지 않고 사용할 경우 다음과 같은 문제 발생

```kotlin
fun main() {
    var age: Int
    println(age) // 컴파일 에러 발생
    var score: Int
    score = 30
    println(score) // 정상 동작
}
```

**컴파일 에러**
`Kotlin: Variable 'a' must be initialized` 

## 변수타입

### Integer types (정수형)

- 정수형을 표현하는 정수타입은 총 4가지
- 사이즈에 따라 다르다 → 표현할 수 있는 숫자에 범위가 다르다.
- 주로 `Int`를 사용하거나 숫자 범위를 넘게 되면 `Long`도 같이 사용하게 된다.

| 변수타입 | 사이즈(bit) | Min Value | Max Value |
| --- | --- | --- | --- |
| Byte | 8 | -128 | 127 |
| Short | 16 | -32,768 | 32,767 |
| Int | 32 | -2,147,483,648 | 2,147,483,647 |
| Long | 64 | -9,223,372,036,854,775,808 | 9,223,372,036,854,775,807 |

```kotlin
fun main() {
        val one = 1 // Int
        val threeBillion = 3000000000 // Long
        val oneLong = 1L // Long
        val oneByte: Byte = 1
        val threeBillionUnderbar = 3_000_000_000
}
```

### **Floating-point types(실수형)**

- Float는 표현 길이가 낮아 주로 Double 사용

| 변수타입 | 사이즈(bit) |
| --- | --- |
| Float | 32 |
| Double | 64 |

### **Boolean**

**`true` or `false`**

### String

- 문자열을 담을 때 사용되는 변수 타입

```kotlin
fun main() {
val name: String = " "
}
```

- 문자열(string) 사이에 변수를 사용할 수 있습니다.

```kotlin
fun main() { 
	// 예시 1
	val name: String = " println(" ${name}
	// 예시 2
	val age: Int = 10
	val result: String = "이름은 ${name}이고 나이는 &{age} 입니다."
	println(result)
}
```

## **Null Safety**

변수 선언 시 변수 타입 바로 뒤에
