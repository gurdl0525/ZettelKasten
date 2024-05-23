**Asynchronous Server Gateway Interface**란?

ASGL. 즉, 비동기를 사용하는 web server를 의미한다. (동기는 WSGL)
- callback, [[Promise]], async / await 구문을 사용
![[ASGI.png]]


# Async로 동작한다 await를 통해 기다린다면 의미가 있는가?
![[Async.png]]
이 의문은 위 사진을 통해 해결할 수 있다.

`Task2`에서 `Get Data from Server`가 호출 되었다고 해보자.

이때 `Task2`는 정상적으로 수행하다가 `Get Data from Server`가 필요한 시점에
`Get Data from Server`가 종료 되었다면 다음 동작을 실행하는 것이고, 아니라면 기다리는 것이다.