---
title: Powershell alias 영구 등록
category: Powershell
---

> Powershell alias 영구 등록

- 메모장으로 $PROFILE을 연다.

```bash
$ notepad $PROFILE
```

- new-alias를 설정해준다. (alias는 호출 개념이기 때문에 명령줄을 function으로 만들어주어야 한다.)

```bash
function gotoblog { set-location "D:/sookyeongyeom.github.io" }
new-alias blog gotoblog
```

![image](https://user-images.githubusercontent.com/98504939/155273992-a6040d05-d640-42f8-82b7-627c98e50eaf.png)

<br>

> 결과

![image](https://user-images.githubusercontent.com/98504939/155274196-9377577c-fe6d-42ca-a105-0632b400079d.png)