# Database (데이터베이스)

>  작성자: 이재준



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

#### RDBMS

1. 스키마가 존재해서 정해진 스키마에 따라 데이터를 저장하여야 함
2. Foreign Key를 활용하여 테이블 간의 조인을 통해 데이터를 조회 할 수 있음

#### NOSQL (Not Only SQL)

1. 스키마가 없기 때문에 자유료운 데이터구조
2. 테이블 간의 관계를 정의하지 않기 때문에 모든 데이터를 가지고 있어야 함

**장점**

1. 자유로운 데이터 구조
2. 데이터의 조회나 삽입 시 **속도가 더 빠르다**.
3. **데이터 분산이 용이**하며 성능 향상을 위한 **Scale-out 이 가능**

**단점**

1. 데이터 중복이 발생할 수 있으며 중복된 데이터가 변경될 경우 모든 컬렉션에서 수행해야함
2. 스키마가 존재하지 않으므로 명확한 데이터 구조를 보장받지 못함

##### 종류

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

## Hbase vs Cassandra

#### 공통점 
* Big Data를 처리하기 위한 분산형 Column-based 데이터베이스.

* Replication을 통해 정합성을 보장하며 linear scalability를 가지고 있다.

  

#### 차이점
##### Cassandra 
* Column형 데이터베이스지만 row key를 인덱스로 갖는 key-value형 데이터베이스이기도 하다.



출처 https://sarc.io/index.php/nosql/174-2014-05-26-13-53-07



## Partitioning 

`파티셔닝 (= Vertical Partitioning)`

* 데이터베이스 내 테이블을 컬럼 단위로 나누어 관리하는 기법
* 하나의 Entity를 2개 이상으로 분리

**특징** 

* update나 insert 같은 작업이 분산되어서 성능 향상
* Join 비용이 발생 할 수 있다.
* Index를 별도로 파티셔닝 할 수 없다. => 테이블과 index를 같이 파티셔닝 하여야 한다.

`수평 파티셔닝 (Horizontal Partitioning)`

* 같은 데이터베이스 내에서 레코드 단위로 하나의 큰 테이블을 쪼개어 저장하는 방법

## Sharding
`샤딩 `

* 하나의 큰 테이블을 레코드 단위로 쪼개 각각 다른 DB에 분산하여 저장하는 방법

**특징**

* 데이터의 개수를 기준으로 나누어 파티셔닝
* 인덱스의 개수가 줄어 성능 향상

* 데이터를 찾는 과정이 복잡하므로 Latency 증가



Shard Key를 어떻게 정의하느냐에 따라 데이터를 효율적으로 분산시키는 것이 결정.

### Hash Sharding
* Database id를 Hashing 하여 결정
* 데이터가 많아지면 Scale-out 하기가 어렵다.
### Dynamic Sharding
* Dynamic하게 key를 바꿀 수 있다. 
* 확장에 용이하다. Locator Service를 통해 Shard Key



## 데이터 무결성

