---
title: SQL Injection
category: Webhacking
---

# SQL Injection : 개념 및 공격 기법

 

## 1. SQL Injection 개념

보안상의 취약점을 이용하여, 임의의 SQL문을 주입하고 실행되게 하여 DB가 비정상적인 동작을 하도록 조작하는 행위

1. OWASP TOP 10 중 첫 번째에 속해 있으며, 공격이 비교적 쉬운 편이고 공격에 성공할 경우 큰 피해를 입힐 수 있음

2. 인증 우회, 시스템 명령어 삽입, 웹쉘 생성 등

 

## 2. SQL Injection 공격 기법

1. Error based SQL Injection

2. UNION based SQL Injection

3. Blind SQL Injection (1)

4. Blind SQL Injection (2)

5. Stored Procedure SQL Injection

6. Mass SQL Injection

<br>

### 2-1. Error based SQL Injection

[1] 논리적 에러를 이용함

[2] 에러가 발생되는 사이트에서는 에러 정보들을 이용하여 DB 및 쿼리 구조 등의 정보를 추측 가능

 

#### EXAMPLE (로그인)

① 공격 대상 : SELECT * FROM Users WHERE id = 'INPUT1' AND password = 'INPUT2'

② 공격 예시 : SELECT * FROM Users WHERE id = '' OR 1=1 -- ' AND password = 'INPUT2'

③ 과정 : 싱글쿼터를 닫아주기 위한 싱글쿼터와, OR 1=1 구문을 이용해 WHERE 절을 모두 참으로 만들고, -- 를 넣어줌으로써 뒤의 구문을 모두 주석 처리 해버림

④ 결과 : Users 테이블에 있는 모든 정보를 조회하게 됨으로써 가장 먼저 만들어진 계정 (보통 관리자 계정) 으로 로그인할 수 있게 됨 → 관리자 계정 탈취

<br>

### 2-2. UNION based SQL Injection

[1] UNION : 두 개의 쿼리문에 대한 결과를 통합해 하나의 테이블로 보여주게 하는 키워드

[2] 정상적인 쿼리문에 하나의 추가 쿼리를 삽입하여 원하는 정보를 획득함

[3] UNION Injection이 성공하기 위해서는 두 가지의 조건이 있음

⑴ 조건 1 : UNION하는 두 테이블의 컬럼 수가 같아야 함

⑵ 조건 2 : UNION하는 두 테이블의 데이터 형이 같아야 함

 

#### EXAMPLE (게시글 조회)

① 공격 대상 : SELECT * FROM Board WHERE title LIKE '%INPUT%' OR contents '%INPUT%'

② 공격 예시 : SELECT * FROM Board WHERE title LIKE '% ' UNION SELECT null,id,passwd FROM Users -- INPUT%' OR contents '%INPUT%'

③ 해설 : 위의 쿼리문은 Board라는 테이블에서 게시글을 검색하는 쿼리문이다. 입력값을 tiltle 과 contents 컬럼의 데이터와 비교한 뒤 비슷한 글자가 있는 게시글을 출력한다. 여기서 입력값으로 UNION 키워드와 함께 컬럼 수를 맞춰서 SELECT 구문을 넣어주게 되면 두 쿼리문이 합쳐져서 하나의 테이블로 보여지게 된다.

④ 과정 : 사용자의 id와 passwd를 요청하는 쿼리문을 주입함

⑤ 결과 : 사용자의 개인정보가 게시글과 함께 화면에 보여짐

<br>

### 2-3. Blind SQL Injection (1)

[1] Boolean based SQL

[2] 사용되는 SQL문 : limit, SUBSTR, ASCII..

[3] 특정한 값이나 데이터를 전달받는 것이 아닌, 쿼리를 통해 나온 참과 거짓의 정보만을 통해 정보를 취득함

[4] 에러가 발생되지 않는 사이트에서는 논리적 에러를 이용하거나 UNION을 이용할 수가 없기 때문에, Blind를 통해 정상적인 쿼리가 수행되는지, 혹은 쿼리가 수행되지 않아 쿼리 결과가 없는지를 판단함

[5] 서버가 응답하는 성공과 실패 여부를 이용하여 DB의 테이블 정보 등을 추출해 낼 수 있음

 

#### EXAMPLE (로그인 폼 통해 DB의 테이블 명 알아내기)

① 공격 대상 : SELECT * FROM Users WHERE id = 'INPUT1' AND password = 'INPUT2'

