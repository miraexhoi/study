# **@JsonProperty 란?**

**Jackson 라이브러리에서 제공하는 어노테이션으로 JSON 데이터와 객체 간 매핑할 필드명을 지정할 때 사용**

SB 에는 Jackson 기본 내장, JSON 요쳥/응답 처리 시 사용

### **@JsonProperty 를 사용하는 이유**

1. JSON 필드명과 Java 필드명이 다를 때 매핑을 맞춰줌
2. JSON 직렬화(객체 → JSON 변환) 와 역직렬화(JSON → 객체 변환) 시 특정 필드명 강제 가능
3. Snake_case 와 CamelCase 변환 쉽게 처리 가능

### 

### **@JsonProperty 를 사용 예제**

예제 1. JSON 필드명이 다를 때 DTO 매핑

```
@JsonIgnoreProperties(ignoreUnknown = true)
class TestDTO(

    @get:JsonProperty("org_tid")
    override val cancelTrxId: String,

    @get:JsonProperty("cancel_amt")
    override val cancelAmount: String,

...
) {}
```

예제 2. @RequestParam 으로 사용

```
@GetMapping
public ResponseVO<> get(
	@RequestParam("test_param1") String testParam1,
    @RequestParam("test_param2") String testParam2
) {
	RequestPVO pvo = new RequestPVO();
    pvo.setTestParam1(testParam1);
    pvo.setTestParam2(testParam2);

	...  

	return new ResponseVO<>();
}
```

예제 3. @ModelAttribute 로 사용하기 

```
@Setter
public class RequestPVO {

	private String testParam1;
	private String testParam2;

	public void setTest_param1(String test_param1) {
    	this.testParam1 = test_param1;
    }

	public void setTest_param2(String test_param2) {
    	this.testParam2 = test_param2;
    }
}

...

@GetMapping
public ResponseVO<> get(@ModelAttribute RequestPVO pvo) {

	...  

	return new ResponseVO<>();
}
```

### 참고

- @RequestBody 
  : Json 형태의 데이터를 Java 객체에 매핑할 때 사용하는 어노테이션
- @JsonProperty 
  : Jackson 라이브러리 어노테이션. 직렬화, 역직렬화 시 필드명과 객체의 속성명이 다를 때 사용

코틀린에서 `@get:` 어노테이션은 프로퍼티가 아닌 생성된 자바 게터 메서드에 어노테이션 적용할 때 사용 (필드 x, 컴파일된 자바 게터 메서드)  
ex. `@get:JsonProperty("name") val name: String` 처럼 사용 (JSON 직렬화 시 게터 메서드에 어노테이션 명시)
