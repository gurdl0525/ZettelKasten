파이썬은 인터프리터를 실행할 때 몇가지 global 변수를 갖는다.

이중 하나가 바로 \_\_name\_\_인 것이다.

파이썬 파일은 모듈을 호출하는데 `.py` 파일 확장자에 의해 식별된다.
만약 인터프리터가 직접 실행한다면 \_\_name\_\_ 변수는 \_ \_ main\_\_  으로 설정된다.

하지만 코드가 `.py` 파일로부터 실행이 됐다면 \_\_name\_\_ 변수는 그 모듈의 이름대로 설정될 것이다.

예를 들어 example.py가 있을 때
```python
# example.py
def out():
	print(__name__)

if __name__ == '__main__':
	out()
```

직접 인터프리터로 example.py를 실행한다면 아래와 같은 output이 나올 것이다.
```
__main__
```

하지만 여기서 example2.py를 정의 해보자.
```python
# example2.py
import example

if __name__ == '__main__':
	example.out()
```
example2.py는 example.py의 out을 호출하고 있다.

이를 실행해보면 다음과 같은 output을 받을 수 있다.
```
example
```