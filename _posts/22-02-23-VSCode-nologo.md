---
title: VSCode 터미널 시작 안내 문구 끄기
category: VSCode
---

> VSCode 터미널 시작 안내 문구 끄기

- Ctrl+,을 눌러 설정으로 들어간 후 우측 상단의 버튼을 누르면 settings.json이 열린다.

![image](https://user-images.githubusercontent.com/98504939/155279421-0c5d7ded-e6e3-44d2-8967-ac364ffb6e35.png)

- settings.json에 다음 내용을 추가해준다.

```bash
"terminal.integrated.profiles.windows": {
        "PowerShell": {
            "source": "PowerShell",
            "icon": "terminal-powershell",
            "args": [
                "-NoLogo"
            ]
        }
    }
```

![image](https://user-images.githubusercontent.com/98504939/155278857-47bca1fb-1504-402c-b892-7e3304d73470.png)

<br>

> 결과

![image](https://user-images.githubusercontent.com/98504939/155279063-a257f921-93fa-41c5-935e-ee466dfec57a.png)
