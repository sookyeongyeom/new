---
title: Jekyll Chirpy 테마 - 전체 포스팅 개수 출력하기 | Chirpy 커스터마이징
category: Blog
---

# 1. 계기

내가 사용 중인 테마는 <span style="color:rgb(218, 139, 139); font-weight:bold">Chirpy</span>인데,

심플하면서도 필요한 기능은 다 들어가있기 때문에 깃헙 블로그에서 자주 보이는 인기 테마다.

커스터마이징하면서 조금 아쉬웠던 점은 전체 포스팅 개수를 보여주는 방법을 안내하지 않는다는 것이었다.

공식적으로는 없더라도 누군가는 구현했을법 한데... 서치해봐도 선례가 나오지 않았다 ㅠㅠ

포스팅 개수를 한 눈에 보고 싶은 니즈는 나에게만 있는 것인가...

목마른 사람이 우물판다고... 템플릿에 렌더링된 객체들을 응용해서 구현해봤다.

# 2. 생김새

<img src="https://user-images.githubusercontent.com/98504939/153731730-8c0d3dbe-5ad1-472d-b64d-4bd1168f256f.png">

HOME 화면의 상단에 출력했다.

- 원본 테마를 보면 다른 탭들과는 다르게 HOME의 경우에만 &lt;h1&gt; 부분이 휑하니 비어있어서 포스팅 개수가 들어가기 딱 적절해보였다.
- [Chirpy 원본 데모](https://chirpy.cotes.page/)

# 3. 전체 포스팅 개수 출력 방법

템플릿 문법을 처음 다뤄보기도 하고, 단서를 바탕으로 객체를 역으로 파악하느라 구현하는 건 한참 헤맸지만...

최종 적용 방법은 정말 간단하다! ( ｯ◕ ܫ◕)ｯ'

이 글에서는 나와 같이 HOME 화면에 띄우는 경우를 예시로 들어 안내한다.

## 템플릿에 다음 코드를 추가한다. (끝!)

_layouts 디렉토리 내부의 home.html 을 열어보면, <\!-- Get default posts --> 단락이 있다.

해당 단락 바로 위에 다음 코드를 추가해준다.

```html
<!-- Total post size -->
{% raw %}{% for category in site.categories %}
{% assign category_name = category | first %}
{% assign many = site.categories[category_name] | size %}
{% assign total = total | plus: many %}
{% if forloop.last %}
<h1>Total ({{ total }})</h1>
{% endif %}
{% endfor %}{% endraw %}
```

추가 후 저장하면 바로 적용되는 모습을 볼 수 있다!

## home.html이 아닌 다른 레이아웃에 적용하고 싶다면?

마찬가지로 해당 코드를 원하는 레이아웃의 원하는 자리에 삽입해주면 정상 적용된다.