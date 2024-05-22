실제 데이터를 디스크에 저장하거나 디스크로부터 데이터를 읽어오는 부분은 스토리지 엔진이 전담한다.
MySQL 서버에서 MySQL 엔진은 하나지만 스토리지 엔진은 여러 개를 동시에 사용할 수 있다.


MySQL엔진은 mysql 버전에 따라 나뉜다면 스토리지 엔진은 [[InnoDB]], [[MyISAM]] Archive등으로 나뉜다.

테이블이 사용할 스토리지 엔진을 지정하여 해당 테이블에 대한 모든 읽기 작업이나 변경 작업을 맡길 수 있다.
```sql
CREATE TABLE test_table (fd1 INT, fd2 INT) ENGINE=INNODB;
```

