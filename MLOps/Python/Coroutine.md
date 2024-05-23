코루틴을 호출하고 코루틴 객체가 생성 및 반환된다고 하여 해당 코루틴이 바로 실행되지는 않는다

아래 세가지 방법으로 코루틴을 실행할 수 있다.
1. await
2. asyncio.run()
3. asyncio.create_task()