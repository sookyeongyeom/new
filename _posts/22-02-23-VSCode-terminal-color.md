---
title: VSCode 터미널 색 테마 커스터마이징
category: VSCode
---

> VSCode 터미널 색 테마 커스터마이징

- [VSCode-base16-term](https://glitchbone.github.io/vscode-base16-term/#/) 에 들어가 원하는 터미널 색 테마를 고른 후 Copy to clipboard를 누른다.

- VSCode로 돌아와 Ctrl+,을 눌러 설정으로 들어간 후 우측 상단의 버튼을 누르면 settings.json이 열린다.

![image](https://user-images.githubusercontent.com/98504939/155279421-0c5d7ded-e6e3-44d2-8967-ac364ffb6e35.png)

- 복사한 내용을 settings.json에 다음의 형식으로 추가해준다.

```bash
"workbench.colorCustomizations": {
        # 이 부분에 붙여넣기!
}
```

![image](https://user-images.githubusercontent.com/98504939/155280079-4dac6e86-a836-4cb3-9018-a48a8ec6fc3c.png)


<br>

> 결과

![image](https://user-images.githubusercontent.com/98504939/155280370-47aec927-7334-4fe2-8d1c-e378fb46f8b5.png)