파이썬은 자바와 마찬가지로 인터프리터를 사용한다.

![[Python Compile 과정.png]]

python은 C언어로 구현되었다는 얘기를 들어보았을 것이다.
파이썬은 cpython, jython, pypy 등의 구현체를 사용한다.

1차적으로 인터프리터를 통해 Python Script로 작성한 코드는 Byte Code로 변환된다. 
그다음 가상환경(Virtual Machine)에 의해 Machine Language로 변경된다.

결과적으로
**Python Script(.py) -> Byte Code(.cpy) -> Machine Language** 의 과정