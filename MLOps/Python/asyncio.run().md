아래 세가지 역할을 수행하는 함수이다.

1. 현재의 쓰레드에 새 이벤트 루프를 설정
2. 해당 이벤트 루프에서 인자로 넘어오는 코루틴을 태스크로 예약하여 실행
3. 해당 태스크의 실행이 완료되면 이벤트 루프 close

3.7 이전 버전의 asyncio.run() 내부 코드
```python
loop = asyncio.get_event_loop()
loop.run_until_complete(first_coroutine())
loop.close()
```

### asyncio.get_event_loop()
현재 쓰레드에 설정된 이벤트 루프를 가져오는 함수
  
이벤트 루프가 없다면 새로 생성하여 현재 쓰레드에 설정한 뒤 반환한다.
즉, 이 함수의 호출은 코루틴의 실행을 위해 이벤트 루프를 준비하는 과정으로 볼 수 있다.