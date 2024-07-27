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

### Nginx 를 사용하는 이유
1. **높은 성능과 적은 메모리 사용**  
   비동기 I/O 방식 사용 → 빠른 응답 시간 보장
3. **리버스 프록시 사용 가능**  
   인터넷과 백엔드 사이에 있는 서버 영역을 뜻하는 리버스 프록시 (로드 밸런싱)
   + 캐싱 서버로도 이용 가능 / 보안 효과
5. **SSL 지원**  
   웹사이트와 사용자 간의 통신을 암호화하고 보안을 유지하는데 사용되는 프로토콜  
   Nginx는 HTTPS 인증서를 제공 (SSL은 HTTPS로 알려진 보안 HTTP 프로토콜의 기반 기술)
7. **데이터 압축**  
   요청이 text일 경우 Gzip을 사용해 해당 데이터 압축 가능
9. **비동기 처리**  
   Nginx는 **이벤트 루프 방식**을 사용해 높은 성능 제공  
   여러 요청이 들어왔을때 많은 트래픽 동시 처리 → 빠른 응답 시간

### Nginx 설정
```shell
sudo yum install nginx
```
```shell
sudo vim /etc/nginx/nginx.conf
```
  위 설정파일에서 `location` 수정
```shell
sudo service nginx restart
```
