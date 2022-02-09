---
title: Python-MySql 연동하기 with PyMySql
category: Python
---

# Python-MySql 연동하기 with PyMySql

> PyMySql DB 연결

```python
import pymysql

conn = pymysql.connect(user='유저명', passwd='패스워드',
                       host='IP', db='데이터베이스명', charset='utf8')
cursor = conn.cursor()
```

<br>

> PyMySql 쿼리 실행 (단일행 삽입)

```python
query = "INSERT INTO post (id, name, title, link, published, topic, platform) VALUE (0, %s, %s, %s, %s, %s, %s)"
data = (name, title, link, published, topic, platform)
cursor.execute(query, data)
conn.commit()
```

<br>

> PyMySql 쿼리 실행 (다중행 삽입)

```python
query = "INSERT INTO post (id, name, title, link, published, topic, platform) VALUE (0, %s, %s, %s, %s, %s, %s)"
data = [(name, title, link, published, topic, platform), (name2, title2, link2, published2, topic2, platform2)...]
cursor.executemany(query, data)
conn.commit()
```

<br>

> PyMySql DB 연결 해제

```python
conn.close()
```