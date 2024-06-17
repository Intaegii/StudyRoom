
### 트랜잭션이란
* 트랜잭션(Transaction) 이란
    * 데이터베이스의 상태를 변환시키는 하나의 논리적인 작업 단위를 구성하는 연산들의 집합이다.
        * 예를들어, A계좌에서 B계좌로 일정 금액을 이체한다고 가정하자.
          1. A계좌의 잔액을 확인한다.
          2. A계좌의 금액에서 이체할 금액을 빼고 다시 저장한다.
          3. B계좌의 잔액을 확인한다.
          4. B계좌의 금액에서 이체할 금액을 더하고 다시 저장한다.
        * 이러한 과정들이 모두 합쳐져 계좌이체라는 하나의 작업단위를 구성한다.
    * 하나의 트랜잭션은 Commit 되거나 Rollback 된다.
        * Commit 연산
            * 한개의 논리적 단위(트랜잭션)에 대한 작업이 성공적으로 끝나 데이터베이스가 다시 일관된 상태에 있을 때, 이 트랜잭션이 행한 갱신 연산이 완료된 것을 트랜잭션 관리자에게 알려주는 연산이다.
        * Rollback 연산
            * 하나의 트랜잭션 처리가 비정상적으로 종료되어 데이터베이스의 일관성을 깨뜨렸을 때, 이 트랜잭션의 일부가 정상적으로 처리되었더라도 트랜잭션의 원자성을 구현하기 위해 이 트랜잭션이 행한 모든 연산을 취소(Undo)하는 연산이다.
            * Rollback 시에는 해당 트랜잭션을 재시작하거나 폐기한다.
    * 데이터베이스 응용 프로그램은 트랜잭션들의 집합으로 정의 할 수 있다.
* 트랜잭션의 성질(ACID)
    * 원자성(Atomicity), All or nothing
        * 트랜잭션의 모든 연산들은 정상적으로 수행 완료되거나 아니면 전혀 어떠한 연산도 수행되지 않은 상태를 보장해야 한다.
    * 일관성(Consistency)
        * 트랜잭션 완료 후에도 데이터베이스가 일관된 상태로 유지되어야 한다.
    * 독립성(Isolation)
        * 하나의 트랜잭션이 실행하는 도중에 변경한 데이터는 이 트랜잭션이 완료될 때까지 다른 트랜잭션이 참조하지 못한다.
    * 지속성(Durability)
        * 성공적으로 수행된 트랜잭션은 영원히 반영되어야 한다.
* 트랜잭션의 필요성
    * 현금 인출기를 작동하는 도중에 기계오류나 정전 등과 같은 예기치 않은 상황이 발생하여 카드가 나오지 않거나 기계가 멈추는 경우
    * 각각 다른 지점의 은행에서 동시에 인출할 때, 하나의 지점이 다른 지점에서 저장한 잔액을 덮어 쓰는 경우
    * 위와 같은 상황이 발생되지 않도록 방지하기 위해, 즉, 트랜잭션의 성질인 ACID를 제공받기위해 트랜잭션을 사용한다.
* 트랜잭션의 상태  
    <img src="./images/transaction-status.png" width="70%" height="70%">
    * 활동(Active)
        * 트랜잭션이 실행 중에 있는 상태, 연산들이 정상적으로 실행 중인 상태
    * 장애(Failed)
        * 트랜잭션이 실행에 오류가 발생하여 중단된 상태
    * 철회(Aborted)
        * 트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태
    * 부분 완료(Partially Committed)
        * 트랜잭션이 마지막 연산까지 실행했지만, Commit 연산이 실행되기 직전의 상태
    * 완료(Committed)
        * 트랜잭션이 성공적으로 종료되어 Commit 연산을 실행한 후의 상태