② 공격 예시 : SELECT * FROM Users WHERE id = 'abc123' and ASCII(SUBSTR((SELECT name FROM information_schema.tables WHERE table_type='base table' limit 0,1),1,1)) > 100 (로그인이 될 때까지 시도) -- INPUT1' AND password = 'INPUT2'

③ 해설 : 위의 쿼리문은 DB의 테이블 명을 알아내는 쿼리문이다.

④ 과정 : 임의로 가입한 abc123이라는 아이디와 함께 뒤의 구문을 주입한다. 해당 구문은 테이블 명을 조회하는 구문으로 limit 키워드를 통해 하나의 테이블만 조회하고, SUBSTR 함수로 첫 글자만, ASCII를 통해서 ascii 값으로 변환한다. 만약 조회되는 테이블 명이 Users 라면 'U' 자가 ascii 값으로 조회가 될 것이고, 뒤의 100이라는 숫자 값과 비교하게 된다.

⑤ 결과 : 거짓이면 로그인 실패가 될 것이고, 참이 될 때까지 뒤의 100이라는 숫자를 변경해 가면서 비교하면 된다. 공격자는 이 프로세스를 자동화 스크립트로 만들어 단기간 내에 테이블 명을 알아낼 수 있다. 

<br>

### 2-4. Blind SQL Injection (2)

[1] Time based SQL

[2] 사용되는 SQL문 : SLEEP, BENCHMARK..

[3] 쿼리 결과를 특정 시간만큼 지연시키는 것

[4] Blind와 마찬가지로 에러가 발생되지 않는 조건에서 사용하며, 참 혹은 거짓이라는 결과값이 나오지 않으므로 시간을 재는 것

[5] 궁극적으로는 DB 구조를 파악하기 위함

 

#### EXAMPLE (로그인 폼 통해 DB의 길이 알아내기)

① 공격 대상 : SELECT * FROM Users WHERE id = 'INPUT1' AND password = 'INPUT2'

② 공격 예시 : SELECT * FROM Users WHERE id = 'abc123' OR (LENGTH(DATABASE())=1 (SLEEP 할 때까지 시도) AND SLEEP(2)) -- INPUT1' AND password = 'INPUT2'

③ 해설 : LENGTH는 문자열의 길이를 반환하고, DATABASE는 DB의 이름을 반환한다.

④ 과정 : LENGTH(DATABASE()) = 1 이 참이면 SLEEP(2)가 동작하고, 거짓이면 동작하지 않는다.

⑤ 결과 : 숫자 1 부분을 조작하여 DB의 길이를 알아낼 수 있다.

⑥ 예외 : SLEEP이라는 단어가 치환 처리 되어있는 경우, BENCHMARK나 WAIT 함수를 사용할 수 있다.

<br>

### 2-5. Stored Procedure SQL Injection

[1] Stored Procedure (저장 프로시저) : 편의를 위해 일련의 쿼리들을 모아 하나의 함수처럼 모아둔 것

[2] 대표적으로, MS SQL에서 사용할 수 있는 xp_cmdshell을 통해 윈도우 명령어를 실행할 수 있음 → 자주 악용됨

[3] 단, 공격자가 시스템 권한을 획득해야 하므로 공격난이도가 높음.

[4] 공격에 성공한다면 서버에 직접적인 피해를 입힐 수 있음.

<br>

### 2-6. Mass SQL Injection

[1] 다량의 SQL Injection 공격

[2] 한 번의 공격으로 다량의 DB가 조작되어 큰 피해를 입히는 것을 의미

[3] 보통 MS-SQL을 사용하는 ASP 기반 웹 애플리케이션에서 많이 사용됨

[4] 쿼리문은 Hex* 인코딩* 방식으로 인코딩하여 공격함

[5] DB 값을 변조하여 DB에 악성 스크립트를 삽입하고, 사용자들이 변조된 사이트에 접속 시 좀비 PC로 감염되게 함.

[6] 이렇게 감염된 좀비 PC들은 DDoS* 공격에 사용됨.



* 인코딩 : 문자들의 집합을 부호화하는 방법. 즉, 컴퓨터가 이용할 수 있는 신호로 만드는 것

* 인코딩 기준 : ASCII, Hex, URL, Base 64, 유니코드..

* Hex : 16을 밑으로 하는 기수법. 0~9와 A~F를 사용하고, 대소문자는 구별하지 않음

* DDoS : Distributed Denial of Service. 대량의 패킷 또는 요청을 생성하여 대상 시스템을 마비시키는 공격 기법