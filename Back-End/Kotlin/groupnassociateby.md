# 코틀린 groupBy와 associateBy 차이 

### associateBy

특정 키 값을 기준으로 List 형태를 만들어서 반환함 (1:1 방식 그룹화)

List의 원소에서 두 값을 묶어서 Map의 <Key, Value> 타입으로 재생성

**groupBy() 와는 달리, key 가 중복이 되면 마지막 요소를 Map 의 value 로 저장**

```
data class Person(val name: String, val age: Int)

val people = listOf(
    Person("Alice", 21),
    Person("Alice", 22),
    Person("Alice", 23),
    Person("Bob", 25),
    Person("Charlie", 21),
    Person("David", 25),
    Person("Eve", 30)
)

val associatedByName = people.associateBy { it.name }

println(associatedByName)
// 출력 결과:
// {Alice=Person(name=Alice, age=23), 
// Bob=Person(name=Bob, age=25), 
// Charlie=Person(name=Charlie, age=21), 
// David=Person(name=David, age=25), 
// Eve=Person(name=Eve, age=30)}
```

Alice라는 동명이인이 3명이고 각자의 나이 또한 다름 → `associateBy`를 통해 이름 기준 그룹화를 진행할 경우, 가장 마지막 요소만 출력

반복 가능한 객체를 수신객체로 수신 후, 반환하는 값을 key값으로 지정하고, 이에 수신받았던 객체 타입을 1:1로 지정

### groupBy

키 값을 기준으로 아이템을 그룹화 하긴 하지만 단 하나의 요소만 만들어 반환함 (1:N 방식 그룹화)

Map<K, List<T>> 형태로 만듦 → **key 가 중복이 되어도 value 가 List<T> 이므로 전부 저장**
- **Key : group을 묶어줄 조건**
- **Value : Key 조건에 만족하는 원소들 리스트**

```
data class Person(val name: String, val age: Int)

val people = listOf(
    Person("Alice", 21),
    Person("Bob", 25),
    Person("Charlie", 21),
    Person("David", 25),
    Person("Eve", 30)
)

val groupedByAge = people.groupBy { it.age }

println(groupedByAge)
// 출력 결과:
// {21=[Person(name=Alice, age=21), Person(name=Charlie, age=21)], 
//  25=[Person(name=Bob, age=25), Person(name=David, age=25)], 
//  30=[Person(name=Eve, age=30)]}
```

나이를 기준으로 그루핑 → 21이라는 나이를 키값으로 위 두 사람이 리스트 타입으로 매핑

반복 가능한 요소를 참조 객체로 수신 후, 마지막 반환하는 라인을 키값으로 지정함과 동시에, 수신받았던 참조 객체 타입을 리스트 형태로 지정
