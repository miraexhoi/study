# SQL 인젝션 (SQL Injection)

SQL 인젝션은 웹 애플리케이션에서 **사용자의 입력값이 SQL 쿼리에 안전하게 처리되지 않을 때 발생하는 보안 취약점**이다.  
공격자는 **이 취약점을 이용해 쿼리를 조작하여 인증을 우회하거나, 데이터를 조작하거나, 테이블 자체를 삭제할 수도** 있다.  

예를 들어, 로그인 검증 시 아래와 같은 코드를 사용한다고 가정해 보자.

```java
public boolean login(String username, String password) {
    String sql = "SELECT * FROM users WHERE username = '" + username + "' AND password = '" + password + "'";

    try (Connection conn = DriverManager.getConnection("url");
         Statement stmt = conn.createStatement();
         ResultSet rs = stmt.executeQuery(sql)) {
        return rs.next();
    } catch (SQLException e) {
        throw new RuntimeException("Database error", e);
    }
}
```

사용자가 로그인 폼에 아래와 같이 입력한다면

```sql
username: admin' -- 
password: (아무거나)
```
생성되는 쿼리는 다음과 같이 변형된다.
```sql
SELECT * FROM users WHERE username = 'admin' -- ' AND password = '1q2w3e4r!';
```
-- 이후는 주석 처리되므로, 비밀번호 조건은 무시되어 admin 사용자에 대한 정보가 반환된다.  
이처럼 공격자는 SQL 쿼리를 조작하여 인증을 우회하거나 데이터베이스의 정보를 탈취할 수 있다.  

이 외에도 공격자는 다음과 같은 페이로드를 사용할 수 있다.
- `' OR '1'='1` : 항상 참이 되는 조건
- `' UNION SELECT * FROM accounts --` : 다른 테이블의 정보 조회
- `'; DROP TABLE users; --` : 테이블 삭제

### SQL 인젝션을 방지하는 방법은 무엇일까?
1. PreparedStatement를 사용하면 place holder(?)에 값을 바인딩하고 내부적으로 이스케이프 처리하기에 SQL 인젝션을 방지할 수 있다.  
  ```sql
  String sql = "SELECT * FROM users WHERE username = ? AND password = ?";
  PreparedStatement pstmt = conn.prepareStatement(sql);
  pstmt.setString(1, username);
  pstmt.setString(2, password);
  ```
2. JPA, Hibernate와 같은 ORM 프레임워크를 사용하면 SQL 쿼리를 직접 작성하지 않고도 데이터베이스와 상호작용할 수 있다.
3. 사용자 입력에 대해 공격에 사용되는 SQL 구문의 포함 여부를 검증한다.
4. 웹 애플리케이션에서 사용하는 데이터베이스 계정에 최소한의 권한만 부여한다.
5. SQL 오류나 예외 메시지를 사용자에게 직접 노출하지 않도록 한다.
