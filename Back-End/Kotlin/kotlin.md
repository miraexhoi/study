# Kotlin
### 코틀린을 배워야 하는 이유
- 간결하고 안전한 언어
- 여러 플랫폼에서 사용 (다양한 개발 가능)
- 자바와 100% 호환 가능

### 간결성

- 자바의 경우 getter, setter 명시적인 위임과 같이 불필요한데 반드시 써야하는 준비 코드가 존재합니다.  
  그러나 코틀린은 코드를 간결하게 줄여줍니다.

### 안정성

- 강력한 타입추론
- Null 안정성

### 코틀린으로 할 수 있는 것

- 안드로이드 앱 개발
- 서버 개발
- 멀티플랫폼 개발

### C 프로그램

- 윈도우에서 컴파일한 실행 파일을 다른 운영체제에서 실행할 수 없습니다.

### JVM

Java Virtual Machine의 약자로 직역하면 자바를 실행하기 위한 가상 기계

### JVM 프로그램

- JVM이 설치된 모든 OS에서 `*.class` 파일 실행이 가능합니다.

### 프로그램 실행

```kotlin
def main() {
	println("Hello World")
}
```

### Kotlin 의 문제점
### JPA와 궁합이 좋지 않음

JPA 는 JAVA 를 기준으로 나온 ORM 표준이다. 하지만 Kotlin 은 개발 철학이 Java, JPA 와 맞지 않는 경우가 존재한다.  
Kotlin과 JPA 를 키워드로 검색해 보면 다양한 이슈와 해결 방안을 소개하는 글을 찾을 수 있다.

### 번거로운 Private Setter 설정

Kotlin으로 Entity를 선언하는 경우에는 property의 setter를 노출하지 않기 위해 val 키워드를 사용한다.  
 
하지만 해당 프로퍼티는 클래스 내부에서도 수정이 불가능하고, JPA의 변경 감지 기능도 사용할 수 없다.  
이를 해결하기 위해 var 키워드를 사용하고, setter를 protected로 선언하는 방법을 사용할 수 있다.  

하지만 이렇게 작성하게 되면 생성자와 클래스 내부, 두 번의 Property 선언과 Property마다 protected set 문구가 필요하다.  
보통 Java를 Kotlin으로 바꿀 때 이전보다 더 간결해지는 경우가 많은데, 이 경우는 오히려 행사 코드가 늘어아게 된다.  

### 복잡한 QueryDSL 설정
QueryDSL은 Java와 Kotlin을 모두 지원하지만, Kotlin을 사용하는 경우 gradle 설정이 복잡해진다.    

Kotlin으로 QueryDSL을 사용하는 경우 kapt 플러그인을 사용해야 하는데,  
kapt 플러그인은 Java의 annotationProcessor와 같은 역할을 한다.    
이 플러그인의 공식 문서를 보면 현재 관리모드로 더 이상 추가기능을 지원하지 않는다고 나와 있다.    

Github 이슈에 관련 내용이 올라와 있는데, 1년 이상 지난 이슈이지만 아직 해결되지 않은 상태이다.  
