# Kotlin - Beginner tour contents

#### [Variables](https://.org/docs/kotlin-tour-hello-world.html)
    
### 변수
    
- 읽기 전용 변수 `val`  → 지정 후 변경 불가
- 변경 가능한 변수 `var`

### 문자열 템플릿

변수의 내용을 표준 출력으로 출력하는 방법

방법: 달러 기호($) 뒤에 중괄호({}) 안에 코드 삽입

```kotlin
val customers = 10
println("There are $customers customers")
// There are 10 customers

println("There are ${customers + 1} customers")
// There are 11 customers
```
    
#### [Basic types](https://kotlinlang.org/docs/kotlin-tour-basic-types.html)
    

| **Category** | **Basic types** | **Example code** |
| --- | --- | --- |
| Integers | `Byte`, `Short`, `Int`, `Long` | `val year: Int = 2020` |
| Unsigned integers 
(부호 없는 정수) | `UByte`, `UShort`, `UInt`, `ULong` | `val score: UInt = 100u` |
| Floating-point numbers
(부동 소수점 숫자) | `Float`, `Double` | `val currentTemp: Float = 24.5f`, `val price: Double = 19.99` |
| Booleans | `Boolean` | `val isEnabled: Boolean = true` |
| Characters | `Char` | `val separator: Char = ','` |
| Strings | `String` | `val message: String = "Hello, world!"` |

```kotlin
// Variable declared without initialization
val d: Int
// Variable initialized
d = 3

// Variable explicitly typed and initialized
val e: String = "hello"

// Variables can be read because they have been initialized
println(d) // 3
println(e) // hello
```

```kotlin
// Variable declared without initialization
val d: Int

// Triggers an error
println(d)
// Variable 'd' must be initialized
```
    
#### [Collections](https://kotlinlang.org/docs/kotlin-tour-collections.html)
    

| **Collection type** | **Description** |
| --- | --- |
| Lists | **Ordered collections** of items |
| Sets | **Unique unordered collections** of items |
| Maps | Sets of **key-value pairs** where keys are unique and map to only one value |

### List

리스트는 항목이 추가된 순서대로 저장하며, 중복 항목을 허용

- 읽기 전용 목록을 만들려면 ( `List` ) `listOf()` 함수 사용
	
	```kotlin
	// 읽기 전용 목록
	val readOnlyShapes = listOf("triangle", "square", "circle")
	println(readOnlyShapes)
	// 결과: [triangle, square, circle]
	```
	
- 변경 가능한 리스트( `MutableList`) 를 생성하려면 `mutableListOf()` 함수 사용
	
	```kotlin
	// 명시적 타입 선언이 있는 가변 리스트
	val shapes: MutableList<String> = mutableListOf("triangle", "square", "circle")
	println(shapes)
	// 결과: [triangle, square, circle]
	```
	
- \* **캐스팅 (casting)**
	
	원치 않는 수정을 방지하려면 변경 가능한 목록을 읽기 전용 뷰로 만들어 할당 가능
	
	```kotlin
	val shapes: MutableList<String> = mutableListOf("triangle", "square", "circle")
	val shapesLocked: List<String> = shapes
	```
	
- 리스트는 순서대로 정렬되어 있으므로 리스트의 항목에 접근하려면 인덱스 접근 연산자 `[]` 를 사용
	
	```kotlin
	val readOnlyShapes = listOf("triangle", "square", "circle")
	println("The first item in the list is: ${readOnlyShapes[0]}")
	// The first item in the list is: triangle
	```
	
- 리스트의 첫 번째 항목이나 마지막 항목을 가져오려면 각각  `.first()` 및 `.last()` 함수를 사용
	
	```kotlin
	val readOnlyShapes = listOf("triangle", "square", "circle")
	println("The first item in the list is: ${readOnlyShapes.first()}")
	// The first item in the list is: triangle
	```
	
  `.first()` 와 `.last()` 는 확장 함수 → 객체 이름 뒤에 함수 이름을 쓰고 마침표(.)를 찍음
	
- 리스트에 있는 항목 수를 얻으려면  `.count()` 함수를 사용
	
	```kotlin
	val readOnlyShapes = listOf("triangle", "square", "circle")
	println("This list has ${readOnlyShapes.count()} items")
	// This list has 3 items
	```
	
- 변경 가능한 목록에서 항목을 추가하거나 제거하려면 각각 `.add()` 및 `.remove()` 함수 사용
	
	```kotlin
	// Add "pentagon" to the list
	shapes.add("pentagon") 
	println(shapes)  
	// [triangle, square, circle, pentagon]
	
	// Remove the first "pentagon" from the list
	shapes.remove("pentagon") 
	println(shapes)  
	// [triangle, square, circle]
	```
	

