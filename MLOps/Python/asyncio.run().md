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

아래는 이벤트를 실행 했을 시의 대략적인 의사 
코드다.
```python
while True:
	if task_queue:
		task = task_queue.pop()
		task.run()
	else:
		check_is_IO_ready()
```
### loop.run_until_complete(first_coroutine())
앞서 생성한 이벤트 루프 객체를 이용하여 실제로 이벤트 루프를 실행시키는 함수

#### 코루틴 체인의 형성
1. 인자로 넘어오는 코루틴 객체를 이용하여 태스크 객체를 생성
   -> 그 과정에서 해당 태스크 객체가 나타내는 태스크의 실행이 이벤트 루프에 의해 즉시 예약
