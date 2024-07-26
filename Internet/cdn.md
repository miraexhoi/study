# CDN(Content Delivery Network)이란 무엇인가?
> Content Delivery Network의 약자로서 지리적인 제약 없이 전 세계 사용자에게  
> 빠르고 안전하게 컨텐츠 전송을 할 수 있는 기술(콘텐츠 전송 네트워크)을 말한다.  
> 이를 통해 컨텐츠의 **병목현상**을 피할 수 있다.


### CDN 작동 원리
CDN는 서버를 분산시켜 캐싱해두고 사용자의 컨텐츠 요청이 들어오면 사용자와 가장 가까운 위치에 존재하는  
서버로 매핑시켜 요청된 콘텐츠의 캐싱된 내용을 내어주는 방식으로 빠르게 데이터 전송 가능  

만약 서버가 파일을 찾는데 실패하는 경우 CDN 플랫폼의 다른 서버에서 컨텐츠를 찾은다음 응답 전송

- **ORIGIN SERVER** CDN을 사용하지 않고 Origin Server 하나만을 사용하는 경우

![image](https://github.com/user-attachments/assets/4951a79c-a1de-44c0-8c6d-979c2822d451)

- **CDN SERVER** 각 지역에 CDN Server를 사용하는 경우

![image](https://github.com/user-attachments/assets/646f78b0-eae1-4280-8188-9e56cc2b8827)

위와 같이 CDN은 각 지역에 캐시 서버(PoP, Point of presence)를 분산 배치하여  
사용자의 요청에 대해 Origin 서버가 아니라 CDN 서버를 통해 콘텐츠를 전달하는 방식

사용자는 지리적으로 가까운 CDN 서버에서 콘텐츠를 가져오기 때문에  
Origin 서버에 비해 훨씬 더 빠른 속도로 콘텐츠 사용 가능

***이때 CDN 서버의 경우 콘텐츠 전송에 목적을 둔 서버이며, 엣지 서버라고도 함**

### CDN 캐싱 방식
**1. Static Caching**
- Origin Server 에 있는 Content를 운영자가 미리 Cache Server에 복사 해두어  
  사용자가 Cache Server에 Content 요청 시 무조건 Cache Server 존재  
- 대부분의 국내 CDN에서 이 방식 사용 (게임 클라이언트 다운로드 등)

**2. Dynamic Caching**
- Origin Server에 있는 Content를 운영자가 미리 Cache Server에 복사 x  
- 유저가 Content를 요청  
  → 해당 Content가 없는 경우 Origin Server로부터 다운로드 받아 전달  
  → 있는 경우 캐싱된 Content 전달  
- 각각의 Content는 일정 시간 이후 Cache Server에서 삭제 될 수 있다.


### CDN 활용 시 주요 장점
**페이지 로드 시간 단축** [CDN 활용 시 가장 주된 장점]   
- 가까운 CDN 서버에서 콘텐츠를 전송해 주기 때문에 페이지 로드 시간이 단축되며,  
  이는 사용자의 이탈률을 줄이는 효과로 이어져 사용자가 사이트에서 보내는 시간이 늘어남.

**트래픽 급증에 대한 처리**  
- CDN은 로드를 여러 서버에 분산하는 분산 처리로  
  Origin 서버에 미치는 영향을 줄이기 때문에 DDoS 공격 등의 트래픽 급증 처리 가능.  
- 또한 하나의 CDN 서버가 오프라인으로 전환되었을 때,  
  다른 CDN 서버가 해당 서버를 대체하여 서비스가 중단되지 x  

**대역폭 사용량 및 비용 절감**  
- CDN 서버의 캐싱으로 콘텐츠의 복사본을 저장해 놓는 방식으로    
  Origin 서버로부터 전송되어야 하는 데이터의 양이 줄어들어  
  Origin 서버에서의 대역폭 사용량 및 비용 절감.