> :arrow_double_up:[Top](#4-database)    :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#4-database)    :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)
> - [http://limkydev.tistory.com/100](http://limkydev.tistory.com/100)
> - [http://coding-factory.tistory.com/226](http://coding-factory.tistory.com/226)
> - [http://yimoyimo.tk/transaction_DI/](http://yimoyimo.tk/transaction_DI/)
> - [https://d2.naver.com/helloworld/407507](https://d2.naver.com/helloworld/407507)

### 트랜잭션 격리 수준
* Isolation Level 이란?
    * 트랜잭션에서 일관성이 없는 데이터를 허용하도록 하는 수준
* Isolation Level 의 필요성
    * 데이터베이스는 ACID 같이 트랜잭션이 원자적이면서도 독립적인 수행을 하도록 한다.
    * 그래서 Locking 이라는 개념이 등장한다.
        * 트랜잭션이 DB를 다루는 동안 다른 트랜잭션이 관여하지 못하게 막는 것
    * 하지만 무조건적인 Locking으로 동시에 수행되는 많은 트랜잭션들을 순서대로 처리하는 방식으로 구현되면 DB의 성능은 떨어지게 된다.
    * 반대로 응답성을 높이기 위해 Locking 범위를 줄인다면 잘못된 값이 처리 될 여지가 있다.
    * 그래서 최대한 효율적인 Locking 방법이 필요하다.
* Isolation Level 의 종류
    1. Read Uncommitted (레벨 0)
        * SELECT 문장이 수행되는 동안 해당 데이터에 Shared Lock이 걸리지 않는 Level
        * 트랜잭션에 처리중인 혹은 아직 커밋되지 않은 데이터를 다른 트랜잭션이 읽는 것을 허용한다.
        * 따라서, 어떤 사용자가 A라는 데이터를 B라는 데이터로 변경하는 동안 다른 사용자는 아직 완료되지 않은(Uncommitted 혹은 Dirty) 트랜잭션이지만 변경된 데이터인 B를 읽을 수 있다.
        * 데이터베이스의 일관성을 유지할 수 없다.
    2. Read Committed (레벨 1)
        * SELECT 문장이 수행되는 동안 해당 데이터에 Shared Lock이 걸리는 Level
        * 트랜잭션이 수행되는 동안 다른 트랜잭션이 접근할 수 없어 대기하게 된다.
        * Commit이 이루어진 트랜잭션만 조회할 수 있다.
        * 따라서, 어떤 사용자가 A라는 데이터를 B라는 데이터로 변경하는 동안 다른 사용자는 해당 데이터에 접근할 수 없다.
        * SQL Server가 Default로 사용하는 Isolation Level
    3. Repeatable Read (레벨 2)
        * 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 Shared Lock이 걸리는 Level
        * 트랜잭션이 범위 내에서 조회한 데이터의 내용이 항상 동일함을 보장한다.
        * 따라서, 다른 사용자는 그 영역에 해당되는 데이터에 대한 수정이 불가능하다.
    4. Serializable (레벨 3)
        * 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 Shared Lock이 걸리는 Level
        * 완벽한 읽기 일관성 모드를 제공한다.
        * 따라서, 다른 사용자는 그 영역에 해당되는 데이터에 대한 수정 및 입력이 불가능하다.
    * Isolation level 조정은 동시성이 증가되는데 반해 데이터 무결성에 문제가 발생할 수 있고, 데이터의 무결성을 유지하는 데 반해 동시성이 떨어질 수 있다.
    * 레벨이 높아질수록 비용이 높아진다.
* 낮은 단계의 Isolation Level 이용시 발생하는 현상  
    <img src="./images/isolation-level.png" width="70%" height="70%">
    * Dirty Read
        * 커밋되지 않은 수정 중인 데이터를 다른 트랜잭션에서 읽을 수 있도록 허용할 때 발생하는 현상
        * 어떤 트랜잭션에서 아직 실행이 끝난지 않은 다른 트랜잭션에 의한 변경 사항을 보게 되는 되는 경우
    * Non-Repeatable Read
        * 한 트랜잭션에서 같은 쿼리를 두 번 수행할 때 그 사이에 다른 트랜잭션이 값을 수정 또는 삭제함으로써 두 쿼리의 결과가 상이하게 나타나는 비 일관성 현상
    * Phantom Read
        * 한 트랜잭션 안에서 일정 범위의 레코드를 두 번 이상 읽을 때, 첫 번째 쿼리에서 없던 레코드가 두 번째 쿼리에서 나타나는 현상
        * 이는 트랜잭션 도중 새로운 레코드가 삽입되는 것을 허용하기 때문에 나타난다.

> :arrow_double_up:[Top](#4-database)    :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#4-database)    :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)
> - [http://hundredin.net/2012/07/26/isolation-level/](http://hundredin.net/2012/07/26/isolation-level/)
> - [http://egloos.zum.com/ljlave/v/1530887](http://egloos.zum.com/ljlave/v/1530887)

### Join
* 조인이란
    * **한 데이터베이스 내의 여러 테이블의 레코드를 조합하여 하나의 열로 표현한 것**이다.
    * 따라서 조인은 테이블로서 저장되거나, 그 자체로 이용할 수 있는 결과 셋을 만들어 낸다.
* 조인의 필요성
    * 관계형 데이터베이스의 구조적 특징으로 정규화를 수행하면 의미 있는 데이터의 집합으로 테이블이 구성되고, 각 테이블끼리는 관계(Relationship)를 갖게 된다. 
    * 이와 같은 특징으로 관계형 데이터베이스는 저장 공간의 효율성과 확장성이 향상되게 된다.
    * 다른 한편으로는 서로 관계있는 데이터가 여러 테이블로 나뉘어 저장되므로, 각 테이블에 저장된 데이터를 효과적으로 검색하기 위해 조인이 필요하다.

<img src="./images/join-table.png" width="70%" height="70%">

* 조인의 종류
    1. **내부 조인(INNER JOIN)**
        * 여러 애플리케이션에서 사용되는 가장 흔한 결합 방식이며, 기본 조인 형식으로 간주된다.
        * 내부 조인은 조인 구문에 기반한 2개의 테이블(A, B)의 컬럼 값을 결합함으로써 새로운 결과 테이블을 생성한다.
        * **명시적 조인 표현**(explicit)과 **암시적 조인 표현**(implicit) 2개의 다른 조인식 구문이 있다.
        * 명시적 조인 표현
            * 테이블에 조인을 하라는 것을 지정하기 위해 JOIN 키워드를 사용하며, 그리고 나서 다음의 예제와 같이 ON 키워드를 조인에 대한 구문을 지정하는데 사용한다.
                ```sql
                SELECT *
                FROM employee INNER JOIN department
                ON employee.DepartmentID = department.DepartmentID;
                ```
        * 암시적 조인 표현
            * SELECT 구문의 FROM 절에서 그것들을 분리하는 컴마를 사용해서 단순히 조인을 위한 여러 테이블을 나열하기만 한다.
                ```sql
                SELECT *
                FROM employee, department
                WHERE employee.DepartmentID = department.DepartmentID;
                ```
        * 결과  
            <img src="./images/inner-join.png" width="70%" height="70%">
        1. **동등 조인(EQUI JOIN)**
            * 비교자 기반의 조인이며, 조인 구문에서 **동등비교만을 사용**한다.
            * 다른 비교 연산자(<와 같은)를 사용하는 것은 동등 조인으로서의 조인의 자격을 박탈하는 것이다.
        2. **자연 조인(NATURAL JOIN)**
            * 동등 조인의 한 유형으로 조인 구문이 조인된 테이블에서 동일한 컬럼명을 가진 2개의 테이블에서 모든 컬럼들을 비교함으로써, 암시적으로 일어나는 구문이다.
            * 결과적으로 나온 조인된 테이블은 동일한 이름을 가진 컬럼의 각 쌍에 대한 단 하나의 컬럼만 포함하고 있다.
            * SQL
                ```sql
                SELECT * FROM employee NATURAL JOIN department;
                ```
            * 결과  
                <img src="./images/natural-join.png" width="50%" height="50%">
        3. **교차 조인(CROSS JOIN)**
            * 조인되는 두 테이블에서 곱집합을 반환한다. 
            * 즉, 두 번째 테이블로부터 각 행과 첫 번째 테이블에서 각 행이 한번씩 결합된 열을 만들 것이다.
            * 예를 들어 m행을 가진 테이블과 n행을 가진 테이블이 교차 조인되면 m*n 개의 행을 생성한다
            * 명시적 조인 표현
                ```sql
                SELECT * FROM employee CROSS JOIN department;
                ```
            * 암시적 조인 표현
                ```sql
                SELECT * FROM employee, department;
                ```
            * 결과  
                <img src="./images/cross-join.png" width="70%" height="70%">
    2. **외부 조인(OUTER JOIN)**
        * 조인 대상 테이블에서 특정 테이블의 데이터가 모두 필요한 상황에서 외부 조인을 활용하여 효과적으로 결과 집합을 생성할 수 있다.
        1. **왼쪽 외부 조인(LEFT OUTER JOIN)**
            * 우측 테이블에 조인할 컬럼의 값이 없는 경우 사용한다.
            * 즉, 좌측 테이블의 모든 데이터를 포함하는 결과 집합을 생성한다.
            * SQL
                ```sql
                SELECT *
                FROM employee LEFT OUTER JOIN department
                ON employee.DepartmentID = department.DepartmentID;
                ```
            * 결과  
                <img src="./images/left-outer-join.png" width="70%" height="70%">
        2. **오른쪽 외부 조인(RIGHT OUTER JOIN)**
            * 좌측 테이블에 조인할 컬럼의 값이 없는 경우 사용한다.
            * 즉, 우측 테이블의 모든 데이터를 포함하는 결과 집합을 생성한다.
            * SQL
                ```sql
                SELECT *
                FROM employee RIGHT OUTER JOIN department
                ON employee.DepartmentID = department.DepartmentID;
                ```
            * 결과  
                <img src="./images/right-outer-join.png" width="70%" height="70%">
        3. **완전 외부 조인(FULL OUTER JOIN)**
            * 양쪽 테이블 모두 OUTER JOIN이 필요할 때 사용한다.
            * SQL
                ```sql
                SELECT *
                FROM employee FULL OUTER JOIN department
                ON employee.DepartmentID = department.DepartmentID;
                ```
            * 결과  
                <img src="./images/full-outer-join.png" width="70%" height="70%">
    3. **셀프 조인(SELF JOIN)**
        * 한 테이블에서 자기 자신에 조인을 시키는 것이다.
* 조인을 사용할 때 주의사항
    * SQL 문장의 의미를 제대로 파악
        * SQL을 어떻게 작성하느냐에 따라 성능이 크게 좌우된다. 어떤 질의를 수행할 것인지를 명확하게 정의한 후, 비효율을 제거하여 최적의 SQL을 작성해야 한다.
    * 명확한 조인 조건 제공
        * 조인 조건을 명확하게 제공하지 않을 경우, 의도치 않게 CROSS JOIN(Cartesian Product)이 수행될 수 있다.
* 조인을 사용할 때 고려사항
    * 조인할 대상의 집합을 최소화
        * 집합을 최소화할 방법이 있으면, 조건을 먼저 적용하여 관계를 맺을 집합을 최소화한 후, 조인을 맺는 것이 효율적이다.
    * 효과적인 인덱스의 활용
        * 인덱스를 활용하면, 조인 연산의 비용을 극적으로 낮출 수 있다.
