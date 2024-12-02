# Grafana 란?

[Grafana Playground 에서 맛보기](https://play.grafana.org/d/000000012/grafana-play-home?orgId=1)

Grafana란 시계열 메트릭 데이터를 시각화 하는데 대시보드를 제공해주는 오픈소스이다.

다양한 DB를 연결하여 DB의 데이터를 가져과 시각화 할 수 있으며, 그래프를 그리는 것도 간단히 마우스 클릭으로 완료할 수 있다.

시각화한 그래프에서 특정 수치 이상으로 값이 치솟을 때 알림을 전달받을 수 있는 기능도 제공 → 운영 관점에서 굉장히 유용

또한 일반 사용자들이 만들어놓은 대시보드를 import 해서 사용할 수 있고 그 대시보드를 커스터마이징 할 수 있다.

### Grafana vs Datadog
이 둘의 가장 큰 차이로는 데이터독은 데이터를 직접 저장하고 있지만 그라파나틑 외부 데이터 소스를 정의하고  
해당 데이터 소스에 쿼리를 통해서 데이터를 동적으로 가져와 시각화를 수행한다.

 

또한 Datadog은 모니터링을 제공하는 상용 서비스이고, Grafana는 오픈소스 프로젝트입니다.

#### Docker로 Grafana 설치 (로컬)
먼저 로컬 환경에서 Grafana를 설치한다. 역시 Docker 기반으로 설치를 할 것이다. 터미널에 다음을 입력하면 바로 설치를 할 수 있다.
```
$ docker run --name=grafana -p 3000:3000 grafana/grafana
```


끝이다. 이후 이어지는 절에서, docker-compose를 통해서 Prometheus와 Grafana를 다음과 같이 코드로 구성한다.

`src/part2/ch01/docker-compose.yml`
```
version: "3"

services:
  prometheus:
    container_name: prometheus
    image: prom/prometheus:latest
    ports:
      - 9090:9090

  grafana:
    container_name: grafana
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
```

로컬에서 docker-compose로 구성되는 인프라스트럭처를 관리하려면 터미널에 다음을 입력하면 된다.

```
# 현재 위치
$ pwd
# docker-compose.yml이 있는 위치
/Users/gurumee/Workspace/gurumee-book-prometheus/src/part2/ch01

# 컴포넌트 실행
$  docker compose up -d
[+] Running 2/2
⠿ Container prometheus  Started                                                                                                                                                                                                   0.9s
⠿ Container grafana     Started         

# 컴포넌트 상태 확인
$ docker ps
CONTAINER ID   IMAGE                    COMMAND                  CREATED          STATUS          PORTS                                       NAMES
3a0b00ceb302   e511606aee56             "/run.sh"                16 seconds ago   Up 15 seconds   0.0.0.0:3000->3000/tcp, :::3000->3000/tcp   grafana
f3ba27ef35a8   9dfc442be98c             "/bin/prometheus --c…"   23 secons ago   Up 15 seconds   0.0.0.0:9090->9090/tcp, :::9090->9090/tcp   prometheus

# 컴포넌트 중지
$ docker compose down -v
[+] Running 3/3
 ⠿ Container prometheus  Removed                                                                                                                                                                                                   0.3s
 ⠿ Container grafana     Removed                                                                                                                                                                                                   0.2s
 ⠿ Network ch01_default  Removed    
```

### Grafana 설치 (서버)
서버에서 Grafana는 다음과 같이 설치할 수 있다.
```
# rpm install
$ sudo tee /etc/yum.repos.d/grafa.repo <<EOF
[grafana]
name=grafana
baseurl=https://packages.grafana.com/oss/rpm
repo_gpgcheck=1
enabled=1
gpgcheck=1
gpgkey=https://packages.grafana.com/gpg.key
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
EOF

# grafana install
$ sudo yum install grafana -y
```

그럼 자동으로 Grafana가 설치되고 grafana-server라는 이름으로 서비스가 등록된다. 이제 터미널에 다음을 입력해서 Grafana를 실행하면 된다.

```
$ sudo systemctl start grafana-server

# 그라파나 상태 확인
$ sudo systemctl status grafana-server
● grafana-server.service - Grafana instance
Loaded: loaded (/usr/lib/systemd/system/grafana-server.service; enabled; vendor preset: disabled)
Active: active (running) since 목 2021-01-14 07:04:46 UTC; 3 days ago
Docs: http://docs.grafana.org
....
```


### TODO :: Grafana와 Prometheus 연동하는 법 공부하기
