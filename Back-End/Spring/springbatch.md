# Spring Batch란 무엇인가?

대량의 데이터 처리를 위한 경량화된 프레임워크로, 반복적인 일괄 처리(Batch Processing) 작업을 효율적으로 처리할 수 있는 기능을 제공한다. 
대용량 데이터 처리나 주기적인 업무 처리 등을 효율적으로 처리할 수 있고, 대용량 데이터 처리에 적합한 분산 방식의 처리를 지원한다.

#### 특징 1. 대용량 데이터 처리
Spring Batch는 방대한 양의 데이터를 처리할 수 있다. 데이터 처리 작업을 분산 처리할 수 있어서, 대용량 데이터 처리에 적합하다.

#### 특징 2. 트랜잭션 관리
Spring Batch는 트랜잭션 관리를 지원한다. 데이터 처리 중 실패한 작업은 롤백하여 데이터 일관성을 유지할 수 있다.

#### 특징 3. 재시도 기능
Spring Batch는 작업 중 실패한 경우, 작업을 재시도할 수 있는 기능을 제공한다. 또한, 재시도 횟수를 설정할 수 있다.

### Spring Batch 구조
- **Job**: 배치 작업의 최상위 구성 요소.
- **Step**: Job을 구성하는 하위 단위로, 실제 작업이 실행되는 단계.
- **JobInstance**: 특정 Job에 대한 실행 정보.
- **JobExecution**: Job 실행 시 생성되는 실행 단위.
- **StepExecution**: Step 실행 시 생성되는 실행 단위.

### 기본 컴포넌트

#### Job
- 배치 작업의 전체 흐름을 정의하는 객체.
- 여러 Step을 포함하며 순차적 또는 조건부로 실행 가능.

```java
@Bean
public Job exampleJob(JobBuilderFactory jobBuilderFactory, Step exampleStep) {
    return jobBuilderFactory.get("exampleJob")
                            .start(exampleStep)
                            .build();
}
```
