**Asynchronous Server Gateway Interface**란?

ASGL. 즉, 비동기를 사용하는 web server를 의미한다. (동기는 WSGL)
- callback, Promise, async / await 구문을 사용

# WAS와 GI의 차이
1. WAS는 실행 환경 및 관련 기능들을 제공하는 반면에, GI는 웹 서버와 웹 애플리케이션 사이의 프로토콜을 정의한다.
2. WAS는 웹 애플리케이션을 직접 실행하는 반면에, GI는 애플리케이션과 웹 서버간의 메시지 전달 역할 만을 한다.
![[ASGI.png]]

Nginx, Apache와 같은 리벅스 프록시와 같이 사용하면, 사실상 WAS의 역할을 하기 때문에 GI가 탄생함.


# Async로 동작해도 await를 통해 기다린다면 의미가 있는가?
![[Async.png]]
이 의문은 위 사진을 통해 해결할 수 있다.

`Task2`에서 `Get Data from Server`가 호출 되었다고 해보자.

이때 `Task2`는 정상적으로 수행하다가 `Get Data from Server`가 필요한 시점에
`Get Data from Server`가 종료 되었다면 다음 동작을 실행하는 것이고, 아니라면 기다리는 것이다.

이를 JS Code로 보면 다음과 같다.
```javascript
async function f() {

  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("완료!"), 1000)
  });

  let result = await promise; // 프라미스가 이행될 때까지 기다림 (*)

  alert(result); // "완료!"
}

f();
```

그럼 await하지 않은 순간에는 병렬처리가 가능한가?
이는 Python 코드로 알아보겠다
```python
import asyncio  
  
  
async def example2() -> int:  
    for i in ['A', 'B', 'C', 'D', 'E']:  
        print(i)  
  
    return 1248124  
  
  
async def example():  
    res = example2()  
  
    for i in range(5):  
        print(i)  
  
    print(await res)
  
asyncio.run(example())
```

위 코드에서는 example2()을 호출한 순간 부터 A, B, C...등의 print가 시작되고
동시에 0, 1, 2...도 print 되는지, res값이 await를 통해 정상적으로 반환 되는지를 의도했다.

단 예상과 달리 output은 다음과 같았다.
```console
0
1
2
3
4
A
B
C
D
E
1248124
```
왜 이런 결과가 나왔을까?

await를 호출한 시점에서 event의 종료를 기다리기 때문에 
event의 call 또한 await 시점에서 시작된다고 볼 수 있다.

때문에 `res = example2()`는 사실상 의미가 없고 await res 시점에서 event가 동작한다.

두 함수를 동시에 실행 시키려면 다음과 같은 방법이 있다.
```python
import asyncio  
  
  
async def example2() -> int:  
    for i in range(5):  
        await asyncio.sleep(0.7)  
        print('example2-' + str(i))  
  
  
async def example():  
    for i in range(5):  
        await asyncio.sleep(1)  
        print('example1-' + str(i))  
  
  
async def main():  
    await asyncio.gather(  
        example(),  
        example2()  
    )  
  
asyncio.run(main())
```

아래 output이 실행 결과 이다.
```
example2-0
example1-0
example2-1
example1-1
example2-2
example2-3
example1-2
example2-4
example1-3
example1-4
```
