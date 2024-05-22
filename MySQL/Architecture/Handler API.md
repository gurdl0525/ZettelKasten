MySQL 엔진의 쿼리 실행기에서 데이터를 쓰거나 읽어야 할 때는 
각 스토리지 엔진에 쓰기 또는 읽기를 요청하는데, 이러한 요청을 핸들러 요청이라함.

이때 사용되는 API를 핸들러 API라고 함.

[[InnoDB]] 또한 이 핸들러 API를 이용해 [[MySQL Engine]]과 데이터를 주고 받는다.

다음은 Handler API를 이용한 레코드 작업 확인 Query이다
```sql
SHOW GLOBAL STATUS LIKE 'Handler%';
```
