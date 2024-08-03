# NoSQL
> Not Only SQL 혹은 Non-Relational Operational DataBase의 약자로 비관계형 데이터베이스
주로 빅데이터, 분산 시스템 환경에서 대용량의 데이터를 처리하는데 적합

NoSQL의 핵심은 **Horizontal Scalability(수평확장)과 High Availability(고가용성)** 이다.  
→ 기존의 RDBMS : Consistency(일관성), Availability(가용성)

### NoSQL 특징
**① RDBMS와 달리 데이터 간의 관계 (Relation)를 정의하지 않는다.**  
RDBMS는 데이터 간의 관계를 Foreign Key로 정의하고 Join 연산을 수행할 수 있지만  
NoSQL은 Key-Value 형태로 저장되기 때문에 Join 연산이 불가능하다.

**② RDBMS에 비해 대용량의 데이터를 저장할 수 있다.**  
 
**③ 분산형 구조로 설계되어 있다.**  
여러 곳의 서버에 데이터를 분산 저장하여 특정 서버에 장애가 발생했을 때도 데이터 유실 혹은 서비스 중지가 발생하지 않도록 한다.

**④ 고정되어 있지 않은 테이블 스키마를 갖는다.**  

RDBMS와 달리 테이블(컬렉션)의 스키마가 유동적이고 데이터를 저장하는 컬럼이 각기 다른 이름과 다른 데이터 타입을 갖는 것이 허용된다.

### CAP
- RDBMS **ACID(원자성, 일관성, 고립성, 영구성)** 특성을 따른다. → DB의 트랜잭션이 안전하게 수행된다는 것을 보장하기 위한 특징  
- 분산형 구조는 **일관성(Consistency), 가용성(Availability), 분산 허용(Partitioning Tolerance)** 3가지 특징을 가지고 있다.  

CAP 이론은 이 중 두가지만 만족할 수 있다는 이론이다. NoSQL은 이 **CAP 이론**을 따른다.  

### NoSQL 장단점
#### 장점
- RDBMS에 비해 저렴한 비용으로 분산처리와 병렬 처리 가능
- 비정형 데이터 구조 설계로 설계 비용이 감소
- Big Data 처리에 효과적
- 가변적인 구조로 데이터 저장 가능
- 데이터 모델의 유연한 변화 가능

#### 단점
- 데이터 업데이트 중 장애가 발생하면 데이터 손실 발생 가능
- 많은 인덱스를 사용하려면 충분한 메모리가 필요. 인덱스 구조가 메모리에 저장
- 데이터 일관성이 항상 보장되지 않음

→ 즉, 최종적 일관성 (Eventually Consistent)를 지향

### NoSQL 종류
**1. Key-Value Database**  
ex. ***Redis**, Oracle NoSQL DB, VoldeMorte  

<img width="362" alt="스크린샷 2024-08-03 오후 5 13 06" src="https://github.com/user-attachments/assets/318db871-f6c9-45f8-af84-5f54ec77240f">

**2. Wide-Column Database**  
ex. Hbase, Cassandra, GoogleBigTable, Vertica  

**3. Document Database**  
ex. ***MongoDB**, CouchDB, Riak, Azure Cosmos DB  

**4. Graph Database**  
ex. Sones, AllegroGraph, neo4j, BlazeGraph, OrientDB  

### SQL vs NoSQL 사용 시기
SQL : 명확한 스키마를 보장할 경우, 관계를 맺고 있는 데이터가 자주 변경될 경우 NoSQL에서는 여러 컬랙션을 수정해야
NoSQL : 정확한 데이터 구조를 알 수 없거나 데이터의 구조가 변경, 확장될 경우

ex. 페이스북이나 트위터 같은 SNS 는 게시글을 저장하는데 NoSQL 사용
