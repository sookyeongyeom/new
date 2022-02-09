---
title: 이모티콘(emoji) 저장하기
category: MySql
---

# MySql 이모티콘(emoji) 저장하기
 

utf8은 가변 문자열을 3byte 단위로 저장하기 때문에 이모지를 저장하지 못한다. (이모지는 4byte 단위)

▶ 문자셋을 utf8mb4로 변경해주어야 한다.

<br>

> MySql 설정 파일에 다음 내용을 추가

```bash
$ vim /etc/mysql/my.cnf
```

```bash
[client]
default-character-set = utf8mb4

[mysql]
default-character-set = utf8mb4

[mysqld]
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
```

<br>

> MySql 재시작

```bash
$ service mysql restart
```

<br>

> MySql 변경된 문자셋 확인

```bash
$ mysql -u root -p
```

```sql
>> SHOW GLOBAL VARIABLES WHERE Variable_name LIKE 'character\_set\_%' OR Variable_name LIKE 'collation%';
```

<br>

> 기존 데이터베이스 및 테이블의 문자셋 변경

```sql
>> ALTER DATABASE [데이터베이스명] DEFAULT CHARACTER SET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
>> use [데이터베이스명]
>> ALTER TABLE [테이블명] DEFAULT CHARACTER SET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
```

<br>

> 참고

이미 생성한 컬럼의 데이터정렬방식은 자동으로 변경되지 않아 직접 바꿔주었다.