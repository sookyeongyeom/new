---
title: Powershell 시스템에서 한글 인식하게끔 하기
date: 22-02-23 18:00:00 + 0900
category: [Tools, Powershell]
---

> 발단

- $PROFILE에 바탕 화면으로 가는 alias를 생성했으나...

![image](https://user-images.githubusercontent.com/98504939/155289155-897d7b84-a880-4841-a400-45a59b914510.png)

- 아래와 같이 한글이 깨지는 오류가 나는 상황이다.

![image](https://user-images.githubusercontent.com/98504939/155289176-75265a22-cb69-4a34-8e0e-cc46960077f6.png)

<br>

> 해결 방법

단순히 한글을 콘솔에 출력하는 문제가 아니라 시스템에서 한글을 인식할 수 있게끔 해주어야 하므로 해당 파일의 인코딩 형식을 바꿔주어야 한다.

- VSCode로 $PROFILE을 열어준다.

```bash
$ code $PROFILE
```

![image](https://user-images.githubusercontent.com/98504939/155289197-1cba65fd-3e12-4e5b-b1b2-c36d051a5c8d.png)

- 최하단 상태바의 우측에 **UTF-8**이라고 적혀있는 것이 현재의 인코딩 형식이다. 해당 부분을 클릭한다.

![image](https://user-images.githubusercontent.com/98504939/155293517-97e1813b-4aab-490d-9861-e5a8bb853080.png)

- **[인코딩하여 저장]** 을 선택한다.

![image](https://user-images.githubusercontent.com/98504939/155289478-1a6cfc45-8b2f-4185-a218-a68fccd98ec2.png)

- **[UTF-8 with BOM]** 형식을 선택한다.

![image](https://user-images.githubusercontent.com/98504939/155289595-5fcf88b2-8f0d-4148-9070-61db6090a6e3.png)

- 최하단 상태바의 인코딩 형식이 **UTF-8 with BOM**으로 바뀐 것을 확인할 수 있다.

![image](https://user-images.githubusercontent.com/98504939/155297747-acde9f51-7315-47a4-b4da-5debaa7bb7d3.png)

<br>

> 확인

- Powershell을 새로 연 후 alias를 입력해보면 정상적으로 작동한다.

![image](https://user-images.githubusercontent.com/98504939/155289676-2d3f63dc-26ef-4ea0-98a2-663f02413f44.png)