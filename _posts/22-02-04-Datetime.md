---
title: 날짜 및 시간
category: Python
---

# 날짜 및 시간

> 현재 날짜 및 시간

```python
import datetime

now = datetime.datetime.now()
print(now)
```

<br>

> 원하는 형태로 포맷팅

```python
nowDate = now.strftime('%Y-%m-%d')
print(nowDate)
```

```python
nowTime = now.strftime('%H:%M:%S')
print(nowTime)
```

```python
nowDatetime = now.strftime('%Y-%m-%d %H:%M:%S')
print(nowDatetime)
```