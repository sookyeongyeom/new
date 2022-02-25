---
title: Python 연습문제 만들기
category: [Study, Python]
---

# Python 연습문제 만들기

 
## 0. 요약

1. BMI 계산기

2. 주민등록번호 입력 시 간단 신상 출력

3. 몬스터 자동 공격

4. 마스크 5부제

5. 업다운 게임

6. 학점 계산기

7. 가위바위보

8. 끝말잇기

9. 정답에 가까운 사람이 승리하는 숫자 게임

10. 폭탄 숫자 피하기

11. 미래 예측 키 계산기
 

## 1. BMI 계산기

#### 문제) 신체질량지수인 BMI는 체중(kg)를 신장(m)의 제곱으로 나눈 값입니다. BMI 측정기를 만들고 임의의 체중과 신장을 넣어 출력해보세요. 

```python
def bmi(kg, m):
    bmi = round(kg / m**2)  #정수로 반올림
    if bmi < 20:
        print(f"BMI: {bmi}\n당신은 저체중입니다.")
    elif bmi >= 20 and bmi <= 24:
        print(f"BMI: {bmi}\n당신은 정상입니다.")
    elif bmi >= 25 and bmi <= 29:
        print(f"BMI: {bmi}\n당신은 과체중입니다.")
    else:
        print(f"BMI: {bmi}\n당신은 비만입니다.")
```

```bash
bmi(50.5, 1.55)
python
BMI: 21
당신은 정상입니다.
```
 
## 2. 주민등록번호 입력 시 간단 신상 출력

#### 문제) 주민등록번호를 인자로 입력받으면 생년월일과 성별을 출력하는 함수를 만들고 직접 인자를 넣어 실행해보세요. (주민등록번호 입력 시 '-'을 포함합니다.)

```python
def my_info(regi):
    front = regi.split("-")[0]
    back = regi.split("-")[1]
    year = front[:2]
    month = front[2:4]
    day = front[4:]
    my_gen = back[:1]
    if int(my_gen)==1 or int(my_gen)==3:
        gender = "남성"
    else:
        gender = "여성"
    print_info(year, month, day, gender)
    
def print_info(year, month, day, gender):
    first_two = 19  #연도 앞 두자리
    if int(year[0]) <= 2:  #00, 10, 20년대
        first_two = 20
    print(f"저는 {first_two}{year}년 {month}월 {day}일에 태어난 {gender}입니다.")
    
my_info("980220-2XXXXXX")
my_info("011117-4XXXXXX")
```

```bash
저는 1998년 02월 20일에 태어난 여성입니다.
저는 2001년 11월 17일에 태어난 여성입니다.
```
 
## 3. 몬스터 자동 공격


#### 문제) 몬스터의 체력이 0이 될 때까지 계속하여 공격하는 게임을 만들어보세요. 한번 공격할 때마다 플레이어의 레벨이 1씩 상승하고, 공격이 성공했다는 문구와 함께 현재 플레이어의 LV과 몬스터의 남은 체력을 출력합니다. (공격력 = 레벨 * 10)


```python
mon_hp = 100  #몬스터의 체력
lv = 1  #플레이어 초기 LV
attack = 10  #플레이어 초기 공격력
i = 1
while True:
    if i==1:  #Welcome
        print(f"현재 플레이어의 LV은 {lv}입니다.")
        print("게임을 시작합니다.")
        print("*  *  *  *  *  *  *  *  *")
    mon_hp -= attack
    lv += 1
    if mon_hp <= 0:  #몬스터 사망 시
        mon_hp = 0
        print(f"공격에 성공하여 몬스터가 쓰러졌습니다!!\n플레이어 LV: {lv}\n몬스터 남은 체력: {mon_hp}")
        print("*  *  *  *  *  *  *  *  *")
        print("게임이 종료되었습니다.")
        break
    print(f"{i}회 공격에 성공했습니다!\n플레이어 LV: {lv}\n몬스터 남은 체력: {mon_hp}")
    print("*  *  *  *  *  *  *  *  *")
    attack = lv * 10  #공격력 증가
    i += 1
```

