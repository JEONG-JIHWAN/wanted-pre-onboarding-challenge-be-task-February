1. 관계형 데이터베이스(RDBMS)와 비관계형 데이터베이스(NoSQL)의 장단점 비교

- 관게형 데이터베이스
- 장점
  - 명확한 데이터구조를 보장한다.
  - 각 데이터를 중복 없이 한번만 저장 할 수 있다.
- 단점
  - 시스템이 커질 경우 join문이 많은 복잡한 쿼리가 만들어질 수 있다.
  - 성능 향상을 위해서 서버의 성능을 향상 시켜야하는 scale-up만을 지원한다.
  - 스키마로 인해 데이터가 유연하지 못하다. 나중에 스키마가 변경될 경우 번거롭고 어렵다.
- 비관계형 데이터베이스
- 장점
  - 유연하며 자유로운 데이터 구조를 가질 수 있다.
  - 데이터 분산이 용이하며 성능 향상을 위한 scale-up 뿐만 아니라 scale-out도 가능하다.
- 단점
  - 데이터 중복이 발생할 수 있으며 중복된 데이터가 변경될 경우 수정을 모든 컬렉션에서 수행을 해야한다.
  - 명확한 데이터구조를 보장하지 않으며 데이터 구조 결정이 어려울 수 있다.

2. 트랜잭션(transaction)이란 무엇인가요?

- 트랜잭션이란 하나의 논리적 기능을 수행하기 위한 작업의 단위. 데이터베이스에 접근하는 방법은 쿼리이므로 여러개의 쿼리들을 하나로 묶는 단위라고도 할 수 있다.
- 트랜잭션 내의 모든 작업이 성공해서 데이터베이스에 정상 반영하는 것을 커밋, 작업 중 하나라도 실패해서 이전으로 되돌리는 것을 롤백이라고 한다. 커밋과 롤백으로 인해 데이터의 무결성이 보장된다.

- 트랜잭션은 4가지 특징이 있다.  
- 원자성(Atomicity): 트랜잭션 내에서 실행한 작업들은 모두 성공하거나 모두 실패해야한다.  
- 일관성(Consistency): 모든 트랜잭션은 일관성있는 데이터베이스 상태를 유지해야한다. 예를 들어 데이터베이스에서 정한 무결성 제약 조건을 항상 만족해야한다.  
- 격리성(Isolation): 동시에 실행되는 트랜잭션들이 서로에게 영향을 미치지 않도록 격리한다. 격리성은 동시성과 관련된 성능 이슈로 인해 격리 수준을 선택할 수 있다.  
- 지속성(Durability): 성공적으로 수행된 트랜잭션은 영원히 반영되어야 하는 것을 의미한다. 이는 데이터베이스에 시스템 장애가 발생해도 데이터베이스 로그 등을 사용해서 원래 상태로 복구해야 한다.  

3. MySQL에서 조인(join)의 역할은 무엇인가요? 다양한 join의 방식에 대해 설명해주세요.  
JOIN은 데이터베이스 내의 여러 테이블에서 가져온 레코드들을 조합하여 하나의 테이블로 표현하는 것을 말한다.  
- (INNER) JOIN: 결합 시 두 테이블에서 ON절의 조건에 만족하는 레코드들만 합쳐주는 조인 
- LEFT/RIGHT OUTER JOIN: 기준 테이블들의 레코드들은 모두 출력되며, 조건에 만족하지 않으면 해당 레코드의 기준이 아닌 테이블의 필드값은 모두 NULL로 표시된다. 기준 테이블이 아닌 테이블은 기준 테이블과 공통된 부분의 값에 대해서만 JOIN 작업이 이루어잔다. 
이너 조인과 달리 조인하는 테이블의 순서가 중요하다. 어떤 순서로 테이블을 조인하는지에 따라 결과 테이블에 조회되는 행의 개수며 구성이 달라질 수 있다. 
- FULL OUTER JOIN: 양쪽의 테이블의 모든 레코드들에 대해서 JOIN이 이루어진다. 성능상 거의 사용하지 않는다.  
- CROSS JOIN: 모든 행에 대해 JOIN이 이루어지며, 조인하는 테이블들의 레코드의 곱만큼 조합한다.
- SELF JOIN: 자기 자신과 조인하는 것이다. 

4. MySQL에서 인덱스(index)란 무엇인가요?

- 인덱스란 테이블에서 데이터를 빠르게 찾을 수 있도록 하기 위해 사용된다. 
- MySQL 8.0 기준으로 InnoDB Engine은 spatial indexes를 제외하고 인덱스를 위한 자료구조로 B-tree를 사용한다.
- 인덱스를 사용하면 테이블 전체를 읽지 않아도 되므로, 검색과 질의에 대한 처리가 빠르게 이루어진다. 하지만 인덱스가 설정된 필드 값을 포함한 데이터의 삽입, 삭제, 수정 작업이 원본 테이블에서 이루어질 경우, 인덱스도 함께 수정되어야 한다.
