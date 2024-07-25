# Nginx란?
> **트래픽이 많은 웹사이트의 서버(WAS)를 도와주는 비동기 이벤트 기반구조의 웹 서버 프로그램**  
  "고성능, 확장성, 고가용성 웹서버, 역방향 프록시 서버 및 웹 가속기(HTTP 로드밸런서, 콘텐츠 캐시 등의 기능 결합)이다."  

클라이언트로부터 요청을 받았을 때 요청에 맞는 정적 파일을 응답해주는 HTTP Web Server로 활용되기도 하고,  
Reverse Proxy Server로 활용하여 WAS 서버의 부하를 줄일 수 있는 로드 밸런서로 활용되기도 한다.

![image](https://github.com/user-attachments/assets/b6b4ff04-e0bd-4d0d-b86d-b7f09f131aaa)
- **Client** : 서비스를 이용하기 위해 네트워크를 통해 요청을 보내는 주체
- **Web Server** : 클라이언트 요청에 따라 정적 파일을 응답하여 제공하는 소프트웨어
- **WAS** : 틀라이언트 요청에 동적인 처리를 담당하는 영역
- **DB** : 조직이나 개인이 필요한 정보를 체계적으로 저장, 관리 및 검색할 수 있는 시스템

주로 Client - Web Werver - WAS - DB 순으로 **요청** / DB - WAS - Web Server - Client 순으로 **응답**