```bash
현재 플레이어의 LV은 1입니다.
게임을 시작합니다.
*  *  *  *  *  *  *  *  *
1회 공격에 성공했습니다!
플레이어 LV: 2
몬스터 남은 체력: 90
*  *  *  *  *  *  *  *  *
2회 공격에 성공했습니다!
플레이어 LV: 3
몬스터 남은 체력: 70
*  *  *  *  *  *  *  *  *
3회 공격에 성공했습니다!
플레이어 LV: 4
몬스터 남은 체력: 40
*  *  *  *  *  *  *  *  *
공격에 성공하여 몬스터가 쓰러졌습니다!!
플레이어 LV: 5
몬스터 남은 체력: 0
*  *  *  *  *  *  *  *  *
게임이 종료되었습니다.
```
 
## 4. 마스크 5부제

#### 문제) 마스크 5부제는 생년의 끝자리를 기준으로 마스크를 구매할 수 있는 요일을 정한 제도입니다. 끝자리가 1, 6인 사람은 월요일, 2, 7인 사람은 화요일, 3, 8인 사람은 수요일, 4, 9인 사람은 목요일, 5, 0인 사람은 금요일에 구매할 수 있습니다. 사용자가 태어난 년도를 입력하면 사용자의 마스크 구매 가능 요일을 출력하게 만들어보세요.


```python
born = int(input("태어난 년도를 입력해주세요:")[3])

def can_buy(day):
    print(f"당신의 마스크 구입 가능 요일은 {day}입니다.")
    
if born == 1 or born == 6:
    can_buy("월요일")
elif born == 2 or born == 7:
    can_buy("화요일")
elif born == 3 or born == 8:
    can_buy("수요일")
elif born == 4 or born == 9:
    can_buy("목요일")
else:
    can_buy("금요일")
```

```bash
태어난 년도를 입력해주세요: 1998
당신의 마스크 구입 가능 요일은 수요일입니다.
```

## 5. 업다운 게임

#### 문제) 1부터 30까지의 정수 중 컴퓨터가 랜덤으로 정한 숫자를 알아맞히는 랜덤 숫자 게임을 만들어보세요. 정답이 아닐 시 사용자가 입력한 숫자보다 높은지(UP), 낮은지(DOWN) 알려주는 힌트를 출력해주세요. 게임이 종료되면 몇번만에 정답을 맞췄는지도 출력해보세요.

```python
import random

ran = random.randrange(31)
i = 1

while True:
    if i == 1:
        guess = int(input("GUESS:"))
    else:
        guess = int(input("GUESS AGAIN:"))
    if ran > guess:
        print(">> UP..")
    elif ran < guess:
        print(">> DOWN..")
    else:
        print(">> YOU GOT IT!!")
        print(f">>>> {i}번만에 게임이 종료되었습니다.")
        break
    i += 1
```

```bash
GUESS: 15
>> DOWN..
GUESS AGAIN: 7
>> DOWN..
GUESS AGAIN: 5
>> DOWN..
GUESS AGAIN: 3
>> UP..
GUESS AGAIN: 4
>> YOU GOT IT!!
>>>> 5번만에 게임이 종료되었습니다.
```
 

## 6. 학점 계산기
 

#### 문제) 사용자로부터 각 과목의 성적을 입력받은 후, 평점 평균을 계산하여 출력하게 만들어보세요. (단, 모든 과목은 학점수가 동일하며, 평점은 +, -, 0를 구분하여 4.3점 만점입니다.)

```python
#성적입력예시 : A+ B- C0 A0 B0 C+
scores = input("이번 학기의 성적을 알려주세요 (공백으로 구분, 알파벳±0 형태로):").split(" ")

total = 0

def alpha(score):
    if score == "A":
        alpha_score = 4
    elif score == "B":
        alpha_score = 3
    elif score == "C":
        alpha_score = 2
    elif score == "D":
        alpha_score = 1
    else:
        alpha_score = 0
    return alpha_score

for score in scores:
    if score[1] == "+":
        total += 0.3
        total += alpha(score[0])
    elif score[1] == "-":
        total -= 0.3
        total += alpha(score[0])
    else:
        total += alpha(score[0])
        
print(f"이번 학기의 평점 평균은 {round(total/len(scores), 2)}점입니다.")
```

```bash
이번 학기의 성적을 알려주세요 (공백으로 구분, 알파벳±0 형태로): A+ A0 A- B+ B0 C+
이번 학기의 평점 평균은 3.43점입니다.
```
 
## 7. 가위바위보
 

