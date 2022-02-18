---
title: checked 상태에 따라 label 꾸미기
category: CSS
---

> checked 상태에 따라 label 꾸미기

- HTML

```html
<input type="radio" id="yes" value="yes" checked>
<label for="yes"></label>
```

- CSS

```css
#yes+label {
    display: inline-block;
    width: 68px;
    height: 31px;
    background: url("https://user-images.githubusercontent.com/98504939/154197039-22c2a53c-f13a-4124-b92a-5b888da8bea8.svg") no-repeat 0 0px / contain;
}

#yes:checked+label {
    background: url("https://user-images.githubusercontent.com/98504939/154194073-0af2ed1f-d718-4b33-aa30-0c978356ff2d.svg") no-repeat 0 0px / contain;
}
```

<br>

> 결과

![image](https://user-images.githubusercontent.com/98504939/154652915-df153b13-0046-406b-ab6b-ab6547fa000d.png)