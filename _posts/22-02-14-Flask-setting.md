---
title: Flask 서버 배포 기본 세팅 (feat. 가비아 서버호스팅)
date: 22-02-14 07:00:00 + 0900
category: Flask
---

# 0. 요약
1. 방화벽 허용
2. Flask run 시 외부 접속 허용 옵션 적용

# 1. 방화벽 허용

## [1] [My가비아 > 콘솔] 클릭
![image](https://user-images.githubusercontent.com/98504939/153792680-aea67717-ccaa-411b-a5a2-e0955250c15f.png)
 
<br>

## [2] [보안/관리] 클릭
![image](https://user-images.githubusercontent.com/98504939/153792689-633e3909-1034-4353-8630-65c4ecd94b30.png)

<br>

## [3] [방화벽 정책 관리] 클릭
![image](https://user-images.githubusercontent.com/98504939/153792704-1cdaa79d-e83e-49dd-889e-1e7dbc055eb0.png)

<br>

## [4] 한번 더 [방화벽 정책 관리] 클릭
![image](https://user-images.githubusercontent.com/98504939/153792710-a19eca67-3ad3-4275-99e1-3d1cdbf0f042.png)

<br>

## [5] [보안 정책 추가] 클릭
![image](https://user-images.githubusercontent.com/98504939/153792717-b43b73cf-0ef9-408f-a06a-e394404d490c.png)

<br>

## [6] 추가할 정책 내용을 작성한다.
![image](https://user-images.githubusercontent.com/98504939/153792727-adf6961e-6e92-44f4-a9bd-100d896f31ab.png)
- 정책 이름 : Flask (원하는대로 작성하면 된다.)
- IP/그룹 : 그대로 둬야 모든 IP에서 접속할 수 있다.
- 서비스 : USER
- 프로토콜 : TCP/UDP (두 경우 모두 혀용할 수 있도록 정책을 하나 더 생성해준다.)

<br>

## [7] 저장하고 빠져나온 후 방화벽 건수를 확인한다.
![image](https://user-images.githubusercontent.com/98504939/153793705-c4be4dd8-2675-4cc2-9053-330b728e24b4.png)
- 추가한 만큼 늘어나있다면 정상적으로 추가된 것이다.

<br>

# 2. Flask run 시 외부 접속 허용 옵션 적용

```bash
flask run --host=0.0.0.0
```

<br>

# 3. 접속 확인

이제 **[서버IP주소:5000/경로]** 로 정상적으로 접속할 수 있다.