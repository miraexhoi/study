# @Component vs @Bean?

### 1. 선언 위치의 차이

- `@Component`: 클래스 레벨에 선언되며, 주로 직접 구현한 클래스에 사용된다.
- `@Bean`: 메서드 레벨에 선언되며, 외부 라이브러리에서 제공하는 객체를 스프링 빈으로 등록할 때 주로 사용된다.

예를 들어, `BCrypt`를 활용한 패스워드 암호화 모듈을 `@Component`로 등록하려면 아래와 같이 클래스 레벨에서 선언할 수 있다.

```java
@Component
public class PasswordEncoder {
    public String encode(String seed) {
        return new BCryptPasswordEncoder().encode(seed);
    }

    public boolean matches(String seed, String password) {
        return new BCryptPasswordEncoder().matches(seed, password);
    }
}
```

만약 위 코드에서 @Component 대신 @Bean을 사용하려고 시도하면,  
@Bean이 메서드에만 적용 가능하기 때문에 IDE에서 오류 표시 → @Bean의 Target은 METHOD만 지정하고 있기 때문

> 참고: 아래는 ElementType의 일부로, @Bean이 METHOD에만 사용 가능하도록 지정된 것을 보여준다.   
  @Component와 달리, 클래스에 사용되려면 TYPE으로 선언되어야 한다.

```java
public enum ElementType {
    /** Class, interface (including annotation interface), enum, or record
     * declaration */
    TYPE,

    /** Field declaration (includes enum constants) */
    FIELD,

    /** Method declaration */
    METHOD,
```

### 2. 사용법의 차이
@Component: 내부에서 직접 접근 가능한 클래스에 사용한다. 해당 클래스가 프로젝트에서 직접 구현한 클래스일 때 적합하다.

@Bean: 외부 라이브러리가 제공하는 객체를 스프링 빈으로 등록할 때 사용한다. 라이브러리에 포함된 객체는 @Component로 선언할 수 없기 때문에, 이를 빈으로 등록하려면 @Bean을 사용해야 한다.

예를 들어, 아래 코드에서는 PasswordEncoder 클래스를 직접 작성했기 때문에 @Component를 사용할 수 있다.

```java
@Component
public class PasswordEncoder {
    public String encode(String seed) {
        return new BCryptPasswordEncoder().encode(seed);
    }

    public boolean matches(String seed, String password) {
        return new BCryptPasswordEncoder().matches(seed, password);
    }
}
```

위 코드에서 Component 어노테이션을 쓸 수 있는 이유는 PasswordEncoder라는 class를 내가 직접 만들었기 때문이다.  
만약 이 코드가 라이브러리에 있는 코드라면 나는 이 클래스에 Component를 추가할 수 없다. 따라서 **라이브러에 있는 객체를 사용할 때는 Bean을 활용**해야 한다.
