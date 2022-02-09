---
title: MySql 사용자 추가
category: MySql
---

# MySql 사용자 추가

> MySql 사용자 추가
```sql
>> create user '사용자명'@'%' identified by '비밀번호';
```

<br>

> 전체 데이터베이스 접근 권한 부여
```sql
>> grant all privileges on *.* to '사용자명'@'%';
```