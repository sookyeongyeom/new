---
title: checked 상태에 따라 display ON/OFF
category: CSS
---

> checked 상태에 따라 display ON/OFF

- HTML

```html
<input type="checkbox" id="other" onclick="tool_other()" value="other">
<label for="other"></label>

<div id="other_text" style="display: none;"><input type="text" placeholder="선택지에 없으나 다룰 줄 아는 툴을 적어주세요."></div>
```

- Javascript

```javascript
function tool_other() {
    other = document.getElementById('other').checked;
    if (other) {
        document.getElementById('other_text').style.display = "block";
    } else {
        document.getElementById('other_text').style.display = "none";
    }
}
```

<br>

> 결과

![image](https://user-images.githubusercontent.com/98504939/154655033-f52d4ccb-d8e8-4ea8-962b-893cbe66c640.png)
![image](https://user-images.githubusercontent.com/98504939/154655040-5ffb60bc-4d05-467d-bb00-7a198b7f166a.png)