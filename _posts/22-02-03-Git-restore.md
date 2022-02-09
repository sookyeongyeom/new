---
title: Git 변경 사항 되돌리기
category: Git
---

# Git 변경 사항 되돌리기


> Local 변경 사항 되돌리기
 

1. 전체 파일을 마지막 Commit으로 되돌리기

```bash
$ git checkout .
```

2. 특정 파일에 대한 변경 사항만 되돌리기

```bash
$ git checkout '파일명'
```

<br>

> Add 되돌리기
 

1. 전체 파일을 Unstage

```bash
$ git reset HEAD
```

2. 특정 파일만 Unstage

```bash
$ git reset HEAD '파일명'
```

<br>

> Commit 되돌리기 (주의)
 

1. Commit을 취소하고 해당 파일들은 Staged 상태로 Working Directory에 보존하기

```bash
$ git reset --soft HEAD^
```

2. Commit을 취소하고 해당 파일들은 Unstaged 상태로 Working Directory에 보존하기

```bash
$ git reset --mixed HEAD^  # 기본 옵션
$ git reset HEAD^  # 위와 동일
$ git reset HEAD~2  # 마지막 2개의 commit을 취소
```

3. Commit을 취소하고 해당 파일들은 Unstaged 상태로 Working Directory에서도 삭제하기

```bash
$ git reset --hard HEAD^
```
 
<br>

> 과거로 갔다가 현재로 돌아오기
 

1. 과거로 돌아가기

```bash
$ git checkout HEAD~1  # 한 단계 전으로 돌아가기
$ git checkout HEAD~4  # 네 단계 전으로 돌아가기
```

2. 다시 돌아오기

```bash
$ git checkout [Branch명]
```