# 스프링 트랜잭션

### Transaction이란?
DBMS 또는 유사한 시스템의 상호작용 단위.  
이론적으로 DBS는 각각의 트랜잭션에 대해 ACID를 보장한다.  
하지만, 실제로는 성능향상을 위해 종종 완화하기도 한다.  
한마디로, **Transaction(트랜잭션)은 쪼갤 수 없는 여러 작업들을 논리적으로 묶은 최소 단위로 묶은 것**이다.  

### Transaction의 특징
**1. 원자성(Atomicity)**  
트랙잭션의 연산은 DB에 모두 반영되던지, 모두 반영되지 않아야 한다.  
하나라도 실패한다면 앞서 성공한 것들을원상 복구 시켜야한다.

**2. 일관성(Consistency)**  
트랜잭션의 작업 처리 결과는 항상 일관성 있어야 한다.

**3. 독립성(Isolation)**  
어떤 트랜잭션도 다른 트랜잭션의 작업에 끼어들 수 없다.

**4. 지속성(Durability)**  
트랜잭션이 완료된다면, 결과는 영구적이어야 한다.

### 트랜잭션의 원자성을 보장하는 방법
트랙잭션은 로직을 수행하고 모든 로직이 성공적으로 수행되었을 경우에는 모든 결과를 DB에 일괄적으로 commit 하고,  
하나라도 실패한다면 모든 작업을 원상 복구(rollback) 시킨다.

아래와 같이 try문 안에 원자성을 보장해야 하는 로직을 작성하고, try 문 안에서 예외가 발생했을 경우에 모든 것을 rollback 시키는 방법으로 구현할 수 있다.
```java
public void sendMoney(Long senderId, Long receiverId, Long value) {
		Connection connection = dataSource.getConnection();
		connection.setAutoCommit(false);

		try {
        // 한번에 처리되어야 하는 로직
				connection.commit();	
		} catch(SQLException e) {
				connection.rollback();
				throw new RemittanceException();
		}
}
```

### Transaction과 AOP
위와 같이 Transaction에 관한 처리를 해줄 수 있지만, 위의 방식에는 문제가 있다.  
Transactionan의 원자성을 보장해주기 위한 코드가 비즈니스 로직과 함께 존재. 따라서, 개발자는 핵심 비지니스 로직에 집중할 수 x

Transaction에 관한 connection 관련 코드와 try~catch 코드가 중복 된다.  
Transaction을 처리해주어야 하는 곳이 여러 곳이라면 해당 try~catch를 반복적으로 작성해줘야 한다.

여기서 생각할 수 있는 개념이 AOP(Aspect Oriented Programming)로, 관점 지향 프로그래밍이라는 뜻
