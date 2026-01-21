# 코틀린 Null 안정성(Null Safety) **이란?**

코틀린은 기본적으로 `Null`이 변수에 담길 수 없게 제한하고 있을 정도로 `Null`에 대해 심각하게 다룬다. 

Java를 기반으로 둔 코틀린은 Java에서 문제로 여겨졌던NPE(NullPointerException) 를 대응하고 나온 언어  
(**즉, 코틀린은 기본적으로 값이 null 아니고 NotNull**) 
→ 개발자는 더욱 안전하고 신뢰성 있는 코드를 작성할 수 있다. 

### **코틀린에 Null Safety가 있는 이유?**

: 주로 자바와 같은 언어에서 흔히 발생하는 Null Pointer Exception(NPE) 문제를 해결하기 위함.  
이런 예외는 종종 애플리케이션의 충돌을 초래하며, 디버깅이 까다로움 (런타임시에 null의 가능성)

### **Kotlin Null 처리 방법**

### **1. Nullable과 Non-nullable 타입**

```kotlin
var nonNullable: String = "Hello, Kotlin!"  // Non-nullable (null을 허용하지 않음)
var nullable: String? = null               // Nullable (null을 허용)
```

### **2. Safe Call Operator (?.)**

?. 연산자를 사용하여 null 가능성이 있는 객체의 메소드나 속성에 안전하게 접근할 수 있다.  
객체가 null이 아니면 메소드나 속성에 접근하고, null이면 연산 전체가 null을 리턴한다. 

```kotlin
var nullable: String? = null 

val length: Int? = nullable?.length  // nullable이 null이면 length는 null
```

### **3. Elvis Operator (?:)**

Elvis 연산자 ?:는 왼쪽 피연산자가 null이 아니면 그 값을, null이면 오른쪽 값을 리턴한다.  
이를 통해 null 처리를 간결하게 할 수 있다.

```kotlin
var nullable: String? = null 

// nullable이 null이면 safeLength는 0
val safeLength: Int = if(nullable != null) nullable.length else 0		// if-else
val safeLength: Int = nullable?.length ?: 0  							// Elvis
```

### **4. Not-null Assertion Operator (!!)**

!! 연산자는 강제로 non-null 값을 요구할 때 사용한다. 개발자 판단 아래 null이 아님을 확신하는 것.  
만약 변수가 null이면, 이 연산자를 사용했을 때 NPE 가 발생 (런타임)  
\* 정말 필요한 경우가 아니라면 잘 쓰지 않는 것이 좋음 (NPE를 코틀린이 아닌 우리가 다루겠다면 사용할 것..)

```kotlin
var nullable: String? = null  

val unsafeLength: Int = nullable!!.length  // nullable이 null이면 예외 발생
```

### **5. Safe Casts (as?)**

as? 연산자는 타입 캐스팅을 시도하되, 캐스팅이 불가능하면 null을 리턴한다.  
타입 캐스팅 시 예외 발생을 방지할 수 있다.

```kotlin
var nullable: String? = null       

val aNumber: Int? = nullable as? Int  // 캐스팅 실패 시 aNumber는 null
```

### ++ Safe call 사칙연산

```kotlin
println(cats?  + 1) // 온갖 에러
```

`Nullable`한 변수로 연산을 할때는 `.plus()`, `.minus()`, `.rem()`와 같은 메소드들을 사용해야 한다.

```kotlin
println(cats?.plus(1)) // 2
println(cats?.times(8)) // 8
```
