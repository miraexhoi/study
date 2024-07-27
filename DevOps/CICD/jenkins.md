# Jenkins
> 모든 언어의 조합과 소스 코드 레포지토리에 대한 **CI/CD 환경을 구축하기 위한 도구**  
> **빌드, 테스트, 배포 프로세스를 자동화**하여 소프트웨어 품질과 개발 생산성 향상

- Java Runtime Environment에서 동작
- 다양한 플러그인들을 활용해서 각종 자동화 작업을 처리
- 일련의 자동화 작업의 순서들의 집합인 CI/CD 파이프라인 구축

### Jenkins의 기능
1. **컴파일 오류 검출**
2. **자동화 테스트를 수행**
3. **정적 코드 분석에 의한 코딩 규약 준수 여부 체크**
4. **프로파일링 툴을 이용한 소스코드 변경에 따른 성능 변화 감시**
5. **결합 테스트 환경에 대한 배포작업**

### Jenkins의 구성
젠킨스에서의 작업 실행은 마스터 노드와 에이전트 노드에 의해 처리된다.  
- **Jenkins Master**  
젠킨스 설정 및 구성, 사용자 인증, 플러그인 관리 등 전반적인 관리와 조정 작업을 담당  
- **Jenkins Agents**  
마스터 노드에 의해 파이프라인에 정의된 작업을 실제로 수행

<p align="left"><img src="https://github.com/user-attachments/assets/3b2d4029-6eb7-4afa-8721-46dd11538285" width="750" height="400"/></p>

### Jenkins 파이프라인
Jenkins pipeline은 **Declarative(선언형) VS Scripted(스크립트형)** 이렇게 두 가지 형태가 있다.  
또한 주요 항목으로 **Pipeline, Node, Stage, Step** 가 있다.
 - **Pipeline**  
   애플리케이션의 빌드, 테스트 및 배포 단계를 포함하는 전체 빌드 프로세스를 정의  
   pipeline 의 블록은 선언형 파이프라인 구문의 핵심 부분  
   Jenkinsfile 의 시작 지점에 선언  

    ```shell
      pipeline {   // 세부 작성 필요 }
    ```
 - **Node**  
   node 의 블록은 스크립트형 파이프라인 구문의 핵심 부분  
   Jenkinsfile 의 시작 지점에 선언  

    ```shell
      node {   // 세부 작성 필요 }
    ```
 - **Stage**  
   stage 블록은 전체 파이프라인 단계를 통해 수행되는 작업의 하위 집합  
     ex. jenkins를 통해서 테스트 → 빌드 → 배포 → 서버재시작을 수행  
     → 테스트, 빌드, 배포, 서버재시작이 각각 하나의 stage가 됨  
 - **Step**  
   단일 작업을 나타내며, 특정 시점에서 수행할 작업을 안내  
   
   ```shell
     stage('build-application-admin') {   steps {     echo 'Build Start "${APP_ADMIN}"'     sh './gradlew --gradle-user-home ${GRADLE_HOME} ${APP_ADMIN}:clea ${APP_ADMIN}:build -x test'     echo 'Build End "${APP_ADMIN}"'   } }
    ```
   admin 어플리케이션의 빌드를 담당하는 하나의 stage  
   하나의 stage 안에 배포하는 작업을 담당하고 있는 step 에서 수행할 작업을 안내  
