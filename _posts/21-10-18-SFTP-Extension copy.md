---
title: VSCode에서 SFTP Extension 사용하기
category: [Study, VSCode]
---

# VSCode SFTP Extension

 

## 1. SFTP란?

보안성이 강화된 파일 전송 프로토콜이다.

이름도 기능도 FTP와 유사하나, SSH을 기반으로 만들어진 확장 프로토콜이다.

따라서 Port 번호는 22번을 이용한다.

 

## 2. VSCode에서 SFTP Extension의 역할

가상 환경에 올린 리눅스로 개발을 하다보면 명확히 불편한 점이 있다.

Host PC와 Guest PC 간의 소스 코드 공유가 녹록치 않다는 점이다.

물론 Git을 이용할 수도 있지만, 일일이 Push & Pull로 작업 상황을 맞춰주는게 생각보다 귀찮다.

그냥 한쪽에서 수정을 하면, 반대쪽의 파일도 바로 수정한 내용으로 업데이트되게끔 할 순 없을까?

바로 이런 경우에 SFTP 확장을 사용하면 된다.




# VSCode에서 SFTP Extension을 사용하는 방법

 

## 0. 들어가기 전

이 포스팅은 서버에서 작성한 파일을 로컬로 받아오는 방향으로 작성되었습니다.

서버에 SSH 설치가 되어있지 않으면 연결이 불가능하므로 아래 절차를 따라주세요.

- SSH 설치 여부 확인

```bash
$ sudo dpkg -l | grep ssh
```

- 설치가 되어있지 않을 시 아래 과정을 따라주세요

```bash
$ sudo apt update
$ sudo apt install openssh-server
$ sudo systemctl status ssh (SSH가 active 상태인지 확인*)
$ sudo ufw status (방화벽이 inactive 상태인지 확인*)
```
 

- SSH는 active, 방화벽은 inactive 상태라면 **1. SFTP Extension 설치** 로 넘어가주세요.

- 만약 SSH가 inactive 상태라면

```bash
$ sudo systemctl enable ssh
$ sudo systemctl start ssh
```

- 만약 방화벽이 active 상태라면

```bash
$ sudo ufw allow ssh
```

 

## 1. SFTP Extension 설치

- VSCode 좌측 작업바를 보면 타일 모양으로 된 메뉴가 있다. (Extension Menu)

- 클릭해서 들어간 후, sftp라고 검색한다.

- 화면 상에 보이는 Extension을 설치해준다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F4Cecg%2Fbtrh9BJCwh0%2FkqMYkx5WYgdfjHZvh7EULk%2Fimg.png">


 

## 2. 연결할 로컬 폴더 만들기

- 서버에 연결될 로컬 공간을 만들어줘야 한다.

- 적당히 폴더를 하나 생성한 후 VSCode 상에서 열어준다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F1B259%2Fbtrh8DAVKuG%2FXkBEKlAzhklYRPg9ZgUst1%2Fimg.png">

 

## 3. 환경 설정하기

- F1을 누르고 검색창에 sftp라고 입력한다.

- SFTP: Config를 클릭한다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FeFrhkE%2Fbtrh5YFxSBQ%2FZj9nXjbe3YCwUGpP26PJp1%2Fimg.png">


- 아래와 같은 파일이 열린다. (sftp.json)

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fonv4i%2FbtricDGc8Aq%2FgV3KjpOi266o7N0X9sbMlK%2Fimg.png">


- 원하는대로 설정을 변경해준다.

    + name : 연결에 대해 설명

    + host : 연결할 대상 (서버) 의 IP 주소

    + protocol : sftp

    + port : 22

    + username : 연결할 대상 (서버) 사용자의 이름

    + password : 연결할 대상 (서버) 사용자의 비밀번호

    + remotePath : 로컬과 연결할 서버의 파일 경로

    + uploadOnSave : True일 경우, 로컬에서 변경 사항을 저장할 때마다 서버 파일에 동기화됨

- 이 외 다른 옵션들도 있으니 필요하면 찾아보고 추가해준다.

 

## 4. 서버와 연결

- F1을 누르고 검색창에 sftp라고 입력한다.

- SFTP: List All을 클릭한다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZtOX3%2FbtriaT3QkdJ%2FnWgeGB9YkcihVuXWXbhEKK%2Fimg.png">

- 방금 설정했던 name과 IP 주소가 보인다.

- 클릭한다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fd94QH7%2Fbtrh95wzMMf%2FJG4zzTajMmbbKzTUSTUr11%2Fimg.png">

- 불러오고 싶은 파일을 선택한다.
(디렉토리 내의 모든 파일을 불러오고 싶다면 맨 위의 [. choose current folder] 를 클릭한다.)

<img  src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FGRtyV%2Fbtrh9Rk9aPL%2FK8k5QMfP7FClce8eN2PHu1%2Fimg.png">

- 모든 파일이 로컬 폴더 안에 동기화되는 것을 볼 수 있다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbBCi9p%2Fbtrh5ZxF4vg%2F9tFkz5chIrRyDKsngJND7k%2Fimg.png">

 

## 5. No Such File 오류

로컬에서 파일 변경 후 저장 시 VSCode 우측 하단에 [No Such File] 오류가 뜬다면 아래의 과정을 따라주세요.

- 아래 경로의 파일을 열어주세요.

```
C:/Users/"계정명"/.vscode/extensions/liximomo.sftp-1.12.9/node_modules/ssh2-streams/lib/sftp.js
```

- 338번 라인의 내용을 아래와 같이 변경해주세요.

```shell
if (code === STATUS_CODE.OK) {
// 이 부분을
if (code === STATUS_CODE.OK || code === STATUS_CODE.NO_SUCH_FILE) {
// 이렇게 변경하고 저장 후 다시 로드해주세요
```

- 저장 후 다시 로드하면 오류가 사라집니다.

 

## 6. 이외

- 환경 설정 시 sftp.json 에서 uploadOnSave를 On으로 설정했다면 로컬에서 저장할 때마다 서버에 내용이 동기화된다.

- 반대로 서버에서 변경한 사항을 로컬로 동기화하고 싶을 때는 위에서와 똑같이 [F1 누르고 - SFTP: List All 클릭 - 클릭 - 클릭..] 해주면 된다.

- 로컬이나 서버 한쪽에서 Git을 함께 활용하면 버전 관리까지 가능해 강력한 편의성을 얻을 수 있다.