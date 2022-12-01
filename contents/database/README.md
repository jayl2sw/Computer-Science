# Database (데이터베이스)

>  작성자: 이재준



**목차**

* [DBMS란?](#DBMS(Database Management System)란?)
* [Transaction의 특징](#Transaction의 특징)
* [RDBMS vs NoSQL](#RDBMS vs NoSQL)
* [데이터베이스 분할 (Partition)](#데이터베이스 분할(Partition))
* [Join의 수행 원리](#Join의 수행 원리)



## DBMS(Database Management System) 란?

데이터 베이스내 데이터에 접근하는 것을 도와주는 시스템
질의 처리기 + 저장 시스템으로 이루어져 있음

## Transaction의 특징 (ACID)

트랜잭션(Transaction) : 데이터 처리의 가장 작은 단위

* 데이터베이스의 무결성과 일관성을 위해 다음과 같은 특징을 가진다.

### 원자성 (Atomicity)

* 트랜잭션의 작업이 부분적으로 실행되거나 중단되지 않는 것을 보장
* All or Nothing, 작업 단위를 일부분만 실행 X

### 일관성 (Consistency)

* 트랜잭션 이후, 데이터베이스의 상태는 이전과 같이 유효

* 트랜잭션이 일어난 이후의 데이터베이스는 데이터베이스의 제약이나 규칙을 만족

### 격리성 (Isolation)

* 모든 트랜잭션은 다른 트랜잭션으로부터 독립적
* 서로에게 영향을 미치지 않음

### 지속성 (Durability)

* 성공적으로 수행된 트랜잭션은 영원히 해당 데이터베이스에 반영됨
* 해당 트랜잭션에 대한 로그가 남음



## RDBMS vs NoSQL

### 차이점

* 가장 큰 차이점은 스키마의 존재 여부와 관계
* `스키마(schema)` : 데이터를 저장하기위한 테이블마다의 규칙

### RDBMS

1. 스키마가 존재해서 정해진 스키마에 따라 데이터를 저장하여야 함
2. Foreign Key를 활용하여 테이블 간의 조인을 통해 데이터를 조회 할 수 있음

### NOSQL (Not Only SQL)

1. 스키마가 없기 때문에 자유료운 데이터구조
2. 테이블 간의 관계를 정의하지 않기 때문에 모든 데이터를 가지고 있어야 함

**장점**

1. 자유로운 데이터 구조
2. 데이터의 조회나 삽입 시 **속도가 더 빠르다**.
3. **데이터 분산이 용이**하며 성능 향상을 위한 **Scale-out 이 가능**

**단점**

1. 데이터 중복이 발생할 수 있으며 중복된 데이터가 변경될 경우 모든 컬렉션에서 수행해야함
2. 스키마가 존재하지 않으므로 명확한 데이터 구조를 보장받지 못함

**종류**

* Key-Value Database (Redis)
  * 데이터가 Key-Value 쌍으로 저장되며 값은 어떤 형태의 데이터이든 가능. 
  * Query 속도가 매우 빠르다.
* Document Database (Mongo DB)
  * Key와 Document의 형태로 저장.
  * Value가 계층적인 형태인 도큐먼트로 저장 => 객체지향에서의 객체와 유사
  * Query 속도가 빠르다.
* Wide Column Database (HBase)
  * Column-family Model 기반의 Database.
  * Key는 (Row, Column-family, Column-name)을 가진다. Key에서 필드를 결정.



## 데이터베이스 분할 (Partition)

한 테이블 내의 데이터의 양이 너무 많은 경우 쿼리의 조회 성능이 저하되거나 테이블의 관리가 어려워 질 때, 쿼리 성능 개선, 관리 용이성, 가용성 향상을 위해 파티셔닝을 통해 문제를 해결할 수 있다.



### Partitioning 

`파티셔닝 (= Vertical Partitioning)`

* 데이터베이스 내 테이블을 컬럼 단위로 나누어 관리하는 기법
* 하나의 Entity를 2개 이상으로 분리

**특징** 

* update나 insert 같은 작업이 분산되어서 성능 향상
* Join 비용이 발생 할 수 있다.
* Index를 별도로 파티셔닝 할 수 없다. => 테이블과 index를 같이 파티셔닝 하여야 한다.

`수평 파티셔닝 (Horizontal Partitioning)`

* 같은 데이터베이스 내에서 레코드 단위로 하나의 큰 테이블을 쪼개어 저장하는 방법



### Sharding
`샤딩 `

* 하나의 큰 테이블을 레코드 단위로 쪼개 각각 다른 DB에 분산하여 저장하는 방법

**특징**

* 데이터의 개수를 기준으로 나누어 파티셔닝
* 인덱스의 개수가 줄어 성능 향상

* 데이터를 찾는 과정이 복잡하므로 Latency 증가



Shard Key를 어떻게 정의하느냐에 따라 데이터를 효율적으로 분산시키는 것이 결정.



#### Hash Sharding
* Database id를 Hashing 하여 결정
* 데이터가 많아지면 Scale-out 하기가 어렵다.
#### Dynamic Sharding
* Dynamic하게 key를 바꿀 수 있다. 
* 확장에 용이하다. Locator Service를 통해 Shard Key



## Join의 수행 원리

### 1. NL(Nested Loops) 조인

**수행 원리**

하나의 테이블(Driving Table)을 기준으로 full-scan 하면서 각 row를 추출할 때마다, 순차적으로 상대 테이블(Driven Table)의 연관된 모든 row들을 조인에 의해 추출한다.

**특징**

1. Index에 의한 Random Access에 기반을 두기 때문에 대용량 데이터 처리시 성능 저하
2. Driving Table로는 row의 수가 적거나, where 절의 조건으로 적절하게 row를 제한할 수 있는 것이어야 함
3. Driven 테이블에는 조인 시 사용할 연결 고리 칼럼에 적절한 Index가 있어야함.
   * 인덱스가 없다면 Driving Table의 각 row마다 join할 때, Driven Table을 full-scan 해야하기 때문에 불리.

**성능 개선 방안**

1. 조인 횟수의 최소화를 위한 조인 순서의 최적화
2. 조인 조건에 대한 인덱스 구성 및 사용

**단점**

인덱스 사용에 따른 Random Access로 인한 오버헤드 발생



### 2. SM(Sort Merge) 조인

**수행 원리**

각 테이블로부터 동시에 독립적으로 데이터를 읽어 들인 후, 기준 column을 대상으로 정렬 작업을 수행한다. 두 테이블의 정렬이 모두 끝나면 조인을 한다.

 **특징**

1. 기준 column에 인덱스가 전혀 없어도 빠른 조인을 수행함
2. where 절의 조건으로 조인 범위를 줄이지 못하는 경우에 효율적임
3. 조인이 되는 두 집합은 모두 정렬되어야 함
4. Random Access가 일어나지 않고 Sorting 작업이 PGA 영역에서만 수행되기 때문에 경합이 발생하지 않음

**성능 개선 방안**

1. 정렬 작업의 속도, 메모리(SORT_AREA_SIZE) 최적화

**사용 용도**

1. Driven Table에 적절한 인덱스가 존재하지 않아 NL Join이 비효율적일때
2. Equal Join이 아닌 범위로 Join을 수행할 때

**단점**

정렬 작업으로 인해 오버헤드가 발생



### 3. Hash 조인

**수행 원리**

Driving Table로 하나를 선택하여 데이터를 먼저 읽어 들인 후, Hashing을 통해 해시 값을 만들어 메모리에 올린다. 다음으로, 조인해야 할 테이블로부터 데이터를 읽어서 hashing을 통해 해시 값을 만든다.  이렇게 생성된 해시 값을 이용하여 조인을 한다.

**특징**

1. 조인을 위해 만든 해시 값을 저장하기 위해 Hash Bucket이 구성되는데, 이를 위해 많은 메모리와 CPU를 필요로 한다.
2. 하드웨어 자원이 넉넉한 상황에서는 다른 조인보다 효율적일 수 있지만, 부족한 상황에서는 오히려 다른 조인보다 비효율적이다.
3. Driven Table의 레코드들을 hashing하여 Driving Table의 레코드에 매칭시켜야 하기 때문에 Equal Join만 가능하다.

**성능 개선 방안**

1. Driving Table을 충분히 작은 것으로 선택하여야 한다.
   * Hash 영역의 사이즈를 초과하게 되면 디스크 영역을 사용하기 때문에 비효율적이다.
2. 각 테이블의 데이터 처리 속도 및 메모리(HASH_AREA_SIZE) 최적화

**사용 용도**

1. 배치작업, 대용량 테이블을 JOIN할 때, 이점을 가진다.



