아래  3개의 Python 파일이 있다고 가정을 할 때
```
rootFolder 
|-- stringLength.py
|-- stringToUpper.py 
⌙-- stringToLower.py
```

```python
# stringLength.py
def stringLength(inStr): return len(inStr)
```

```python
# stringToUpper.py
def stringToUpper(inStr): return inStr.upper()
```

```python
# stringToLower.py
def stringToLower(inStr): return inStr.lower()
```

위 코드들을 아래처럼 사용하려면
```python
# example.py 
import stringLength 
import stringToLower 
import stringToUpper 

some_string = "Hello, Universe!" 
print(stringLength.stringLength(some_string)) 
print(stringToLower.stringToLower(some_string)) 
print(stringToUpper.stringToUpper(some_string))
```

같은 디렉토리에 있어야 한다는 제약 조건이 있습니다.
```
rootFolder 
|-- stringLength.py
|-- stringToUpper.py 
|-- stringToLower.py
`-- example.py
```
위와 같이 root폴더 아래에 모든 파일을 관리하는 것의 단점은 
개발자라면 누구나 알고 있을 것 입니다.


이러한 스크립트들을 관리하기 쉽게 하나의 폴더에 넣어두거나
특정 아키텍쳐를 적용하기 위해서 \_\_init\_\_.py가 필요한 것이다.
```
rootFolder 
|-- string_func 
| |-- __init__.py 
| |-- stringToUpper.py 
| |-- stringToLower.py 
| `-- strengthLength.py 
`-- example.py
```

하면 아래와 같이 import가 가능하다.
```python
# example.py
import string_func.stringLength 
import string_func.stringToLower 
import string_func.stringToUpper 

some_string = "Hello, Universe!" 
print(string_func.stringLength.stringLength(some_string)) 
print(string_func.stringToLower.stringToLower(some_string)) 
print(string_func.stringToUpper.stringToUpper(some_string))
```

여기서 \_\_init\_\_.py를 활용하여 import문을 깔끔하게 줄일 수 있습니다.
```python
# __init__.py 
from .stringLength import stringLength 
from .stringToLower import stringToLower 
from .stringToUpper import stringToUpper
```

```python
# example.py
import string_func

some_string = "Hello, Universe!" 
print(string_func.stringLength.stringLength(some_string)) 
print(string_func.stringToLower.stringToLower(some_string)) 
print(string_func.stringToUpper.stringToUpper(some_string))
```
