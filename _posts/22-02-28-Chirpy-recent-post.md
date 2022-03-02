---
title: Jekyll Chirpy 테마 - 최근 글 출력하기 | Chirpy 커스터마이징
category: [Project, Blog]
---

# 1. 계기

순정 <span style="color:rgb(218, 139, 139); font-weight:bold">Chirpy</span>의 오른쪽 컬럼에 있는 Recently Updated...

![image](https://user-images.githubusercontent.com/98504939/156025670-0e1165a8-0135-48e4-ae59-eb264ded3ae2.png)

은근 제대로 작동하지 않을 때가 많기도 하고 그다지 유용하지 않았다.

그런고로 최근 글을 보여주게끔 바꿔주는게 좋겠다는 생각이 들었다.

구현 방법은 정말 별 게 없지만 혹시나 필요한 사람에게는 도움이 될 수도 있을 것 같아 기록으로 남겨본다!


# 2. 완성본

## Recent Post
![image](https://user-images.githubusercontent.com/98504939/156005182-e4ac3f26-6290-456b-b620-7f85b26fbdfe.png)

(클릭하면 더 크게 볼 수 있다!)

다섯개는 너무 많은 것 같아서 최근 글 세개를 출력하게끔 바꿔주고 조금 꾸며줬다.

이 포스팅은 추가적인 CSS에 대해서는 다루지 않는다.

# 3. 적용 방법

## 템플릿에 다음 코드를 추가한다.

_include > recent-list.html 을 생성하여 다음 코드를 복사 붙여넣기 해준다.

```html
{% raw %}<div id="access-lastmod" class="post">
    <div class="panel-heading"><span style="color:#da8b8b">❤&ensp;</span>Recent Post
    </div>
    <ul class="post-content pl-0 pb-1 ml-1 mt-2">
        {% assign posts = site.posts | slice: 0, 3 %}
        {% for post in posts %}
        {% assign url = post.url | relative_url %}
        <li>
            <a href="{{ url }}">{{ post.title }}</a>
        </li>
        {% endfor %}
    </ul>
</div>{% endraw %}
```

변경 후 저장한다!

## 레이아웃에 들어간 템플릿을 교체해준다. (끝!)

_layout > page.html 에 들어가 panel-wrapper 단락을 찾은 후 표시된 부분의 템플릿을 교체해준다.

- update-list.html → recent-list.html

```html
{% raw %}<div id="panel-wrapper" class="col-xl-3 pl-2 text-muted">

    <div class="access">
      {% include recent-list.html %}    // 여기!
      ...
    </div>{% endraw %}
```

변경 후 저장하면 적용 성공이다!

## 부연 설명

참고로 위 코드는 포스트 제목 앞에 카테고리를 출력하지 않은 버전이다.

카테고리 출력 시 상위 카테고리의 존재 여부에 따라 뽑아와야할 인덱스가 달라지므로 일률적인 코드를 제공하기가 어렵기 때문인데 이에 관한 설명을 조금 덧붙인다.

서로 다른 두 가지의 상황에서 카테고리명은 각각 다음과 같이 인덱스에 배정된다.

1. 상위 카테고리가 존재할 시
    - post.categories[0] = 상위 카테고리
    - post.categories[1] = 하위 카테고리


2. 상위 카테고리가 존재하지 않을 시
    - post.categories[0] = 하위 카테고리


포스트 제목 앞에 카테고리를 짤막하게 출력하고 싶을 때는 아무래도 하위 카테고리를 뽑아오는 것이 사용자 경험 상 바람직한 선택인데, 위와 같이 경우에 따라 하위 카테고리의 인덱스가 달라지므로 모든 상황에서 하위 카테고리를 뽑아오려면 적절한 제어문을 작성해주어야 한다.

liquid 문법 신경쓰랴 객체 찾으랴 재미는 있지만 사실 너무 귀찮은 작업이기 때문에 나는 그냥 모든 카테고리에 대해 상위 카테고리를 만들어준 후 categories[1] 을 공통적으로 출력해준 상태다.

제어문 작성하는게 귀찮다면 그냥 나처럼 카테고리 계층을 통일해주는 식으로 간편하게 해결하고,

모든 상황에 적용 가능한 코드를 짜보고 싶다면 아래 liquid 문법을 참고해보자.

- [Liquid 문법 총 정리](https://heekangpark.github.io/jekyll/06-liquid)

