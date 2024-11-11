# 코틀린 물음표(?) 느낌표(!!)는 무엇일까?

> 개요 : 코틀린 개념 공부가 덜 된 상태로 개발 하던 중 ? 또는 !! 유무로 발생하는 오류를 만나다 ..

코틀린에서는 자바보다 null 처리를 더 명확하게 한다. 따라서 NPE가 발생하는 빈도를 현저히 낮출 수 있다.

코틀린은 JAVA와 100% 호환된다. 동시에 자바의 여러 단점들을 보완하고자 하는데, 자바에서는 null을 허용하지 않는다는 것이다.  
프로그램에서 유저가 입력시 유저가 입력하지 하지 않는경우가 존재하는데, 코틀린은 이러한점에 대해서 null을 유연하게 대처하게 해주고 있다.

```kotlin
// '?' 간단 사용
val myString : String = null //error
val myString : String? = null //not error


// '!' 간단 사용
myObject.name
myObject!!.name
```

### "?" 사용법

먼저, type에 ?를 붙임으로서 **null이 가능한 변수임을 명시적으로 표현**한다.

![image](https://github.com/user-attachments/assets/46fadcdf-a399-44a0-9073-95b5e2f4ded5)

아래와 같이 myString과 myString2에 null 값을 입력해 주었을때 첫번째 줄에는 빨간줄이 뜨면서 오류를 보여주는데, 이는 간단하다.  
기본적으로 변수에는 null 값이 들어갈수 없기때문에 null 을 허용한다는 의미의 `?` 을 선언시 붙여주면 된다.  


### "!!" 사용법

**!! 자체의 의미는 해당 값이 null 값이 아니라는 것을 확신시켜 주는 역할**을 한다.

![image](https://github.com/user-attachments/assets/3365f321-4113-4f00-8a62-6ea4d771f951)

주석에 달린 설명대로 !!을 통해 null이 아님을 보증해줬기 때문에 에러가 나지 않는다.

### Platform Type

코틀린에서는 null이 될수 있음과 없음을 변수에서 선언하여 사용함으로써 NPE 발생 확률을 늦춘다.
다만 자바와 연동에 있어 자바는 이러한 제한없이 쓰기 때문에 문제가 된다.

- **자바의 @Nullable String == 코틀린의 String?**
- **자바의 @NonNull String == 코틀린의 String**

자바의 annotation에 따라 코틀린의 null type이 정해 집니다.(어노테이션은 표준, 안드로이드, 젯브레인 모두를 지원)  
문제는 자바에서 해당 어노테이션 없이 쓰는 변수나 인자들이 대부분이라는 점 → 이런 불분명한 타입은 코틀린에서 플랫폼 타입으로 변환된다.