### Set

리스트는 순서가 있고 중복 항목을 허용하는 반면, 세트는 **순서가 없고 고유한** 항목 만 저장

- 읽기 전용 세트( `Set` )를 생성하려면 `setOf()` 함수를 사용
- 변경 가능한 집합( `MutableSet` ) 을 생성하려면 `mutableSetOf()` 함수를 사용
	
	```kotlin
	// Read-only set
	val readOnlyFruit = setOf("apple", "banana", "cherry", "cherry")
	// Mutable set with explicit type declaration
	val fruit: MutableSet<String> = mutableSetOf("apple", "banana", "cherry", "cherry")
	
	println(readOnlyFruit)
	// [apple, banana, cherry] <- 집합에는 고유한 요소만 포함되므로 중복 "cherry" 항목 제거
	```
	
- 원치 않는 수정을 방지하려면 변경 가능한 집합(`Set`)을 읽기 전용 뷰로 만들어 할당
- 집합은 **순서가 없으므로** 특정 인덱스의 항목에 접근 불가!
- 집합에 있는 항목의 개수를 구하려면 `.count()` 함수를 사용
	
	```kotlin
	println("This set has ${readOnlyFruit.count()} items")
	// This set has 3 items
	```
	
- 어떤 항목이 집합에 속하는지 확인하려면 `in` 연산자 사용
	
	```kotlin
	println("banana" in readOnlyFruit)
	// true
	```
	
- 변경 가능한 집합에서 항목을 추가하거나 제거하려면 각각 `.add()` 및 `.remove()` 함수를 사용
	
	```kotlin
	
	fruit.add("dragonfruit")    // Add "dragonfruit" to the set
	println(fruit)              // [apple, banana, cherry, dragonfruit]
	
	fruit.remove("dragonfruit") // Remove "dragonfruit" from the set
	println(fruit)              // [apple, banana, cherry]
	```
	

### Map

맵은 항목을 키-값 쌍으로 저장. 키를 참조하여 값에 접근.

맵은 리스트처럼 번호가 매겨진 인덱스를 사용하지 않고 값을 찾고 싶을 때 유용

Kotlin이 어떤 값을 가져오려는지 이해할 수 있도록 맵의 모든 키는 고유 & 중복된 값 존재 가능

- 읽기 전용 맵( `Map` ) 을 생성하려면 `mapOf()` 함수를 사용
	
	```kotlin
	// Read-only map
	val readOnlyJuiceMenu = mapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
	println(readOnlyJuiceMenu)
	// result: {apple=100, kiwi=190, orange=100}
	```
	
- 변경 가능한 맵( `MutableMap` ) 을 생성하려면 `mutableMapOf()` 함수를 사용
	
	```kotlin
	// Mutable map with explicit type declaration
	val juiceMenu: MutableMap<String, Int> = mutableMapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
	println(juiceMenu)
	// result: {apple=100, kiwi=190, orange=100}
	```
	

Kotlin은 맵을 생성할 때 저장된 항목의 유형을 추론 가능

유형을 명시적으로 선언하려면 `<>`맵 선언 후 꺾쇠괄호 안에 키와 값의 유형 추가 

(예: `MutableMap<String, Int>` → 키는 `String` 유형이고 값은 `Int` 유형)

맵을 만드는 가장 쉬운 방법은 `to` 각 키와 그에 해당하는 값 사이에 키워드를 사용하는 것

+ 원치 않는 수정을 방지하려면 변경 가능한 맵을 읽기 전용 뷰로 만들어 할당 가능

- 맵의 값에 접근하려면 해당 키와 함께 인덱스 접근 연산자를 사용. `[]`
	
	```kotlin
	// Read-only map
	val readOnlyJuiceMenu = mapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
	println("The value of apple juice is: ${readOnlyJuiceMenu["apple"]}")
	// The value of apple juice is: 100
	```
	
	참고: 맵에 존재하지 않는 키를 사용하여 키-값 쌍에 접근하려고 하면 `null`값이 표시
	
- 인덱스 접근 연산자를 `[]` 사용하여 변경 가능한 맵에 항목을 추가 가능
	
	```kotlin
	val juiceMenu: MutableMap<String, Int> = mutableMapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
	juiceMenu["coconut"] = 150 // Add key "coconut" with value 150 to the map
	println(juiceMenu)
	// {apple=100, kiwi=190, orange=100, coconut=150}
	```
	
- 변경 가능한 맵에서 항목을 제거하려면 다음 `.remove()` 함수를 사용
	
	```kotlin
	val juiceMenu: MutableMap<String, Int> = mutableMapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
	juiceMenu.remove("orange")    // Remove key "orange" from the map
	println(juiceMenu)
	// {apple=100, kiwi=190}
	```
	
