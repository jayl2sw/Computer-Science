# Python

> 작성자: 이재준

* [GIL (Global Interpreter Lock)](#GIL-(Global-Interpreter-Lock))



---

## GIL (Global Interpreter Lock)

**정의**

* 파이썬 인터프리터가 한 스레드만 하나의 바이트 코드를 실핼시킬 수 있도록 하는 Lock
* 하나의 스레드에 모든 자원을 허락하고 그동안 나머지에는 Lock을 걸어 다른 스레드는 실행할 수 없게 한다.



아래 그림은 Python에서 3개의 스레드가 동작하는 예시이다.

각각의 스레드는 GIL을 얻고 동작하며 이 때 해당 스레드를 제외한 나머지 스레드는 동작을 멈추게된다. 이 경우 thread context switch를 위한 비용이 발생되기 때문에 오히려 싱글 스레드 대비 성능이 저하된다.

![img](https://blog.kakaocdn.net/dn/bAMe0O/btqHOZLSxjm/g3KOLQOBuZAFZQ5tz5OrK0/img.png)

**GIL의 사용 이유**

Python의 메모리 관리는 Garbage Collection과 Reference Counting을 이용해 이루어진다. 따라서 파이썬의 모든 객체는 해당 변수가 참조된 수인 reference count를 저장하고 있다. 하지만 멀티 스레드인 경우 여러 스레드가 하나의 객체를 사용한다면 reference count의 관리가 어려워지고 Python은 GIL을 사용하여 모든 객체들에 대한 reference count의 동기화 문제를 해결.



**Python의 멀티스레딩**

Sleep이나 wait 등과 같이 대기하는 상황일 때 multi threading을 이용하면 한개의 쓰레드가 대기 중인 동안 다른 쓰레드가 동작하면서 성능 개선이 일어난다.

