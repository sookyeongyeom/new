---
title: SSH 공개키 인증을 사용하여 로그인하는 방법
category: Computer
---

# SSH 공개키 인증을 사용하여 로그인하는 방법

 

## 들어가기 전

1. 클라이언트 측에는 OpenSSH 클라이언트가, 서버 측에는 OpenSSH 서버가 설치되어있어야 합니다.

2. 간단한 과정이기 때문에 구글링해서 확인 후 설치해주세요.

 

## 전체 과정 요약

1. 클라이언트 측에서 키를 두 개 생성한다.

2. 생성한 키 중 하나를 서버에 복사해준다.

 

## 1. 클라이언트 측에서 키 생성

[1] $ ssh-keygen ▶ 비대칭 Key Pair를 생성한다.


[2] 경로, Passphrase 설정 ▶ 둘 다 설정 안해도 무방 (Enter 두 번 입력)


[3] /.ssh 디렉토리로 들어가기 ▶ 아래와 같이 키가 두 개 생성된 것을 볼 수 있다. (known_hosts는 무시)

1. id_rsa : Private Key (= 개인키)

2. id_rsa.pub : Public Key (= 공개키)


[4] 곧 다시 돌아올 디렉토리이기 때문에 끄지 않고 둔다.

<img width=100% src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcp7woU%2Fbtrighj2VQI%2FbUirTMz7yk0tFKdh2pvg01%2Fimg.png">
 

## 2. 서버에 공개키 복사해주기

[1] $ ssh [서버 사용자명]@[서버 IP주소]

[2] 서버 사용자의 Password 입력 ▶ 서버 접속 성공

[3] $ ls -a ▶ 출력된 리스트 중에 .ssh가 있는 지 확인한다. 없을 시에는 $ mkdir .ssh 를 입력하여 생성해준다.

[4] 아까 열어둔 Windows 디렉토리를 띄우고, id_rsa.pub 파일을 메모장으로 연다.

[5] 메모장에 적힌 내용 (= 공개키) 을 통째로 복사한다.

[6] 터미널로 돌아온다.

[7] $ echo [공개키 전문] >> ~/.ssh/authorized_keys 

[8] $ exit ▶ 서버에서 빠져나온다.

 

## 3. 재접속

[1] $ ssh [서버 사용자명]@[서버 IP주소]

[2] 더 이상 Password를 물어보지 않고 아래와 같이 바로 접속이 된다.

<img width=100% src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPO70w%2FbtrigfNiobq%2FNnpR4KmmgMUEPI3GXHa6m0%2Fimg.png">

 

## 이외-1. 자동 로그인이 안되고 여전히 Password를 물어본다면?

다음은 구글링 키워드다.

[1] ssh 공개키 로그인 안됨 sshd_config

[2] ssh 공개키 로그인 안됨 권한


## 이외-2. 접속할 때마다 명령어를 입력하는 것이 귀찮다면?

서버에 들어갈 때마다 매번 IP를 찾아서 붙여넣기가 귀찮다면

```bash
$ ssh [서버 사용자명]@[서버 IP주소]
```

위의 과정을 일종의 실행 파일로 만들어주면 된다.

[1] $ cd [원하는 디렉토리]

[2] $ vim [실행파일명].bat ▶ 실행파일의 확장자를 반드시 .bat 으로 해준다.


[3] 아래와 같이 적는다.

```bash
@echo off

title Choco-Ubuntu-SSH #원하는 제목
ssh '서버 사용자명'@'서버 IP주소' #-p '포트번호' : 22번이 아닌 포트를 사용하고 싶을 시 주석 풀고 지정

:pause
```

[4] 저장한 후 빠져나온다.

[5] 생성된 실행 파일 클릭 시, 원하는 서버로의 SSH 접속이 완료된 상태의 셸이 열린다.