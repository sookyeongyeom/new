---
title: netstat 포트 확인
date: 22-02-14 09:00:00 + 0900
category: [Study, Linux]
---

> 열려있는 모든 포트 확인

```bash
$ netstat -nap
```

<br>

> LISTEN중인 표트 표시

```bash
$ netstat -nap | grep LISTEN
```

<br>

> 특정 포트 상태 확인

```bash
$ netstat -nap | grep [포트번호]
```