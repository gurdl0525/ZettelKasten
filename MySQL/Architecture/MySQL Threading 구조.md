MySQL 서버는 프로세스 기반이 아니라 스레드 기반으로 작동함.
Foreground와 Background 스레드로 나뉜다.

MySQL 서버에서 실행 중인 스레드의 목록을 확인하는 Query 문
```sql
SELECT thread_id, name, type, processlist_user, processlist_host
FROM perfomance_schema, threads ORDER BY type, thread_id;
```
