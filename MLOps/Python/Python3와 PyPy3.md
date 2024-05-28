![[pypy vs python.png]]
**PyPy3 란?**
Python3의 성능 향상을 위해 만들어진 또 다른 파이썬이다.

위 그림(출처: 공식 Docs)에 따르면 평균적으로 PyPy가
CPython(Python 3에 사용된 구조체: 문맥상 Python을 의미)보다 4.8배 빠른 성능을 자랑한다고 한다.

또한 stackless mode를 지원한다고 하며, 대규모 동시성을 위한 micro-thread를 지원한다고 한다.

PyPy가 이러한 성능을 낼 수 있는 이유는 JIT 사용에 있다.

기본적으로 Python도 자바처럼 JIT와 인터프리터를 동시 사용하는 하이브리드 형태임을 알 것이다.
([[Python Compile 방식]] 참고)

하지만 Python은 PyPy와 다르게 인터프리터가 Byte Code로 변환 후 
VM에서 기계어로 변환 할 때만 JIT 컴파일러를 사용한다.

이해하기 어려우니 그림을 보자.
![[python-compile.png]]

.py파일로 작성된 코드를 인터프리터가 Byte 코드로 변환, 
JIT 컴파일러가 VM의 명령어 따라 기계어 코드로 변환해주는 방식이다.



