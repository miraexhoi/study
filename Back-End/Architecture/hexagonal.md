# 헥사고날 아키텍처
### 개요
최근 새로운 프로젝트를 하나 시작 했는데 나중에 유지보수를 위해서 헥사고날 아키텍처를 적용하기로 했다.
### 헥사고날 아키텍처란?
사전적 의미로는 **육각형 건축물**을 의미하며 여러 소프트웨어 환경에 쉽게 연결할 수 있도록,  
느슨하게 결합된 애플리케이션 구성요소를 만드는 것을 목표로 하는 아키텍처
- 전통적인 계층형 아키텍처의 단점을 보완하기 위해 생성됨
- 도메인 중심 아키텍처의 일종으로 클린 아키텍처를 일반화한 구조 중 하나
- a.k.a. 포트와 어댑터(Ports and Adaters) 아키텍처
  
![image](https://github.com/miraexhoi/study/assets/109408165/981d39b3-5b4b-425c-a433-fe2261373693)
육각형 모양은 사실 아무 의미가 없고 애플리케이션이 다른 시스템이나 어댑터와 연결되는 4개의 면을 나타내기 위해 육각형을 사용함...  


핵심적으로 보아야 하는 것은 코어에서 외부로 향하는 의존성이 없다는 것이다.   
→ 이는 외부 어댑터들이 목적에 맞게 포트와 잘 커뮤니케이션 되도록 구현되었다면 쉽게 교체가 가능하다는 뜻  
즉, 외부와 도메인 로직의 결합성(의존성)을 제거하여 변경할 이유의 수를 줄일 수 있고, 이는 **유지보수성을 높인다**.

### 특징
사용자 인터페이스나 데이터베이스 모두 비즈니스 로직으로부터 분리해야 하는 외부 요소로 취급한다.  
→ 이는 비즈니스 로직이 외부 요소에 의존하지 않고 프레젠테이션 계층과 데이터 소스 계층이 도메인 계층에 의존하도록 만들어야 한다는 것
- **장점**
    - 도메인 비즈니스 모델에 집중
    - 모듈 일부를 배포 용이
    - 아키텍처 확장 용이
    - SOLID 원칙 쉽게 적용
    - 쉬운 테스트 구성
- **단점**
  - 코드가 많아짐
  - 불필요한 오버헤드

### 패키지 구조 (예시)
```shell
payment-system
        ㄴ account
            ㄴ adapter
                ㄴ in
                    ㄴ web
                        ㄴ AccountController
                ㄴ out
                    ㄴ persistence
                        ㄴ AccountPersistenceAdapter
                        ㄴ SpringDataAccountRepository
            ㄴ domain
                ㄴ Account
                    ㄴ Activity
            ㄴ application
                ㄴ SendMoneyService
                ㄴ port
                    ㄴ in
                        ㄴ SendMoneyUseCase
                    ㄴ out
                        ㄴ LoadAccountPort
                        ㄴ UpdateAccountStatePort

```
