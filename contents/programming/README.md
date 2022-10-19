# Proramming

## Java

> 작성자: 이재준

### Java의 컴파일 과정

`컴파일(Compile)`: 개발자가 작성한 소스코드를 바이너리 코드로 변환하는 과정.

* ​	자바의 경우 JVM에서 실행 가능한 바이트 코드 형태의 클래스 파일 생성

1. .java 파일의 build진행 

   * `build` : 소스코드 파일을 실행가능한 형태의 SW로 만드는 일련의 과정

2. 컴파일 진행 - java compiler의 javac의 명령어를 통해 바이트코드(.class) 생성

   (이 때 생성된 바이트 코드는 컴퓨터는 읽을 수 없고 JVM만 읽을 수 있는 코드이다.)

3. 컴파일된 바이트 코드를 class loader를 통해 jvm내로 로드

4. class loader가 동적로딩(Dynamic Loading)을 통해 필요한 클래스들을 로딩 및 링크하여 런타임 데이터 영역(JVM의 메모리)에 올림.

5. 실행엔진(Execution Engine)은 JVM 메모리에 올라온 바이트 코드들을 명령어 단위로 하나씩 가져와서 실행.



### Compiler 언어 vs Interpreter 언어

#### 공통점

* 두 언어 모두 고급 프로그래밍 언어(high-level programming language)를 기계어로 번역하여 실행된다.
  * `고급 프로그래밍 언어` : 사람이 쉽게 이해할 수 있도록 작성된 프로그래밍 언어

#### 차이점

##### Compiler

* 

##### Interpreter

* 



#### JVM의 역할



#### JVM의 구조

#### Runtime Data Areas

#### Garbage Collector

#### Class Loader

#### Execution Engine

#### Java의 접근 제어자의 종류와 특징



#### OOP(Object-Oriented Programming)의 4가지 특징

##### 추상화(Abstraction)

##### 캡슐화(Capsulation)

##### 상속(Inheritance)

##### 다형성(Polymorphism)



#### OOp의 5대 원칙 (SOLID)

#### Interface vs Abstract class

#### Call by Reference vs Call by Value

##### 그렇다면 Java는?



#### Overloading vs Overriding

두 가지 모두 OOP의 다형성과 관련된 용어.

##### Overloading

##### Overriding



---

## Python

