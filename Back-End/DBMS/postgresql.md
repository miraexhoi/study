# PostgreSQL

> 오픈소스 객체-관계형 데이터베이스 관리 시스템(**ORDBMS**)으로, 데이터 무결성과 확장성을 강조하며 다양한 고급 기능을 제공한다.

### 주요 특징

### 1. **SQL 표준 준수**
- ANSI SQL 표준을 대부분 지원하며, 고급 쿼리 기능을 제공
- 복잡한 데이터 처리 및 트랜잭션 관리에 강점

### 2. **확장성**
- 사용자 정의 함수, 자료형, 연산자를 지원
- **JSON/JSONB**와 같은 비정형 데이터 처리 가능
- 다양한 확장(Extensions)을 통해 기능 추가 가능 (예: PostGIS, pg_stat_statements)

### 3. **ACID 준수**
- 트랜잭션의 **원자성(Atomicity)**, **일관성(Consistency)**, **고립성(Isolation)**, **내구성(Durability)** 보장
- 고성능 애플리케이션에서 신뢰할 수 있는 데이터 저장 가능

### 4. **MVCC (다중 버전 동시성 제어)**
- 다중 사용자가 동시에 데이터베이스에 접근해도 일관성을 유지
- **락(Lock)** 사용을 최소화하여 성능 향상

### 5. **플랫폼 독립성**
- 다양한 운영체제에서 동작 (Linux, Windows, macOS 등)
- 클라우드 환경에서도 폭넓게 지원


### 주요 용어 및 개념

### 1. **Database**
PostgreSQL에서 데이터가 저장되는 기본 단위

### 2. **Table**
행(Row)과 열(Column)로 구성된 데이터의 논리적 구조

### 3. **Schema**
데이터베이스 안에서 테이블, 뷰, 함수 등을 그룹화하는 논리적 구조

### 4. **Index**
데이터 검색 속도를 높이기 위한 자료구조 (예: B-Tree, Hash Index)

### 5. **Sequence**
고유한 숫자를 생성하는 객체. 주로 **Primary Key** 생성에 사용

### 6. **JSON/JSONB**
- JSON: 텍스트 기반의 구조화된 데이터 형식
- JSONB: 바이너리 형태로 저장되어 더 빠른 검색 성능 제공


### PostgreSQL의 장점

1. **오픈소스**: 무료로 사용 가능하며, 커뮤니티 지원이 활발
2. **확장 가능한 데이터 유형**: 사용자 정의 데이터 유형 및 범위 데이터 타입 지원
3. **고성능**: 대규모 데이터 처리와 고급 쿼리 최적화 가능
4. **보안**: 다양한 인증 방법과 암호화 지원
5. **복제 및 고가용성**: 스트리밍 복제와 클러스터링 지원


### 기본 명령어

### 1. 데이터베이스 생성 및 접속
```bash
# PostgreSQL 콘솔 접속
psql -U <username> -d <dbname>

# 데이터베이스 생성
CREATE DATABASE <dbname>;

# 데이터베이스 목록 보기
\l
```

### 2. 테이블 생성
```shell
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50),
    email VARCHAR(100),
    created_at TIMESTAMP DEFAULT NOW()
);
```

### 3. 데이터 삽입 및 조회
```shell
-- 데이터 삽입
INSERT INTO users (name, email) VALUES ('Mirae', 'miraexhoi@gmail.com');

-- 데이터 조회
SELECT * FROM users;
```

### 4. 테이블 삭제
```shell
DROP TABLE users;
```
