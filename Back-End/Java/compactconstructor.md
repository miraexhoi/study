# Compact Constructor
### 개요
평소 record class에 관심이 많았는데 프로젝트를 진행하던 중 Compact Constructor에 대한 존재를 알게되었다.

### Compact Constructor란?
record의 생성자가 클래스의 private 필드를 초기화하는 것보다 더 많은 행동을 하기를 원할 때 생성자 커스텀 가능  
이 때 Class Constructor와는 다르게 Compact Constructor는 일반적인 형식보다 더 간략하게 적을 수

### Compact Constructor의 특징
- 파라미터를 작성하지 않아도 ok
- 초기화 로직은 마지막에 자동 호출

### 예시 코드
```java
public RecordCarsDto {  // 매개변수를 받는 부분 생략
    if (Objects.isNull(values)) {
        values = new ArrayList<>();
    }
    if (Objects.isNull(speed)) {
        speed = 10;
    }
    // this.values = values; this.speed = speed; 와 같은 초기화 로직은 마지막에 자동 호출
}
```


~~Compact Constructor 는 record 이외에서는 사용 불가~~
