---
title: Jekyll Chirpy 테마 - 전체 포스팅 개수 출력하기 | Chirpy 커스터마이징
category: [Project, Blog]
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

## 한계점 (22.02.26 Update)

위 코드는 모든 포스팅에 상위 카테고리가 없어야 정상적으로 작동한다.

상위 카테고리가 존재할 시, 그 또한 독립적인 하나의 카테고리로 들어가기 때문에 포스팅 개수가 2배가 되는 문제가 발생한다.

이 문제를 해결하려면 카테고리의 상하위 계층 정보를 검사해주어야 하는데, 그러기에는 카테고리 관련 데이터 구조가 너무 불편하게 생겨먹었다..

상위 카테고리를 꼭 만들고 싶다면 낱개로 남는 카테고리 없이 전부 다 상위 카테고리를 생성해주어 마지막 total 값에서 나누기 2만 해주는 방향으로 접근하는 편이 깔끔할 것 같다 ㅠ

다음은 모든 카테고리에 대해 상위 카테고리를 생성해준 후 total에 나누기 2를 해준 경우의 코드다.

```html
<!-- Total post size -->
{% raw %}{% for category in site.categories %}
{% assign category_name = category | first %}
{% assign many = site.categories[category_name] | size %}
{% assign total = total | plus: many %}
{% if forloop.last %}
<h1>Total ({{ total | divided_by: 2 }})</h1>
{% endif %}
{% endfor %}{% endraw %}
```

이 경우 카테고리는 다음과 같이 세팅해주어야 한다. (낱개로 남아서 돌아다니는 카테고리가 없게!)

![image](https://user-images.githubusercontent.com/98504939/155775310-78e26eb1-0085-4570-837e-0fba39406e04.png)

## home.html이 아닌 다른 레이아웃에 적용하고 싶다면?

마찬가지로 해당 코드를 원하는 레이아웃의 원하는 자리에 삽입해주면 정상 적용된다.