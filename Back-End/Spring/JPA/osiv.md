# OSIV(Open Session In View)란?

OSIV는 **트랜잭션 종료 이후에도 영속성 컨텍스트를 View/응답 단계까지 열어 두는 패턴**이다.

- JPA 기준: `Open EntityManager In View (OEIV)`
- Hibernate 기준: `Open Session In View (OSIV)`
- EntityManager(Session)는 내부에 **영속성 컨텍스트**를 두고 엔티티 관리.

즉, **OSIV는 영속성 컨텍스트(Session)가 “응답 직전까지” 열려 있는 상태**를 의미.  
(API 서버의 경우 응답을 생성할 때까지 열려 있는 것과 동일)

요약: **“트랜잭션이 끝난 뒤에도 영속성 컨텍스트를 열어둬서, 응답 직전까지 엔티티 프록시를 로딩 가능하게 함”**

View 계층에서 지연 로딩을 편하게 처리한다는 장점이 있지만 ,,,
- 요청 전체 구간에서 DB 커넥션/영속성 컨텍스트가 붙잡힐 수 있음  
- N+1 문제가 View 단계까지 늦게 드러남  
- 트랜잭션 경계가 흐려져 설계가 느슨해질 수 있음

실무 API 서버에서는 보통 **OSIV 비활성화**를 권장한다.  
→ 응답 모델을 명확히 구성하고, 필요한 데이터는 **서비스 계층에서 확실히 로딩**하는 방식이 더 안정적

### Spring 설정 예시
- application.yml:
```yaml
spring:
  jpa:
    open-in-view: false
```
