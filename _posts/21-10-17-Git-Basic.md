---
title: Git 기초
category: [Tools, Git]
---

# Git 기초


## 1. Git 영역 정리

1. Working Directory (Local)

   <span style="color:rgb(218, 139, 139)">↓ Add ↓</span>

2. Index (= Staging Area)

   <span style="color:rgb(218, 139, 139)">↓ Commit ↓</span>

3. Repository

   <span style="color:rgb(218, 139, 139)">↓ Push ↓</span>

4. Remote Repository


## 2. Git Upload 순서

1. Init : 저장소 생성

2. Add : 파일을 인덱스에 올리기 (= Staging Area)

3. Commit : 로컬 저장소에 올리기

4. Push : 원격 저장소에 올리기

<br>

> Git Init

- 로컬 저장소로 사용할 폴더로 이동

```bash
$ cd '로컬 저장소로 사용할 폴더의 경로'
```

- 새로운 저장소 생성

```bash
$ git init
```

<br>

> Git Add

- 한 개의 파일을 인덱스에 추가

```bash
$ git add '파일명'
```

- 폴더 내의 모든 파일을 인덱스에 추가

```bash
$ git add .
```

<br>

> Git Commit

- 파일을 로컬 저장소에 올리기 (= 변경 내용 확정)

```bash
$ git commit -m '설명'
```

- 한 번이라도 Add 했었던 파일은 아래 명령으로 Add와 Commit 작업을 한 번에 수행할 수 있다.

```bash
$ git commit -am '설명'
```

<br>

> Git Push

- 원격 저장소 연결 (= Github)

```bash
$ git remote add origin '원격 저장소 Github URL'
```

- 파일을 원격 저장소에 올리기

```bash
$ git push origin '브랜치명'
```

<br>

> Git Pull

- 다른 사람이 (또는 다른 환경에서의 내가) 원격 저장소에 업데이트한 파일이 있을 경우, 아래 명령을 통해 로컬 저장소로 받아올 수 있다.

```bash
$ git pull
```