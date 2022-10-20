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

* 컴파일 언어는 **원시코드**(프로그래머가 작성한 소스코드) **전체를 모두 기계어로 변환**한 후에 CPU/메모리를 통해 코드를 실행
* 런타임 시점에는 컴파일 없이, 실행만 하면 되므로 **코드 실행 속도 빠름**

##### Interpreter

* 원시코드(프로그래머가 작성한 소스코드)를 기계어로 변환하는 과정없이 **한줄 한줄 해석하여 바로 명령어를 실행하는 언어**.
* 인터프리터가 직접 한 줄씩 읽고 따로 기계어로 변환하지 않기 때문에 **빌드 시간이 없다**.  
* Runtime 상황에서 한 줄씩 실시간으로 읽어서 실행하기 때문에 **컴파일 언어에 비해 속도가 느림**.
* 인터프리터만 있다면 실행 가능하기 때문에 **플랫폼에 독립적**이다.



### JVM의 구조

![image](https://user-images.githubusercontent.com/97587245/196827826-374a6cd5-354c-488a-bb9f-83bafc9e0545.png)

#### Class Loader

* 한 번에 메모리에 모든 클래스를 로드하는 것이 아닌, 필요한 순간에 해당 클래스(.class) 파일을 찾아 메모리에 로딩해주는 역할

#### Execution Engine

* `Interpreter` 

  * 자바 컴파일러에 의해 변환된 바이트 코드를 읽고 한 줄씩 기계어로 해석하는 역할	

* `JIT 컴파일러(Just-In Time compiler)` 

  * 런타임 중에 중복 호출되는 메소드들을 캐싱하여 컴파일하는 역할
  * 해당 메소드들이 여러 번 호출할 때 매번 해석하는 것을 방지

* `Garbage Collector`

  * 메모리 관리

    

#### Runtime Data Areas

* JVM이 프로그램을 수행하기 위해 OS로부터 할당받는 메모리 영역



### Stack 영역 vs Heap 영역

#### Stack 영역

* 함수의 호출과 관계되는 지역  변수와 매개 변수가 저장되는 영역
* stack 영역은 함수의 호출과 함께 할당되며, 함수의 호출이 완료되면 소멸.
* 푸시(push)으로 데이터를 저장하고 팝(pop)으로 데이터 반출
* LIFO (Last-In, First-Out) 방식에 따라 동작

* 장점
  * 빠른 액세스
  * 변수의 명시적 할당 해제 X
* 단점
  * 지역 변수만 가능
  * 변수 크기 조정 불가 (컴파일 타임에 크기가 결정)

#### Heap 영역

* 사용자가 직접 관리 하는 메모리 영역
* 사용자에 의해 메모리 공간의 동적 할당 및 해제
  * Java, C#등은 카비지 컬렉터(GC)가 수거함
* 데이터를 항상 유지하고 싶을 때 사용
* 장점
  * 전역 변수
  * 메모리 크기 제한 X
  * 메모리 크기를 동적으로 변경할 수 있다. (런타임에 크기가 결정)
* 단점
  * 느린 액세스
  * 효율적인 공간 사용이 불가능할 때, 메모리가 조각화 되어 해제 될 수 있음
  * 메모리 관리 필수적

#### Stack Overflow, Heap Overflow

* 스택은 메모리의 끝에서부터, 힙은 메모리의 앞에서부터 주소를 채워간다.
* `Stack Overflow` : 스택이 넘쳐 힙을 침범할 경우
* `Heap Overflow` : 힙이 넘쳐 스택을 침범할 경우

### JVM의 역할

* `JVM(Java Virtual Machine)` : 자바 프로그램의 실행하기 위해 물리적 머신과 유사하게 소프트웨어로 구현한 것. 
* 자바 애플리케이션을 Class Loader를 통해 읽어 들여 자바 API와 함께 실행하는 것. 
* JVM은 JAVA와 OS사이에서 중개자 역할을 수행하여 JAVA가 OS에 구애받지 않고 재사용을 가능하게 해준다. 
* 메모리관리, Garbage collection을 수행.

`Garbage Collection` 의 동작 방식

1. Stop The World

   * GC를 실행하는 쓰레드를 제외한 모든 쓰레드들의 작업 중단

2. Mark & Sweep

   * Mark : 메모리의 사용여부 판별
   * Sweep : Mark 단계에서 사용되지 않다고 판별된 메모리를 해제

   

#### 

### Java의 접근 제어자의 종류와 특징

* default
* public
* private
* protected



### OOP(Object-Oriented Programming)의 4가지 특징

#### 추상화(Abstraction)

#### 캡슐화(Capsulation)

#### 상속(Inheritance)

#### 다형성(Polymorphism)



### OOP의 5대 원칙 (SOLID)

### Interface vs Abstract class

### Call by Reference vs Call by Value

##### 그렇다면 Java는?



### Overloading vs Overriding

두 가지 모두 OOP의 다형성과 관련된 용어.

#### Overloading

#### Overriding



---

## Python