- 지도에 있는 항목의 개수를 얻으려면 다음 `.count()` 함수를 사용
	
	```kotlin
	// Read-only map
	val readOnlyJuiceMenu = mapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
	println("This map has ${readOnlyJuiceMenu.count()} key-value pairs")
	// This map has 3 key-value pairs
	```
	
- 특정 키가 맵에 이미 포함되어 있는지 확인하려면 다음 `.containsKey()` 함수를 사용
	
	```kotlin
	val readOnlyJuiceMenu = mapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
	println(readOnlyJuiceMenu.containsKey("kiwi"))
	// true
	```
	
- 맵의 키 또는 값 컬렉션을 얻으려면 각각 `keys` 및 `values` 속성을 사용
	
	```kotlin
	val readOnlyJuiceMenu = mapOf("apple" to 100, "kiwi" to 190, "orange" to 100)
	println(readOnlyJuiceMenu.keys)
	// [apple, kiwi, orange]
	println(readOnlyJuiceMenu.values)
	// [100, 190, 100]
	```
	
- 맵에 키 또는 값이 있는지 확인하려면 `in` 연산자를 사용
	
	```kotlin
	
	println("orange" in readOnlyJuiceMenu.keys)
	// true
	
	// Alternatively, you don't need to use the keys property
	println("orange" in readOnlyJuiceMenu)
	// true
	
	println(200 in readOnlyJuiceMenu.values)
	// false
	```
        

#### [Control flow](https://kotlinlang.org/docs/kotlin-tour-control-flow.html)
    
코틀린은 코드 조각이 참으로 평가되는지 여부에 따라 결정 → **조건식**

또한 코틀린은 반복문을 생성하고 실행 가능

### **조건식**

Kotlin은 조건식을 검사하는 기능 `if` 와 `when` 을 제공 합니다.

`if`둘 중 하나를 선택해야 한다면 `when`, 다음과 같은 이유로 `when` 사용 권장

→ 코드를 더 읽기 쉽게 / 새로운 브랜치를 더 쉽게 추가 /코드 오류 저하

### **If**

사용하려면 `if` 조건식을 괄호`()` 안에 넣고, 결과가 참일 경우 수행할 동작을 중괄호 안에 삽입﻿

```kotlin
val d: Int
val check = true

if (check) {
	d = 1
} else {
	d = 2
}

println(d)
// 1
```

코틀린에는 삼항 연산자 x `condition ? then : else` 대신 `if`표현식으로 사용 가능

(동작당 코드가 한 줄뿐인 경우 중괄호는 `{}`생략 가능)

```kotlin
val a = 1
val b = 2

println(if (a > b) a else b) // Returns a value: 2
```

### When

조건식에 여러 분기가 있을 때 `when` 사용 (+ 특정 **값이나 타입에 대한 다중 분기**를 간결하게 처리)

사용 방법:

1. 평가하고자 하는 값을 괄호 `()` 안에 삽입
2. 가지들을 중괄호`{}` 안에 삽입
3. 각 분기에서 사용하여 `>`각 검사와 검사 성공 시 수행할 동작 구분
- `when`은 문(statement) 또는 표현식(expression)으로 사용 가능.
	
	**문은** 아무것도 반환하지 않지만 동작을 수행
	
	```kotlin
	val obj = "Hello"
	
	when (obj) {
		// Checks whether obj equals to "1"
		"1" -> println("One")
		// Checks whether obj equals to "Hello"
		"Hello" -> println("Greeting")
		// Default statement
		else -> println("Unknown")     
	}
	// Greeting
	```
	
	모든 분기 조건은 조건 중 하나가 충족될 때까지 순차적으로 검사 → 조건을 만족하는 첫 번째 분기만 실행
	
- 다음은 `when` 을 표현식으로 사용하는 예.
	
	→  `when`표현식은 즉시 변수에 할당되고, 이 변수는 나중에 `println()`함수와 함께 사용
	
	```kotlin
	val obj = "Hello"    
	
	val result = when (obj) {
		// If obj equals "1", sets result to "one"
		"1" -> "One"
		// If obj equals "Hello", sets result to "Greeting"
		"Hello" -> "Greeting"
		// Sets result to "Unknown" if no previous condition is satisfied
		else -> "Unknown"
	}
	println(result)
	// Greeting
	```
	
