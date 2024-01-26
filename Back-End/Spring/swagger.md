# Swagger
`Swagger`는 RESTFul 웹 서비스를 만들 때 API 문서를 자동으로 만들어주고, 직접 테스트할 수 있는 UI 제공

### Springfox Swagger vs Spingdoc
- Springfox가 2년 간 업데이트 하지 않는 동안 Springdoc은 webflux라는 논 블록킹 비동기 방식의 웹 개발을 지원하도록 개발되었다.
- Springfox Swagger의 경우 3.00버전을 마지막으로 업데이트가 중단되었다.
- Springdoc이 더 최근에 나왔기에 Springfox를 더 발전시킨 모습이며, 비교적 사용하기 쉽다고 한다.

![image](https://github.com/miraexhoi/study/assets/109408165/66958364-241d-4628-8dfe-af677570e3ed)


#### 특징
- @Tag 어노테이션의 사용 범위가 다르다.
  - Springdoc에서는 클래스단위로 @Tag 어노테이션을 사용해서 그룹핑할 수 있다면,  
    Springfox에서는 클래스뿐만 아니라 메소드 단위로도 같은 어노테이션을 넣어줘야해서 중복되는 코드 양 증가
- Springfox에서는 api 간 정렬이 되지 않는다.  
  - Springdoc에서는 properties 파일을 이용해서 그룹 간, api 간 정렬 가능
 
### Springdoc 사용 방법
build.gradle 파일에 `implementation 'org.springdoc:springdoc-openapi-ui:1.6.9'` 의존성 추가
