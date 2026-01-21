# 코틀린 람다식 (Lambda)

### **람다식이란?**

코틀린에서 함수를 값처럼 다룰 수 있는 익명함수(*함수처럼 동작하는 이름이 없는 함수)*

개발을 하다 보면 이벤트에 대한 핸들러를 등록하거나, 리스트의 모든 원소에 동일한 연산을 적용하기 위해  
동작을 함수에 전달하거나 변수에 저장하는 과정이 요구되는데, 이럴 때 람다를 사용 

→ **결론: 람다를 사용하면 코드 블록을 함수의 인자로 전달하거나 변수에 저장하는 일을 쉽고 간결하게 할 수 있다.**

### **람다식의 기본 구조**

람다식은 val lamdaName : Type = { argumentList -> codeBody } 구조이며 항상 마지막 코드가 리턴값이다.

```
val lambdaName : ArgumentType -> ReturnType = {
  argumentList -> // 코드 본문
}
```


정수를 입력받아 제곱을 반환하는 람다식 함수 예:

아래 코드는 input Int를 output Int로 return한다. (Int) -> (Int)이기 때문에 namber가 Int라는 타입추론이 가능.  
(Int) -> (Int)를 생략하고 number에 타입을 지정하여 선언해줄 수도 있다.

```
val square : (Int) -> (Int) = {number -> number * number}

fun main() {
  println(square(12))
}

// output: 144
```

```
val square : {number: Int -> number * number}

fun main() {
  println(square(12))
}

// output: 144
```

### **람다식의 기본 구조**

**1. 함수의 인자로 전달하기**

람다식은 함수의 인자로 전달될 수 있다.

maxBy는 두 정수를 입력받아 최댓값을 찾는 함수이며 (Int, Int) -> Int 형태의 람다식

```
fun maxBy(operation: (a: Int, b: Int) -> Int): Int {
  val result = operation(6,3)
  return result
}

fun main() {
  val maxResult = maxBy {
    if (a > b) {
      a
    } else {
      b    
    }
  }
  println("최댓값: ${maxResult}")
}

// output: 최댓값: 6
```

**2. 리턴값으로 사용하기**

람다식은 함수의 리턴값으로 활용할 수도 있다.

nameAge 변수에 이름과 나이를 입력받아 문자열을 반환하는 함수를 람다식으로 정의:

```
val nameAge = {name: String, age: Int -> "My name is ${name}, I'm ${age}"}

fun main() {
  println(nameAge("Dobby", 12))
}
```

다른 예시로 성적 등급을 반환하는 람다식 함수:

람다식은 항상 마지막 표현식이 리턴값을 의미하며 리턴의 value 타입을 지정한다.

calculateGrade 함수는 input이 Int이고 output이 String이다. 
정수를 입력하면 문자열로 리턴하는데, 만약 it이 120이라면?

**when문에서는** 120에 해당하는 메시지가 없기 때문에 **반드시 else를 함께 정의해준다.**

Int는 여러 개가 있을 수 있으니 항상 소괄호 안에 작성해준다.

```
val calculateGrade : (Int) -> String = {
  when(it) {
    in 0..40 -> "fail"
    in 41..70 -> "pass"
    in 71..100 -> "perfect"
    else -> "error"
  }
}

fun main() {
  println(calculateGrade(94))
}

// output: perfect
```

**3. 확장 함수(Extension Function)**

확장 함수를 사용하여 기존 클래스에 새로운 기능을 추가할 수 있다.  
this는 해당 클래스의 인스턴스로 확장 함수가 호출된 문자열을 가리킨다.

```
val pizzaGreat : String.() -> String = {
  this + "Pizza is yummy!"
}

fun main() {
  val a = "Pepperoni "
  val b = "Hawaiian "
  println(a.pizzaIsGreat())
  println(b.pizzaIsGreat())
}

// output: Pepperoni Pizza is yummy!
//         Hawaiian Pizza is yummy!
```

this 위치에 따라 새로운 기능이 추가된다.

```
val pizzaIsGreat : String.() -> String = {
  "Pizza is yummy!" + this
}

fun main() {
  val c = "How about you?"
  println(c.pizzaIsGreat())
}

// output: Pizza is yummy! How about you?
```

### **람다의 표현 방식** 

**람다 리터럴 (Lambda Literal)**

람다 리터럴은 중괄호로 output을 내는 방법이다.   
중괄호 안에 파라미터와 해당하는 코드를 정의하는 형태로 사용

 

Double로 받아 Boolean을 리턴하는 람다식을 파라미터로 받는 코드 예:  
람다에 5.4321을 넣어 리턴되는 Boolean값을 invokeLamda 함수에 담았다.

**Double: 실수를 나타내는 타입*

```
fun invokeLambda(lambda: (Double) -> Boolean) : Boolean {
  return lambda(5.4321)
}

fun main() {
  val lambda = {
    number == 4.321
  }
  println(invokeLambda(lambda))
  println(invokeLambda{it > 5.4}) // println(invokeLambda({it > 5.4})) 에서 소괄호 생략
}
```

람다 리터럴을 활용하여 함수를 직관적으로 표현하여 output을 가독성있게 리턴 가능
