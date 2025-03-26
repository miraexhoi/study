# 내 마음대로 되지 않는 테스트코드, 꼭 작성해야 할까? (현실편)

### #01 현실적인 테스트 코드 작성법

**목차 1. 단위 테스트**  

- 무엇을 테스트할 것인가
- **엣지 케이스**는 어디까지 커버해야 하는가 통합 테스트

**목차 2. 통합 테스트**  

- **의존성**을 다루는 방법
- **데이터베이스** 모킹하지 않기

인프런 팀은 TDD 가 아닌, 개발 후 테스트 코드를 추가하는 방식을 사용한다.  
예를 들어, 명세된 회원가입 기능 을 구현한다고 가정해보자.  

`Controller` 쪽에서 사용자 요청을 처리하고 **요청값을 받아 파싱/검증**해서 `Service` 로 넘겨준다.  
그러면 `Service` 쪽 코드에서는 앞에서 받은 값으로 **주요 비지니스 로직을 수행**하게 됨.  

Service 계층에서 필요한 DB 조회/저장 같은 로직은 `Repository` 를 이용해서 이루어 지도록 함.  
마지막으로 서비스 계층에서 반환한 **최종 결과 데이터를 받아 Controller 에서 가공 및 응답한다.**  

### 무엇을 테스트할 것인가?

각 객체들은 회원가입이라는 목적을 달성하기 위해 필요한 일들을  
`Controller`, `Service`, `Entity`, `Repository` 로 나눠서 구현한다.  

그렇다면 테스트 코드는 나눠진 기능명세를 자연스럽게 표현하도록 구현하면 된다.  
여기서 중요한건, **테스트 구현 세부사항이 드러나도록 작성하면 안된다**.  
**구현 세부사항에 집착할수록 깨지기 쉬운 테스트**가 된다.  

Repository 를 목킹 처리해서 이메일 증복 검사에 대한 테스트 코드 예시:  

```jsx
// bad
	it('받은 이메일에 해당하는 계정이 데이터베이스에 이미 존재하는지 확인한다.', async () => {
		// given
		const mockUserApiRepository = mock<UserApiRepository>();
		const service = new UserApiService(mockUserApiRepository, new Crypto());
		const email = 'test@email.com';
		
		// when
		await service.signUp('nickname', email, 'password');
		
		// then
		expect(mockUserApiRepository.findByEmail).toBeCalledTimes(1); /* Mocking */
		expect(mockUserApiRepository.findByEmail).toBeCalledWith(email); /* Mocking */
	}
);
```

`findByEmail` 이란 메서드를 특정 이메일로 몇번이나 호출했냐는 테스트는 중간과정에 속하는 구현 세부사항.  
이렇게 구현 세부사항을 노출하고 검증하게 되면 깨지기 쉬운 테스트가 되기 때문에 좋지 못한 테스트가 된다.  
