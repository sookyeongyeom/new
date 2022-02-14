---
title: iptables 방화벽 포트 개방
date: 22-02-14 08:00:00 + 0900
category: Linux
---

> 방화벽 설정 확인

```bash
$ iptables -nL
```

<br>

> Input

```bash
iptables -I INPUT 1 -p tcp --dport [포트번호] -j ACCEPT
```
```bash
iptables -I INPUT 1 -p udp --dport [포트번호] -j ACCEPT
```

<br>

> Output

```bash
iptables -I OUTPUT 1 -p tcp --dport [포트번호] -j ACCEPT
```
```bash
iptables -I OUTPUT 1 -p udp --dport [포트번호] -j ACCEPT
```

<br>

> 작성한 규칙 확인

```bash
iptables -L -v
```

<br>

> 규칙 삭제

```bash
iptables -D INPUT -p tcp --dport [포트번호] -j ACCEPT
```
```bash
iptables -D INPUT -p udp --dport [포트번호] -j ACCEPT
```
```bash
iptables -D OUTPUT -p tcp --dport [포트번호] -j ACCEPT
```
```bash
iptables -D OUTPUT -p udp --dport [포트번호] -j ACCEPT
```

<br>

> 변경사항 저장

```bash
$ service iptables save
$ /etc/init.d/iptables restart
```

<br>

> 방화벽 활성화/비활성화

```bash
$ /etc/init.d/iptables start
```
```bash
$ /etc/init.d/iptables stop
```