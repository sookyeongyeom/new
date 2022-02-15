---
title: Background (&)
category: Linux
---

> Background에서 작업 실행

```bash
$ python3 file.py &
```

<br>

> Foreground 작업을 Background로 옮기기

- 실행

```bash
$ python3 file.py
```

- 프로세스 일시정지

```bash
Ctrl+Z
```

- 백그라운드에서 재구동

```bash
$ bg
```

- 소유권 포기

```bash
$ disown -h
```

<br>

> Background 작업을 Foreground로 옮기기

- 현재 Background 작업 상태 확인

```bash
$ jobs
```

- Foreground로 옮기기

```bash
$ fg
```

<br>

> Background 작업 확인 (특정 포트)

```bash
$ netstat -nap | grep [포트번호]
```

<br>

> Background 프로세스 종료

```bash
$ kill -9 [프로세스ID]
```