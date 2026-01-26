## Spring AOP

Spring AOP는 기본적으로 **프록시 방식**으로 동작한다. 

***프록시 패턴이란**

어떤 객체를 사용하고자 할 때, 객체를 직접적으로 참조 하는 것이 아니라,  
해당 객체를 대행(대리, proxy)하는 객체를 통해 대상객체에 접근하는 방식을 말한다.

### Spring AOP는 왜 프록시 방식을 사용할까?

그렇다면 Spring은 왜 Target 객체를 직접 참조하지 않고 프록시 객체를 사용할까?

프록시 객체 없이 Target 객체를 사용하고 있다면 Aspect 클래스에 정의된 부가 기능을 사용하기 위해서,  
원하는 위치에 직접 Aspect 클래스를 호출해야 한다. 이 경우 Target 클래스 안에 부가 기능을 호출하 로직이 포함되기 때문에,   
AOP를 적용하지 않았을 때와 동일한 문제가 발생한다. 여러 곳에서 반복적으로 Aspect를 호출하면서 유지보수성이 저하된다.  

**Spring에서는 Target 클래스 또는 상위 인터페이스를 상속하는 프록시 클래스를 생성하고, 프록시 클래스에서 부가 기능 관련된 처리**  
→ Target에서 Aspect을 알 필요 없이 순수한 비즈니스 로직에 집중할 수 있다.

### Spring Proxy 생성 방식

Spring AOP에서 프록시는 **두 가지 방식**으로 생성된다.

**1.JDK Dynamic Proxy (인터페이스 기반)**
- Target이 인터페이스를 구현하고 있으면 기본 선택
- 단점1 ) 구현체에 직접 접근 불가
- 단점2 ) `final`, `private` 메서드에 Advice 적용 불가

- [JDK 동적 프록시 실습 코드](https://github.com/miraexhoi/jdk-dynamic-proxy)

**2.CGLIB Proxy (구현 클래스 상속 기반)**
- 인터페이스가 없거나, 클래스 기반 프록시가 필요할 때 사용
- 특징1 ) 클래스 상속 → `final` 클래스/메서드 불가
- 특징2 ) 현재 Spring에서의 **사실상 기본 전략**

### Bean이 Proxy가 되는 시점

모든 Bean이 프록시가 되는게 아니라 **Pointcut에 매칭되는 Bean만 Proxy로 감싸진다.**

`@Component` 자체는 프록시 여부와 무관 하지만, `@Transactional` 이나 `@Aspect` 등 특정 Advisor 에 매칭되면  
→ **Bean 생성 후 처리기(BeanPostProcessor)** 단계에서 Proxy로 교체한다.  

Spring 내부에서는 `ProxyFactory` 와 `Advisor (Advice + Pointcut)`를 사용해 프록시 생성한다.
