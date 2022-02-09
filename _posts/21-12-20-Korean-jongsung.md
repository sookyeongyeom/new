---
title: 한글 종성 유무의 판별
category: PHP
---

# 한글 종성 유무의 판별


## 1. 전체 코드

```php
$last = iconv_substr($search, -1, 1, "utf-8");
$dec = substr(mb_convert_encoding($last,'HTML-ENTITIES','UTF-8'),2,-1);
$nums = array("3","6","0");

if($dec>=44032 && $dec<=55203){
	if(($dec-44032)%28!=0){
		$josa = "으로";
	}else{
		$josa = "로";
	}
}elseif(in_array($last, $nums)){
	$josa = "으로";
}else{
	$josa = "로";
}
```

 

## 2. 한 줄 씩 뜯어보기


1. 검색어의 마지막 글자를 가져온다. 한글을 있는 그대로 자르려면 iconv_substr를 사용해주어야 한다.
```php
$last = iconv_substr($search, -1, 1, "utf-8");
```

2. $last를 10진수로 바꿔준다.

```php
$dec = substr(mb_convert_encoding($last,'HTML-ENTITIES','UTF-8'),2,-1);
```

3. 발음할 때 삼, 육, 십이 되는 숫자를 배열에 넣어준다.

```php
$nums = array("3","6","0");
```

4. 해당 문자가 한글인지 판별한다.

```php
if($dec>=44032 && $dec<=55203)
```

5. 해당 문자에서 44032을 뺀 값이 28로 나누어 떨어지지 않는다면 → 받침이 있는 글자이다.

```php
if(($dec-44032)%28!=0)
```

▶ 유니코드 = 44032 + (초성 * 21 + 중성) * 28 + 종성

따라서 종성이 있는 글자는 유니코드-44032를 28로 나누었을 때 나머지가 남게 된다.

참고로 위 공식에서의 초성, 중성, 종성은 각 자모의 Index를 말한다.

6. 경우에 따른 조사의 형태를 정해준다.

```php
$josa = "으로" / $josa = "로"
```

 

## 3. 결과

<img width=100% src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FblVALG%2FbtrocdX2iNY%2FQUuJcwFTKTlDGYypp9zT51%2Fimg.png">

<img width=100% src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fk7hzP%2FbtrocCpFdDP%2FqICCDbU6im7e8tpK4xOJ6k%2Fimg.png">