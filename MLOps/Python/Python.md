파이썬은 자바와 마찬가지로 인터프리터를 사용한다.

![[Python Compile 과정.png]]

python은 C언어로 구현되었다는 얘기를 들어보았을 것이다.
파이썬은 cpython, jython, pypy 등의 구현체를 사용한다.

1차적으로 인터프리터를 통해 Python Script로 작성한 코드는 Byte Code로 변환된다. 
그다음 가상환경(Virtual Machine)에 의해 Machine Language로 변경된다.

결과적으로
**Python Script(.py) -> Byte Code(.cpy) -> Machine Language**의 과정을 거친다.

ByteCode로 변환하는 이유는 자바가 그렇듯 
ByteCode를 VM이 독립적으로 실행하므로써 OS에 제약받지 않는 장점 때문이다.
(Python Script 보다 빠르기 때문이기도 하다.)

Script 형태에서 코드를 실행할 때마다 compile, run과정을 거치므로 C언어에 비해 느린편이다.
이를 해결하기 위해 cpython은 caching을 적용한다고 한다.


---
[[__init__.py]]
[[if __name__ == '__main__']]