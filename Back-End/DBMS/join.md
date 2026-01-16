# JOIN 정복하기 - INNER, OUTER(RIGHT/LEFT), CROSS

### INNER JOIN

조인은 기준 테이블, 조인 테이블에  조인 컬럼에 해당하는 값이 **모두 존재하는 경우**에만 데이터 조회

### OUTER JOIN (Left, Right)

아우터 조인에서 LEFT, RIGHT는 기준 테이블을 지정하는 것이며, 조인 조건에서 동일한 데이터가 없어도  
**기준 테이블의 모든 데이터가 조회**되고 조인 테이블에 데이터가 존재할 경우 해당 데이터 참조

**- Left Outer Join**

왼쪽 테이블 기준으로 A, B 테이블을 비교해서 B테이블에서 조인 조건에 해당하는 값 있다면 가져오고 없다면 NULL

→ 즉, WHERE절로 조회 조건을 제한하지 않는 이상 왼쪽 테이블의 값은 모두 
  

**- Right Outer Join**

반대로 우측 테이블을 기준으로 조인을 수행하기 때문에 우측 테이블의 값은 모두 출력  
\+ 우측 테이블 기준으로 조인 조건에 해당하는 값이 있다면 그 값을 가져오고 값이 없다면 NULL  


\* 만약 우측 테이블에만 존재하는 칼럼들을 조회하고 싶다면?  
→ Join 한 요소(FK) 가 NULL 인 경우를 조회하는 WHERE 조건절 추가하기

### 내가 이해한 방법 (테이블 A, B)

| 테이블 A | 테이블 B (col1) | 테이블 B (col2) |
| ----: | -----------: | -----------: |
|     1 |            1 |            1 |
|     2 |            4 |            2 |
|     3 |            5 |            3 |

-  LEFT JOIN 결과 (A 기준)

|  A | B.col1 | B.col2 |
| -: | -----: | -----: |
|  1 |      1 |      1 |
|  2 |      X |      X |
|  3 |      X |      X |

- RIGHT JOIN 결과 (B 기준)

|  A | B.col1 | B.col2 |
| -: | -----: | -----: |
|  1 |      1 |      1 |
|  X |      4 |      2 |
|  X |      5 |      3 |

### CROSS JOIN 

크로스 조인은 모든 경우의 수를 전부 표현해주는 방식  
기준 테이블이 A의 데이터 한 ROW를 B테이블 전체와 JOIN 하는 방식이며, 결과는 **N * M**  

A테이블에 데이터가 3개, B테이블에는 데이터가 4개가 있다면 총 12개를 검색.  

**JPA 에서 주의할 점**

jpa에서는 동적으로 쿼리를 만들어주는 부분이 있다보니 잘못 사용하면, 본인도 모르게 cross join 을 사용할 가능성  

(QueryDSL 또는 specification 를 이용해서 동적으로 쿼리를 만들고 있을 경우 보통 많이 발생하지만 JPQL 로 직접 쿼리를 작성할 때도 주의)  

예시 가정1. **부모와 유저는 1: N 관계**

```
@Data
@Entity
public class Users {

   @Id
   @GeneratedValue(strategy = GenerationType.IDENTITY)
   private Long id;

   private Integer age;

   private String name;

   @ManyToOne(fetch = FetchType.LAZY)
   private Parent parent;
}
```

```
@Data
@Entity
public class Parent {

   @Id
   @GeneratedValue(strategy = GenerationType.IDENTITY)
   private Long id;

   private Integer age;

   private String name;
}
```

예시 가정2. **JPQL로 외부조인 없이 부모의 필드를 조건으로 사용**

```
@Query("SELECT U "
   + "FROM Users U "
   + "WHERE U.parent.name = :s ")
List<Users> findAllByParentName(String s);
```

예시 가정 3. **Cross 조인 발생!**

```
select users0_.id as id1_1_, 
        users0_.age as age2_1_,
        users0_.name as name3_1_,
        users0_.parent_id as parent_i4_1_
        
from users users0_ 
cross join parent parent1_

where users0_.parent_id=parent1_.id
and parent1_.name=?SQL
```
