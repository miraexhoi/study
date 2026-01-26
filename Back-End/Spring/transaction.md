# Spring Transaction 

### @Transactional 이란?

`@Transactional` 은 트랜잭션을 “여는 애노테이션” 이라기 보다는 **트랜잭션 Advice를 적용하기 위한 메타 정보**다.

먼저, Bean 생성 이후 해당 메서드(또는 클래스)가 트랜잭션 대상인지 판단하고, 대상이면 프록시를 생성한다.  
메서드 호출 시 프록시가 트랜잭션 로직을 먼저 수행하기에 즉, 실제 트랜잭션 로직은 **프록시 안에서 실행**된다.  

### 트랜잭션이 필요한 이유

트랜잭션의 목적은 간단하다.

> **여러 작업을 하나의 논리적 단위로 묶고, 전부 성공하거나 전부 실패하게 만드는 것**

예를 들어 결제 처리 로직에서
- 결제 정보 저장
- 주문 상태 변경
- 포인트 차감

이 중 하나라도 실패하면, 나머지 모두 되돌려야 하는데 이 “되돌릴 수 있음”을 보장하기 위한 장치가 트랜잭션이다.

### 트랜잭션 흐름

1. `@Transactional`이 붙은 메서드를 호출
2. 프록시가 메서드 호출을 가로챔
3. `PlatformTransactionManager`를 통해 트랜잭션 시작
4. 실제 Target 메서드 실행
5. 결과에 따라
   - 정상 종료 → commit
   - 예외 발생 → rollback

코드로 표현하면 개념적으로 아래와 같다.

```java
try {
    beginTransaction();
    target.method();
    commit();
} catch (RuntimeException e) {
    rollback();
    throw e;
}
```

이 구조를 이해하면, 이후의 모든 트랜잭션 규칙이 자연스럽게 설명된다.

### 트랜잭션 선언 지점

Spring 애플리케이션에서 트랜잭션은 보통 **Service 계층**에 선언한다.
- Controller: 요청/응답 처리 → x
- Repository: 단일 DB 접근 → x
- Service: 비즈니스 유스케이스 단위 → o

이유는 트랜잭션이 **여러 Repository 호출을 하나로 묶는 경계**이기 때문이다.

즉, 트랜잭션의 단위는 “메서드”가 아니라 **비즈니스 행위 하나**라고 보는 것이 맞다.

### 클래스 레벨 vs 메서드 레벨 `@Transactional`

`@Transactional`은 클래스와 메서드 모두에 선언할 수 있다.

```java
@Transactional(readOnly = true)
class UserService {

    @Transactional
    public void saveUser() {
        ...
    }
}
```

- 클래스 레벨: 기본 정책
- 메서드 레벨: 클래스 설정을 **덮어씀**

보통 실무에서는:

클래스 전체를 `readOnly = true`로 두고.

저장/수정 메서드만 별도로 트랜잭션을 여는 패턴이 자주 사용된다.

### rollback 기준

Spring 트랜잭션의 기본 규칙은 명확하다.
- **RuntimeException, Error** → rollback
- **Checked Exception** → commit

즉, 예외가 발생했다고 해서 무조건 롤백되지 않는다.

또한 아래와 같은 코드에서는 롤백이 발생하지 않는다.

```java
try {
    ...
} catch (Exception e) {
    // 예외를 잡아먹고 끝내면
}
```

예외를 처리해버리면 Spring 입장에서는
“정상 종료된 메서드”로 인식한다.

### 트랜잭션이 적용되지 않는 대표적인 경우

Spring 트랜잭션은 AOP 기반이기 때문에, AOP의 한계를 그대로 가지기 때문에,

아래와 같은  경우 `@Transactional`이 있어도 트랜잭션은 시작되지 않는다.
1. 같은 클래스 내부 메서드 호출 (self-invocation)
2. `private` 메서드
3. 프록시를 거치지 않는 직접 호출

### JPA와 트랜잭션: Dirty Checking

JPA에서 트랜잭션은 특히 중요하다.

JPA는 엔티티를 **1차 캐시(EntityManager)** 에서 관리하며,  
트랜잭션이 종료되는 시점에 변경 여부를 감지해 SQL을 생성한다.

이를 **Dirty Checking(변경 감지)** 이라고 한다.

> 즉, 트랜잭션이 없으면 JPA의 변경 감지는 의미를 잃게된다.
