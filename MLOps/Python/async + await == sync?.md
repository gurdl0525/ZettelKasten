비동기 함수와 await키워드의 조합은 동기와 같은가?
결론 부터 말하면 그렇지 않다.

### 먼저 비동기란 무엇인가?
어떠한 메소드가 실행 중일 때, 추가 동작(다른 메소드의 실행, 네트워크 IO등)이 발생시
스레드의 통제권을 다음 작업으로 넘기는 것이 동기와의 차이점이다.

### 동기는 어떻게 다른데?
동기로 프로그램이 동작한다면 추가 동작(다른 메소드의 실행, 네트워크 IO등)이 발생해도 다음 작업을 실행할 수 없다. 
해당 메소드가 끝날 때까지 애플리케이션 혹은 스레드 전체가 추가 동작의 종료를 기다리는 상태가 된다.

### 그럼 await이 뭔데?
비동기 함수를 call해주고 back해주는 키워드이다.
정확히는 **`Promise`** 객체가 완료될 때까지 기다리고, 완료된 Promise객체의 결과 값을 반환해주는 키워드이다.

### 본론
본격적으로 async + await이 sync처럼 동작하는지 예시와 함께 알아보자.

**가정**
작업 1, 작업 2 요청이 동시에 들어온 상황이다.

**비동기**
```python
import asyncio  
import time  
  
  
async def task_1():  
    print('작업 1 시작')  
    await asyncio.sleep(2)  
    print('작업 1 완료')  
  
  
async def task_2():  
    print('작업 2 시작')  
    await asyncio.sleep(1)  
    print('작업 2 완료')  
  
  
async def main():  
    timestamp = time.time() 

	# 작업 1과 2가 동시에 들어온 상황 가정
    await asyncio.gather(
        task_1(),   
		task_2()  
    )  
    
    print('모든 작업 완료')  
    print(time.time() - timestamp) 
  
  
asyncio.run(main())
```

실행 결과
```
작업 1 시작
작업 2 시작
작업 2 완료
작업 1 완료
모든 작업 완료
2.0017812252044678
```

**동기**
```python
import asyncio  
import time  
  
  
async def task_1():  
    print('작업 1 시작')  
    await asyncio.sleep(2)  
    print('작업 1 완료')  
  
  
async def task_2():  
    print('작업 2 시작')  
    await asyncio.sleep(1)  
    print('작업 2 완료')  
  
  
def sync_wrapper():  
    timestamp = time.time()  

	# 요청이 동시에 들어와도 동기는 하나씩 처리 할 수 밖에 없다.
    asyncio.run(task_1())  
    asyncio.run(task_2())  
      
    print('모든 작업 완료')  
    print(time.time() - timestamp)  
  
  
sync_wrapper()
```

실행 결과
```
작업 1 시작
작업 1 완료
작업 2 시작
작업 2 완료
모든 작업 완료
3.0035829544067383
```

**차이점**

| 항목 / 방식 | 비동기  | 동기   |
| ------- | ---- | ---- |
| 시간      | 2초   | 3초   |
| 종료 순서   | 2, 1 | 1, 2 |
| 실행 순서   | 1, 2 | 1, 2 |