#### 문제) 사용자로부터 선택지를 입력 받아, 컴퓨터와 가위바위보하는 게임을 만들어보세요. 동시에, 총 세번 먼저 이기면 최종 승리하는 삼세판 규칙을 구현해보세요.

```python
import random

global player_win
player_win = 0
global enemy_win
enemy_win = 0

def win():
    print(">> Player가 승리했습니다!!")
    global player_win
    player_win += 1
def draw():
    print("비겼습니다.")
def lose():
    print(">> Enemy가 승리했습니다..")
    global enemy_win
    enemy_win += 1

while True:    
    print(f"◆ Player {player_win} : {enemy_win} Enemy ◆")
    if player_win==3:
        print(">>>> Player가 최종 승리했습니다!!!")
        break
    if enemy_win==3:
        print(">>>> Enemy가 최종 승리했습니다...")
        break
    print("[1]가위 [2]바위 [3]보")
    player = int(input("Player:"))
    enemy = random.randrange(1, 4)
    choice = ["가위", "바위", "보"]
    print(f"Player는 {choice[player-1]}, Enemy는 {choice[enemy-1]}를 선택했습니다!")

    if player==1:
        if enemy==1:
            draw()
        elif enemy==2:
            lose()
        else:
            win()
    elif player==2:
        if enemy==1:
            win()
        elif enemy==2:
            draw()
        else:
            lose()
    else:
        if enemy==1:
            lose()
        elif enemy==2:
            win()
        else:
            draw()
    
    print("* * * * * * * * * * * * * * * * * * * * *")
```

```bash
◆ Player 0 : 0 Enemy ◆
[1]가위 [2]바위 [3]보
Player: 1
Player는 가위, Enemy는 바위를 선택했습니다!
>> Enemy가 승리했습니다..
* * * * * * * * * * * * * * * * * * * * *
◆ Player 0 : 1 Enemy ◆
[1]가위 [2]바위 [3]보
Player: 1
Player는 가위, Enemy는 보를 선택했습니다!
>> Player가 승리했습니다!!
* * * * * * * * * * * * * * * * * * * * *
◆ Player 1 : 1 Enemy ◆
[1]가위 [2]바위 [3]보
Player: 2
Player는 바위, Enemy는 가위를 선택했습니다!
>> Player가 승리했습니다!!
* * * * * * * * * * * * * * * * * * * * *
◆ Player 2 : 1 Enemy ◆
[1]가위 [2]바위 [3]보
Player: 1
Player는 가위, Enemy는 가위를 선택했습니다!
비겼습니다.
* * * * * * * * * * * * * * * * * * * * *
◆ Player 2 : 1 Enemy ◆
[1]가위 [2]바위 [3]보
Player: 3
Player는 보, Enemy는 보를 선택했습니다!
비겼습니다.
* * * * * * * * * * * * * * * * * * * * *
◆ Player 2 : 1 Enemy ◆
[1]가위 [2]바위 [3]보
Player: 2
Player는 바위, Enemy는 바위를 선택했습니다!
비겼습니다.
* * * * * * * * * * * * * * * * * * * * *
◆ Player 2 : 1 Enemy ◆
[1]가위 [2]바위 [3]보
Player: 1
Player는 가위, Enemy는 보를 선택했습니다!
>> Player가 승리했습니다!!
* * * * * * * * * * * * * * * * * * * * *
◆ Player 3 : 1 Enemy ◆
>>>> Player가 최종 승리했습니다!!!
```
 

## 8. 끝말잇기
 

#### 문제) 사용자로부터 문자열을 입력 받아, 혼자서 하는 끝말잇기 게임을 만들어보세요. 단, 두음법칙은 적용되지 않으며, 이미 앞에서 사용한 단어이거나 답이 틀렸을 경우에는 게임이 종료되게 해주세요.

```python
while True:
    used = []
    first = input(">> 첫번째 제시어를 입력해주세요:")
    used.append(first)
    second = input(f"{first} →")
    if second in used:
        print(">> 이미 사용한 단어입니다!")
        print(">>>> GAME OVER")
        break
    else:
        used.append(second)

    while True:
        if first[-1] == second[0]:
            first = second
            second = input(f"{second} →")
            if second in used:
                print(">> 이미 사용한 단어입니다!")
                print(">>>> GAME OVER")
                break
            else:
                used.append(second)
        else:
            print(">> 틀렸습니다!")
            print(">>>> GAME OVER")
            break
            
    break
```

