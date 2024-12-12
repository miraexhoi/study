# Apache Kafka란?

Apache Kafka는 **분산 스트리밍 플랫폼**으로, 실시간 데이터 파이프라인 및 스트리밍 애플리케이션을 구축하기 위해 사용된다.  
**LinkedIn**에서 개발되었으며 현재는 **Apache Software Foundation**에서 관리하고 있다.  

### **Kafka의 특징**
- **고성능**: 대규모 데이터 처리에 적합하며, 초당 수백만 개의 메시지를 처리할 수 있음
- **확장성**: 브로커(Broker)와 파티션(Partition)을 추가하여 손쉽게 확장 가능
- **내구성**: 데이터를 디스크에 저장하여 높은 내구성을 보장
- **분산 시스템**: 여러 노드에서 작동하며, 장애 복구에 유리함

### **핵심 구성 요소**
- **Producer**: 데이터를 Kafka로 전송하는 역할
- **Consumer**: Kafka에서 데이터를 가져가는 역할
- **Broker**: 메시지를 저장하고 전달하는 Kafka 서버
- **Topic**: 데이터가 저장되는 논리적 채널
- **Partition**: 토픽을 물리적으로 나누어 저장하는 단위
- **Offset**: 각 메시지의 고유한 식별자

### **Kafka의 동작 원리**
1. Producer는 데이터를 특정 토픽에 발행
2. Broker는 데이터를 지정된 파티션에 저장
3. Consumer는 해당 파티션에서 메시지를 읽음
4. 메시지는 Offset 기반으로 관리되어 Consumer가 읽은 위치를 추적 가능

### **주요 용도**
- **로그 및 이벤트 데이터 처리**: 웹사이트 활동 추적, 서버 로그 분석
- **실시간 스트리밍**: 데이터 파이프라인, ETL 작업
- **메시징 시스템**: 비동기 작업 처리, 마이크로서비스 간 메시지 전달

### Kafka의 주요 장점
1. **고가용성**: 복제를 통해 데이터를 안정적으로 보관
2. **유연성**: 다양한 언어 클라이언트를 지원 (Java, Python, Go 등)
3. **데이터 보존**: 설정된 기간 동안 데이터를 보관하여 재처리가 가능
4. **확장성**: 노드를 추가하여 처리량을 유연하게 확장

### Kafka 사용 사례
1. **LinkedIn**: 사용자 활동 로그 수집 및 실시간 분석
2. **Uber**: 실시간 위치 데이터 스트리밍
3. **Netflix**: 서비스 상태 모니터링 및 로그 수집

### 기본 명령어 예시
- **Kafka 시작**  
  `bin/kafka-server-start.sh config/server.properties`
- **토픽 생성**  
  `bin/kafka-topics.sh --create --topic <topic-name> --bootstrap-server localhost:9092`
- **메시지 보내기**  
  `bin/kafka-console-producer.sh --topic <topic-name> --bootstrap-server localhost:9092`
- **메시지 소비**  
  `bin/kafka-console-consumer.sh --topic <topic-name> --bootstrap-server localhost:9092 --from-beginning`

---

Kafka는 **실시간 데이터 처리**와 **분산 처리**가 필요한 다양한 환경에서 강력한 도구이다.  
적절한 아키텍처와 설정을 통해 대규모 데이터 파이프라인을 구축하고, 빠르고 안정적으로 데이터를 처리할 수 있다.

