## Key  

검색, 정렬 시 Tuple을 구분할 수 있는 기준이 되는 Attribute

###  1. Candidate Key 후보키

  -> Tuple을 유일하게 식별하기 위해 사용하는 속성들의 부분 집합 (기본키로 사용할 수 있는 속성들)

 -> 다음 2가지 조건을 만족

- 유일성 : Key로 하나의 Tuple을 유일하게 식별할 수 있음
- 최소성 : 꼭 필요한 속성으로만 구성

### 2. Primary Key 기본키 

 -> 후보키 중 선택한 Main Key. Null 값을 가질 수 없으며 동일한 값이 중복될 수 없다

### 3. Alternate Key 대체키

 -> 후보키 중 기본키를 제외한 나머지 키 = 보조키

### 4. Super Key  

 -> 유일성은 만족하지만 최소성은 만족하지 못하는 키

---

## Join

 -> 두 개 이상의 테이블이나 데이터베이스를 연결하여 데이터를 검색하는 방법
 -> 관계형 데이터베이스는 서로 관계있는 데이터가 여러 테이블로 나뉘어 저장되므로, 각 테이블에 저장된 데이터를 효과적으로 검색하기 위해 조인이 필요하다.

* INNER JOIN : 교집합으로, 기준 테이블과 join 테이블의 중복된 값을 보여준다.

  ```sql
  SELECT *
  FROM employee INNER JOIN department
  ON employee.DepartmentID = department.DepartmentID;
  ```

  

* LEFT OUTER JOIN : 오른쪽 테이블에 조인할 칼럼의 값이 없는 경우. 왼쪽 테이블의 모든 데이터를 포함하는 결과 집합을 생성한다. (왼쪽 테이블 기준 JOIN)

  ```sql
  SELECT *
  FROM employee LEFT OUTER JOIN department
  ON employee.DepartmentID = department.DepartmentID;
  ```

* RIGHT OUTER JOIN : 왼쪽 테이블에 조인할 칼럼의 값이 없는 경우에 사용한다. 오른쪽 테이블의 모든 데이터를 포함하는 결과 집합을 생성 (오른쪽 테이블 기준 JOIN)

  ```sql
  SELECT *
  FROM employee RIGHT OUTER JOIN department
  ON employee.DepartmentID = department.DepartmentID;
  ```

* FULL OUTER JOIN : 합집합을 말한다. 왼쪽과 오른쪽 테이블의 모든 데이터가 검색된다. 

  ```sql
  SELECT *
  FROM employee FULL OUTER JOIN department
  ON employee.DepartmentID = department.DepartmentID;
  ```

* CROSS JOIN : 조인되는 두 테이블에서 곱집합을 반환한다. 

  ```sql
  SELECT * 
  FROM employee 
  CROSS JOIN department;
  ```

* SELF JOIN : 한 테이블에서 자기 자신에 조인을 시키는 것이다. 

----

## SQL Injection

해커에 의해 조작된 SQL 쿼리문이 데이터베이스에 그대로 전달되어 비정상적 명령을 실행시키는 공격 기법

### 공격 방법

1. 인증 우회 : 로그인할 때 input 창에 비밀번호를 입력함과 동시에 다른 쿼리문을 함께 입력

2. 데이터 노출 : 시스템에서 발생하는 에러 메시지를 해킹에 활용

### 방어 방법

1. input 값을 받을 때 검증 로직을 추가하여 미리 설정한 특수문자들이 들어왔을 때 요청을 막아낸다.
2. SQL 서버 오류 발생 시, 해당하는 에러 메시지를 감춘다.
3. preparestatement 사용하기

---

## SQL과 NoSQL 차이

* 스키가마 없다. 즉 데이터 관계와 정해진 규격(table-column의 정의)이 없다.
* 관계 정의가 없어 Join이 불가능하다.
* 트랜잭션을 지원하지 않는다.
* 분산처리(수평적 확장)의 기능을 쉽게 제공한다.

---

## 이상 (Anomaly)