```bash
>> 첫번째 제시어를 입력해주세요: 기러기
기러기 → 기차
기차 → 차표
차표 → 표범
표범 → 범인
범인 → 인간성
인간성 → 성실
성실 → 실기
실기 → 기러기
>> 이미 사용한 단어입니다!
>>>> GAME OVER
```
 

## 9. 정답에 가까운 사람이 승리하는 숫자 게임
 

#### 문제) 1부터 50까지의 숫자 중 랜덤으로 숫자 하나를 정답으로 정하고, 컴퓨터가 선택한 숫자와 사용자가 입력한 숫자를 비교하여 정답과 더 가까운 쪽이 승리하는 게임을 만들어보세요!

```python
import random

def guess_game():
    answer = random.randrange(1, 50)
    com_guess = random.randrange(1, 50)
    player_guess = int(input("정답을 맞춰보세요!:"))
    print(f"컴퓨터는 {com_guess}를 선택했고, 플레이어는 {player_guess}를 선택했습니다.")
    com_diff = abs(answer-com_guess)
    player_diff = abs(answer-player_guess)
    print(f"정답은 {answer}입니다.")
    if com_diff<player_diff:
        print("컴퓨터가 승리했습니다...")
    elif com_diff==player_diff:
        print("비겼습니다.")
    else:
        print("플레이어가 승리했습니다!")
        
guess_game()
```
```bash
정답을 맞춰보세요!: 27
컴퓨터는 31를 선택했고, 플레이어는 27를 선택했습니다.
정답은 30입니다.
컴퓨터가 승리했습니다...
```
 
## 10. 폭탄 숫자 피하기
 

#### 문제) 1부터 50까지의 숫자 중 폭탄 숫자를 10개 정하고, 컴퓨터와 사용자가 차례로 숫자 하나씩을 말해 폭탄 숫자를 먼저 말하게 되는 사람이 패배하는 게임을 만들어보세요.

```python
import random

def bomb_game():
    bomb = []
    while len(bomb)<10:
        new = random.randrange(1, 50)
        if new not in bomb:
            bomb.append(new)
        else:
            continue
    i = 1
    while True:
        print(f">> {i}번째 턴입니다.")
        com_guess = random.randrange(1, 50)
        print(f"컴퓨터는 {com_guess}를 선택했습니다.")
        if com_guess in bomb:
            print(f">> {com_guess}은 폭탄이었습니다!")
            print("컴퓨터가 패배했습니다!")
            break
        player_guess = int(input("폭탄을 피하세요!:"))
        print(f"플레이어는 {player_guess}를 선택했습니다.")
        if player_guess in bomb:
            print(f">> {player_guess}은 폭탄이었습니다!")
            print("플레이어가 패배했습니다...")
            break
        i += 1
    
bomb_game()
```

```bash
>> 1번째 턴입니다.
컴퓨터는 16를 선택했습니다.
폭탄을 피하세요!: 24
플레이어는 24를 선택했습니다.
>> 2번째 턴입니다.
컴퓨터는 33를 선택했습니다.
>> 33은 폭탄이었습니다!
컴퓨터가 패배했습니다!
```
 
## 11. 미래 예측 키 계산기
 

#### 문제) 아이의 미래 예측 키는 엄마의 키와 아빠의 키의 평균에, 여자아이는 6.5cm를 빼고 남자아이는 6.5cm를 더하면 된다고 합니다. 엄마의 키와 아빠의 키, 아이의 성별을 입력받고 미래 예측 키를 출력하는 함수를 만드세요.

```python
def my_height():
    mom = int(input("엄마의 키를 입력하세요:"))
    dad = int(input("아빠의 키를 입력하세요:"))
    aver = (mom+dad)/2
    sex = input("여자아이면 F, 남자아이면 M을 입력하세요:")
    if sex=="F":
        height = aver-6.5
    elif sex=="M":
        height = aver+6.5
    print(f"아이의 미래 예측 키는 {height}cm입니다.")
    
my_height()
```
```bash
엄마의 키를 입력하세요: 150
아빠의 키를 입력하세요: 170
여자아이면 F, 남자아이면 M을 입력하세요: M
아이의 미래 예측 키는 166.5cm입니다.
```