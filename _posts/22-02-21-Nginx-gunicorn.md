---
title: Flask production server (Nginx+Gunicorn)
category: Flask
---

> Flask production server 구조

Client - Web Server (Nginx) - WSGI Middleware (Gunicorn) - Web Application (Flask) - DB

위 구조로 세팅해야한다.

Nginx는 Apache와 양대산맥을 이루는 웹서버로, event-driven 방식이라 Apache에 비해 가볍고 빠르다는 장점을 갖고 있다.

Gunicorn은 포트 바인딩 또는 유닉스 소켓 바인딩 방식으로 운영할 수 있는데, 유닉스 계열 시스템에서는 후자를 채택하는 것이 빠르고 효율적이다.

단, 소켓 방식으로 실행한 Gunicorn 서버는 단독으로 접속할 수 없기 때문에 Nginx와 같은 웹서버를 앞단에 배치하여 웹서버-소켓-WSGI서버를 연결해주어야 한다.

→ 그 말은 즉슨? 포트 바인딩 방식으로 실행한 Gunicorn 서버는 웹서버 없이도 단독으로 접속이 가능하다. 다만 웹서버를 따로 둠으로써 얻을 수 있는 다양한 효용들이 있기 때문에 소켓의 성능 + 웹서버의 효용을 모두 얻기 위해 위와 같은 방식으로 세팅하는 것이 일반적인 것으로 보인다.

<br>

> Gunicorn 세팅 방법

- 설치

```bash
$ pip install gunicorn
```

<br>

- 테스트

```bash
# 포트바인딩
gunicorn --bind 0:5000 "app:create_app()"
```
```bash
# 소켓바인딩 (bgflask=프로젝트명)
gunicorn --bind unix:/tmp/bgflask.sock "app:create_app()"
```

<br>

- 서비스 파일 생성 (/etc/systemd/system/bgflask.service)

```bash
[Unit]
Description=Gunicorn instance to serve bgflask
After=network.target

[Service]
User=root
WorkingDirectory=/rss/python-server/bgflask
Environment="PATH=/rss/python-server/env"
ExecStart=/usr/local/bin/gunicorn --workers 2 --bind unix:/tmp/bgflask.sock "app:create_app()"

[Install]
WantedBy=multi-user.target
```

<br>

- 환경 변수 파일 생성 (/rss/python-server/env/bgflask.env)

```bash
FLASK_APP=app
FLASK_ENV=production
```

<br>

- 서비스 실행 및 등록

```bash
$ systemctl start bgflask.service
```
```bash
$ systemctl enable bgflask.service
```

<br>

- 오류 발생 시 로그 확인

```bash
$ cat /var/log/syslog
```

<br>

> Nginx 세팅 방법

- 설치

```bash
$ apt install nginx
```

<br>

- Nginx 설정 파일 생성 (HTTPS 적용)

```bash
$ cd /etc/nginx/sites-available/
```
```bash
$ vim bgflask
```
```bash
server {
        listen 80;
        server_name sookyeongyeom.com;

        location / {
                return 307 https://sookyeongyeom.com;
        }
}

server {
        listen 443;
        listen [::]:443;
        ssl on;
        server_name sookyeongyeom.com;

        ssl_certificate /etc/letsencrypt/live/sookyeongyeom.com/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/sookyeongyeom.com/privkey.pem;

        location = /favicon.ico { access_log off; log_not_found off; }

        location / {
                include proxy_params;
                proxy_pass http://unix:/tmp/bgflask.sock;
        }
}
```

<br>

- Nginx 설정 파일을 환경 파일로 등록

```bash
$ cd /etc/nginx/sites-enabled/
```
```bash
$ rm default
```
```bash
$ ln -s /etc/nginx/sites-available/bgflask
```

<br>

- Nginx 재시작

```bash
$ systemctl restart nginx
```

<br>

- Nginx 문법 오류 여부 확인 (오류 있을 시 설정 파일 재작성 후 Nginx를 껐다가 다시 켜야한다.)

```bash
$ nginx -t
```

<br>

> 확인

포트 번호 없이 입력해도 정상 접속되며, http로 접근 시 https로 redirect된다.

<br>

> 추가할 사항

phpmyadmin을 서버 블록에 따로 정의해주어야 웹브라우저를 통해 접근이 가능하다.

구글에 있는 예제를 그대로 가져와서 몇번 테스트해봤으나 버전이나 소켓명 문제인지 해결이 안됐다.

그렇다고 mysql을 터미널에서 그대로 쓰자니 불편하기도 하고 무엇보다 커맨드라인에서 한글이 먹지 않았다.

왜 그런가 찾아보니 mysql 버전 문제로 readline 옵션을 껴서 재컴파일을 해주어야 한다고 하는데 생각만해도 한숨 나오는...

지금 당장 급한건 아니니 일단 두고 조만간 phpmyadmin을 서버 블록에 설정해주는 방향으로 가야겠다.