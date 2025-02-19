# 트랜잭셔널 아웃박스 패턴(Transactional Outbox Pattern)

분산 시스템에서 단일 작업에 데이터베이스 쓰기 작업과 메시지 혹은 이벤트 발행이 모두 포함된 경우 발생하는  
이중 쓰기 문제를 해결하기 위해서 사용할 수 있다. 예를 들어, 다음과 같은 코드가 존재한다고 가정하면,

```java
@Transactional
public void propagateSample() {
   Product product = new Product("신규 상품");
   productRepository.save(product);
   eventPublisher.propagate(new NewProductEvent(product.getId()));
}
```

위와 같이 신규 상품을 생성하고, 아래는 이벤트를 발행하는 코드를 트랜잭션 AOP 로직이 적용된 간단한 의사코드로 작성한 코드이다.

```java
public void doInTransaction() {
   try {
     transaction.begin();
     Product product = new Product("신규 상품");
     productRepository.save(product);
     eventPublisher.propagate(new NewProductEvent(product.getId()));
     transaction.commit();
   } catch(Exception e) {
     transaction.rollback();
   }
}
```

위와 같은 코드에서 트랜잭션은 커밋됐지만 이벤트 발행은 실패할 수 있으며, 반대로 이벤트 발행은 성공했지만 커밋 연산이 모종의 이유로 실패하여  
트랜잭션은 롤백 될 수 있다. 이러한 이중 쓰기로 인해 발생하는 문제는 전체 서비스의 데이터 정합성에 문제를 만들거나 서비스 장애로 이어진다.  
그렇기 때문에 서비스 로직의 실행과 이벤트 발행을 원자적으로 함께 수행하는 것을 **트랜잭셔널 메시징(Transactional Messaing)** 을 사용한다.  

```java
@Transactional
public void propagateSample() {
   Product product = new Product("신규 상품");
   productRepository.save(product);
   productOutboxRepository.save(new ProductEvent(product.getId()));
}
```

Product 발행 이벤트를 저장하기 위한 Outbox 테이블을 만들고, 같은 트랜잭션 내부에서 이벤트를 저장한다. 원자성을 보장해 주는 데이터베이스  
트랜잭션을 사용하기 때문에 이벤트와 신규 상품은 **모두 저장되거나 모두 실패한다**. 별도의 프로세스가 Outbox 테이블에 저장된 레코드들을  
주기적으로 폴링하여 외부 시스템에 성공할 때까지 이벤트를 발행하는 것이 **T.O.P 의 기본적인 구현 방식**이다.