정규화를 해야 하는 이유는 잘못된 테이블 설계로 인해 Anomaly (이상 현상)가 나타나기 때문이다.

### 1. 삽입 이상

원하지 않는 자료가 삽입된다든지, 삽입하는데 자료가 부족해 삽입이 되지 않아 발생하는 문제점을 말한다. (불필요한 데이터를 추가해야지 삽입할 수 있는 상황)

### 2. 갱신 이상

정확하지 않거나 일부의 튜플만 갱신되어 정보가 모호해지거나 일관성이 없어져 정확한 정보 파악이 되지 않는 문제점을 말한다. (일부만 변경하여, 데이터가 불일치하는 모순의 문제)

### 3. 삭제 이상

하나의 자룜나 삭제하고 싶지만, 그 자료가 포함된 튜플 전체가 삭제됨으로 원하지 않는 정보 손실이 발생하는 문제점을 말한다. (튜플 삭제로 인해 꼭 필요한 데이터까지 함께 삭제되는 문제)

---

## Index

* 데이터베이스에서 검색 속도를 높이기 위한 기술을 말한다. 
* Table의 Column을 색인화한다. 
  -> 해당 Table의 Record를 Full Scan하지 않음 
  -> 색인화 된 (B+ Tree 구조로) Index 파일 검색으로 검색 속도 향상   
* 인덱스는 항상 정렬된 상태를 유지하기 때문에 원하는 값을 탐색하는데는 빠르지만 새로운 값을 추가하거나 삭제, 수정하는 경우에는 쿼리문 실행 속도가 느려진다.

---

## Transaction

* 데이터베이스의 상태를 변화시키는 하나의 논리적인 작업 단위를 구성하는 연산들의 집합

* 하나의 트랜잭션은 Commit 되거나 Rollback 된다.
  * Commit : 하나의 트랜잭션이 성공적으로 끝났고, DB가 일관성있는 상태일 때 이를 트랜잭션 관리자에게 알려주기 위해 사용하는 연산
  * Rollback : 하나의 트랜잭션 처리가 비정상적으로 종료되어 데이터베이스의 일관성을 깨뜨렸을 때, 이 트랜잭션의 일부가 정상적으로 처리되었더라도 트랜잭션의 원자성을 구현하기 위해 이 트랜잭션이 행한 모든 연산을 취소(Undo)하는 연산

### 트랜잭션의 특징

* 원자성 (Atomicity) : 트랜잭션이 DB에 모두 반영되거나, 혹은 전혀 반영되지 않아야 된다.
* 일관성 (Consistency) : 트랜잭션 완료 후에도 데이터베이스가 일관된 상태료 유지되어야 한다.
* 독립성 (Isolation) : 각각의 트랜잭션은 서로 간섭없이 독립적으로 수행되어야 한다.
* 지속성 (Durability) : 트랜잭션이 성공적으로 완료되었으면, 그 결과는 영구적으로 반영되어야 한다.

### 트랜잭션의 상태

![transaction-status](C:\Users\ymink\OneDrive\바탕 화면\transaction-status.png)

* Active  : 트랜잭션이 실행 중에 있는 상태, 연산들이 정상적으로 실행 중인 상태
* Failed : 트랜잭션 실행에 오류가 발생하여 중단된 상태
* Aborted : 트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태
* Partially Committed : 트랜잭션이 마지막 연산까지 실행했지만, Commit  연산이 실행되기 직전의 상태
* Committed : 트랜잭션이 성공적으로 종료되어 Commit 연산을 실행한 후의 상태

---

## 트랜잭션 격리 수준 (Transaction Isolation Level)

트랜잭션에서 일관성 없는 데이터를 허용하도록 하는 수준

### Isolation Level의 필요성

데이터베이스는 ACID 특징과 같이 트랜잭션이 독립적인 수행을 하도록 한다. 

따라서 Locking을 통해 트랜잭션이 DB를 다루는 동안 다른 트랜잭션이 관여햐지 못하도록 막는 것이 필요하다. 