- 지금까지 `when` 예시들은 모두 `obj` 주어가 있었지만, 주어 없이도 사용 가능
	
	이 예제는 주어가 **없는**`when` 표현식을 사용하여 일련의 부울 표현식을 확인
	
	```kotlin
	fun main() {
		val trafficLightState = "Red" // This can be "Green", "Yellow", or "Red"
	
		val trafficAction = when {
			trafficLightState == "Green" -> "Go"
			trafficLightState == "Yellow" -> "Slow down"
			trafficLightState == "Red" -> "Stop"
			else -> "Malfunction"
		}
	
		println(trafficAction)
		// Stop
	}
	```
	
	+ 하지만, `trafficLightState` 제목을 다르게 하여 동일한 코드 사용 가능
	
	```kotlin
	fun main() {
		val trafficLightState = "Red" // This can be "Green", "Yellow", or "Red"
	
		val trafficAction = when (trafficLightState) {
			"Green" -> "Go"
			"Yellow" -> "Slow down"
			"Red" -> "Stop"
			else -> "Malfunction"
		}
	
		println(trafficAction)  
		// Stop
	}
	```
	

### Ranges

Kotlin에서 범위를 생성하는 가장 일반적인 방법은 `..` 연산자를 사용하는 것.

- `1..4` == `1, 2, 3, 4`
- 끝값을 포함하지 않는 범위를 선언하려면 `..<`연산자를 사용 → `1..<4` == `1, 2, 3`
- 범위를 역순으로 선언하려면  `downTo` 를 사용 →  `4 downTo 1` == `4, 3, 2, 1`
- 1이 아닌 간격으로 증가하는 범위를 지정하려면 `step` 과 원하는 증가 값을 사용.
→ `1..5 step 2` ==  `1, 3, 5`

`Char` 범위 에 대해서도 같은 작업을 수행 가능

- `'a'..'d'` == `'a', 'b', 'c', 'd'`
- `'z' downTo 's' step 2` == `'z', 'x', 'v', 't'`

### Loops

프로그래밍에서 가장 흔하게 사용되는 반복문 구조는  `for` 과 `while`

 `for` 은 특정 범위의 값을 순회하며 작업을 수행,  `while` 특정 조건이 충족될 때까지 작업을 계속

### For

반복자와 범위를 괄호`()` 안에 넣고 `in` 키워드를 지정.중괄호`{}` 안에 수행할 작업을 추가.

```kotlin
for (number in 1..5) { 
	// number is the iterator and 1..5 is the range
	print(number)
}
// 12345
```

컬렉션은 반복문을 사용하여 순회 가능

```kotlin
val cakes = listOf("carrot", "cheese", "chocolate")

for (cake in cakes) {
	println("Yummy, it's a $cake cake!")
}
// Yummy, it's a carrot cake!
// Yummy, it's a cheese cake!
// Yummy, it's a chocolate cake!
```

### While

`while` 은 두 가지 방식으로 사용 가능

- 조건식이 참일 때 코드 블록을 실행 ( `while`)
- 먼저 코드 블록을 실행한 다음 조건식을 확인 ( `do-while`)

첫 번째 사용 사례( `while`):

- while 루프가 계속 실행될 조건식을 괄호`()` 안에 선언
- 중괄호`{}` 안에 수행할 작업을 입력

```kotlin
var cakesEaten = 0
while (cakesEaten < 3) {
	println("Eat a cake")
	cakesEaten++
}
// Eat a cake
// Eat a cake
// Eat a cake
```

두 번째 사용 사례( `do-while`):

- while 루프가 계속 실행될 조건식을 괄호`()` 안에 선언
- `{}`중괄호 안에 `do` 키워드를 사용하여 수행할 동작을 정의

```kotlin
var cakesEaten = 0
var cakesBaked = 0
while (cakesEaten < 3) {
	println("Eat a cake")
	cakesEaten++
}
do {
	println("Bake a cake")
	cakesBaked++
} while (cakesBaked < cakesEaten)
// Eat a cake
// Eat a cake
// Eat a cake
// Bake a cake
// Bake a cake
// Bake a cake
```
    
#### [Functions](https://kotlinlang.org/docs/kotlin-tour-functions.html)

코드 조각이 참으로 평가되는지 여부에 따라 결정 가능  

이러한 코드 조각을 이라고 함 → 코틀린은 또한 반복문을 생성 및 실행 가능

```kotlin
fun hello() {
	return println("Hello, world!")
}

fun main() {
	hello()
	// Hello, world!
}
```

Kotlin:

- 함수 매개변수는 괄호 안에 작성 `()`
- 각 매개변수는 유형을 가져야 하며, 여러 매개변수는 쉼표로 구분 `,`
- 함수의 반환 타입은 함수의 괄호 뒤에 `()`콜론으로 구분하여 작성 `:`
- 함수의 본문은 중괄호 안에 작성됩니다 `{}`
- `-out` 키워드는 `return`함수를 종료하거나 함수에서 값을 반환하는 데 사용
