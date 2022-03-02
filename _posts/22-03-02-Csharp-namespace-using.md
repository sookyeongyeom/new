---
title: namespace & using
date: 22-03-02 17:00:00 + 0900
category: [Notes, C#]
---

> namespace

- 일종의 스코프로, 큰 영역을 지정하는 키워드다.

- namespace는 유일한 이름을 가져야 한다.

- 다른 namespace의 클래스끼리는 이름이 같아도 상관 없다. (단, 이 경우 해당 namespace를 동시에 using 시키면 오류가 발생한다.)

- using 키워드를 이용하여 다른 namespace의 클래스를 가져와 사용할 수 있다.

<br>

> using

- 다른 namespace의 클래스를 가져와 사용할 때, 코드가 길어지는 것을 피할 수 있다.

- program.cs 맨 위에 using System; 을 적는 이유는, Console.WriteLine() 등 콘솔 상에 특정 작업을 하기 위해 사용하는 메서드들은 사실 System 이라는 namespace에서 가져오는 것이기 때문이다. using System; 을 적어주지 않는다면 System.Console.WriteLine() 라고 적어야 동일한 작업을 수행할 수 있는데, 이렇게 코드가 길어지는 것을 방지하기 위해 using 키워드가 존재한다.

- namespace의 특정 클래스를 가져오기 위해서는 static 한정자를 사용한다. using static System.Console; 이렇게 적어주면 WriteLine() 만 적어도 동일한 작업을 수행할 수 있다.