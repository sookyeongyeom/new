---
title: HTTPS 자물쇠 달기 (Let's Encrypt)
category: Linux
---

> Let's Encrypt란?

- 무료 SSL 인증서

- 3분 만에 간단히 웹사이트에 HTTPS를 적용할 수 있다.

- 무료인 대신 기간 제한이 있다. 그러나 갱신도 무료다. 자동 갱신해주는 방법도 있으니 필요하다면 찾아보자.

<br>

> 사용 방법

- [Let's Encrypt](https://certbot.eff.org/)에 들어간다.

- 내 웹사이트 환경을 선택한다.

- 안내하는대로 따라하면 3분 안에 모든 과정이 끝난다.

<br>

> 예시

- Apache + Ubuntu 18

```bash
$ sudo snap install core; sudo snap refresh core
```

```bash
$ sudo apt-get remove certbot
```

```bash
$ sudo snap install --classic certbot
```

```bash
$ sudo ln -s /snap/bin/certbot /usr/bin/certbot
```

```bash
$ sudo certbot --apache
```

<br>

> HTTPS 적용 확인

- 웹사이트를 확인하면 자물쇠가 달려있다!

![image](https://user-images.githubusercontent.com/98504939/154647700-6ca358f5-f2a3-4fab-889d-f051835fb3b9.png)