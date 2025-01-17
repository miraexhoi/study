# Amazon ElastiCache란?

[실습코드 보러가기](https://github.com/miraexhoi/elasticache-asynchronous-messaging)  

ElastiCache는 **Fully managed 분산 인메모리(In-memory) 캐싱 서비스**이다.  
**데이터베이스**나 다른 **백엔드 스토리지**에서 가져오는 데이터를 **캐싱(Cache)하여 액세스 속도를 향상**시키는 데 사용된다.  
즉, ElastiCache는 쉽게 말해서 **데이터를 더 빨리 가져오기 위한** 메모리 기반의 저장소 서비스이다.  

![image](https://github.com/user-attachments/assets/a147be2c-43a0-47f5-ae74-3687c40b34d6)

### ElastiCache 특징 ( ⚠ 캐시 엔진에 따라 다르다 )
#### Fully managed (완전 관리형)
- AWS의 완전 관리형 서비스로, 데이터베이스 확장, 장애 감지 및 복구, 백업 등은 AWS에 의해 관리 ← 개발자 입장에서는 관리 쉬움
#### Scalable (확장 및 축소 능력): ⚠ 엔진에 따라 다르다.
- ElastiCache for Redis는 애플리케이션의 요구에 따라 클러스터 크기를 자동으로 확장 / 축소 가능
#### High availability (고가용성): ⚠ 엔진에 따라 다름
- ElastiCache for Redis는 Multi-AZ(Multi-Availability Zone) 설정을 사용할 경우 가용성이 99.99%

RDS나 Redshift와 같은 다른 데이터베이스 서비스와 연계하여 쿼리 결과를 ElastiCache에 캐시함으로써 전체적인 성능을 향상 가능

### ElastiCache이 지원하는 캐시 엔진 (2가지)
ElastiCache에는 "KVS"(Key-Value Store)형 데이터베이스 엔진이 2개 준비되어 있으며, 데이터베이스를 구축할 때 선택할 수 있다.

#### ※ Key-Value형
저장할 데이터(Value)와 그것을 특정하기 위한 키(Key)가 쌍을 이루는 구성의 데이터셋을 의미한다.

#### 1. Redis -  (특징: 고급 기능 탑재)
- Redis는 Memcached보다 고기능의 데이터베이스 엔진이다.
- **Single Thread**로 작동한다. 즉, 한 번에 하나의 작업만 처리한다.
- **Snapshot (Amazon S3에 저장) 기능을 통한 백업 및 복원이 가능**하며, 데이터를 **영구적으로 보존**할 수 있다.
- **"자동 페일오버"와 "Multi AZ"가 있다. (장애 대책 기능)**
  - **자동 페일오버**: 프라이머리 노드에 장애가 발생하면 자동으로 레플리카 노드가 프라이머리 노드로 승격
  - **Multi AZ**: AZ를 넘나드는 복제가 가능 → 프라이머리 노드가 있는 AZ에 장애가 발생해도 다른 레플리카 노드를 승격시켜 운영 지속 가능
- **[보안 기능]**: Redis는 Memcached에는 없는 보안 기능을 제공한다.
  - 저장된 데이터의 암호화나 SSL/TLS를 통한 통신 암호화
  - 클라이언트를 비밀번호로 인증하는 Redis 인증 등을 지원
  - 이러한 기능을 사용하려면, ElastiCache 데이터베이스를 생성할 때 Redis를 선택하고 암호화 활성화

#### 2. Memcached - (특징: 심플한 기능)
- Memcached는 **단순한 캐싱 활용**에 적합
- **Multi Thread**로 작동한다. 즉, 여러 스레드가 동시에 요청을 처리 가능
- Redis와 달리 Memcached는 **데이터의 영구 보존이나 백업 기능 존재하지 x**
- 그렇기 때문에 **장애나 재부팅이 발생하면 캐시 데이터가 남지 않고 사라짐**
- 계속 유지해야 하는 데이터는 스토리지나 다른 DB 서비스에 저장하고, 속도를 높이기 위한 캐시로 사용하는 경우에 적합

### Redis와 Memcached 공통점
1. in-memory DB로써 빠른 속도
2. key-value 형태로 데이터 저장
3. 캐시나 새션, 상태 정보 저장에 최적화

| **특징** | **Redis** | **Memcached** |
| --- | --- | --- |
| **Multi Thread (멀티스레드)** | **-**(**Single thread, 싱글 스레드**) | **Yes**(**Multi thread, 멀티 스레드**) |
| **고급 데이터 타입 지원** | **Yes**(lists, sets, sorted sets, hashes, bit arrays, hyperloglogs를 지원한다) | -(주로 문자열 기반의 key와 value만 지원하며, 고급 데이터 구조는 지원하지 않는다) |
| **자동 페일오버** | **Yes** | - |
| **Multi AZ** | **Yes** | - |
| **레플리케이션** | **Yes** | - |
| **백업 및 복원** | **Yes** | - |
| **보안 기능** | **Yes** | - |
| Pub/Sub | Yes | - |
| **Use Case** | ・복잡한 데이터 타입이 필요한 경우・영구화가 필요한 경우・페일오버가 필요한 경우・pub/sub가 필요한 경우 | ・심플한 데이터 타입(키-값)만으로 충분한 경우・멀티스레드가 필요한 경우 |


### Caching Strategies (캐싱 전략)
ElastiCache는 애플리케이션 성능 향상을 위해 주로 사용된다.  
데이터를 어떻게 저장할 것인가는 데이터의 일관성과 가용성을 유지하면서 성능을 최대화하는 데 중요하다.  
이를 캐싱 전략이라고 하며 대표적인 2 가지 캐시 전략이 있다.  

#### 1. Write-Through : 바로 바로 업데이트
> DB에 데이터를 업데이트(write)할 때마다, 동시에 캐시에도 데이터를 업데이트한다.

이 전략에서는 캐시의 데이터가 항상 **최신 상태로 유지**되므로, **데이터 일관성이 유지**된다.  
그러나 쓰기 성능이 약간 저하될 수 있으며, 액세스되지 않는 데이터가 캐시에 쌓이는 단점이 있다.

#### 2. Cache-Aside (Lazy loading) : 살짝 지연 but 효율적
> DB에 데이터를 업데이트(write) 우선시하고, 필요할 때만 캐시에 데이터를 업데이트한다.

- 요청 발생: 애플리케이션이 **데이터를 DB 요청할 때 먼저 캐시(ElastiCache)를 확인**한다.
  - 만약 캐시에 그 데이터가 있다면, 애플리케이션에 보낸다.  
  - 만약 캐시에 그 데이터가 없다면, 데이터베이스(DB)에서 해당 데이터를 가져온다.
    - **캐시에 저장**: 가져온 데이터를 캐시(ElastiCache)에 저장 → 이후에 동일한 데이터 요청이 들어오면 캐시에서 빠르게 조회


이 방법에서는 요청된 데이터만 캐시되므로 리소스 낭비 감소, 캐시와 DB 간 일시적인 데이터 불일치가 발생 가능성  
또한, **cache miss(캐시 미스: 캐시에서 데이터를 가져올 수 없는 경우)*8가 발생하면 데이터 가져오는 데 시간이 걸릴 수 있다.  


 
