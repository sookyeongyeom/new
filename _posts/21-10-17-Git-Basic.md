---
title: Git 기초
category: Git
---

# Git 기초


## 1. Git 영역 정리

1. Working Directory (Local)

   ↓ Add ↓

2. Index (= Staging Area)

   ↓ Commit ↓

3. Repository

   ↓ Push ↓

4. Remote Repository


## 2. Git Upload 순서

1. Init : 저장소 생성

2. Add : 파일을 인덱스에 올리기 (= Staging Area)

3. Commit : 로컬 저장소에 올리기

4. Push : 원격 저장소에 올리기


### 2-1. Git Init

1. 로컬 저장소로 사용할 폴더로 이동

```bash
$ cd '로컬 저장소로 사용할 폴더의 경로'
```

2. 새로운 저장소 생성

```bash
$ git init
```


### 2-2. Git Add

1. 한 개의 파일을 인덱스에 추가

```bash
$ git add '파일명'
```

2. 폴더 내의 모든 파일을 인덱스에 추가

```bash
$ git add .
```


### 2-3. Git Commit

1. 파일을 로컬 저장소에 올리기 (= 변경 내용 확정)

```bash
$ git commit -m '설명'
```

2. 한 번이라도 Add 했었던 파일은 아래 명령으로 Add와 Commit 작업을 한 번에 수행할 수 있다.

```bash
$ git commit -am '설명'
```


### 2-4. Git Push

1. 원격 저장소 연결 (= Github)

```bash
$ git remote add origin '원격 저장소 Github URL'
```

▶ origin은 Remote Repository의 기본 이름으로, 다른 이름으로 설정해도 된다.

2. 파일을 원격 저장소에 올리기

```bash
$ git push origin main
```

▶ main은 Branch의 기본 이름으로, 원하는 Branch의 이름을 넣어줘도 된다.


### 2-5. Git Pull

1. 다른 사람이 (또는 다른 환경에서의 내가) 원격 저장소에 업데이트한 파일이 있을 경우, 아래 명령을 통해 로컬 저장소로 받아올 수 있다.

```bash
$ git pull
```