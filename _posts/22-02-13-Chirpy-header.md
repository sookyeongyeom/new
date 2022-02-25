---
title: Jekyll Chirpy 테마 - 말머리에 카테고리 출력하기 | Chirpy 커스터마이징
category: [Project, Blog]
---

# 1. 계기

카테고리 구분용 말머리를 자동으로 달아주고 싶다... 는 마음에서 작업해보았다.


# 2. 생김새

## HOME 포스팅 제목에 말머리 추가
<img src="https://user-images.githubusercontent.com/98504939/153746948-4083b38c-0225-48cb-a710-287f12dd84ed.png">

제목 앞에 카테고리명을 출력하고, 카테고리명을 클릭할 시 해당 카테고리로 이동한다.

## Archive 포스팅 제목에 말머리 추가
<img src="https://user-images.githubusercontent.com/98504939/153747051-13ae919a-fdc8-441a-8956-dffdcac997b1.png">

제목 앞에 카테고리명을 출력한다.

HOME과 동일하게 카테고리 링크를 걸어줄 수 있긴 하지만, 왼쪽 시간선의 디자인을 위해 a::before에 동그라미가 설정되어있는 상태라는 점을 고려해야 한다.

즉, 카테고리명과 포스팅 제목을 각각의 다른 a 태그로 지정할 시 동그라미가 총 두 개 생겨버린다... 조랭이떡 마냥...

Class를 지정해서 둘 중 하나에서만 동그라미가 나오게끔 해주면 되지만 해당 부분에 대해서는 이 포스팅에서 다루지 않았다.


# 3. 말머리에 카테고리 출력 방법

말머리에 카테고리명을 출력하고 해당 부분에 카테고리 링크를 달아준 HOME을 기준으로 안내한다.

## 템플릿에 다음 코드를 추가한다. (끝!)

_layout > home.html에 들어가 post-list 단락을 찾은 후 다음과 같이 내용을 변경해준다.

```html
<div id="post-list">
{% raw %}
{% for post in posts %}

    {% assign many = post.categories | size %}
    {% assign last = many | minus: 1 %}
    {% capture _category_url %}/categories/{{ post.categories[last] | slugify | url_encode }}/{% endcapture %}
    <div class="post-preview">
      <h1>
        <a href="{{ _category_url | relative_url }}"><span style="color:rgb(218, 139, 139);">{{ post.categories[last] }} › </span></a>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      </h1>{% endraw %}
```

변경 후 저장하면 적용 성공이다!

카테고리명을 클릭하면 해당 카테고리로 이동하고, 포스팅 제목을 클릭하면 해당 포스팅 내용을 확인할 수 있다.

## 링크 없이 카테고리명만 출력하기

다음은 _layout > archive.html에 적용한 코드다. (카테고리 링크 적용 X)

```html
{% raw %}{% assign many = post.categories | size %}
{% assign last = many | minus: 1 %}
<a href="{{ post.url | relative_url }}"><span style="color:rgb(218, 139, 139);">{{ post.categories[last] }} › </span>{{ post.title }}</a>{% endraw %}
```


## 부연 설명

코드를 보면 유추가 가능하지만 post.categories[Index]로 해당 포스팅의 카테고리를 꺼내올 수 있다.

post.category를 써도 되지만, 상위 카테고리가 존재할 시 카테고리명이 상-하위 구분없이 딱 붙어서 나오기 때문에 가급적 위 방식을 따라준다.

- ex. Wargame > LoS 인 경우 WargameLoS 이런 식으로 전체 카테고리명이 딱 붙어서 나온다. 안 예쁘다 ㅠㅠ

위 코드를 살펴보면 categories 배열의 마지막 요소를 꺼내오고 있다는 점을 알 수 있는데, 이 역시 상-하위 카테고리 관계가 있을 시를 대비한 것이다.

상위 카테고리가 존재할 시 categories[0]에 상위, categories[1]에 하위 (= 실질적) 카테고리명이 담기기 때문에 이러한 상황을 유연하게 커버하려면 categories 배열의 길이를 확인해서 제일 마지막 인덱스를 넣어주어야 해당 포스팅과 가장 가까운 카테고리명을 꺼내올 수 있다.