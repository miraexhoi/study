# Java의 Record와 Kotlin의 Data Class

### Data Class란?
Kotlin의 Data Class는 데이터 저장 목적으로 만든 클래스를 위한 문법이다.

- 기본 구조
```kotlin
data class User(
  val name: String,
  val age: Int
)
```

### Record란?
자바 14부터 코틀린의 Data 클래스와 유사한 Record라는 클래스가 추가되어 자바 16에서 정식으로 지원되기 시작.  
기존 자바에서 DTO 등의 클래스를 만들 때는 Lombok의 도움을 받아 `@Data` 어노테이션을 붙이는 필요성이 줄어들게 되었다.

- 기본 구조
```java
public record Member(
        String account,
        String name,
        int age
) {
    ...
}

```

### 그래서 뭐가 다른건데?
#### 1. Record엔 copy() 메소드가 없지만, Data class엔 존재한다.
  - 원칙적으로 모든 것이 final인 Record의 특성상 copy()를 굳이 지원하지 않는다.
#### 2. Record는 모든 프로퍼티가 final인 반면, Data class의 변수들은 var 또는 val로 사용할 수 있다.
#### 3. Record는 static 변수만 정의할 수 있지만, Data class엔 생성자가 아닌 가변 변수를 정의할 수 있다.
#### 4. Record는 상속이 불가능 하지만, Data class는 Data class가 아닌 클래스로부터 상속받을 수 있다.
  - 다만, 다른 클래스를 상속받은 Data class의 경우 권장되는 방식은 아니다.