하지만 무조건 Locking으로 동시에 수행되는 수많은 트랜잭션들을 순서대로 처리하는 방식으로 구현하게 되면 데이터베이스의 성능은 떨어지게 될 것이다. 

그렇다고 해서, 성능을 높이기 위해 Locking의 범위를 줄인다면 잘못된 값이 처리될 문제가 발생하게 된다.

따라서 최대한 효율적인 Locking 방법이 필요

### Isolation Level 종류

1. Read Uncommitted (레벨 0)

   - SELECT 문장이 수행되는 동안 해당 데이터에 Shared Lock이 걸리지 않는 계층

   - 트랜잭션이 처리중이거나 아직 Commit되지 않은 데이터를 다른 트랜잭션이 읽는 것을 허용함
   - 데이터베이스의 일관성을 유지하는 것이 불가능

2. Read Committed (레벨 1)

   * SELECT 문장이 수행되는 동안 해당 데이터에 Shared Lock이 걸리는 계층
   * 트랜잭션이 수행되는 동안 다른 트랜잭션이 접근할 수 없어 대기하게 됨
   * Commit이 이루어진 트랜잭션만 조회 가능
   * SQL 서버가 Default로 사용하는 Isolation Level 

3. Repeatable Read (레벨 2)

   * 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 Shared Lock이 걸리는 계층
   * 트랜잭션이 범위 내에서 조회한 데이터 내용이 항상 동일함을 보장함
   * 다른 사용자는 트랜잭션 영역에 해당되는 데이터에 대한 수정 불가능

4. Serializable(레벨 3)

   * 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 Shared Lock이 걸리는 계층
   * 완벽한 읽기 일관성 모드를 제공함
   * 다른 사용자는 트랜잭션 영역에 해당되는 데이터에 대한 수정 및 입력 불가능

### 선택 시 고려사항

* Isolation Level에 대한 조정은 동시성과 데이터 무결성에 연관되어 있음
* 동시성을 증가시키면 데이터 무결성에 문제가 발생하고, 데이터 무결성을 유지하면 동시성이 떨어지게 됨
* 레벨을 높게 조정할수록 발생하는 비용이 증가함

### 낮은 단계 Isolation Level을 활용할 때 발생하는 현상들

* Dirty Read
  * 커밋되지 않은 수정 중인 데이터를 다른 트랜잭션에서 읽을 수 있도록 허용할 때 발생하는 현상
  * 어떤 트랜잭션에서 아직 실행이 끝나지 않은 다른 트랜잭션에 의 한 변경사항을 보게 되는 경우
* Non-Repeatable Read
  * 한 트랜잭션에서 같은 쿼리를 두 번 수행할 때 그 사이에 다른 트랜잭션 값을 수정 또는 삭제하면서 두 쿼리의 결과가 상이하게 나타나는 일관성이 깨진 현상
* Phantom Read
  * 한 트랜잭션 안에서 일정 범위의 레코드를 두 번 이상 읽었을 때, 첫 번째 쿼리에서 없단 레코드가 두 번째 쿼리에서 나타나는 현상
  * 트랜잭션 도중 새로운 레코드 삽입을 허용하기 때문에 나타나는 현상임

---

## Redis

* 인 메모리 캐시 서버
* 메모리(RAM)에 저장해서 디스크 스캐닝이 필요없어 매우 빠름
* 캐싱이 가능해 실시간 채팅에 적합하며 세션 공유를 위한 세션 클러스터링에도 활용된다.
* 백업 과정
  * snapshot : 특정 지점을 설정하고 디스크에 백업
  * AOF(Append Only File) : 명령(쿼리)들을 저장해두고 서버가 셧다운되면 재실행해서 다시 만들어 놓는 것
* 데이터 구조는 key/value 형식으로 이루어져 있다. 

---

정규화

샤딩

교착상태

---

참고 : 
https://gyoogle.dev/blog/computer-science/data-base/Key.html
https://github.com/WeareSoft/tech-interview/blob/master/contents/db.md
https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Database
https://91ms.tistory.com/2?category=711086

