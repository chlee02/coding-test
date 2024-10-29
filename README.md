# 콜라츠 추측 
- 1937년 Collatz란 사람에 의해 제기된 이 추측은, 주어진 수가 1이 될 때까지 다음 작업을 반복하면, 모든 수를 1로 만들 수 있다는 추측입니다. 작업은 다음과 같습니다.
```
1-1. 입력된 수가 짝수라면 2로 나눕니다. 
1-2. 입력된 수가 홀수라면 3을 곱하고 1을 더합니다. 
2. 결과로 나온 수에 같은 작업을 1이 될 때까지 반복합니다. 
```
- 예를 들어, 주어진 수가 6이라면 6 → 3 → 10 → 5 → 16 → 8 → 4 → 2 → 1 이 되어 총 8번 만에 1이 됩니다. 위 작업을 몇 번이나 반복해야 하는지 반환하는 함수, solution을 완성해 주세요. 단, 주어진 수가 1인 경우에는 0을, 작업을 500번 반복할 때까지 1이 되지 않는다면 –1을 반환해 주세요.
 
- 제한 사항 
입력된 수, num은 1 이상 8,000,000 미만인 정수입니다.  
   
```python   
def solution(num): 
    answer = 0 
    while num!=1: 
        if num%2==0: 
            num=num/2  
        else:
            num=(num*3+1)
        answer+=1
        if answer==500:
            answer=-1
            break
    return answer
  
```

# 햄버거 만들기
- 햄버거 가게에서 일을 하는 상수는 햄버거를 포장하는 일을 합니다. 함께 일을 하는 다른 직원들이 햄버거에 들어갈 재료를 조리해 주면 조리된 순서대로 상수의 앞에 아래서부터 위로 쌓이게 되고, 상수는 순서에 맞게 쌓여서 완성된 햄버거를 따로 옮겨 포장을 하게 됩니다. 상수가 일하는 가게는 정해진 순서(아래서부터, 빵 – 야채 – 고기 - 빵)로 쌓인 햄버거만 포장을 합니다. 상수는 손이 굉장히 빠르기 때문에 상수가 포장하는 동안 속 재료가 추가적으로 들어오는 일은 없으며, 재료의 높이는 무시하여 재료가 높이 쌓여서 일이 힘들어지는 경우는 없습니다.

- 예를 들어, 상수의 앞에 쌓이는 재료의 순서가 [야채, 빵, 빵, 야채, 고기, 빵, 야채, 고기, 빵]일 때, 상수는 여섯 번째 재료가 쌓였을 때, 세 번째 재료부터 여섯 번째 재료를 이용하여 햄버거를 포장하고, 아홉 번째 재료가 쌓였을 때, 두 번째 재료와 일곱 번째 재료부터 아홉 번째 재료를 이용하여 햄버거를 포장합니다. 즉, 2개의 햄버거를 포장하게 됩니다.

- 상수에게 전해지는 재료의 정보를 나타내는 정수 배열 ingredient가 주어졌을 때, 상수가 포장하는 햄버거의 개수를 return 하도록 solution 함수를 완성하시오.

- 제한사항
1 ≤ ingredient의 길이 ≤ 1,000,000
ingredient의 원소는 1, 2, 3 중 하나의 값이며, 순서대로 빵, 야채, 고기를 의미합니다.

```python
def solution(ingredient):
    answer=0
    stack=[]
    ingredient.reverse()
    while ingredient:
        stack.append(ingredient.pop())
        if len(stack)>3:
            if stack[-4:]==[1,2,3,1]:
                for i in range(4):
                    stack.pop()
                answer+=1
    return answer
```

# 로또의 최고 순위와 최저 순위
- 로또 6/45(이하 '로또'로 표기)는 1부터 45까지의 숫자 중 6개를 찍어서 맞히는 대표적인 복권입니다. 아래는 로또의 순위를 정하는 방식입니다.
```
순위	당첨 내용
1	6개 번호가 모두 일치
2	5개 번호가 일치
3	4개 번호가 일치
4	3개 번호가 일치
5	2개 번호가 일치
6(낙첨)	그 외
```
- 로또를 구매한 민우는 당첨 번호 발표일을 학수고대하고 있었습니다. 하지만, 민우의 동생이 로또에 낙서를 하여, 일부 번호를 알아볼 수 없게 되었습니다. 당첨 번호 발표 후, 민우는 자신이 구매했던 로또로 당첨이 가능했던 최고 순위와 최저 순위를 알아보고 싶어 졌습니다.
알아볼 수 없는 번호를 0으로 표기하기로 하고, 민우가 구매한 로또 번호 6개가 44, 1, 0, 0, 31 25라고 가정해보겠습니다. 당첨 번호 6개가 31, 10, 45, 1, 6, 19라면, 당첨 가능한 최고 순위와 최저 순위의 한 예는 아래와 같습니다.
```
당첨 번호	31	10	45	1	6	19	결과
최고 순위 번호	31	0→10	44	1	0→6	25	4개 번호 일치, 3등
최저 순위 번호	31	0→11	44	1	0→7	25	2개 번호 일치, 5등
```
- 민우가 구매한 로또 번호를 담은 배열 lottos, 당첨 번호를 담은 배열 win_nums가 매개변수로 주어집니다. 이때, 당첨 가능한 최고 순위와 최저 순위를 차례대로 배열에 담아서 return 하도록 solution 함수를 완성해주세요.

  ```python
  def solution(lottos, win_nums):
    answer = [0,0]
    match=0
    for i in lottos:
        if i in win_nums:
            match+=1
        elif i==0:
            match+=1
    if match<=1:
        answer[0]=6
    else:
        answer[0]=7-match
    match=0
    for i in lottos:
        if i in win_nums:
            match+=1
    if match<=1:
        answer[1]=6
    else:
        answer[1]=7-match
    return answer
  ```

# 붕대 감기
- 어떤 게임에는 붕대 감기라는 기술이 있습니다.
- 붕대 감기는 t초 동안 붕대를 감으면서 1초마다 x만큼의 체력을 회복합니다. t초 연속으로 붕대를 감는 데 성공한다면 y만큼의 체력을 추가로 회복합니다. 게임 캐릭터에는 최대 체력이 존재해 현재 체력이 최대 체력보다 커지는 것은 불가능합니다.
- 기술을 쓰는 도중 몬스터에게 공격을 당하면 기술이 취소되고, 공격을 당하는 순간에는 체력을 회복할 수 없습니다. 몬스터에게 공격당해 기술이 취소당하거나 기술이 끝나면 그 즉시 붕대 감기를 다시 사용하며, 연속 성공 시간이 0으로 초기화됩니다.
- 몬스터의 공격을 받으면 정해진 피해량만큼 현재 체력이 줄어듭니다. 이때, 현재 체력이 0 이하가 되면 캐릭터가 죽으며 더 이상 체력을 회복할 수 없습니다.
- 당신은 붕대감기 기술의 정보, 캐릭터가 가진 최대 체력과 몬스터의 공격 패턴이 주어질 때 캐릭터가 끝까지 생존할 수 있는지 궁금합니다.
- 붕대 감기 기술의 시전 시간, 1초당 회복량, 추가 회복량을 담은 1차원 정수 배열 bandage와 최대 체력을 의미하는 정수 health, 몬스터의 공격 시간과 피해량을 담은 2차원 정수 배열 attacks가 매개변수로 주어집니다. 모든 공격이 끝난 직후 남은 체력을 return 하도록 solution 함수를 완성해 주세요. 만약 몬스터의 공격을 받고 캐릭터의 체력이 0 이하가 되어 죽는다면 -1을 return 해주세요.

```python
def solution(bandage, health, attacks):
    answer = health
    maxhealth=health
    time=0
    count=0 
    for i in attacks:
        for j in range(i[0]-time-1):
            answer+=bandage[1]
            count+=1
            if count==bandage[0]:
                answer+=bandage[2]
                count=0
            if answer>maxhealth:
                answer=maxhealth
        time=i[0]
        answer-=i[1]
        count=0
        if answer<=0:
            return -1
    return answer
```

# 데이터 분석
- AI 엔지니어인 현식이는 데이터를 분석하는 작업을 진행하고 있습니다. 데이터는 ["코드 번호(code)", "제조일(date)", "최대 수량(maximum)", "현재 수량(remain)"]으로 구성되어 있으며 현식이는 이 데이터들 중 조건을 만족하는 데이터만 뽑아서 정렬하려 합니다.
- 주어진 데이터 중 "제조일이 20300501 이전인 물건들을 현재 수량이 적은 순서"로 정렬해야 한다면 조건에 맞게 가공된 데이터는 다음과 같습니다.
```
data = [[3,20300401,10,8],[1,20300104,100,80]]
```
- 정렬한 데이터들이 담긴 이차원 정수 리스트 data와 어떤 정보를 기준으로 데이터를 뽑아낼지를 의미하는 문자열 ext, 뽑아낼 정보의 기준값을 나타내는 정수 val_ext, 정보를 정렬할 기준이 되는 문자열 sort_by가 주어집니다.
- data에서 ext 값이 val_ext보다 작은 데이터만 뽑은 후, sort_by에 해당하는 값을 기준으로 오름차순으로 정렬하여 return 하도록 solution 함수를 완성해 주세요. 단, 조건을 만족하는 데이터는 항상 한 개 이상 존재합니다.

```python
def solution(data, ext, val_ext, sort_by):
    answer = []
    e=0
    s=0
    if ext=="date":
        e=1
    elif ext=="maximum":
        e=2
    elif ext=="remain":
        e=3
    if sort_by=="date":
        s=1
    elif sort_by=="maximum":
        s=2
    elif sort_by=="remain":
        s=3
    for i in data:
        if i[e]<val_ext:
            answer.append(i)
    answer.sort(key=lambda x:x[s])
    return answer
```

# 달리기 경주
- 얀에서는 매년 달리기 경주가 열립니다. 해설진들은 선수들이 자기 바로 앞의 선수를 추월할 때 추월한 선수의 이름을 부릅니다. 예를 들어 1등부터 3등까지 "mumu", "soe", "poe" 선수들이 순서대로 달리고 있을 때, 해설진이 "soe"선수를 불렀다면 2등인 "soe" 선수가 1등인 "mumu" 선수를 추월했다는 것입니다. 즉 "soe" 선수가 1등, "mumu" 선수가 2등으로 바뀝니다.
- 선수들의 이름이 1등부터 현재 등수 순서대로 담긴 문자열 배열 players와 해설진이 부른 이름을 담은 문자열 배열 callings가 매개변수로 주어질 때, 경주가 끝났을 때 선수들의 이름을 1등부터 등수 순서대로 배열에 담아 return 하는 solution 함수를 완성해주세요.

```python
def solution(players, callings):
    answer = players
    players_dic={}
    temp=0
    for i in range(len(players)):
        players_dic[players[i]]=i
    for i in callings:
        temp=players_dic[i]
        answer[temp],answer[temp-1]=answer[temp-1],answer[temp]
        players_dic[i]-=1
        players_dic[answer[temp]]+=1
    return answer
```

# 없는 숫자 더하기
- 0부터 9까지의 숫자 중 일부가 들어있는 정수 배열 numbers가 매개변수로 주어집니다. numbers에서 찾을 수 없는 0부터 9까지의 숫자를 모두 찾아 더한 수를 return 하도록 solution 함수를 완성해주세요.

```python
def solution(numbers):
    answer = 0
    for i in range(1,10):
        if i not in numbers:
            answer+=i
    return answer
```

# 신고 결과 받기
- 신입사원 무지는 게시판 불량 이용자를 신고하고 처리 결과를 메일로 발송하는 시스템을 개발하려 합니다. 무지가 개발하려는 시스템은 다음과 같습니다.
```
각 유저는 한 번에 한 명의 유저를 신고할 수 있습니다.
신고 횟수에 제한은 없습니다. 서로 다른 유저를 계속해서 신고할 수 있습니다.
한 유저를 여러 번 신고할 수도 있지만, 동일한 유저에 대한 신고 횟수는 1회로 처리됩니다.
k번 이상 신고된 유저는 게시판 이용이 정지되며, 해당 유저를 신고한 모든 유저에게 정지 사실을 메일로 발송합니다.
유저가 신고한 모든 내용을 취합하여 마지막에 한꺼번에 게시판 이용 정지를 시키면서 정지 메일을 발송합니다.
```
- 이용자의 ID가 담긴 문자열 배열 id_list, 각 이용자가 신고한 이용자의 ID 정보가 담긴 문자열 배열 report, 정지 기준이 되는 신고 횟수 k가 매개변수로 주어질 때, 각 유저별로 처리 결과 메일을 받은 횟수를 배열에 담아 return 하도록 solution 함수를 완성해주세요.

```python
def solution(id_list, report, k):
    answer = []
    reported=[]
    dic_index={}
    dic_rep={}
    split=[]
    for i in range(len(id_list)):
        dic_index[id_list[i]]=i
        dic_rep[id_list[i]]=[]
        reported.append(0)
        answer.append(0)
    for i in report:
        split=i.split(' ')
        if split[0] not in dic_rep[split[1]]:
            reported[dic_index[split[1]]]+=1
            dic_rep[split[1]].append(split[0])
    for i in id_list:
        if reported[dic_index[i]]>=k:
            for j in dic_rep[i]:
                answer[dic_index[j]]+=1
    return answer
```

# 완주하지 못한 선수
- 수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.
- 마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.
- 제한사항
```
마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
completion의 길이는 participant의 길이보다 1 작습니다.
참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
참가자 중에는 동명이인이 있을 수 있습니다.
```

```python
def solution(participant, completion):
    answer = ''
    dic={}
    for i in participant:
        if i not in dic:
            dic[i]=[1]
        else :
            dic[i].append(1)
    for i in completion:
        dic[i].pop()
    for i in dic:
        if dic[i]:
            answer=i
    return answer
```

# 나머지가 1이 되는 수 찾기
- 자연수 n이 매개변수로 주어집니다. n을 x로 나눈 나머지가 1이 되도록 하는 가장 작은 자연수 x를 return 하도록 solution 함수를 완성해주세요. 답이 항상 존재함은 증명될 수 있습니다.
```python
def solution(n):
    for i in range(1,n):
        if n%i==1:
            return i
```

# 콜라 문제
- 오래전 유행했던 콜라 문제가 있습니다. 콜라 문제의 지문은 다음과 같습니다.
```
정답은 아무에게도 말하지 마세요.
콜라 빈 병 2개를 가져다주면 콜라 1병을 주는 마트가 있다. 빈 병 20개를 가져다주면 몇 병을 받을 수 있는가?
단, 보유 중인 빈 병이 2개 미만이면, 콜라를 받을 수 없다.
```
- 문제를 풀던 상빈이는 콜라 문제의 완벽한 해답을 찾았습니다. 상빈이가 푼 방법은 아래 그림과 같습니다. 우선 콜라 빈 병 20병을 가져가서 10병을 받습니다. 받은 10병을 모두 마신 뒤, 가져가서 5병을 받습니다. 5병 중 4병을 모두 마신 뒤 가져가서 2병을 받고, 또 2병을 모두 마신 뒤 가져가서 1병을 받습니다. 받은 1병과 5병을 받았을 때 남은 1병을 모두 마신 뒤 가져가면 1병을 또 받을 수 있습니다. 이 경우 상빈이는 총 10 + 5 + 2 + 1 + 1 = 19병의 콜라를 받을 수 있습니다.
- 문제를 열심히 풀던 상빈이는 일반화된 콜라 문제를 생각했습니다. 이 문제는 빈 병 a개를 가져다주면 콜라 b병을 주는 마트가 있을 때, 빈 병 n개를 가져다주면 몇 병을 받을 수 있는지 계산하는 문제입니다. 기존 콜라 문제와 마찬가지로, 보유 중인 빈 병이 a개 미만이면, 추가적으로 빈 병을 받을 순 없습니다. 상빈이는 열심히 고심했지만, 일반화된 콜라 문제의 답을 찾을 수 없었습니다. 상빈이를 도와, 일반화된 콜라 문제를 해결하는 프로그램을 만들어 주세요.
- 콜라를 받기 위해 마트에 주어야 하는 병 수 a, 빈 병 a개를 가져다 주면 마트가 주는 콜라 병 수 b, 상빈이가 가지고 있는 빈 병의 개수 n이 매개변수로 주어집니다. 상빈이가 받을 수 있는 콜라의 병 수를 return 하도록 solution 함수를 작성해주세요.

```python
def solution(a, b, n):
    i=0
    while n>=a:
        n=(n-(a-b))
        i+=1
    return i*b
```

# 체육복
- 점심시간에 도둑이 들어, 일부 학생이 체육복을 도난당했습니다. 다행히 여벌 체육복이 있는 학생이 이들에게 체육복을 빌려주려 합니다. 학생들의 번호는 체격 순으로 매겨져 있어, 바로 앞번호의 학생이나 바로 뒷번호의 학생에게만 체육복을 빌려줄 수 있습니다. 예를 들어, 4번 학생은 3번 학생이나 5번 학생에게만 체육복을 빌려줄 수 있습니다. 체육복이 없으면 수업을 들을 수 없기 때문에 체육복을 적절히 빌려 최대한 많은 학생이 체육수업을 들어야 합니다.
- 전체 학생의 수 n, 체육복을 도난당한 학생들의 번호가 담긴 배열 lost, 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열 reserve가 매개변수로 주어질 때, 체육수업을 들을 수 있는 학생의 최댓값을 return 하도록 solution 함수를 작성해주세요.
- 제한사항
```
전체 학생의 수는 2명 이상 30명 이하입니다.
체육복을 도난당한 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
여벌의 체육복을 가져온 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
여벌 체육복이 있는 학생만 다른 학생에게 체육복을 빌려줄 수 있습니다.
여벌 체육복을 가져온 학생이 체육복을 도난당했을 수 있습니다. 이때 이 학생은 체육복을 하나만 도난당했다고 가정하며, 남은 체육복이 하나이기에 다른 학생에게는 체육복을 빌려줄 수 없습니다.
```

```python
def solution(n, lost, reserve):
    get=set()
    lost_set=set(lost)
    reserve_set=set(reserve)
    dup_set=set(lost_set&reserve_set)
    for i in dup_set:
        lost_set.remove(i)
        reserve_set.remove(i)
        get.add(i)
    for i in lost_set:
        if i-1 in reserve_set:
            get.add(i)
            reserve_set.remove(i-1)
        elif i+1 in reserve_set:
            get.add(i)
            reserve_set.remove(i+1)
    return n-len(lost)+len(get)
```

# 이상한 문자 만들기
- 문자열 s는 한 개 이상의 단어로 구성되어 있습니다. 각 단어는 하나 이상의 공백문자로 구분되어 있습니다. 각 단어의 짝수번째 알파벳은 대문자로, 홀수번째 알파벳은 소문자로 바꾼 문자열을 리턴하는 함수, solution을 완성하세요.
- 제한 사항
```
문자열 전체의 짝/홀수 인덱스가 아니라, 단어(공백을 기준)별로 짝/홀수 인덱스를 판단해야합니다.
첫 번째 글자는 0번째 인덱스로 보아 짝수번째 알파벳으로 처리해야 합니다.
```

```python
def solution(s):
    answer = ''
    index=0
    for i in range(len(s)):
        if s[i]==' ':
            index=0
            answer+=' '
        else:
            if index%2==0:
                answer+=s[i].upper()
            else:
                answer+=s[i].lower()
            index+=1
    return answer
```

# 서울에서 김서방 찾기
- String형 배열 seoul의 element중 "Kim"의 위치 x를 찾아, "김서방은 x에 있다"는 String을 반환하는 함수, solution을 완성하세요. seoul에 "Kim"은 오직 한 번만 나타나며 잘못된 값이 입력되는 경우는 없습니다.

```python
def solution(seoul):
    answer1="김서방은 "
    answer2="에 있다"
    index=str(seoul.index("Kim"))
    answer=answer1+index+answer2
    return answer
```

# 모의고사
- 수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.
- 1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...
- 2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...
- 3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...
- 1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.

```python
def solution(answers):
    score=[0,0,0]
    b=[2,1,2,3,2,4,2,5]
    c=[3,3,1,1,2,2,4,4,5,5]
    for i in range(len(answers)):
        if answers[i]==i%5+1:
            score[0]+=1
        if answers[i]==b[i%8]:
            score[1]+=1
        if answers[i]==c[i%10]:
            score[2]+=1
    answer=[i+1 for i,j in enumerate(score) if j==max(score)]
    return answer
```

# 기사단원의 무기
- 숫자나라 기사단의 각 기사에게는 1번부터 number까지 번호가 지정되어 있습니다. 기사들은 무기점에서 무기를 구매하려고 합니다.
- 각 기사는 자신의 기사 번호의 약수 개수에 해당하는 공격력을 가진 무기를 구매하려 합니다. 단, 이웃나라와의 협약에 의해 공격력의 제한수치를 정하고, 제한수치보다 큰 공격력을 가진 무기를 구매해야 하는 기사는 협약기관에서 정한 공격력을 가지는 무기를 구매해야 합니다.
- 예를 들어, 15번으로 지정된 기사단원은 15의 약수가 1, 3, 5, 15로 4개 이므로, 공격력이 4인 무기를 구매합니다. 만약, 이웃나라와의 협약으로 정해진 공격력의 제한수치가 3이고 제한수치를 초과한 기사가 사용할 무기의 공격력이 2라면, 15번으로 지정된 기사단원은 무기점에서 공격력이 2인 무기를 구매합니다. 무기를 만들 때, 무기의 공격력 1당 1kg의 철이 필요합니다. 그래서 무기점에서 무기를 모두 만들기 위해 필요한 철의 무게를 미리 계산하려 합니다.
- 기사단원의 수를 나타내는 정수 number와 이웃나라와 협약으로 정해진 공격력의 제한수치를 나타내는 정수 limit와 제한수치를 초과한 기사가 사용할 무기의 공격력을 나타내는 정수 power가 주어졌을 때, 무기점의 주인이 무기를 모두 만들기 위해 필요한 철의 무게를 return 하는 solution 함수를 완성하시오.

```python
def solution(number, limit, power):
    answer = 0
    for i in range(1,number+1):
        count=0
        for j in range(1,int(i**0.5)+1):
            if i%j==0:
                count+=2
        if i**0.5%1==0:
            count-=1
        if count>limit:
            answer+=power
        else:
            answer+=count
    return answer
```

# 덧칠하기
- 어느 학교에 페인트가 칠해진 길이가 n미터인 벽이 있습니다. 벽에 동아리 · 학회 홍보나 회사 채용 공고 포스터 등을 게시하기 위해 테이프로 붙였다가 철거할 때 떼는 일이 많고 그 과정에서 페인트가 벗겨지곤 합니다. 페인트가 벗겨진 벽이 보기 흉해져 학교는 벽에 페인트를 덧칠하기로 했습니다.
- 넓은 벽 전체에 페인트를 새로 칠하는 대신, 구역을 나누어 일부만 페인트를 새로 칠 함으로써 예산을 아끼려 합니다. 이를 위해 벽을 1미터 길이의 구역 n개로 나누고, 각 구역에 왼쪽부터 순서대로 1번부터 n번까지 번호를 붙였습니다. 그리고 페인트를 다시 칠해야 할 구역들을 정했습니다.
- 벽에 페인트를 칠하는 롤러의 길이는 m미터이고, 롤러로 벽에 페인트를 한 번 칠하는 규칙은 다음과 같습니다.
- 롤러가 벽에서 벗어나면 안 됩니다.
- 구역의 일부분만 포함되도록 칠하면 안 됩니다.
- 즉, 롤러의 좌우측 끝을 구역의 경계선 혹은 벽의 좌우측 끝부분에 맞춘 후 롤러를 위아래로 움직이면서 벽을 칠합니다. 현재 페인트를 칠하는 구역들을 완전히 칠한 후 벽에서 롤러를 떼며, 이를 벽을 한 번 칠했다고 정의합니다.
- 한 구역에 페인트를 여러 번 칠해도 되고 다시 칠해야 할 구역이 아닌 곳에 페인트를 칠해도 되지만 다시 칠하기로 정한 구역은 적어도 한 번 페인트칠을 해야 합니다. 예산을 아끼기 위해 다시 칠할 구역을 정했듯 마찬가지로 롤러로 페인트칠을 하는 횟수를 최소화하려고 합니다.
- 정수 n, m과 다시 페인트를 칠하기로 정한 구역들의 번호가 담긴 정수 배열 section이 매개변수로 주어질 때 롤러로 페인트칠해야 하는 최소 횟수를 return 하는 solution 함수를 작성해 주세요.

```python
def solution(n, m, section):
    answer = 0
    com=0
    for i in section:
        if i>=com:
            com=i+m
            answer+=1
    return answer
```

# 푸드 파이트 대회
- 수웅이는 매달 주어진 음식을 빨리 먹는 푸드 파이트 대회를 개최합니다. 이 대회에서 선수들은 1대 1로 대결하며, 매 대결마다 음식의 종류와 양이 바뀝니다. 대결은 준비된 음식들을 일렬로 배치한 뒤, 한 선수는 제일 왼쪽에 있는 음식부터 오른쪽으로, 다른 선수는 제일 오른쪽에 있는 음식부터 왼쪽으로 순서대로 먹는 방식으로 진행됩니다. 중앙에는 물을 배치하고, 물을 먼저 먹는 선수가 승리하게 됩니다.
- 이때, 대회의 공정성을 위해 두 선수가 먹는 음식의 종류와 양이 같아야 하며, 음식을 먹는 순서도 같아야 합니다. 또한, 이번 대회부터는 칼로리가 낮은 음식을 먼저 먹을 수 있게 배치하여 선수들이 음식을 더 잘 먹을 수 있게 하려고 합니다. 이번 대회를 위해 수웅이는 음식을 주문했는데, 대회의 조건을 고려하지 않고 음식을 주문하여 몇 개의 음식은 대회에 사용하지 못하게 되었습니다.
- 예를 들어, 3가지의 음식이 준비되어 있으며, 칼로리가 적은 순서대로 1번 음식을 3개, 2번 음식을 4개, 3번 음식을 6개 준비했으며, 물을 편의상 0번 음식이라고 칭한다면, 두 선수는 1번 음식 1개, 2번 음식 2개, 3번 음식 3개씩을 먹게 되므로 음식의 배치는 "1223330333221"이 됩니다. 따라서 1번 음식 1개는 대회에 사용하지 못합니다.
- 수웅이가 준비한 음식의 양을 칼로리가 적은 순서대로 나타내는 정수 배열 food가 주어졌을 때, 대회를 위한 음식의 배치를 나타내는 문자열을 return 하는 solution 함수를 완성해주세요.

```python
def solution(food):
    answer = ''
    for i in range(1,len(food)):
        for j in range(food[i]//2):
            answer+=str(i)
    reverse=answer[::-1]
    answer=answer+str(0)+reverse
    return answer
```

# 이웃한 칸
- 각 칸마다 색이 칠해진 2차원 격자 보드판이 있습니다. 그중 한 칸을 골랐을 때, 위, 아래, 왼쪽, 오른쪽 칸 중 같은 색깔로 칠해진 칸의 개수를 구하려고 합니다.
- 보드의 각 칸에 칠해진 색깔 이름이 담긴 이차원 문자열 리스트 board와 고른 칸의 위치를 나타내는 두 정수 h, w가 주어질 때 board[h][w]와 이웃한 칸들 중 같은 색으로 칠해져 있는 칸의 개수를 return 하도록 solution 함수를 완성해 주세요.

```python
def solution(board, h, w):
    answer = 0
    n=len(board)
    dh=[0,1,-1,0]
    dw=[1,0,0,-1]
    for i in range(4):
        h_check=h+dh[i]
        w_check=w+dw[i]
        if 0<=h_check<n and 0<=w_check<n:
            if board[h][w]==board[h_check][w_check]:
                answer+=1
    return answer
```

# 조건에 부합하는 중고거래 댓글 조회하기
- 다음은 중고거래 게시판 정보를 담은 USED_GOODS_BOARD 테이블과 중고거래 게시판 첨부파일 정보를 담은 USED_GOODS_REPLY 테이블입니다. USED_GOODS_BOARD 테이블은 다음과 같으며 BOARD_ID, WRITER_ID, TITLE, CONTENTS, PRICE, CREATED_DATE, STATUS, VIEWS은 게시글 ID, 작성자 ID, 게시글 제목, 게시글 내용, 가격, 작성일, 거래상태, 조회수를 의미합니다.
```
Column name	Type	Nullable
BOARD_ID	VARCHAR(5)	FALSE
WRITER_ID	VARCHAR(50)	FALSE
TITLE	VARCHAR(100)	FALSE
CONTENTS	VARCHAR(1000)	FALSE
PRICE	NUMBER	FALSE
CREATED_DATE	DATE	FALSE
STATUS	VARCHAR(10)	FALSE
VIEWS	NUMBER	FALSE
```
- USED_GOODS_REPLY 테이블은 다음과 같으며 REPLY_ID, BOARD_ID, WRITER_ID, CONTENTS, CREATED_DATE는 각각 댓글 ID, 게시글 ID, 작성자 ID, 댓글 내용, 작성일을 의미합니다.
```
Column name	Type	Nullable
REPLY_ID	VARCHAR(10)	FALSE
BOARD_ID	VARCHAR(5)	FALSE
WRITER_ID	VARCHAR(50)	FALSE
CONTENTS	VARCHAR(1000)	TRUE
CREATED_DATE	DATE	FALSE
```
- USED_GOODS_BOARD와 USED_GOODS_REPLY 테이블에서 2022년 10월에 작성된 게시글 제목, 게시글 ID, 댓글 ID, 댓글 작성자 ID, 댓글 내용, 댓글 작성일을 조회하는 SQL문을 작성해주세요. 결과는 댓글 작성일을 기준으로 오름차순 정렬해주시고, 댓글 작성일이 같다면 게시글 제목을 기준으로 오름차순 정렬해주세요.

```mysql
SELECT B.TITLE, B.BOARD_ID, R.REPLY_ID, R.WRITER_ID, R.CONTENTS, DATE_FORMAT(R.CREATED_DATE, '%Y-%m-%d')
FROM USED_GOODS_BOARD B JOIN USED_GOODS_REPLY R
ON B.BOARD_ID=R.BOARD_ID
WHERE MONTH(B.CREATED_DATE)=10 AND YEAR(B.CREATED_DATE)=2022
ORDER BY R.CREATED_DATE, B.TITLE ASC
```

# 재구매가 일어난 상품과 회원 리스트 구하기
- 다음은 어느 의류 쇼핑몰의 온라인 상품 판매 정보를 담은 ONLINE_SALE 테이블 입니다. ONLINE_SALE 테이블은 아래와 같은 구조로 되어있으며 ONLINE_SALE_ID, USER_ID, PRODUCT_ID, SALES_AMOUNT, SALES_DATE는 각각 온라인 상품 판매 ID, 회원 ID, 상품 ID, 판매량, 판매일을 나타냅니다.
- 동일한 날짜, 회원 ID, 상품 ID 조합에 대해서는 하나의 판매 데이터만 존재합니다.
- ONLINE_SALE 테이블에서 동일한 회원이 동일한 상품을 재구매한 데이터를 구하여, 재구매한 회원 ID와 재구매한 상품 ID를 출력하는 SQL문을 작성해주세요. 결과는 회원 ID를 기준으로 오름차순 정렬해주시고 회원 ID가 같다면 상품 ID를 기준으로 내림차순 정렬해주세요.

```mysql
SELECT USER_ID, PRODUCT_ID
FROM ONLINE_SALE
GROUP BY USER_ID, PRODUCT_ID HAVING COUNT(*)>1
ORDER BY USER_ID ASC, PRODUCT_ID DESC
```

# 대여 횟수가 많은 자동차들의 월별 대여 횟수 구하기
- 다음은 어느 자동차 대여 회사의 자동차 대여 기록 정보를 담은 CAR_RENTAL_COMPANY_RENTAL_HISTORY 테이블입니다. CAR_RENTAL_COMPANY_RENTAL_HISTORY 테이블은 아래와 같은 구조로 되어있으며, HISTORY_ID, CAR_ID, START_DATE, END_DATE 는 각각 자동차 대여 기록 ID, 자동차 ID, 대여 시작일, 대여 종료일을 나타냅니다.
- CAR_RENTAL_COMPANY_RENTAL_HISTORY 테이블에서 대여 시작일을 기준으로 2022년 8월부터 2022년 10월까지 총 대여 횟수가 5회 이상인 자동차들에 대해서 해당 기간 동안의 월별 자동차 ID 별 총 대여 횟수(컬럼명: RECORDS) 리스트를 출력하는 SQL문을 작성해주세요. 결과는 월을 기준으로 오름차순 정렬하고, 월이 같다면 자동차 ID를 기준으로 내림차순 정렬해주세요. 특정 월의 총 대여 횟수가 0인 경우에는 결과에서 제외해주세요.

```mysql
SELECT MONTH(START_DATE) MONTH, CAR_ID, COUNT(HISTORY_ID) RECORDS
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE CAR_ID IN(
    SELECT CAR_ID
    FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
    WHERE MONTH(START_DATE) IN (8,9,10)
    GROUP BY CAR_ID
    HAVING COUNT(HISTORY_ID)>=5)
AND MONTH(START_DATE) IN (8,9,10)
GROUP BY MONTH, CAR_ID
HAVING COUNT(HISTORY_ID)>=1
ORDER BY MONTH ASC, CAR_ID DESC
```

# 있었는데요 없었습니다
- ANIMAL_INS 테이블은 동물 보호소에 들어온 동물의 정보를 담은 테이블입니다. ANIMAL_INS 테이블 구조는 다음과 같으며, ANIMAL_ID, ANIMAL_TYPE, DATETIME, INTAKE_CONDITION, NAME, SEX_UPON_INTAKE는 각각 동물의 아이디, 생물 종, 보호 시작일, 보호 시작 시 상태, 이름, 성별 및 중성화 여부를 나타냅니다.
- ANIMAL_OUTS 테이블은 동물 보호소에서 입양 보낸 동물의 정보를 담은 테이블입니다. ANIMAL_OUTS 테이블 구조는 다음과 같으며, ANIMAL_ID, ANIMAL_TYPE, DATETIME, NAME, SEX_UPON_OUTCOME는 각각 동물의 아이디, 생물 종, 입양일, 이름, 성별 및 중성화 여부를 나타냅니다. ANIMAL_OUTS 테이블의 ANIMAL_ID는 ANIMAL_INS의 ANIMAL_ID의 외래 키입니다.
- 관리자의 실수로 일부 동물의 입양일이 잘못 입력되었습니다. 보호 시작일보다 입양일이 더 빠른 동물의 아이디와 이름을 조회하는 SQL문을 작성해주세요. 이때 결과는 보호 시작일이 빠른 순으로 조회해야합니다.

```mysql
SELECT I.ANIMAL_ID, I.NAME
FROM ANIMAL_INS I INNER JOIN ANIMAL_OUTS O
WHERE I.ANIMAL_ID=O.ANIMAL_ID AND I.DATETIME>O.DATETIME
ORDER BY I.DATETIME
```

# 특정 기간동안 대여 가능한 자동차들의 대여비용 구하기
- 다음은 어느 자동차 대여 회사에서 대여 중인 자동차들의 정보를 담은 CAR_RENTAL_COMPANY_CAR 테이블과 자동차 대여 기록 정보를 담은 CAR_RENTAL_COMPANY_RENTAL_HISTORY 테이블과 자동차 종류 별 대여 기간 종류 별 할인 정책 정보를 담은 CAR_RENTAL_COMPANY_DISCOUNT_PLAN 테이블 입니다.
- CAR_RENTAL_COMPANY_CAR 테이블은 아래와 같은 구조로 되어있으며, CAR_ID, CAR_TYPE, DAILY_FEE, OPTIONS 는 각각 자동차 ID, 자동차 종류, 일일 대여 요금(원), 자동차 옵션 리스트를 나타냅니다.
- 자동차 종류는 '세단', 'SUV', '승합차', '트럭', '리무진' 이 있습니다. 자동차 옵션 리스트는 콤마(',')로 구분된 키워드 리스트(예: ''열선시트,스마트키,주차감지센서'')로 되어있으며, 키워드 종류는 '주차감지센서', '스마트키', '네비게이션', '통풍시트', '열선시트', '후방카메라', '가죽시트' 가 있습니다.
- CAR_RENTAL_COMPANY_RENTAL_HISTORY 테이블은 아래와 같은 구조로 되어있으며, HISTORY_ID, CAR_ID, START_DATE, END_DATE 는 각각 자동차 대여 기록 ID, 자동차 ID, 대여 시작일, 대여 종료일을 나타냅니다.
- CAR_RENTAL_COMPANY_DISCOUNT_PLAN 테이블은 아래와 같은 구조로 되어있으며, PLAN_ID, CAR_TYPE, DURATION_TYPE, DISCOUNT_RATE 는 각각 요금 할인 정책 ID, 자동차 종류, 대여 기간 종류, 할인율(%)을 나타냅니다.
- 할인율이 적용되는 대여 기간 종류로는 '7일 이상' (대여 기간이 7일 이상 30일 미만인 경우), '30일 이상' (대여 기간이 30일 이상 90일 미만인 경우), '90일 이상' (대여 기간이 90일 이상인 경우) 이 있습니다. 대여 기간이 7일 미만인 경우 할인정책이 없습니다.
- CAR_RENTAL_COMPANY_CAR 테이블과 CAR_RENTAL_COMPANY_RENTAL_HISTORY 테이블과 CAR_RENTAL_COMPANY_DISCOUNT_PLAN 테이블에서 자동차 종류가 '세단' 또는 'SUV' 인 자동차 중 2022년 11월 1일부터 2022년 11월 30일까지 대여 가능하고 30일간의 대여 금액이 50만원 이상 200만원 미만인 자동차에 대해서 자동차 ID, 자동차 종류, 대여 금액(컬럼명: FEE) 리스트를 출력하는 SQL문을 작성해주세요. 결과는 대여 금액을 기준으로 내림차순 정렬하고, 대여 금액이 같은 경우 자동차 종류를 기준으로 오름차순 정렬, 자동차 종류까지 같은 경우 자동차 ID를 기준으로 내림차순 정렬해주세요.

```mysql
SELECT C.CAR_ID, C.CAR_TYPE, ROUND((C.DAILY_FEE *((100-D.DISCOUNT_RATE)*0.01))*30) FEE
FROM CAR_RENTAL_COMPANY_CAR C JOIN CAR_RENTAL_COMPANY_DISCOUNT_PLAN D
ON C.CAR_TYPE=D.CAR_TYPE AND D.DURATION_TYPE='30일 이상'
WHERE C.CAR_ID NOT IN (SELECT CAR_ID
                     FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
                     WHERE START_DATE BETWEEN '2022-11-01' AND '2022-11-30'
                     OR END_DATE BETWEEN '2022-11-01' AND '2022-11-30'
                     OR START_DATE<'2022-11-01' AND END_DATE>'2022-11-30'
)
AND (C.CAR_TYPE='세단' OR C.CAR_TYPE='SUV')
AND ROUND((C.DAILY_FEE *((100-D.DISCOUNT_RATE)*0.01))*30)>=500000
AND ROUND((C.DAILY_FEE *((100-D.DISCOUNT_RATE)*0.01))*30)<2000000
ORDER BY FEE DESC, C.CAR_TYPE, C.CAR_ID DESC
```

# 오프라인/온라인 판매 데이터 통합하기
- 다음은 어느 의류 쇼핑몰의 온라인 상품 판매 정보를 담은 ONLINE_SALE 테이블과 오프라인 상품 판매 정보를 담은 OFFLINE_SALE 테이블 입니다. ONLINE_SALE 테이블은 아래와 같은 구조로 되어있으며 ONLINE_SALE_ID, USER_ID, PRODUCT_ID, SALES_AMOUNT, SALES_DATE는 각각 온라인 상품 판매 ID, 회원 ID, 상품 ID, 판매량, 판매일을 나타냅니다.
- 동일한 날짜, 회원 ID, 상품 ID 조합에 대해서는 하나의 판매 데이터만 존재합니다.
- OFFLINE_SALE 테이블은 아래와 같은 구조로 되어있으며 OFFLINE_SALE_ID, PRODUCT_ID, SALES_AMOUNT, SALES_DATE는 각각 오프라인 상품 판매 ID, 상품 ID, 판매량, 판매일을 나타냅니다.
- 동일한 날짜, 상품 ID 조합에 대해서는 하나의 판매 데이터만 존재합니다.
- ONLINE_SALE 테이블과 OFFLINE_SALE 테이블에서 2022년 3월의 오프라인/온라인 상품 판매 데이터의 판매 날짜, 상품ID, 유저ID, 판매량을 출력하는 SQL문을 작성해주세요. OFFLINE_SALE 테이블의 판매 데이터의 USER_ID 값은 NULL 로 표시해주세요. 결과는 판매일을 기준으로 오름차순 정렬해주시고 판매일이 같다면 상품 ID를 기준으로 오름차순, 상품ID까지 같다면 유저 ID를 기준으로 오름차순 정렬해주세요.

```mysql
SELECT DATE_FORMAT(SALES_DATE, '%Y-%m-%d') SALES_DATE, PRODUCT_ID, USER_ID, SALES_AMOUNT
FROM ONLINE_SALE
WHERE SALES_DATE BETWEEN '2022-03-01' AND '2022-03-31'
UNION ALL
SELECT DATE_FORMAT(SALES_DATE, '%Y-%m-%d') SALES_DATE, PRODUCT_ID, NULL USER_ID, SALES_AMOUNT
FROM OFFLINE_SALE
WHERE SALES_DATE BETWEEN '2022-03-01' AND '2022-03-31'
ORDER BY SALES_DATE, PRODUCT_ID , USER_ID
```

# 입양 시각 구하기(2)
- ANIMAL_OUTS 테이블은 동물 보호소에서 입양 보낸 동물의 정보를 담은 테이블입니다. ANIMAL_OUTS 테이블 구조는 다음과 같으며, ANIMAL_ID, ANIMAL_TYPE, DATETIME, NAME, SEX_UPON_OUTCOME는 각각 동물의 아이디, 생물 종, 입양일, 이름, 성별 및 중성화 여부를 나타냅니다.
- 보호소에서는 몇 시에 입양이 가장 활발하게 일어나는지 알아보려 합니다. 0시부터 23시까지, 각 시간대별로 입양이 몇 건이나 발생했는지 조회하는 SQL문을 작성해주세요. 이때 결과는 시간대 순으로 정렬해야 합니다.

```mysql
WITH RECURSIVE HOURS AS(
    SELECT 0 AS NUM
    UNION ALL
    SELECT NUM+1 FROM HOURS
    WHERE NUM<23
)
SELECT NUM HOUR, IFNULL(COUNT, 0) COUNT
FROM (
    SELECT HOUR(DATETIME) HOUR, COUNT(*) COUNT
    FROM ANIMAL_OUTS
    GROUP BY HOUR(DATETIME)) A
    RIGHT JOIN HOURS H
ON A.HOUR=H.NUM
ORDER BY NUM
```

# 도넛과 막대 그래프
- 도넛 모양 그래프, 막대 모양 그래프, 8자 모양 그래프들이 있습니다. 이 그래프들은 1개 이상의 정점과, 정점들을 연결하는 단방향 간선으로 이루어져 있습니다.
- 크기가 n인 도넛 모양 그래프는 n개의 정점과 n개의 간선이 있습니다. 도넛 모양 그래프의 아무 한 정점에서 출발해 이용한 적 없는 간선을 계속 따라가면 나머지 n-1개의 정점들을 한 번씩 방문한 뒤 원래 출발했던 정점으로 돌아오게 됩니다. 도넛 모양 그래프의 형태는 다음과 같습니다.
- 크기가 n인 막대 모양 그래프는 n개의 정점과 n-1개의 간선이 있습니다. 막대 모양 그래프는 임의의 한 정점에서 출발해 간선을 계속 따라가면 나머지 n-1개의 정점을 한 번씩 방문하게 되는 정점이 단 하나 존재합니다. 막대 모양 그래프의 형태는 다음과 같습니다.
- 크기가 n인 8자 모양 그래프는 2n+1개의 정점과 2n+2개의 간선이 있습니다. 8자 모양 그래프는 크기가 동일한 2개의 도넛 모양 그래프에서 정점을 하나씩 골라 결합시킨 형태의 그래프입니다. 8자 모양 그래프의 형태는 다음과 같습니다.
- 도넛 모양 그래프, 막대 모양 그래프, 8자 모양 그래프가 여러 개 있습니다. 이 그래프들과 무관한 정점을 하나 생성한 뒤, 각 도넛 모양 그래프, 막대 모양 그래프, 8자 모양 그래프의 임의의 정점 하나로 향하는 간선들을 연결했습니다. 그 후 각 정점에 서로 다른 번호를 매겼습니다.
- 이때 당신은 그래프의 간선 정보가 주어지면 생성한 정점의 번호와 정점을 생성하기 전 도넛 모양 그래프의 수, 막대 모양 그래프의 수, 8자 모양 그래프의 수를 구해야 합니다.
- 그래프의 간선 정보를 담은 2차원 정수 배열 edges가 매개변수로 주어집니다. 이때, 생성한 정점의 번호, 도넛 모양 그래프의 수, 막대 모양 그래프의 수, 8자 모양 그래프의 수를 순서대로 1차원 정수 배열에 담아 return 하도록 solution 함수를 완성해 주세요.

```python
def solution(edges):
    answer = [0,0,0,0]
    vertex=[[] for i in range(len(edges)+10)]
    start=[0 for i in range(len(edges)+10)]
    arrive=[0 for i in range(len(edges)+10)]
    temp=0
    t=0
    for i in edges:
        start[i[0]]+=1
        arrive[i[1]]+=1
        if start[i[0]]==start[answer[0]]:
            temp=i[0]
        if start[i[0]]>start[answer[0]]:
            if arrive[i[0]]==0:
                answer[0]=i[0]
            if start[i[0]]==3:
                break
    if arrive[answer[0]]!=0:
        answer[0]=temp
    for i in edges:
        vertex[i[0]].append(i[1])
    for i in vertex[answer[0]]:
        t=i
        while(len(vertex[t])==1):
            t=vertex[t][0]
            if t==i:
                answer[1]+=1
                break
        if len(vertex[t])==0:
            answer[2]+=1
        elif len(vertex[t])==2:
            answer[3]+=1
    return answer
```

# 혼자 놀기의 달인
- 혼자서도 잘 노는 범희는 어느 날 방구석에 있는 숫자 카드 더미를 보더니 혼자 할 수 있는 재미있는 게임을 생각해냈습니다.
- 숫자 카드 더미에는 카드가 총 100장 있으며, 각 카드에는 1부터 100까지 숫자가 하나씩 적혀있습니다. 2 이상 100 이하의 자연수를 하나 정해 그 수보다 작거나 같은 숫자 카드들을 준비하고, 준비한 카드의 수만큼 작은 상자를 준비하면 게임을 시작할 수 있으며 게임 방법은 다음과 같습니다.
- 준비된 상자에 카드를 한 장씩 넣고, 상자를 무작위로 섞어 일렬로 나열합니다. 상자가 일렬로 나열되면 상자가 나열된 순서에 따라 1번부터 순차적으로 증가하는 번호를 붙입니다.
- 그 다음 임의의 상자를 하나 선택하여 선택한 상자 안의 숫자 카드를 확인합니다. 다음으로 확인한 카드에 적힌 번호에 해당하는 상자를 열어 안에 담긴 카드에 적힌 숫자를 확인합니다. 마찬가지로 숫자에 해당하는 번호를 가진 상자를 계속해서 열어가며, 열어야 하는 상자가 이미 열려있을 때까지 반복합니다.
- 이렇게 연 상자들은 1번 상자 그룹입니다. 이제 1번 상자 그룹을 다른 상자들과 섞이지 않도록 따로 둡니다. 만약 1번 상자 그룹을 제외하고 남는 상자가 없으면 그대로 게임이 종료되며, 이때 획득하는 점수는 0점입니다.
- 그렇지 않다면 남은 상자 중 다시 임의의 상자 하나를 골라 같은 방식으로 이미 열려있는 상자를 만날 때까지 상자를 엽니다. 이렇게 연 상자들은 2번 상자 그룹입니다.
- 1번 상자 그룹에 속한 상자의 수와 2번 상자 그룹에 속한 상자의 수를 곱한 값이 게임의 점수입니다.
- 상자 안에 들어있는 카드 번호가 순서대로 담긴 배열 cards가 매개변수로 주어질 때, 범희가 이 게임에서 얻을 수 있는 최고 점수를 구해서 return 하도록 solution 함수를 완성해주세요.
 
```python
def solution(cards):
    answer = 0
    group=[]
    used=[]
    num=0
    temp1=0
    temp2=0
    for i in cards:
        if i not in used:
            group.append([])
            t=i
            while(1):
                group[num].append(t)
                used.append(t)
                t=cards[t-1]
                if t==i:
                    break
            num+=1
    for i in group:
        if len(i)>temp1:
            temp2=temp1
            temp1=len(i)
        elif len(i)>temp2:
            temp2=len(i)
    answer=temp1*temp2
    return answer
```

# 삼각 달팽이
- 정수 n이 매개변수로 주어집니다. 다음 그림과 같이 밑변의 길이와 높이가 n인 삼각형에서 맨 위 꼭짓점부터 반시계 방향으로 달팽이 채우기를 진행한 후, 첫 행부터 마지막 행까지 모두 순서대로 합친 새로운 배열을 return 하도록 solution 함수를 완성해주세요.

```python
def solution(n):
    answer = [0 for i in range((n*(n+1))//2)]
    index=0
    p=1
    t1=n
    t2=1
    for i in range(1,len(answer)+1):
        answer[index]=i
        if p%3==1:
            if t2<t1:
                if p==1:
                    index+=t2
                else:
                    index=index+t2+p//3*2
                t2+=1
            else:
                p+=1
                t2=1
                t1-=1
                index+=1
        elif p%3==2:
            if t2<t1:
                index+=1
                t2+=1
            else:
                t2=1
                t1-=1
                index=index-n+p//3
                p+=1
        elif p%3==0:
            if t2<t1:
                index=index-n+t2+p//3-1
                t2+=1
            else:
                t2=1
                t1-=1
                index=index+(p//3)*2
                p+=1
    return answer
```

# 두 원 사이의 정수 쌍
- x축과 y축으로 이루어진 2차원 직교 좌표계에 중심이 원점인 서로 다른 크기의 원이 두 개 주어집니다. 반지름을 나타내는 두 정수 r1, r2가 매개변수로 주어질 때, 두 원 사이의 공간에 x좌표와 y좌표가 모두 정수인 점의 개수를 return하도록 solution 함수를 완성해주세요.
- ※ 각 원 위의 점도 포함하여 셉니다.

```python
from math import floor, ceil

def solution(r1, r2):
    answer = 0
    for i in range(1,r2+1):
        max_y=floor((r2*r2-i*i)**(1/2))
        min_y=ceil((r1*r1-i*i)**(1/2)) if r1>i else 0
        answer+=max_y-min_y+1
    answer=answer*4
    return answer
```

# 광물 캐기
- 마인은 곡괭이로 광산에서 광석을 캐려고 합니다. 마인은 다이아몬드 곡괭이, 철 곡괭이, 돌 곡괭이를 각각 0개에서 5개까지 가지고 있으며, 곡괭이로 광물을 캘 때는 피로도가 소모됩니다. 각 곡괭이로 광물을 캘 때의 피로도는 아래 표와 같습니다.
```
곡괭이\광물    다이아몬드    철    돌
다이아몬드        1         1      1
철               5         1      1
돌               25        5      1
```
- 예를 들어, 철 곡괭이는 다이아몬드를 캘 때 피로도 5가 소모되며, 철과 돌을 캘때는 피로도가 1씩 소모됩니다. 각 곡괭이는 종류에 상관없이 광물 5개를 캔 후에는 더 이상 사용할 수 없습니다.
- 마인은 다음과 같은 규칙을 지키면서 최소한의 피로도로 광물을 캐려고 합니다.
```
사용할 수 있는 곡괭이중 아무거나 하나를 선택해 광물을 캡니다.
한 번 사용하기 시작한 곡괭이는 사용할 수 없을 때까지 사용합니다.
광물은 주어진 순서대로만 캘 수 있습니다.
광산에 있는 모든 광물을 캐거나, 더 사용할 곡괭이가 없을 때까지 광물을 캡니다.
```
- 즉, 곡괭이를 하나 선택해서 광물 5개를 연속으로 캐고, 다음 곡괭이를 선택해서 광물 5개를 연속으로 캐는 과정을 반복하며, 더 사용할 곡괭이가 없거나 광산에 있는 모든 광물을 캘 때까지 과정을 반복하면 됩니다.
- 마인이 갖고 있는 곡괭이의 개수를 나타내는 정수 배열 picks와 광물들의 순서를 나타내는 문자열 배열 minerals가 매개변수로 주어질 때, 마인이 작업을 끝내기까지 필요한 최소한의 피로도를 return 하는 solution 함수를 완성해주세요.

```python
def solution(picks, minerals):
    answer = 0
    t=0
    num=0
    arr=[]
    dp=picks[0]
    ip=picks[1]
    sp=picks[2]
    for i in minerals:
        if i=="diamond":
            t+=100
        elif i=="iron":
            t+=10
        elif i=="stone":
            t+=1
        num+=1
        if num==5:
            arr.append(t)
            t=0
            num=0
    if len(arr)<(dp+ip+sp):
        arr.append(t)
    else:
        while(len(arr)>(dp+ip+sp)):
            arr.pop(-1)
    arr.sort(reverse=True)
    for i in arr:
        if dp>=1:
            answer+=i//100
            i=i%100
            answer+=i//10
            i=i%10
            answer+=i
            dp-=1
        elif ip>=1:
            answer+=(i//100)*5
            i=i%100
            answer+=i//10
            i=i%10
            answer+=i
            ip-=1
        elif sp>=1:
            answer+=(i//100)*25
            i=i%100
            answer+=(i//10)*5
            i=i%10
            answer+=i
            sp-=1
    return answer
```

# 무인도 여행
- 메리는 여름을 맞아 무인도로 여행을 가기 위해 지도를 보고 있습니다. 지도에는 바다와 무인도들에 대한 정보가 표시돼 있습니다. 지도는 1 x 1크기의 사각형들로 이루어진 직사각형 격자 형태이며, 격자의 각 칸에는 'X' 또는 1에서 9 사이의 자연수가 적혀있습니다. 지도의 'X'는 바다를 나타내며, 숫자는 무인도를 나타냅니다. 이때, 상, 하, 좌, 우로 연결되는 땅들은 하나의 무인도를 이룹니다. 지도의 각 칸에 적힌 숫자는 식량을 나타내는데, 상, 하, 좌, 우로 연결되는 칸에 적힌 숫자를 모두 합한 값은 해당 무인도에서 최대 며칠동안 머물 수 있는지를 나타냅니다. 어떤 섬으로 놀러 갈지 못 정한 메리는 우선 각 섬에서 최대 며칠씩 머물 수 있는지 알아본 후 놀러갈 섬을 결정하려 합니다.
- 지도를 나타내는 문자열 배열 maps가 매개변수로 주어질 때, 각 섬에서 최대 며칠씩 머무를 수 있는지 배열에 오름차순으로 담아 return 하는 solution 함수를 완성해주세요. 만약 지낼 수 있는 무인도가 없다면 -1을 배열에 담아 return 해주세요.

```python
import sys
sys.setrecursionlimit(10**5)

def solution(maps):
    answer = [0]
    for i in range(len(maps)):
        maps[i]=list(maps[i])
    used=[[0 for i in range(len(maps[0]))] for j in range(len(maps))]
    for i in range(len(maps)):
        for j in range(len(maps[0])):
            if maps[i][j]!='X' and not used[i][j]:
                check(j,i,maps,used,answer)
                answer.append(0)
    if answer[0]==0:
        answer[0]=-1
    elif answer[-1]==0:
        answer.pop()
    answer.sort()
    return answer

def check(x,y,maps,used,answer):
    if maps[y][x]!='X' and not used[y][x]:
        answer[-1]+=int(maps[y][x])
        used[y][x]=1
        if x-1>=0: check(x-1,y,maps,used,answer)
        if x+1<len(maps[0]): check(x+1,y,maps,used,answer)
        if y-1>=0: check(x,y-1,maps,used,answer)
        if y+1<len(maps): check(x,y+1,maps,used,answer)
    return

```

# 디펜스 게임
- 준호는 요즘 디펜스 게임에 푹 빠져 있습니다. 디펜스 게임은 준호가 보유한 병사 n명으로 연속되는 적의 공격을 순서대로 막는 게임입니다. 디펜스 게임은 다음과 같은 규칙으로 진행됩니다.
```
준호는 처음에 병사 n명을 가지고 있습니다.
매 라운드마다 enemy[i]마리의 적이 등장합니다.
남은 병사 중 enemy[i]명 만큼 소모하여 enemy[i]마리의 적을 막을 수 있습니다.
    예를 들어 남은 병사가 7명이고, 적의 수가 2마리인 경우, 현재 라운드를 막으면 7 - 2 = 5명의 병사가 남습니다.
    남은 병사의 수보다 현재 라운드의 적의 수가 더 많으면 게임이 종료됩니다.
게임에는 무적권이라는 스킬이 있으며, 무적권을 사용하면 병사의 소모없이 한 라운드의 공격을 막을 수 있습니다.
무적권은 최대 k번 사용할 수 있습니다.
```
- 준호는 무적권을 적절한 시기에 사용하여 최대한 많은 라운드를 진행하고 싶습니다.
- 준호가 처음 가지고 있는 병사의 수 n, 사용 가능한 무적권의 횟수 k, 매 라운드마다 공격해오는 적의 수가 순서대로 담긴 정수 배열 enemy가 매개변수로 주어집니다. 준호가 몇 라운드까지 막을 수 있는지 return 하도록 solution 함수를 완성해주세요.
 
```python
from heapq import heappush, heappop

def solution(n, k, enemy):
    heap=[]
    for i, e in enumerate(enemy):
        heappush(heap,e)
        if len(heap)>k:
            n-=heappop(heap)
        if n<0:
            return i
    return len(enemy)
```

# 방문 길이
- 게임 캐릭터를 4가지 명령어를 통해 움직이려 합니다. 명령어는 다음과 같습니다.

U: 위쪽으로 한 칸 가기

D: 아래쪽으로 한 칸 가기

R: 오른쪽으로 한 칸 가기

L: 왼쪽으로 한 칸 가기

- 캐릭터는 좌표평면의 (0, 0) 위치에서 시작합니다. 좌표평면의 경계는 왼쪽 위(-5, 5), 왼쪽 아래(-5, -5), 오른쪽 위(5, 5), 오른쪽 아래(5, -5)로 이루어져 있습니다.
- 예를 들어, "ULURRDLLU"로 명령했다면 1번 명령어부터 7번 명령어까지 다음과 같이 움직입니다. 8번 명령어부터 9번 명령어까지 다음과 같이 움직입니다.
- 이때, 우리는 게임 캐릭터가 지나간 길 중 캐릭터가 처음 걸어본 길의 길이를 구하려고 합니다. 예를 들어 위의 예시에서 게임 캐릭터가 움직인 길이는 9이지만, 캐릭터가 처음 걸어본 길의 길이는 7이 됩니다. (8, 9번 명령어에서 움직인 길은 2, 3번 명령어에서 이미 거쳐 간 길입니다)
- 단, 좌표평면의 경계를 넘어가는 명령어는 무시합니다.
- 명령어가 매개변수 dirs로 주어질 때, 게임 캐릭터가 처음 걸어본 길의 길이를 구하여 return 하는 solution 함수를 완성해 주세요.

```python
def solution(dirs):
    answer = 0
    dic_ver=[[0 for i in range(11)] for i in range(10)]
    dic_hor=[[0 for i in range(10)] for i in range(11)]
    index=[5,5]
    for i in dirs:
        if i=='U':
            if index[1]!=10:
                if dic_hor[index[0]][index[1]]==0:
                    answer+=1
                    dic_hor[index[0]][index[1]]=1
                index[1]+=1
        elif i=='D':
            if index[1]!=0:
                if dic_hor[index[0]][index[1]-1]==0:
                    answer+=1
                    dic_hor[index[0]][index[1]-1]=1
                index[1]-=1
        elif i=='R':
            if index[0]!=10:
                if dic_ver[index[0]][index[1]]==0:
                    answer+=1
                    dic_ver[index[0]][index[1]]=1
                index[0]+=1
        elif i=='L':
            if index[0]!=0:
                if dic_ver[index[0]-1][index[1]]==0:
                    answer+=1
                    dic_ver[index[0]-1][index[1]]=1
                index[0]-=1
    return answer
```

# 스킬트리
- 선행 스킬이란 어떤 스킬을 배우기 전에 먼저 배워야 하는 스킬을 뜻합니다. 예를 들어 선행 스킬 순서가 스파크 → 라이트닝 볼트 → 썬더일때, 썬더를 배우려면 먼저 라이트닝 볼트를 배워야 하고, 라이트닝 볼트를 배우려면 먼저 스파크를 배워야 합니다.
- 위 순서에 없는 다른 스킬(힐링 등)은 순서에 상관없이 배울 수 있습니다. 따라서 스파크 → 힐링 → 라이트닝 볼트 → 썬더와 같은 스킬트리는 가능하지만, 썬더 → 스파크나 라이트닝 볼트 → 스파크 → 힐링 → 썬더와 같은 스킬트리는 불가능합니다.
- 선행 스킬 순서 skill과 유저들이 만든 스킬트리1를 담은 배열 skill_trees가 매개변수로 주어질 때, 가능한 스킬트리 개수를 return 하는 solution 함수를 작성해주세요.

```python
def solution(skill, skill_trees):
    answer = 0
    skill_arr=list(skill)
    for i in skill_trees:
        skills=list(i)
        pre=0
        for j in skills:
            if j in skill:
                if j==skill_arr[pre]:
                    pre+=1
                else:
                    answer-=1
                    break
        answer+=1
    return answer
```

# 프로세스
- 운영체제의 역할 중 하나는 컴퓨터 시스템의 자원을 효율적으로 관리하는 것입니다. 이 문제에서는 운영체제가 다음 규칙에 따라 프로세스를 관리할 경우 특정 프로세스가 몇 번째로 실행되는지 알아내면 됩니다.
```
1. 실행 대기 큐(Queue)에서 대기중인 프로세스 하나를 꺼냅니다.
2. 큐에 대기중인 프로세스 중 우선순위가 더 높은 프로세스가 있다면 방금 꺼낸 프로세스를 다시 큐에 넣습니다.
3. 만약 그런 프로세스가 없다면 방금 꺼낸 프로세스를 실행합니다.
  3.1 한 번 실행한 프로세스는 다시 큐에 넣지 않고 그대로 종료됩니다.
```
- 예를 들어 프로세스 4개 [A, B, C, D]가 순서대로 실행 대기 큐에 들어있고, 우선순위가 [2, 1, 3, 2]라면 [C, D, A, B] 순으로 실행하게 됩니다.
- 현재 실행 대기 큐(Queue)에 있는 프로세스의 중요도가 순서대로 담긴 배열 priorities와, 몇 번째로 실행되는지 알고싶은 프로세스의 위치를 알려주는 location이 매개변수로 주어질 때, 해당 프로세스가 몇 번째로 실행되는지 return 하도록 solution 함수를 작성해주세요.

```python
def solution(priorities, location):
    answer = 0
    length=len(priorities)
    i=0
    while(max(priorities)>0):
        if priorities[i]==0:
            priorities.append(0)
            i+=1
        elif priorities[i]<max(priorities):
            priorities.append(priorities[i])
            priorities[i]=0
            i+=1
        else:
            priorities.append(0)
            priorities[i]=0
            answer+=1
            if i%length==location:
                return answer
            i+=1
```

# 마법의 엘리베이터
- 마법의 세계에 사는 민수는 아주 높은 탑에 살고 있습니다. 탑이 너무 높아서 걸어 다니기 힘든 민수는 마법의 엘리베이터를 만들었습니다. 마법의 엘리베이터의 버튼은 특별합니다. 마법의 엘리베이터에는 -1, +1, -10, +10, -100, +100 등과 같이 절댓값이 10c (c ≥ 0 인 정수) 형태인 정수들이 적힌 버튼이 있습니다. 마법의 엘리베이터의 버튼을 누르면 현재 층 수에 버튼에 적혀 있는 값을 더한 층으로 이동하게 됩니다. 단, 엘리베이터가 위치해 있는 층과 버튼의 값을 더한 결과가 0보다 작으면 엘리베이터는 움직이지 않습니다. 민수의 세계에서는 0층이 가장 아래층이며 엘리베이터는 현재 민수가 있는 층에 있습니다.
- 마법의 엘리베이터를 움직이기 위해서 버튼 한 번당 마법의 돌 한 개를 사용하게 됩니다.예를 들어, 16층에 있는 민수가 0층으로 가려면 -1이 적힌 버튼을 6번, -10이 적힌 버튼을 1번 눌러 마법의 돌 7개를 소모하여 0층으로 갈 수 있습니다. 하지만, +1이 적힌 버튼을 4번, -10이 적힌 버튼 2번을 누르면 마법의 돌 6개를 소모하여 0층으로 갈 수 있습니다.
- 마법의 돌을 아끼기 위해 민수는 항상 최소한의 버튼을 눌러서 이동하려고 합니다. 민수가 어떤 층에서 엘리베이터를 타고 0층으로 내려가는데 필요한 마법의 돌의 최소 개수를 알고 싶습니다. 민수와 마법의 엘리베이터가 있는 층을 나타내는 정수 storey 가 주어졌을 때, 0층으로 가기 위해 필요한 마법의 돌의 최소값을 return 하도록 solution 함수를 완성하세요.

```python
from math import log10, ceil

def solution(storey):
    answer = 0
    for i in range(1, ceil(log10(storey))+2):
        if (storey%10**i)//10**(i-1)>=6:
            answer+=10-(storey%10**i)//10**(i-1)
            storey+=(10-(storey%10**i)//10**(i-1))*10**(i-1)
        elif (storey%10**i)//10**(i-1)<5:
            answer+=(storey%10**i)//10**(i-1)
            storey-=(storey%10**i//10**(i-1))*10**(i-1)
        else:
            if (storey%10**(i+1))//10**i>=5:
                answer+=10-(storey%10**i)//10**(i-1)
                storey+=(10-(storey%10**i)//10**(i-1))*10**(i-1)
            else:
                answer+=(storey%10**i)//10**(i-1)
                storey-=(storey%10**i//10**(i-1))*10**(i-1)
    return answer
```

# 귤 고르기
- 경화는 과수원에서 귤을 수확했습니다. 경화는 수확한 귤 중 'k'개를 골라 상자 하나에 담아 판매하려고 합니다. 그런데 수확한 귤의 크기가 일정하지 않아 보기에 좋지 않다고 생각한 경화는 귤을 크기별로 분류했을 때 서로 다른 종류의 수를 최소화하고 싶습니다.
- 예를 들어, 경화가 수확한 귤 8개의 크기가 [1, 3, 2, 5, 4, 5, 2, 3] 이라고 합시다. 경화가 귤 6개를 판매하고 싶다면, 크기가 1, 4인 귤을 제외한 여섯 개의 귤을 상자에 담으면, 귤의 크기의 종류가 2, 3, 5로 총 3가지가 되며 이때가 서로 다른 종류가 최소일 때입니다.
- 경화가 한 상자에 담으려는 귤의 개수 k와 귤의 크기를 담은 배열 tangerine이 매개변수로 주어집니다. 경화가 귤 k개를 고를 때 크기가 서로 다른 종류의 수의 최솟값을 return 하도록 solution 함수를 작성해주세요.

```python
def solution(k, tangerine):
    answer = 0
    dic={}
    for i in tangerine:
        if i not in dic:
            dic[i]=1
        else:
            dic[i]+=1
    dic_sorted=sorted(dic, key=lambda x:dic[x], reverse=True)
    i=0
    while(k>0):
        k-=dic[dic_sorted[i]]
        answer+=1
        i+=1
    return answer
```

# 롤케이크 자르기
- 철수는 롤케이크를 두 조각으로 잘라서 동생과 한 조각씩 나눠 먹으려고 합니다. 이 롤케이크에는 여러가지 토핑들이 일렬로 올려져 있습니다. 철수와 동생은 롤케이크를 공평하게 나눠먹으려 하는데, 그들은 롤케이크의 크기보다 롤케이크 위에 올려진 토핑들의 종류에 더 관심이 많습니다. 그래서 잘린 조각들의 크기와 올려진 토핑의 개수에 상관없이 각 조각에 동일한 가짓수의 토핑이 올라가면 공평하게 롤케이크가 나누어진 것으로 생각합니다.
- 예를 들어, 롤케이크에 4가지 종류의 토핑이 올려져 있다고 합시다. 토핑들을 1, 2, 3, 4와 같이 번호로 표시했을 때, 케이크 위에 토핑들이 [1, 2, 1, 3, 1, 4, 1, 2] 순서로 올려져 있습니다. 만약 세 번째 토핑(1)과 네 번째 토핑(3) 사이를 자르면 롤케이크의 토핑은 [1, 2, 1], [3, 1, 4, 1, 2]로 나뉘게 됩니다. 철수가 [1, 2, 1]이 놓인 조각을, 동생이 [3, 1, 4, 1, 2]가 놓인 조각을 먹게 되면 철수는 두 가지 토핑(1, 2)을 맛볼 수 있지만, 동생은 네 가지 토핑(1, 2, 3, 4)을 맛볼 수 있으므로, 이는 공평하게 나누어진 것이 아닙니다. 만약 롤케이크의 네 번째 토핑(3)과 다섯 번째 토핑(1) 사이를 자르면 [1, 2, 1, 3], [1, 4, 1, 2]로 나뉘게 됩니다. 이 경우 철수는 세 가지 토핑(1, 2, 3)을, 동생도 세 가지 토핑(1, 2, 4)을 맛볼 수 있으므로, 이는 공평하게 나누어진 것입니다. 공평하게 롤케이크를 자르는 방법은 여러가지 일 수 있습니다. 위의 롤케이크를 [1, 2, 1, 3, 1], [4, 1, 2]으로 잘라도 공평하게 나뉩니다. 어떤 경우에는 롤케이크를 공평하게 나누지 못할 수도 있습니다.
- 롤케이크에 올려진 토핑들의 번호를 저장한 정수 배열 topping이 매개변수로 주어질 때, 롤케이크를 공평하게 자르는 방법의 수를 return 하도록 solution 함수를 완성해주세요.

```python
def solution(topping):
    answer = 0
    divide1=set()
    divide2=set(topping)
    dic={}
    for i in topping:
        if i not in dic:
            dic[i]=1
        else:
            dic[i]+=1
    for i in range(len(topping)):
        a=topping.pop()
        dic[a]-=1
        if dic[a]==0:
            divide2.remove(a)
        divide1.add(a)
        if len(divide1)==len(divide2):
            answer+=1
    return answer
```

# 정수 삼각형
- 위와 같은 삼각형의 꼭대기에서 바닥까지 이어지는 경로 중, 거쳐간 숫자의 합이 가장 큰 경우를 찾아보려고 합니다. 아래 칸으로 이동할 때는 대각선 방향으로 한 칸 오른쪽 또는 왼쪽으로만 이동 가능합니다. 예를 들어 3에서는 그 아래칸의 8 또는 1로만 이동이 가능합니다.
- 삼각형의 정보가 담긴 배열 triangle이 매개변수로 주어질 때, 거쳐간 숫자의 최댓값을 return 하도록 solution 함수를 완성하세요.

```python
def solution(triangle):
    for i in range(len(triangle)-2,-1,-1):
        for j in range(len(triangle[i])):
            triangle[i][j]=max(triangle[i+1][j]+triangle[i][j],triangle[i+1][j+1]+triangle[i][j])
    return triangle[0][0]
```

# 야근 지수
- 회사원 Demi는 가끔은 야근을 하는데요, 야근을 하면 야근 피로도가 쌓입니다. 야근 피로도는 야근을 시작한 시점에서 남은 일의 작업량을 제곱하여 더한 값입니다. Demi는 N시간 동안 야근 피로도를 최소화하도록 일할 겁니다.Demi가 1시간 동안 작업량 1만큼을 처리할 수 있다고 할 때, 퇴근까지 남은 N 시간과 각 일에 대한 작업량 works에 대해 야근 피로도를 최소화한 값을 리턴하는 함수 solution을 완성해주세요.

```python
from heapq import heapify,heappush,heappop

def solution(n, works):
    answer = 0
    w=0
    if sum(works)<=n:
        return 0
    works=[-1*i for i in works]
    heapify(works)
    while n:
        w=heappop(works)
        w+=1
        heappush(works,w)
        n-=1
    for i in works:
        answer+=i**2
    return answer
```

# 최고의 집합
- 자연수 n 개로 이루어진 중복 집합(multi set, 편의상 이후에는 "집합"으로 통칭) 중에 다음 두 조건을 만족하는 집합을 최고의 집합이라고 합니다.
1. 각 원소의 합이 S가 되는 수의 집합
2.위 조건을 만족하면서 각 원소의 곱 이 최대가 되는 집합
- 예를 들어서 자연수 2개로 이루어진 집합 중 합이 9가 되는 집합은 다음과 같이 4개가 있습니다.
- { 1, 8 }, { 2, 7 }, { 3, 6 }, { 4, 5 }
- 그중 각 원소의 곱이 최대인 { 4, 5 }가 최고의 집합입니다.
- 집합의 원소의 개수 n과 모든 원소들의 합 s가 매개변수로 주어질 때, 최고의 집합을 return 하는 solution 함수를 완성해주세요.

```python
def solution(n, s):
    answer = []
    if n==1:
        answer.append(s)
        return answer
    elif n==s:
        answer=[1 for i in range(s)]
        return answer
    elif n>s:
        answer.append(-1)
        return answer
    else:
        q=s//n
        r=s%n
        answer=[q for i in range(n)]
        for i in range(r):
            answer[i]+=1
        answer.sort()
    return answer
```

# 숫자 게임
- xx 회사의 2xN명의 사원들은 N명씩 두 팀으로 나눠 숫자 게임을 하려고 합니다. 두 개의 팀을 각각 A팀과 B팀이라고 하겠습니다. 숫자 게임의 규칙은 다음과 같습니다.
```
먼저 모든 사원이 무작위로 자연수를 하나씩 부여받습니다.
각 사원은 딱 한 번씩 경기를 합니다.
각 경기당 A팀에서 한 사원이, B팀에서 한 사원이 나와 서로의 수를 공개합니다. 그때 숫자가 큰 쪽이 승리하게 되고, 승리한 사원이 속한 팀은 승점을 1점 얻게 됩니다.
만약 숫자가 같다면 누구도 승점을 얻지 않습니다.
```
- 전체 사원들은 우선 무작위로 자연수를 하나씩 부여받았습니다. 그다음 A팀은 빠르게 출전순서를 정했고 자신들의 출전 순서를 B팀에게 공개해버렸습니다. B팀은 그것을 보고 자신들의 최종 승점을 가장 높이는 방법으로 팀원들의 출전 순서를 정했습니다. 이때의 B팀이 얻는 승점을 구해주세요.
- A 팀원들이 부여받은 수가 출전 순서대로 나열되어있는 배열 A와 i번째 원소가 B팀의 i번 팀원이 부여받은 수를 의미하는 배열 B가 주어질 때, B 팀원들이 얻을 수 있는 최대 승점을 return 하도록 solution 함수를 완성해주세요.

```python
def solution(A, B):
    answer = 0
    A.sort(reverse=True)
    B.sort(reverse=True)
    num=0
    for i in range(len(A)):
        if B[num]>A[i]:
            answer+=1
            num+=1
    return answer
```

# 기지국 설치
- N개의 아파트가 일렬로 쭉 늘어서 있습니다. 이 중에서 일부 아파트 옥상에는 4g 기지국이 설치되어 있습니다. 기술이 발전해 5g 수요가 높아져 4g 기지국을 5g 기지국으로 바꾸려 합니다. 그런데 5g 기지국은 4g 기지국보다 전달 범위가 좁아, 4g 기지국을 5g 기지국으로 바꾸면 어떤 아파트에는 전파가 도달하지 않습니다.
- 예를 들어 11개의 아파트가 쭉 늘어서 있고, [4, 11] 번째 아파트 옥상에는 4g 기지국이 설치되어 있습니다. 만약 이 4g 기지국이 전파 도달 거리가 1인 5g 기지국으로 바뀔 경우 모든 아파트에 전파를 전달할 수 없습니다. (전파의 도달 거리가 W일 땐, 기지국이 설치된 아파트를 기준으로 전파를 양쪽으로 W만큼 전달할 수 있습니다.)
- 이때, 우리는 5g 기지국을 최소로 설치하면서 모든 아파트에 전파를 전달하려고 합니다. 위의 예시에선 최소 3개의 아파트 옥상에 기지국을 설치해야 모든 아파트에 전파를 전달할 수 있습니다.
- 아파트의 개수 N, 현재 기지국이 설치된 아파트의 번호가 담긴 1차원 배열 stations, 전파의 도달 거리 W가 매개변수로 주어질 때, 모든 아파트에 전파를 전달하기 위해 증설해야 할 기지국 개수의 최솟값을 리턴하는 solution 함수를 완성해주세요

```python
from math import ceil

def solution(n, stations, w):
    answer = 0
    k=0
    for i in stations:
        if i-w-1<=0:
            k=i+w
        else:
            if i-w-k-1>0:
                answer+=ceil((i-w-k-1)/(w*2+1))
            k=i+w
    if k<n:
        answer+=ceil((n-k)/(w*2+1))
    return answer
```

# 베스트앨범
- 스트리밍 사이트에서 장르 별로 가장 많이 재생된 노래를 두 개씩 모아 베스트 앨범을 출시하려 합니다. 노래는 고유 번호로 구분하며, 노래를 수록하는 기준은 다음과 같습니다.
```
속한 노래가 많이 재생된 장르를 먼저 수록합니다.
장르 내에서 많이 재생된 노래를 먼저 수록합니다.
장르 내에서 재생 횟수가 같은 노래 중에서는 고유 번호가 낮은 노래를 먼저 수록합니다.
```
- 노래의 장르를 나타내는 문자열 배열 genres와 노래별 재생 횟수를 나타내는 정수 배열 plays가 주어질 때, 베스트 앨범에 들어갈 노래의 고유 번호를 순서대로 return 하도록 solution 함수를 완성하세요.

```python
def solution(genres, plays):
    answer = []
    dic={}
    for i in genres:
        if i not in dic:
            dic[i]=[[],0]
    for i in range(len(plays)):
        dic[genres[i]][0].append([plays[i],i])
        dic[genres[i]][1]+=plays[i]
    for i in dic.keys():
        dic[i][0].sort(key=lambda x:(x[0],-x[1]), reverse=True)
    genres_sorted=sorted(dic.items(), key=lambda x:x[1][1], reverse=True)
    for i in genres_sorted:
        if len(i[1][0])==1:
            answer.append(i[1][0][0][1])
        else:
            for j in range(2):
                answer.append(i[1][0][j][1])
    return answer
```

# 스티커 모으기(2)
- N개의 스티커가 원형으로 연결되어 있습니다. 다음 그림은 N = 8인 경우의 예시입니다.
- 원형으로 연결된 스티커에서 몇 장의 스티커를 뜯어내어 뜯어낸 스티커에 적힌 숫자의 합이 최대가 되도록 하고 싶습니다. 단 스티커 한 장을 뜯어내면 양쪽으로 인접해있는 스티커는 찢어져서 사용할 수 없게 됩니다.
- 예를 들어 위 그림에서 14가 적힌 스티커를 뜯으면 인접해있는 10, 6이 적힌 스티커는 사용할 수 없습니다. 스티커에 적힌 숫자가 배열 형태로 주어질 때, 스티커를 뜯어내어 얻을 수 있는 숫자의 합의 최댓값을 return 하는 solution 함수를 완성해 주세요. 원형의 스티커 모양을 위해 배열의 첫 번째 원소와 마지막 원소가 서로 연결되어 있다고 간주합니다.

```python
def solution(sticker):
    answer = 0
    a1=[]
    a2=[]
    for i in sticker:
        a1.append(i)
        a2.append(i)
    if len(sticker)<=3:
        return max(sticker)
    for i in range(1,len(a1)-1):
        if i==1:
            a1[i]=max(a1[i-1],a1[i])
        else:
            a1[i]=max(a1[i-2]+a1[i],a1[i-1])
    for i in range(2,len(a2)):
        if i==2:
            a2[i]=max(a2[i-1],a2[i])
        else:
            a2[i]=max(a2[i-2]+a2[i],a2[i-1])
    answer=max(max(a1),max(a2))
    return answer
``` 

# 섬 연결하기
- n개의 섬 사이에 다리를 건설하는 비용(costs)이 주어질 때, 최소의 비용으로 모든 섬이 서로 통행 가능하도록 만들 때 필요한 최소 비용을 return 하도록 solution을 완성하세요.
- 다리를 여러 번 건너더라도, 도달할 수만 있으면 통행 가능하다고 봅니다. 예를 들어 A 섬과 B 섬 사이에 다리가 있고, B 섬과 C 섬 사이에 다리가 있으면 A 섬과 C 섬은 서로 통행 가능합니다.
```python
def solution(n, costs):
    answer = 0
    check=[0]
    min_distance=10000000
    t=0
    while len(check)<n:
        for i in range(len(costs)):
            if (costs[i][0] in check and costs[i][1] not in check) or (costs[i][1] in check and costs[i][0] not in check):
                if costs[i][2]<min_distance:
                    min_distance=costs[i][2]
                    t=i
        if costs[t][0] in check:
            check.append(costs[t][1])
        else:
            check.append(costs[t][0])
        answer+=costs[t][2]
        costs.pop(t)
        min_distance=10000000
        t=0
    return answer
```


# 디스크 컨트롤러  
- 하드디스크는 한 번에 하나의 작업만 수행할 수 있습니다. 디스크 컨트롤러를 구현하는 방법은 여러 가지가 있습니다. 가장 일반적인 방법은 요청이 들어온 순서대로 처리하는 것입니다.
- 각 작업에 대해 [작업이 요청되는 시점, 작업의 소요시간]을 담은 2차원 배열 jobs가 매개변수로 주어질 때, 작업의 요청부터 종료까지 걸린 시간의 평균을 가장 줄이는 방법으로 처리하면 평균이 얼마가 되는지 return 하도록 solution 함수를 작성해주세요. (단, 소수점 이하의 수는 버립니다)

```python
from heapq import heappush, heappop

def solution(jobs):
    cur_time=0
    pro_time=0
    heap=[]
    fin=0
    fin_time=0
    run=0
    i=0
    jobs.sort(key=lambda x:x[0])
    while(fin<len(jobs)):
        for j in range(i,len(jobs)):
            if jobs[i][0]==cur_time:
                heappush(heap,[jobs[i][1],jobs[i][0]])
                i+=1
            else:
                break
        if run==1:
            if cur_time==fin_time:
                run=0
        if run==0:
            if heap:
                run=1
                t=heappop(heap)
                pro_time+=(cur_time+t[0]-t[1])
                fin+=1
                fin_time=cur_time+t[0]
        cur_time+=1
    return pro_time//len(jobs)
```

# 가장 긴 팰린드롬
- 앞뒤를 뒤집어도 똑같은 문자열을 팰린드롬(palindrome)이라고 합니다.
- 문자열 s가 주어질 때, s의 부분문자열(Substring)중 가장 긴 팰린드롬의 길이를 return 하는 solution 함수를 완성해 주세요.
- 예를들면, 문자열 s가 "abcdcba"이면 7을 return하고 "abacde"이면 3을 return합니다.

```python
def solution(s):
    answer = 1
    if len(s)==1:
        return 1
    for i in range(len(s)-1):
        l=0
        j=1
        if s[i]==s[i+1]:
            l=2
            if l>answer:
                answer=l
            while 1:
                if i-j<0 or i+1+j>=len(s):
                    break
                elif s[i-j]==s[i+1+j]:
                    l=2+2*j
                    if l>answer:
                        answer=l
                    j+=1
                else:
                    break
        if i==0:
            continue
        j=0
        if s[i-1]==s[i+1]:
            l=3
            if l>answer:
                answer=l
            while 1:
                if i-1-j<0 or i+1+j>=len(s):
                    break
                elif s[i-1-j]==s[i+1+j]:
                    l=3+2*j
                    if l>answer:
                        answer=l
                    j+=1
                else:
                    break
    return answer
```

# 연속 펄스 부분 수열의 합
- 어떤 수열의 연속 부분 수열에 같은 길이의 펄스 수열을 각 원소끼리 곱하여 연속 펄스 부분 수열을 만들려 합니다. 펄스 수열이란 [1, -1, 1, -1 …] 또는 [-1, 1, -1, 1 …] 과 같이 1 또는 -1로 시작하면서 1과 -1이 번갈아 나오는 수열입니다.
- 예를 들어 수열 [2, 3, -6, 1, 3, -1, 2, 4]의 연속 부분 수열 [3, -6, 1]에 펄스 수열 [1, -1, 1]을 곱하면 연속 펄스 부분수열은 [3, 6, 1]이 됩니다. 또 다른 예시로 연속 부분 수열 [3, -1, 2, 4]에 펄스 수열 [-1, 1, -1, 1]을 곱하면 연속 펄스 부분수열은 [-3, -1, -2, 4]이 됩니다.
- 정수 수열 sequence가 매개변수로 주어질 때, 연속 펄스 부분 수열의 합 중 가장 큰 것을 return 하도록 solution 함수를 완성해주세요.

```python
def solution(sequence):
    answer = [0 for i in range(len(sequence))]
    for i in range(len(sequence)):
        if i%2==0:
            sequence[i]=-sequence[i]
    answer[0]=sequence[0]
    for i in range(1,len(sequence)):
        answer[i]=max(answer[i-1],0)+sequence[i]
    answer1=max(answer)
    for i in range(len(sequence)):
        sequence[i]=-sequence[i]
    answer[0]=sequence[0]
    for i in range(1,len(sequence)):
        answer[i]=max(answer[i-1],0)+sequence[i]
    answer2=max(answer)
    return max(answer1,answer2)
```

# 합승 택시 요금
- 밤늦게 귀가할 때 안전을 위해 항상 택시를 이용하던 무지는 최근 야근이 잦아져 택시를 더 많이 이용하게 되어 택시비를 아낄 수 있는 방법을 고민하고 있습니다. "무지"는 자신이 택시를 이용할 때 동료인 어피치 역시 자신과 비슷한 방향으로 가는 택시를 종종 이용하는 것을 알게 되었습니다. "무지"는 "어피치"와 귀가 방향이 비슷하여 택시 합승을 적절히 이용하면 택시요금을 얼마나 아낄 수 있을 지 계산해 보고 "어피치"에게 합승을 제안해 보려고 합니다.
- 지점의 개수 n, 출발지점을 나타내는 s, A의 도착지점을 나타내는 a, B의 도착지점을 나타내는 b, 지점 사이의 예상 택시요금을 나타내는 fares가 매개변수로 주어집니다. 이때, A, B 두 사람이 s에서 출발해서 각각의 도착 지점까지 택시를 타고 간다고 가정할 때, 최저 예상 택시요금을 계산해서 return 하도록 solution 함수를 완성해 주세요.

```python
from heapq import heappush,heappop

def solution(n, s, a, b, fares):
    INF = 100001 * n
    answer = INF
    graph = [[INF] * (n+1) for _ in range(n+1)]
    for start,end,f in fares:
        graph[start][end] = f
        graph[end][start] = f
    for k in range(n+1):
        for i in range(n+1):
            for j in range(n+1):
                graph[i][j] = min(graph[i][j], graph[i][k]+graph[k][j])
    for x in range(1,n+1):
        graph[x][x] = 0
    for x in range(1,n+1):
        answer = min(graph[s][x]+graph[x][a]+graph[x][b],answer)
    return answer
```


# 풍선 터트리기
- 일렬로 나열된 n개의 풍선이 있습니다. 모든 풍선에는 서로 다른 숫자가 써져 있습니다. 당신은 다음 과정을 반복하면서 풍선들을 단 1개만 남을 때까지 계속 터트리려고 합니다.
```
임의의 인접한 두 풍선을 고른 뒤, 두 풍선 중 하나를 터트립니다.
터진 풍선으로 인해 풍선들 사이에 빈 공간이 생겼다면, 빈 공간이 없도록 풍선들을 중앙으로 밀착시킵니다.
```
- 여기서 조건이 있습니다. 인접한 두 풍선 중에서 번호가 더 작은 풍선을 터트리는 행위는 최대 1번만 할 수 있습니다. 즉, 어떤 시점에서 인접한 두 풍선 중 번호가 더 작은 풍선을 터트렸다면, 그 이후에는 인접한 두 풍선을 고른 뒤 번호가 더 큰 풍선만을 터트릴 수 있습니다.
- 당신은 어떤 풍선이 최후까지 남을 수 있는지 알아보고 싶습니다. 위에 서술된 조건대로 풍선을 터트리다 보면, 어떤 풍선은 최후까지 남을 수도 있지만, 어떤 풍선은 무슨 수를 쓰더라도 마지막까지 남기는 것이 불가능할 수도 있습니다.
- 일렬로 나열된 풍선들의 번호가 담긴 배열 a가 주어집니다. 위에 서술된 규칙대로 풍선들을 1개만 남을 때까지 터트렸을 때 최후까지 남기는 것이 가능한 풍선들의 개수를 return 하도록 solution 함수를 완성해주세요.
 ```python
def solution(a):
    if len(a)<=2:
        return len(a)
    answer = 2
    arr_front=[0 for i in range(len(a))]
    arr_back=[0 for i in range(len(a))]
    minimum=1000000001
    for i in range(len(a)):
        if a[i]<minimum:
            minimum=a[i]
        arr_front[i]=minimum
    minimum=1000000001
    for i in range(len(a)-1,-1,-1):
        if a[i]<minimum:
            minimum=a[i]
        arr_back[i]=minimum
    for i in range(1,len(a)-1):
        if arr_front[i-1]>a[i] or arr_back[i+1]>a[i]:
            answer+=1
    return answer
```

# 다단계 칫솔 판매
- 민호는 다단계 조직을 이용하여 칫솔을 판매하고 있습니다. 판매원이 칫솔을 판매하면 그 이익이 피라미드 조직을 타고 조금씩 분배되는 형태의 판매망입니다. 어느정도 판매가 이루어진 후, 조직을 운영하던 민호는 조직 내 누가 얼마만큼의 이득을 가져갔는지가 궁금해졌습니다. 예를 들어, 민호가 운영하고 있는 다단계 칫솔 판매 조직이 아래 그림과 같다고 합시다.
- 민호는 center이며, 파란색 네모는 여덟 명의 판매원을 표시한 것입니다. 각각은 자신을 조직에 참여시킨 추천인에 연결되어 피라미드 식의 구조를 이루고 있습니다. 조직의 이익 분배 규칙은 간단합니다. 모든 판매원은 칫솔의 판매에 의하여 발생하는 이익에서 10% 를 계산하여 자신을 조직에 참여시킨 추천인에게 배분하고 나머지는 자신이 가집니다. 모든 판매원은 자신이 칫솔 판매에서 발생한 이익 뿐만 아니라, 자신이 조직에 추천하여 가입시킨 판매원에게서 발생하는 이익의 10% 까지 자신에 이익이 됩니다. 자신에게 발생하는 이익 또한 마찬가지의 규칙으로 자신의 추천인에게 분배됩니다. 단, 10% 를 계산할 때에는 원 단위에서 절사하며, 10%를 계산한 금액이 1 원 미만인 경우에는 이득을 분배하지 않고 자신이 모두 가집니다.
- 각 판매원의 이름을 담은 배열 enroll, 각 판매원을 다단계 조직에 참여시킨 다른 판매원의 이름을 담은 배열 referral, 판매량 집계 데이터의 판매원 이름을 나열한 배열 seller, 판매량 집계 데이터의 판매 수량을 나열한 배열 amount가 매개변수로 주어질 때, 각 판매원이 득한 이익금을 나열한 배열을 return 하도록 solution 함수를 완성해주세요. 판매원에게 배분된 이익금의 총합을 계산하여(정수형으로), 입력으로 주어진 enroll에 이름이 포함된 순서에 따라 나열하면 됩니다.

```python
from math import ceil, floor

def solution(enroll, referral, seller, amount):
    answer = [0 for i in range(len(enroll))]
    dic={}
    for i in range(len(enroll)):
        dic[enroll[i]]=[i,referral[i]]
    for i in range(len(amount)):
        s=seller[i]
        earn=amount[i]*100
        while referral[dic[s][0]]!="-":
            if earn==0:
                break
            answer[dic[s][0]]+=ceil(earn*0.9)
            earn=floor(earn*0.1)
            s=dic[s][1]
        if earn>0:
            answer[dic[s][0]]+=ceil(earn*0.9)
    return answer
```

# 순위
- n명의 권투선수가 권투 대회에 참여했고 각각 1번부터 n번까지 번호를 받았습니다. 권투 경기는 1대1 방식으로 진행이 되고, 만약 A 선수가 B 선수보다 실력이 좋다면 A 선수는 B 선수를 항상 이깁니다. 심판은 주어진 경기 결과를 가지고 선수들의 순위를 매기려 합니다. 하지만 몇몇 경기 결과를 분실하여 정확하게 순위를 매길 수 없습니다.
- 선수의 수 n, 경기 결과를 담은 2차원 배열 results가 매개변수로 주어질 때 정확하게 순위를 매길 수 있는 선수의 수를 return 하도록 solution 함수를 작성해주세요.

```python
def solution(n, results):
    if n==1:
        return 1
    answer = 0
    number=[i for i in range(n+1)]
    tree=[]
    p_dic={}
    c_dic={}
    for i in results:
        if i[0] not in tree:
            tree.append(i[0])
            number[i[0]]=Node()
        if i[1] not in tree:
            tree.append(i[1])
            number[i[1]]=Node()
        number[i[0]].child.append(number[i[1]])
        number[i[1]].parent.append(number[i[0]])
    for i in range(1,n+1):
        if len(number[i].p_search(p_dic))+len(number[i].c_search(c_dic))==n-1:
            answer+=1
    return answer

class Node:
    def __init__(self):
        self.parent=[]
        self.child=[]
        
    def p_search(self, p_dic):
        if self in p_dic:
            return p_dic[self]
        else:
            s=set()
            for j in self.parent:
                s.add(j)
                s=s.union(j.p_search(p_dic))
            p_dic[self]=s
            return s

    def c_search(self, c_dic):
        if self in c_dic:
            return c_dic[self]
        else:
            s=set()
            for j in self.child:
                s.add(j)
                s=s.union(j.c_search(c_dic))
            c_dic[self]=s
            return s
```

# 단속카메라
- 고속도로를 이동하는 모든 차량이 고속도로를 이용하면서 단속용 카메라를 한 번은 만나도록 카메라를 설치하려고 합니다.
- 고속도로를 이동하는 차량의 경로 routes가 매개변수로 주어질 때, 모든 차량이 한 번은 단속용 카메라를 만나도록 하려면 최소 몇 대의 카메라를 설치해야 하는지를 return 하도록 solution 함수를 완성하세요.

```python
def solution(routes):
    answer = 0
    routes.sort(key=lambda x:x[0])
    m=-30000
    for i, j in routes:
        if i>m:
            answer+=1
            m=j
        m=min(m,j)
    return answer
```

# 이중우선순위큐
- 이중 우선순위 큐는 다음 연산을 할 수 있는 자료구조를 말합니다.
```
명령어	수신 탑(높이)
I 숫자	큐에 주어진 숫자를 삽입합니다.
D 1	큐에서 최댓값을 삭제합니다.
D -1	큐에서 최솟값을 삭제합니다.
```
- 이중 우선순위 큐가 할 연산 operations가 매개변수로 주어질 때, 모든 연산을 처리한 후 큐가 비어있으면 [0,0] 비어있지 않으면 [최댓값, 최솟값]을 return 하도록 solution 함수를 구현해주세요.

```python
from heapq import heappush, heappop

def solution(operations):
    answer = []
    pos_heap=[]
    neg_heap=[]
    for i in operations:
        if i[0]=="I":
            num=int(i[2:])
            heappush(pos_heap,num)
            heappush(neg_heap,-num)
        elif i[0]=="D":
            if not pos_heap:
                continue
            elif i[2]=="1":
                m=heappop(neg_heap)
                pos_heap.remove(-m)
            else:
                n=heappop(pos_heap)
                neg_heap.remove(-n)
    if not neg_heap:
        answer.append(0)
    else:
        answer.append(-heappop(neg_heap))
    if not pos_heap:
        answer.append(0)
    else:
        answer.append(heappop(pos_heap))
    return answer
```

# 네트워크
- 네트워크란 컴퓨터 상호 간에 정보를 교환할 수 있도록 연결된 형태를 의미합니다. 예를 들어, 컴퓨터 A와 컴퓨터 B가 직접적으로 연결되어있고, 컴퓨터 B와 컴퓨터 C가 직접적으로 연결되어 있을 때 컴퓨터 A와 컴퓨터 C도 간접적으로 연결되어 정보를 교환할 수 있습니다. 따라서 컴퓨터 A, B, C는 모두 같은 네트워크 상에 있다고 할 수 있습니다.
- 컴퓨터의 개수 n, 연결에 대한 정보가 담긴 2차원 배열 computers가 매개변수로 주어질 때, 네트워크의 개수를 return 하도록 solution 함수를 작성하시오.

```python
def solution(n, computers):
    answer = 0
    visited=[]
    for i in range(n):
        if i not in visited:
            answer+=1
            search(i,computers,visited)
    return answer


def search(n,computers,visited):
    for i in range(len(computers)):
        if computers[n][i]==1:
            if i not in visited:
                visited.append(i)
                search(i,computers,visited)
```

# 등굣길
- 계속되는 폭우로 일부 지역이 물에 잠겼습니다. 물에 잠기지 않은 지역을 통해 학교를 가려고 합니다. 집에서 학교까지 가는 길은 m x n 크기의 격자모양으로 나타낼 수 있습니다.
- 가장 왼쪽 위, 즉 집이 있는 곳의 좌표는 (1, 1)로 나타내고 가장 오른쪽 아래, 즉 학교가 있는 곳의 좌표는 (m, n)으로 나타냅니다.
- 격자의 크기 m, n과 물이 잠긴 지역의 좌표를 담은 2차원 배열 puddles이 매개변수로 주어집니다. 오른쪽과 아래쪽으로만 움직여 집에서 학교까지 갈 수 있는 최단경로의 개수를 1,000,000,007로 나눈 나머지를 return 하도록 solution 함수를 작성해주세요.

```python
def solution(m, n, puddles):
    case=[[0 for i in range(m)] for i in range(n)]
    case[0][0]=1
    for i in range(n):
        for j in range(m):
            if i==0 and j==0:
                continue
            if [j+1,i+1] not in puddles:
                if i==0:
                    case[i][j]=case[i][j-1]
                elif j==0:
                    case[i][j]=case[i-1][j]
                else:
                    case[i][j]=case[i][j-1]+case[i-1][j]
    return case[n-1][m-1]%1000000007
```

# 가장 먼 노드
- n개의 노드가 있는 그래프가 있습니다. 각 노드는 1부터 n까지 번호가 적혀있습니다. 1번 노드에서 가장 멀리 떨어진 노드의 갯수를 구하려고 합니다. 가장 멀리 떨어진 노드란 최단경로로 이동했을 때 간선의 개수가 가장 많은 노드들을 의미합니다.
- 노드의 개수 n, 간선에 대한 정보가 담긴 2차원 배열 vertex가 매개변수로 주어질 때, 1번 노드로부터 가장 멀리 떨어진 노드가 몇 개인지를 return 하도록 solution 함수를 작성해주세요.

```python
from collections import deque

def solution(n, edge):
    answer = 0
    dic={}
    visited=[[0,0] for i in range(n+1)]
    visited[1]=[1,0]
    dis=0
    q=deque([1])
    for i in range(1,n+1):
        dic[i]=set()
    for i,j in edge:
        dic[i].add(j)
        dic[j].add(i)
    while q:
        dis+=1
        ad=[]
        while q:
            ad.append(q.popleft())
        for i in ad:
            for j in dic[i]:
                if not visited[j][0]:
                    visited[j][0]=1
                    visited[j][1]=dis
                    q.append(j)
    for i in visited:
        if i[1]==dis-1:
            answer+=1
    return answer
```

# 부대복귀
- 강철부대의 각 부대원이 여러 지역에 뿔뿔이 흩어져 특수 임무를 수행 중입니다. 지도에서 강철부대가 위치한 지역을 포함한 각 지역은 유일한 번호로 구분되며, 두 지역 간의 길을 통과하는 데 걸리는 시간은 모두 1로 동일합니다. 임무를 수행한 각 부대원은 지도 정보를 이용하여 최단시간에 부대로 복귀하고자 합니다. 다만 적군의 방해로 인해, 임무의 시작 때와 다르게 되돌아오는 경로가 없어져 복귀가 불가능한 부대원도 있을 수 있습니다.
- 강철부대가 위치한 지역을 포함한 총지역의 수 n, 두 지역을 왕복할 수 있는 길 정보를 담은 2차원 정수 배열 roads, 각 부대원이 위치한 서로 다른 지역들을 나타내는 정수 배열 sources, 강철부대의 지역 destination이 주어졌을 때, 주어진 sources의 원소 순서대로 강철부대로 복귀할 수 있는 최단시간을 담은 배열을 return하는 solution 함수를 완성해주세요. 복귀가 불가능한 경우 해당 부대원의 최단시간은 -1입니다.

```python
from collections import deque

def solution(n, roads, sources, destination):
    answer = []
    dic={}
    visited=[[0,-1] for i in range(n+1)]
    visited[destination]=[1,0]
    dis=0
    q=deque([int(destination)])
    for i in range(1,n+1):
        dic[i]=set()
    for i,j in roads:
        dic[i].add(j)
        dic[j].add(i)
    while q:
        dis+=1
        ad=[]
        while q:
            ad.append(q.popleft())
        for i in ad:
            for j in dic[i]:
                if not visited[j][0]:
                    visited[j][0]=1
                    visited[j][1]=dis
                    q.append(j)
    for i in sources:
        answer.append(visited[i][1])
    return answer
```

# 거스름돈
- Finn은 편의점에서 야간 아르바이트를 하고 있습니다. 야간에 손님이 너무 없어 심심한 Finn은 손님들께 거스름돈을 n 원을 줄 때 방법의 경우의 수를 구하기로 하였습니다.
- 거슬러 줘야 하는 금액 n과 Finn이 현재 보유하고 있는 돈의 종류 money가 매개변수로 주어질 때, Finn이 n 원을 거슬러 줄 방법의 수를 return 하도록 solution 함수를 완성해 주세요.

```python
def solution(n, money):
    arr=[0 for i in range(n+1)]
    arr[0]=1
    for i in money:
        for j in range(i,n+1):
            arr[j]+=arr[j-i]
    return arr[n]
```

# 유사 칸토어 비트열
- 수학에서 칸토어 집합은 0과 1 사이의 실수로 이루어진 집합으로, [0, 1]부터 시작하여 각 구간을 3등분하여 가운데 구간을 반복적으로 제외하는 방식으로 만들어집니다.
- 남아는 칸토어 집합을 조금 변형하여 유사 칸토어 비트열을 만들었습니다. 유사 칸토어 비트열은 다음과 같이 정의됩니다.
- 0 번째 유사 칸토어 비트열은 "1" 입니다.
- n(1 ≤ n) 번째 유사 칸토어 비트열은 n - 1 번째 유사 칸토어 비트열에서의 1을 11011로 치환하고 0을 00000로 치환하여 만듭니다.
- 남아는 n 번째 유사 칸토어 비트열에서 특정 구간 내의 1의 개수가 몇 개인지 궁금해졌습니다.
- n과 1의 개수가 몇 개인지 알고 싶은 구간을 나타내는 l, r이 주어졌을 때 그 구간 내의 1의 개수를 return 하도록 solution 함수를 완성해주세요.

```python
def solution(n, l, r):
    answer = 0
    for i in range(l-1,r):
        while i>=5:
            if i%5==2:
                break
            i=i//5
        if i<5 and i!=2:
            answer+=1
    return answer
```

# 요격 시스템
- A 나라가 B 나라를 침공하였습니다. B 나라의 대부분의 전략 자원은 아이기스 군사 기지에 집중되어 있기 때문에 A 나라는 B 나라의 아이기스 군사 기지에 융단폭격을 가했습니다.
- A 나라의 공격에 대항하여 아이기스 군사 기지에서는 무수히 쏟아지는 폭격 미사일들을 요격하려고 합니다. 이곳에는 백발백중을 자랑하는 요격 시스템이 있지만 운용 비용이 상당하기 때문에 미사일을 최소로 사용해서 모든 폭격 미사일을 요격하려 합니다.
- A 나라와 B 나라가 싸우고 있는 이 세계는 2 차원 공간으로 이루어져 있습니다. A 나라가 발사한 폭격 미사일은 x 축에 평행한 직선 형태의 모양이며 개구간을 나타내는 정수 쌍 (s, e) 형태로 표현됩니다. B 나라는 특정 x 좌표에서 y 축에 수평이 되도록 미사일을 발사하며, 발사된 미사일은 해당 x 좌표에 걸쳐있는 모든 폭격 미사일을 관통하여 한 번에 요격할 수 있습니다. 단, 개구간 (s, e)로 표현되는 폭격 미사일은 s와 e에서 발사하는 요격 미사일로는 요격할 수 없습니다. 요격 미사일은 실수인 x 좌표에서도 발사할 수 있습니다.
- 각 폭격 미사일의 x 좌표 범위 목록 targets이 매개변수로 주어질 때, 모든 폭격 미사일을 요격하기 위해 필요한 요격 미사일 수의 최솟값을 return 하도록 solution 함수를 완성해 주세요.

```python
def solution(targets):
    answer = 1
    targets.sort(key=lambda x:x[0])
    e=targets[0][1]
    for i,j in targets:
        if i>=e:
            answer+=1
            e=j
        e=min(e,j)
    return answer
```

# 조이스틱
- 조이스틱으로 알파벳 이름을 완성하세요. 맨 처음엔 A로만 이루어져 있습니다.
- ex) 완성해야 하는 이름이 세 글자면 AAA, 네 글자면 AAAA
- 조이스틱을 각 방향으로 움직이면 아래와 같습니다.
```
▲ - 다음 알파벳
▼ - 이전 알파벳 (A에서 아래쪽으로 이동하면 Z로)
◀ - 커서를 왼쪽으로 이동 (첫 번째 위치에서 왼쪽으로 이동하면 마지막 문자에 커서)
▶ - 커서를 오른쪽으로 이동 (마지막 위치에서 오른쪽으로 이동하면 첫 번째 문자에 커서)
```
- 만들고자 하는 이름 name이 매개변수로 주어질 때, 이름에 대해 조이스틱 조작 횟수의 최솟값을 return 하도록 solution 함수를 만드세요

```python
from string import ascii_uppercase

def solution(name):
    answer = 0
    dic={}
    for i in range(len(ascii_uppercase)):
        dic[ascii_uppercase[i]]=i
    dif=[0 for i in range(len(name))]
    for i in range(len(dif)):
        if name[i]!='A':
            answer+=min(dic[name[i]],26-dic[name[i]])
            dif[i]=1
    con=0
    t=0
    idx=0
    last=len(name)
    for i in range(len(dif)):
        if dif[i]==0:
            last=i
            t+=1
            if t>=con:
                con=t
                idx=i
        else:
            t=0
    answer+=min(min(len(name)-idx-1,idx-con)+len(name)-con-1,last)
    return answer
```

# 숫자 블록
- 그렙시에는 숫자 0이 적힌 블록들이 설치된 도로에 다른 숫자가 적힌 블록들을 설치하기로 하였습니다. 숫자 블록을 설치하는 규칙은 다음과 같습니다.
- 블록에 적힌 번호가 n 일 때, 가장 첫 블록은 n * 2번째 위치에 설치합니다. 그 다음은 n * 3, 그 다음은 n * 4, ...위치에 설치합니다. 기존에 설치된 블록은 빼고 새로운 블록을 집어넣습니다.
- 블록은 1이 적힌 블록부터 숫자를 1씩 증가시키며 순서대로 설치합니다. 예를 들어 1이 적힌 블록은 2, 3, 4, 5, ... 인 위치에 우선 설치합니다. 그 다음 2가 적힌 블록은 4, 6, 8, 10, ... 인 위치에 설치하고, 3이 적힌 블록은 6, 9, 12... 인 위치에 설치합니다.
- 이렇게 3이 적힌 블록까지 설치하고 나면 첫 10개의 블록에 적힌 번호는 [0, 1, 1, 2, 1, 3, 1, 2, 3, 2]가 됩니다.
- 그렙시는 길이가 1,000,000,000인 도로에 1부터 10,000,000까지의 숫자가 적힌 블록들을 이용해 위의 규칙대로 모두 설치 했습니다.
- 그렙시의 시장님은 특정 구간에 어떤 블록이 깔려 있는지 알고 싶습니다.
- 구간을 나타내는 두 정수 begin, end 가 매개변수로 주어 질 때, 그 구간에 깔려 있는 블록의 숫자 배열을 return하는 solution 함수를 완성해 주세요.

```python
from math import ceil

def solution(begin, end):
    answer = []
    for i in range(begin, end+1):
        answer.append(div(i)[-1])
    return answer

def div(n):
    if n==1:
        return [0]
    arr1=[]
    arr2=[]
    for i in range(1,ceil(n**(1/2))+1):
        if n%i==0 and i!=n:
            arr1.append(i)
    for i in arr1:
        if n//i<=10000000 and n//i!=n:
            arr2.append(n//i)
    arr1+=arr2
    arr1=set(arr1)
    arr1=list(arr1)
    arr1.sort()
    return arr1
```

# 혼자서 하는 틱택토
- 틱택토는 두 사람이 하는 게임으로 처음에 3x3의 빈칸으로 이루어진 게임판에 선공이 "O", 후공이 "X"를 번갈아가면서 빈칸에 표시하는 게임입니다. 가로, 세로, 대각선으로 3개가 같은 표시가 만들어지면 같은 표시를 만든 사람이 승리하고 게임이 종료되며 9칸이 모두 차서 더 이상 표시를 할 수 없는 경우에는 무승부로 게임이 종료됩니다.
- 할 일이 없어 한가한 머쓱이는 두 사람이 하는 게임인 틱택토를 다음과 같이 혼자서 하려고 합니다.
- 혼자서 선공과 후공을 둘 다 맡는다.
- 틱택토 게임을 시작한 후 "O"와 "X"를 혼자서 번갈아 가면서 표시를 하면서 진행한다.
- 틱택토는 단순한 규칙으로 게임이 금방 끝나기에 머쓱이는 한 게임이 종료되면 다시 3x3 빈칸을 그린 뒤 다시 게임을 반복했습니다. 그렇게 틱택토 수 십 판을 했더니 머쓱이는 게임 도중에 다음과 같이 규칙을 어기는 실수를 했을 수도 있습니다.
- "O"를 표시할 차례인데 "X"를 표시하거나 반대로 "X"를 표시할 차례인데 "O"를 표시한다.
- 선공이나 후공이 승리해서 게임이 종료되었음에도 그 게임을 진행한다.
- 게임 도중 게임판을 본 어느 순간 머쓱이는 본인이 실수를 했는지 의문이 생겼습니다. 혼자서 틱택토를 했기에 게임하는 과정을 지켜본 사람이 없어 이를 알 수는 없습니다. 그러나 게임판만 봤을 때 실제로 틱택토 규칙을 지켜서 진행했을 때 나올 수 있는 상황인지는 판단할 수 있을 것 같고 문제가 없다면 게임을 이어서 하려고 합니다.
- 머쓱이가 혼자서 게임을 진행하다 의문이 생긴 틱택토 게임판의 정보를 담고 있는 문자열 배열 board가 매개변수로 주어질 때, 이 게임판이 규칙을 지켜서 틱택토를 진행했을 때 나올 수 있는 게임 상황이면 1을 아니라면 0을 return 하는 solution 함수를 작성해 주세요.

```python
def solution(board):
    answer = 1
    o=0
    x=0
    row_o=0
    row_x=0
    row_d1=[]
    row_d2=[]
    for i in range(3):
        for j in range(3):
            if board[i][j]=='O':
                o+=1
            elif board[i][j]=='X':
                x+=1
            if i==j:
                row_d1.append(board[i][j])
        if board[i]=="OOO":
            row_o+=1
        elif board[i]=="XXX":
            row_x+=1
    row_d2.append(board[0][2])
    row_d2.append(board[1][1])
    row_d2.append(board[2][0])
    row_1=[]
    for i in range(3):
        row_1.append(board[i][0])
    if row_1==['O','O','O']:
        row_o+=1
    if row_1==['X','X','X']:
        row_x+=1
    row_2=[]
    for i in range(3):
        row_2.append(board[i][1])
    if row_2==['O','O','O']:
        row_o+=1
    if row_2==['X','X','X']:
        row_x+=1
    row_3=[]
    for i in range(3):
        row_3.append(board[i][2])
    if row_3==['O','O','O']:
        row_o+=1
    if row_3==['X','X','X']:
        row_x+=1
    if row_d1==['O','O','O']:
        row_o+=1
        print("d1")
    if row_d1==['X','X','X']:
        row_x+=1
    if row_d2==['O','O','O']:
        row_o+=1
    if row_d2==['X','X','X']:
        row_x+=1
    if row_o==1 and row_x==1:
        answer=0
    if row_x>=2:
        answer=0
    if row_o>=3:
        answer=0
    if row_o>=1 and x>=o:
        answer=0
    if row_x==1 and o>x:
        answer=0
    if o<x:
        answer=0
    if o-x>=2:
        answer=0
    return answer
```

# 점 찍기
- 좌표평면을 좋아하는 진수는 x축과 y축이 직교하는 2차원 좌표평면에 점을 찍으면서 놀고 있습니다. 진수는 두 양의 정수 k, d가 주어질 때 다음과 같이 점을 찍으려 합니다.
- 원점(0, 0)으로부터 x축 방향으로 a*k(a = 0, 1, 2, 3 ...), y축 방향으로 b*k(b = 0, 1, 2, 3 ...)만큼 떨어진 위치에 점을 찍습니다.
- 원점과 거리가 d를 넘는 위치에는 점을 찍지 않습니다.
- 예를 들어, k가 2, d가 4인 경우에는 (0, 0), (0, 2), (0, 4), (2, 0), (2, 2), (4, 0) 위치에 점을 찍어 총 6개의 점을 찍습니다.
- 정수 k와 원점과의 거리를 나타내는 정수 d가 주어졌을 때, 점이 총 몇 개 찍히는지 return 하는 solution 함수를 완성하세요.

```python
def solution(k, d):
    answer = 0
    for i in range(0,d+1,k):
        answer+=int((d**2-i**2)**(0.5))//k+1
    return answer
```

# 하노이의 탑
- 하노이 탑(Tower of Hanoi)은 퍼즐의 일종입니다. 세 개의 기둥과 이 기동에 꽂을 수 있는 크기가 다양한 원판들이 있고, 퍼즐을 시작하기 전에는 한 기둥에 원판들이 작은 것이 위에 있도록 순서대로 쌓여 있습니다. 게임의 목적은 다음 두 가지 조건을 만족시키면서, 한 기둥에 꽂힌 원판들을 그 순서 그대로 다른 기둥으로 옮겨서 다시 쌓는 것입니다.
- 한 번에 하나의 원판만 옮길 수 있습니다.
- 큰 원판이 작은 원판 위에 있어서는 안됩니다.
- 하노이 탑의 세 개의 기둥을 왼쪽 부터 1번, 2번, 3번이라고 하겠습니다. 1번에는 n개의 원판이 있고 이 n개의 원판을 3번 원판으로 최소 횟수로 옮기려고 합니다.
- 1번 기둥에 있는 원판의 개수 n이 매개변수로 주어질 때, n개의 원판을 3번 원판으로 최소로 옮기는 방법을 return하는 solution를 완성해주세요.

```python
import sys
sys.setrecursionlimit(100000)

def solution(n):
    answer = []
    hanoi(n,1,2,3,answer)
    return answer

def hanoi(n,dep,mid,arr,answer):
    if n>=2:
        hanoi(n-1,dep,arr,mid,answer)
    answer.append([dep,arr])
    if n>=2:
        hanoi(n-1,mid,dep,arr,answer)
    return
```

# 테이블 해시 함수
- 완호가 관리하는 어떤 데이터베이스의 한 테이블은 모두 정수 타입인 컬럼들로 이루어져 있습니다. 테이블은 2차원 행렬로 표현할 수 있으며 열은 컬럼을 나타내고, 행은 튜플을 나타냅니다.
- 첫 번째 컬럼은 기본키로서 모든 튜플에 대해 그 값이 중복되지 않도록 보장됩니다. 완호는 이 테이블에 대한 해시 함수를 다음과 같이 정의하였습니다.
- 해시 함수는 col, row_begin, row_end을 입력으로 받습니다.
- 테이블의 튜플을 col번째 컬럼의 값을 기준으로 오름차순 정렬을 하되, 만약 그 값이 동일하면 기본키인 첫 번째 컬럼의 값을 기준으로 내림차순 정렬합니다.
- 정렬된 데이터에서 S_i를 i 번째 행의 튜플에 대해 각 컬럼의 값을 i 로 나눈 나머지들의 합으로 정의합니다.
- row_begin ≤ i ≤ row_end 인 모든 S_i를 누적하여 bitwise XOR 한 값을 해시 값으로서 반환합니다.
- 테이블의 데이터 data와 해시 함수에 대한 입력 col, row_begin, row_end이 주어졌을 때 테이블의 해시 값을 return 하도록 solution 함수를 완성해주세요.

```python
def solution(data, col, row_begin, row_end):
    answer = 0
    data.sort(key=lambda x:(x[col-1],-x[0]))
    s=[]
    for i in range(row_begin,row_end+1):
        temp=0
        for j in data[i-1]:
            temp+=j%i
        s.append(temp)
    for i in s:
        answer=answer^i
    return answer
```

# 줄 서는 방법
- n명의 사람이 일렬로 줄을 서고 있습니다. n명의 사람들에게는 각각 1번부터 n번까지 번호가 매겨져 있습니다. n명이 사람을 줄을 서는 방법은 여러가지 방법이 있습니다. 예를 들어서 3명의 사람이 있다면 다음과 같이 6개의 방법이 있습니다.
```
[1, 2, 3]
[1, 3, 2]
[2, 1, 3]
[2, 3, 1]
[3, 1, 2]
[3, 2, 1]
```
- 사람의 수 n과, 자연수 k가 주어질 때, 사람을 나열 하는 방법을 사전 순으로 나열 했을 때, k번째 방법을 return하는 solution 함수를 완성해주세요.

```python
from math import factorial

def solution(n, k):
    answer = []
    k-=1
    num=[i for i in range(n+1)]
    for i in range(n,1,-1):
        t=factorial(i-1)
        answer.append(num.pop(k//t+1))
        k=k%t
    answer.append(num[1])
    return answer
```

# 행렬 테두리 회전하기
- rows x columns 크기인 행렬이 있습니다. 행렬에는 1부터 rows x columns까지의 숫자가 한 줄씩 순서대로 적혀있습니다. 이 행렬에서 직사각형 모양의 범위를 여러 번 선택해, 테두리 부분에 있는 숫자들을 시계방향으로 회전시키려 합니다. 각 회전은 (x1, y1, x2, y2)인 정수 4개로 표현하며, 그 의미는 다음과 같습니다.
- x1 행 y1 열부터 x2 행 y2 열까지의 영역에 해당하는 직사각형에서 테두리에 있는 숫자들을 한 칸씩 시계방향으로 회전합니다.
- 행렬의 세로 길이(행 개수) rows, 가로 길이(열 개수) columns, 그리고 회전들의 목록 queries가 주어질 때, 각 회전들을 배열에 적용한 뒤, 그 회전에 의해 위치가 바뀐 숫자들 중 가장 작은 숫자들을 순서대로 배열에 담아 return 하도록 solution 함수를 완성해주세요.

```python
from collections import deque

def solution(rows, columns, queries):
    answer = []
    matrix=[[i for i in range(j*columns+1,(j+1)*columns+1)] for j in range(rows)]
    for i in queries:
        arr=rotate(matrix, i)
        matrix=arr[0]
        answer.append(arr[1])
    return answer

def rotate(matrix, query):
    d=deque()
    i=[query[0],query[1]]
    for j in range(query[3]-query[1]+1):
        d.append(matrix[i[0]-1][i[1]-1])
        if j<query[3]-query[1]:
            i[1]+=1
    for j in range(query[2]-query[0]):
        i[0]+=1
        d.append(matrix[i[0]-1][i[1]-1])
    for j in range(query[3]-query[1]):
        i[1]-=1
        d.append(matrix[i[0]-1][i[1]-1])
    for j in range(query[2]-query[0]-1):
        i[0]-=1
        d.append(matrix[i[0]-1][i[1]-1])
    d.rotate(1)
    i=[query[0],query[1]]
    t=0
    for j in range(query[3]-query[1]+1):
        matrix[i[0]-1][i[1]-1]=d[t]
        t+=1
        if j<query[3]-query[1]:
            i[1]+=1
    for j in range(query[2]-query[0]):
        i[0]+=1
        matrix[i[0]-1][i[1]-1]=d[t]
        t+=1
    for j in range(query[3]-query[1]):
        i[1]-=1
        matrix[i[0]-1][i[1]-1]=d[t]
        t+=1
    for j in range(query[2]-query[0]-1):
        i[0]-=1
        matrix[i[0]-1][i[1]-1]=d[t]
        t+=1
    return [matrix,min(d)]
```

# 수식 최대화
- IT 벤처 회사를 운영하고 있는 라이언은 매년 사내 해커톤 대회를 개최하여 우승자에게 상금을 지급하고 있습니다.
- 이번 대회에서는 우승자에게 지급되는 상금을 이전 대회와는 다르게 다음과 같은 방식으로 결정하려고 합니다.
- 해커톤 대회에 참가하는 모든 참가자들에게는 숫자들과 3가지의 연산문자(+, -, *) 만으로 이루어진 연산 수식이 전달되며, 참가자의 미션은 전달받은 수식에 포함된 연산자의 우선순위를 자유롭게 재정의하여 만들 수 있는 가장 큰 숫자를 제출하는 것입니다.
- 단, 연산자의 우선순위를 새로 정의할 때, 같은 순위의 연산자는 없어야 합니다. 즉, + > - > * 또는 - > * > + 등과 같이 연산자 우선순위를 정의할 수 있으나 +,* > - 또는 * > +,-처럼 2개 이상의 연산자가 동일한 순위를 가지도록 연산자 우선순위를 정의할 수는 없습니다. 수식에 포함된 연산자가 2개라면 정의할 수 있는 연산자 우선순위 조합은 2! = 2가지이며, 연산자가 3개라면 3! = 6가지 조합이 가능합니다.
- 만약 계산된 결과가 음수라면 해당 숫자의 절댓값으로 변환하여 제출하며 제출한 숫자가 가장 큰 참가자를 우승자로 선정하며, 우승자가 제출한 숫자를 우승상금으로 지급하게 됩니다.
- 예를 들어, 참가자 중 네오가 아래와 같은 수식을 전달받았다고 가정합니다.
- "100-200*300-500+20"
- 일반적으로 수학 및 전산학에서 약속된 연산자 우선순위에 따르면 더하기와 빼기는 서로 동등하며 곱하기는 더하기, 빼기에 비해 우선순위가 높아 * > +,- 로 우선순위가 정의되어 있습니다.
대회 규칙에 따라 + > - > * 또는 - > * > + 등과 같이 연산자 우선순위를 정의할 수 있으나 +,* > - 또는 * > +,- 처럼 2개 이상의 연산자가 동일한 순위를 가지도록 연산자 우선순위를 정의할 수는 없습니다.
- 수식에 연산자가 3개 주어졌으므로 가능한 연산자 우선순위 조합은 3! = 6가지이며, 그 중 + > - > * 로 연산자 우선순위를 정한다면 결괏값은 22,000원이 됩니다.
- 반면에 * > + > - 로 연산자 우선순위를 정한다면 수식의 결괏값은 -60,420 이지만, 규칙에 따라 우승 시 상금은 절댓값인 60,420원이 됩니다.
- 참가자에게 주어진 연산 수식이 담긴 문자열 expression이 매개변수로 주어질 때, 우승 시 받을 수 있는 가장 큰 상금 금액을 return 하도록 solution 함수를 완성해주세요.

```python
import copy

def solution(expression):
    answer = 0
    b=""
    arr=[]
    for i in expression:
        if i not in ['-','+','*']:
            b+=i
        else:
            arr.append(b)
            arr.append(i)
            b=""
    arr.append(b)
    carr=copy.deepcopy(arr)
    t=abs(cal(carr,'*','+','-'))
    if t>=answer:
        answer=t
    carr=copy.deepcopy(arr)
    t=abs(cal(carr,'*','-','+'))
    if t>=answer:
        answer=t
    carr=copy.deepcopy(arr)
    t=abs(cal(carr,'+','*','-'))
    if t>=answer:
        answer=t
    carr=copy.deepcopy(arr)
    t=abs(cal(carr,'+','-','*'))
    if t>=answer:
        answer=t
    carr=copy.deepcopy(arr)
    t=abs(cal(carr,'-','+','*'))
    if t>=answer:
        answer=t
    carr=copy.deepcopy(arr)
    t=abs(cal(carr,'-','*','+'))
    if t>=answer:
        answer=t
    return answer

def cal(arr,op1,op2,op3):
    i=0
    for j in range(len(arr)):
        if arr[i]==op1:
            if op1=='+':
                arr[i]=int(arr[i-1])+int(arr[i+1])
                del arr[i-1]
                del arr[i]
                i-=1
            elif op1=='-':
                arr[i]=int(arr[i-1])-int(arr[i+1])
                del arr[i-1]
                del arr[i]
                i-=1
            elif op1=='*':
                arr[i]=int(arr[i-1])*int(arr[i+1])
                del arr[i-1]
                del arr[i]
                i-=1
        i+=1
        if i==len(arr):
            break
    i=0
    for j in range(len(arr)):
        if arr[i]==op2:
            if op2=='+':
                arr[i]=int(arr[i-1])+int(arr[i+1])
                del arr[i-1]
                del arr[i]
                i-=1
            elif op2=='-':
                arr[i]=int(arr[i-1])-int(arr[i+1])
                del arr[i-1]
                del arr[i]
                i-=1
            elif op2=='*':
                arr[i]=int(arr[i-1])*int(arr[i+1])
                del arr[i-1]
                del arr[i]
                i-=1
        i+=1
        if i==len(arr):
            break
    i=0
    for j in range(len(arr)):
        if arr[i]==op3:
            if op3=='+':
                arr[i]=int(arr[i-1])+int(arr[i+1])
                del arr[i-1]
                del arr[i]
                i-=1
            elif op3=='-':
                arr[i]=int(arr[i-1])-int(arr[i+1])
                del arr[i-1]
                del arr[i]
                i-=1
            elif op3=='*':
                arr[i]=int(arr[i-1])*int(arr[i+1])
                del arr[i-1]
                del arr[i]
                i-=1
        i+=1
        if i==len(arr):
            break
    return arr[0]
```

# 124 나라의 숫자
- 124 나라가 있습니다. 124 나라에서는 10진법이 아닌 다음과 같은 자신들만의 규칙으로 수를 표현합니다.
```
124 나라에는 자연수만 존재합니다.
124 나라에는 모든 수를 표현할 때 1, 2, 4만 사용합니다.
예를 들어서 124 나라에서 사용하는 숫자는 다음과 같이 변환됩니다.

10진법	124 나라	10진법	124 나라
1	1	6	14
2	2	7	21
3	4	8	22
4	11	9	24
5	12	10	41
```
- 자연수 n이 매개변수로 주어질 때, n을 124 나라에서 사용하는 숫자로 바꾼 값을 return 하도록 solution 함수를 완성해 주세요.

```python
def solution(n):
    answer = ''
    t=[3**i for i in range(16,-1,-1)]
    arr=[0 for i in range(17)]
    for i in range(17):
        while n>=t[i]:
            n-=t[i]
            arr[i]+=1
    s=-1
    for i in range(17):
        if s==-1 and arr[i]!=0:
            s=i
    for i in range(16,s,-1):
        if arr[i]<=0:
            arr[i-1]-=1
            arr[i]+=3
    for i in range(s,17):
        if arr[i]==1:
            answer+='1'
        elif arr[i]==2:
            answer+='2'
        elif arr[i]==3:
            answer+='4'
    return answer
```

# 시소 짝꿍
- 어느 공원 놀이터에는 시소가 하나 설치되어 있습니다. 이 시소는 중심으로부터 2(m), 3(m), 4(m) 거리의 지점에 좌석이 하나씩 있습니다.
- 이 시소를 두 명이 마주 보고 탄다고 할 때, 시소가 평형인 상태에서 각각에 의해 시소에 걸리는 토크의 크기가 서로 상쇄되어 완전한 균형을 이룰 수 있다면 그 두 사람을 시소 짝꿍이라고 합니다.
-  즉, 탑승한 사람의 무게와 시소 축과 좌석 간의 거리의 곱이 양쪽 다 같다면 시소 짝꿍이라고 할 수 있습니다.
- 사람들의 몸무게 목록 weights이 주어질 때, 시소 짝꿍이 몇 쌍 존재하는지 구하여 return 하도록 solution 함수를 완성해주세요.

```python
def solution(weights):
    answer = 0
    dic={}
    arr=[]
    for i in weights:
        if i in dic:
            dic[i]+=1
        else:
            dic[i]=1
    for i in dic:
        if dic[i]>=2:
            answer+=dic[i]*(dic[i]-1)//2
        arr.append(i)
    for i in range(len(arr)):
        temp=[arr[i]*2,arr[i]*3,arr[i]*4]
        for j in range(i+1,len(arr)):
            if arr[j]*2 in temp:
                answer+=dic[arr[i]]*dic[arr[j]]
            elif arr[j]*3 in temp:
                answer+=dic[arr[i]]*dic[arr[j]]
            elif arr[j]*4 in temp:
                answer+=dic[arr[i]]*dic[arr[j]]
    return answer
```

# 숫자 카드 나누기
- 철수와 영희는 선생님으로부터 숫자가 하나씩 적힌 카드들을 절반씩 나눠서 가진 후, 다음 두 조건 중 하나를 만족하는 가장 큰 양의 정수 a의 값을 구하려고 합니다.
- 철수가 가진 카드들에 적힌 모든 숫자를 나눌 수 있고 영희가 가진 카드들에 적힌 모든 숫자들 중 하나도 나눌 수 없는 양의 정수 a
- 영희가 가진 카드들에 적힌 모든 숫자를 나눌 수 있고, 철수가 가진 카드들에 적힌 모든 숫자들 중 하나도 나눌 수 없는 양의 정수 a
- 예를 들어, 카드들에 10, 5, 20, 17이 적혀 있는 경우에 대해 생각해 봅시다. 만약, 철수가 [10, 17]이 적힌 카드를 갖고, 영희가 [5, 20]이 적힌 카드를 갖는다면 두 조건 중 하나를 만족하는 양의 정수 a는 존재하지 않습니다. 하지만, 철수가 [10, 20]이 적힌 카드를 갖고, 영희가 [5, 17]이 적힌 카드를 갖는다면, 철수가 가진 카드들의 숫자는 모두 10으로 나눌 수 있고, 영희가 가진 카드들의 숫자는 모두 10으로 나눌 수 없습니다. 따라서 철수와 영희는 각각 [10, 20]이 적힌 카드, [5, 17]이 적힌 카드로 나눠 가졌다면 조건에 해당하는 양의 정수 a는 10이 됩니다.
- 철수가 가진 카드에 적힌 숫자들을 나타내는 정수 배열 arrayA와 영희가 가진 카드에 적힌 숫자들을 나타내는 정수 배열 arrayB가 주어졌을 때, 주어진 조건을 만족하는 가장 큰 양의 정수 a를 return하도록 solution 함수를 완성해 주세요. 만약, 조건을 만족하는 a가 없다면, 0을 return 해 주세요.

```python
from math import ceil

def solution(arrayA, arrayB):
    answer = 0 
    arrayA.sort()
    arrayB.sort()
    dA=[arrayA[0]]
    dB=[arrayB[0]]
    for i in range(2,ceil(arrayA[0]**(1/2))+1):
        if arrayA[0]%i==0:
            dA.append(i)
            dA.append(arrayA[0]//i)
    for i in range(2,ceil(arrayB[0]**(1/2))+1):
        if arrayB[0]%i==0:
            dB.append(i)
            dB.append(arrayB[0]//i)
    dA.sort(reverse=True)
    dB.sort(reverse=True)
    dAA=[]
    dBB=[]
    for i in dA:
        flag=0
        for j in arrayA:
            if j%i!=0:
                flag=1
                break
        if flag==0:
            dAA.append(i)
    for i in dB:
        flag=0
        for j in arrayB:
            if j%i!=0:
                flag=1
                break
        if flag==0:
            dBB.append(i)
    for i in range(len(dAA)):
        flag=0
        for j in range(len(arrayB)):
            if arrayB[j]%dAA[i]==0:
                flag=1
                break
        if flag==0:
            answer=dAA[i]
            break
    for i in range(len(dBB)):
        if dBB[i]<=answer:
            break
        flag=0
        for j in range(len(arrayA)):
            if arrayA[j]%dBB[i]==0:
                flag=1
                break
        if flag==0:
            answer=dBB[i]
            break
    return answer
```

# 큰 수 만들기
- 어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다.
- 예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다. 이 중 가장 큰 숫자는 94 입니다.
- 문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다. number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.

```python
def solution(number, k):
    answer = ''
    number=list(number)
    if k==1:
        number.remove(min(number))
        for i in range(len(number)):
            answer+=number[i]
        return answer
    loop=0
    while k>0:
        if k==1:
            number.remove(min(number[loop],number[loop+1]))
            break
        temp=[]
        for i in range(loop,k+1+loop):
            temp.append(number[i])
            if number[i]==9:
                break
        max_index=temp.index(max(temp))
        k-=max_index
        del number[loop:max_index+loop]
        loop+=1
    for i in range(len(number)):
        answer+=number[i]
    return answer
```

# 전력망을 둘로 나누기
- n개의 송전탑이 전선을 통해 하나의 트리 형태로 연결되어 있습니다. 당신은 이 전선들 중 하나를 끊어서 현재의 전력망 네트워크를 2개로 분할하려고 합니다. 이때, 두 전력망이 갖게 되는 송전탑의 개수를 최대한 비슷하게 맞추고자 합니다.
- 송전탑의 개수 n, 그리고 전선 정보 wires가 매개변수로 주어집니다. 전선들 중 하나를 끊어서 송전탑 개수가 가능한 비슷하도록 두 전력망으로 나누었을 때, 두 전력망이 가지고 있는 송전탑 개수의 차이(절대값)를 return 하도록 solution 함수를 완성해주세요.

```python
import copy

def solution(n, wires):
    answer = n
    wires.sort()
    for i in range(len(wires)):
        s1=set()
        s2=set()
        temp=wires[:]
        temp.pop(i)
        s1.add(temp[0][0])
        s1.add(temp[0][1])
        t=[]
        for j in range(1,len(temp)):
            if temp[j][0] in s1:
                s1.add(temp[j][1])
            elif temp[j][1] in s1:
                s1.add(temp[j][0])
            else:
                t.append(temp[j])
        for j in range(len(t)):
            if t[j][0] in s1:
                s1.add(temp[j][1])
            elif t[j][1] in s1:
                s1.add(temp[j][0])
            else:
                s2.add(t[j][0])
                s2.add(t[j][1])
        if not s2:
            diff=n-2
        else:
            diff=abs(len(s1)-len(s2))
        if diff<answer:
            answer=diff
    return answer
```

# 카펫
- Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 노란색으로 칠해져 있고 테두리 1줄은 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다.
- Leo는 집으로 돌아와서 아까 본 카펫의 노란색과 갈색으로 색칠된 격자의 개수는 기억했지만, 전체 카펫의 크기는 기억하지 못했습니다.
- Leo가 본 카펫에서 갈색 격자의 수 brown, 노란색 격자의 수 yellow가 매개변수로 주어질 때 카펫의 가로, 세로 크기를 순서대로 배열에 담아 return 하도록 solution 함수를 작성해주세요.

```python
def solution(brown, yellow):
    answer = []
    for i in range(3,brown//2):
        if (i-2)*(brown//2-i)==yellow:
            answer.append(brown//2+2-i)
            answer.append(i)
            break
    return answer
```

# 할인 행사
- XYZ 마트는 일정한 금액을 지불하면 10일 동안 회원 자격을 부여합니다. XYZ 마트에서는 회원을 대상으로 매일 한 가지 제품을 할인하는 행사를 합니다. 할인하는 제품은 하루에 하나씩만 구매할 수 있습니다. 알뜰한 정현이는 자신이 원하는 제품과 수량이 할인하는 날짜와 10일 연속으로 일치할 경우에 맞춰서 회원가입을 하려 합니다.
- 예를 들어, 정현이가 원하는 제품이 바나나 3개, 사과 2개, 쌀 2개, 돼지고기 2개, 냄비 1개이며, XYZ 마트에서 14일간 회원을 대상으로 할인하는 제품이 날짜 순서대로 치킨, 사과, 사과, 바나나, 쌀, 사과, 돼지고기, 바나나, 돼지고기, 쌀, 냄비, 바나나, 사과, 바나나인 경우에 대해 알아봅시다. 첫째 날부터 열흘 간에는 냄비가 할인하지 않기 때문에 첫째 날에는 회원가입을 하지 않습니다. 둘째 날부터 열흘 간에는 바나나를 원하는 만큼 할인구매할 수 없기 때문에 둘째 날에도 회원가입을 하지 않습니다. 셋째 날, 넷째 날, 다섯째 날부터 각각 열흘은 원하는 제품과 수량이 일치하기 때문에 셋 중 하루에 회원가입을 하려 합니다.
- 정현이가 원하는 제품을 나타내는 문자열 배열 want와 정현이가 원하는 제품의 수량을 나타내는 정수 배열 number, XYZ 마트에서 할인하는 제품을 나타내는 문자열 배열 discount가 주어졌을 때, 회원등록시 정현이가 원하는 제품을 모두 할인 받을 수 있는 회원등록 날짜의 총 일수를 return 하는 solution 함수를 완성하시오. 가능한 날이 없으면 0을 return 합니다.

```python
def solution(want, number, discount):
    answer = 0
    dic={}
    s=0
    for i in range(len(want)):
        dic[want[i]]=i
        s+=number[i]
    for i in range(len(discount)-9):
        get=[0 for k in range(len(number))]
        for j in range(s):
            if discount[i+j] not in dic:
                break
            get[dic[discount[i+j]]]+=1
        if get==number:
            answer+=1
    return answer
```

# 더 맵게
- 매운 것을 좋아하는 Leo는 모든 음식의 스코빌 지수를 K 이상으로 만들고 싶습니다. 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 Leo는 스코빌 지수가 가장 낮은 두 개의 음식을 아래와 같이 특별한 방법으로 섞어 새로운 음식을 만듭니다.
- 섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)
- Leo는 모든 음식의 스코빌 지수가 K 이상이 될 때까지 반복하여 섞습니다.
- Leo가 가진 음식의 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수 K가 주어질 때, 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞어야 하는 최소 횟수를 return 하도록 solution 함수를 작성해주세요.

```python
from heapq import heapify, heappush, heappop

def solution(scoville, K):
    answer = 0
    heapify(scoville)
    while scoville[0]<K:
        if len(scoville)==1:
            return -1
        t1=heappop(scoville)
        t2=heappop(scoville)
        heappush(scoville,t1+t2*2)
        answer+=1
    return answer
```
`

# 주식가격
- 초 단위로 기록된 주식가격이 담긴 배열 prices가 매개변수로 주어질 때, 가격이 떨어지지 않은 기간은 몇 초인지를 return 하도록 solution 함수를 완성하세요.

```python
def solution(prices):
    answer = [0 for i in range(len(prices))]
    s=[]
    for i in range(len(prices)):
        while s and prices[i]<s[-1][1]:
            t=s.pop()
            answer[t[0]]=i-t[0]
        s.append([i,prices[i]])
    for i in range(len(prices)):
        if answer[i]==0:
            answer[i]=len(prices)-i-1
    return answer
```

# 2개 이하로 다른 비트
- 양의 정수 x에 대한 함수 f(x)를 다음과 같이 정의합니다.
- x보다 크고 x와 비트가 1~2개 다른 수들 중에서 제일 작은 수
- 정수들이 담긴 배열 numbers가 매개변수로 주어집니다. numbers의 모든 수들에 대하여 각 수의 f 값을 배열에 차례대로 담아 return 하도록 solution 함수를 완성해주세요.

```python
def solution(numbers):
    answer = []
    for i in numbers:
        b=bin(i)[2:]
        if b[-1]=='0':
            answer.append(int(b,2)+1)
        else:
            t=1
            while True:
                if len(b)==t or b[-1-t]=='0':
                    break
                t+=1
            answer.append(int(b,2)+2**(t-1))
    return answer
``` 

# 뒤에 있는 큰 수 찾기
- 정수로 이루어진 배열 numbers가 있습니다. 배열 의 각 원소들에 대해 자신보다 뒤에 있는 숫자 중에서 자신보다 크면서 가장 가까이 있는 수를 뒷 큰수라고 합니다.
- 정수 배열 numbers가 매개변수로 주어질 때, 모든 원소에 대한 뒷 큰수들을 차례로 담은 배열을 return 하도록 solution 함수를 완성해주세요. 단, 뒷 큰수가 존재하지 않는 원소는 -1을 담습니다.

```python
def solution(numbers):
    answer = [-1 for i in range(len(numbers))]
    numbers=list(enumerate(numbers))
    s=[]
    for i in numbers:
        while s:
            if i[1]>s[-1][1]:
                t=s.pop()
                answer[t[0]]=i[1]
            else:
                break
        s.append(i)
    return answer
```

# 모음 사전
- 사전에 알파벳 모음 'A', 'E', 'I', 'O', 'U'만을 사용하여 만들 수 있는, 길이 5 이하의 모든 단어가 수록되어 있습니다. 사전에서 첫 번째 단어는 "A"이고, 그다음은 "AA"이며, 마지막 단어는 "UUUUU"입니다.
- 단어 하나 word가 매개변수로 주어질 때, 이 단어가 사전에서 몇 번째 단어인지 return 하도록 solution 함수를 완성해주세요.

```python
def solution(word):
    answer = 0
    word_list=list(word)
    w=[]
    v=['A','E','I','O','U']
    while True:
        if len(w)<5:
            w.append('A')
        else:
            if w[-1]=='U':
                while w[-1]=='U':
                    w.pop()
            w[-1]=v[v.index(w[-1])+1]
        answer+=1
        if w==word_list:
            return answer
```

# 땅따먹기
- 땅따먹기 게임을 하려고 합니다. 땅따먹기 게임의 땅(land)은 총 N행 4열로 이루어져 있고, 모든 칸에는 점수가 쓰여 있습니다. 1행부터 땅을 밟으며 한 행씩 내려올 때, 각 행의 4칸 중 한 칸만 밟으면서 내려와야 합니다. 단, 땅따먹기 게임에는 한 행씩 내려올 때, 같은 열을 연속해서 밟을 수 없는 특수 규칙이 있습니다.
- 예를 들면,
```
| 1 | 2 | 3 | 5 |

| 5 | 6 | 7 | 8 |

| 4 | 3 | 2 | 1 |
```
로 땅이 주어졌다면, 1행에서 네번째 칸 (5)를 밟았으면, 2행의 네번째 칸 (8)은 밟을 수 없습니다.
- 마지막 행까지 모두 내려왔을 때, 얻을 수 있는 점수의 최대값을 return하는 solution 함수를 완성해 주세요. 위 예의 경우, 1행의 네번째 칸 (5), 2행의 세번째 칸 (7), 3행의 첫번째 칸 (4) 땅을 밟아 16점이 최고점이 되므로 16을 return 하면 됩니다.

```python
def solution(land):
    s=[[0,0,0,0] for i in range(len(land))]
    s[0]=land[0]
    for i in range(1,len(land)):
        for j in range(4):
            s[i][j]=max(land[i][j]+s[i-1][j-1],land[i][j]+s[i-1][j-2],land[i][j]+s[i-1][j-3])
    return max(s[-1])
```

# 구명보트
- 무인도에 갇힌 사람들을 구명보트를 이용하여 구출하려고 합니다. 구명보트는 작아서 한 번에 최대 2명씩 밖에 탈 수 없고, 무게 제한도 있습니다.
- 예를 들어, 사람들의 몸무게가 [70kg, 50kg, 80kg, 50kg]이고 구명보트의 무게 제한이 100kg이라면 2번째 사람과 4번째 사람은 같이 탈 수 있지만 1번째 사람과 3번째 사람의 무게의 합은 150kg이므로 구명보트의 무게 제한을 초과하여 같이 탈 수 없습니다.
- 구명보트를 최대한 적게 사용하여 모든 사람을 구출하려고 합니다.
- 사람들의 몸무게를 담은 배열 people과 구명보트의 무게 제한 limit가 매개변수로 주어질 때, 모든 사람을 구출하기 위해 필요한 구명보트 개수의 최솟값을 return 하도록 solution 함수를 작성해주세요.

```python
def solution(people, limit):
    answer = 0
    last=len(people)-1
    people.sort(reverse=True)
    for i in range(len(people)):
        if people[i]>200:
            answer+=1
        else:
            if people[i]+people[last]<=limit:
                last-=1
            answer+=1
        if i>=last:
            break
    return answer
```

# 야근 지수
- 회사원 Demi는 가끔은 야근을 하는데요, 야근을 하면 야근 피로도가 쌓입니다. 야근 피로도는 야근을 시작한 시점에서 남은 일의 작업량을 제곱하여 더한 값입니다. Demi는 N시간 동안 야근 피로도를 최소화하도록 일할 겁니다.Demi가 1시간 동안 작업량 1만큼을 처리할 수 있다고 할 때, 퇴근까지 남은 N 시간과 각 일에 대한 작업량 works에 대해 야근 피로도를 최소화한 값을 리턴하는 함수 solution을 완성해주세요.

```python
from heapq import heapify,heappush,heappop

def solution(n, works):
    answer = 0
    w=0
    if sum(works)<=n:
        return 0
    works=[-1*i for i in works]
    heapify(works)
    while n:
        w=heappop(works)
        w+=1
        heappush(works,w)
        n-=1
    for i in works:
        answer+=i**2
    return answer
```

# 귤 고르기
- 경화는 과수원에서 귤을 수확했습니다. 경화는 수확한 귤 중 'k'개를 골라 상자 하나에 담아 판매하려고 합니다. 그런데 수확한 귤의 크기가 일정하지 않아 보기에 좋지 않다고 생각한 경화는 귤을 크기별로 분류했을 때 서로 다른 종류의 수를 최소화하고 싶습니다.
- 예를 들어, 경화가 수확한 귤 8개의 크기가 [1, 3, 2, 5, 4, 5, 2, 3] 이라고 합시다. 경화가 귤 6개를 판매하고 싶다면, 크기가 1, 4인 귤을 제외한 여섯 개의 귤을 상자에 담으면, 귤의 크기의 종류가 2, 3, 5로 총 3가지가 되며 이때가 서로 다른 종류가 최소일 때입니다.
- 경화가 한 상자에 담으려는 귤의 개수 k와 귤의 크기를 담은 배열 tangerine이 매개변수로 주어집니다. 경화가 귤 k개를 고를 때 크기가 서로 다른 종류의 수의 최솟값을 return 하도록 solution 함수를 작성해주세요.

```python
def solution(k, tangerine):
    answer = 0
    dic={}
    for i in tangerine:
        if i not in dic:
            dic[i]=1
        else:
            dic[i]+=1
    dic_sorted=sorted(dic, key=lambda x:dic[x], reverse=True)
    i=0
    while(k>0):
        k-=dic[dic_sorted[i]]
        answer+=1
        i+=1
    return answer
```

# 두 원 사이의 정수 쌍
- x축과 y축으로 이루어진 2차원 직교 좌표계에 중심이 원점인 서로 다른 크기의 원이 두 개 주어집니다. 반지름을 나타내는 두 정수 r1, r2가 매개변수로 주어질 때, 두 원 사이의 공간에 x좌표와 y좌표가 모두 정수인 점의 개수를 return하도록 solution 함수를 완성해주세요.
- ※ 각 원 위의 점도 포함하여 셉니다.

```python
from math import floor, ceil

def solution(r1, r2):
    answer = 0
    for i in range(1,r2+1):
        max_y=floor((r2*r2-i*i)**(1/2))
        min_y=ceil((r1*r1-i*i)**(1/2)) if r1>i else 0
        answer+=max_y-min_y+1
    answer=answer*4
    return answer
```

# 타겟 넘버
- n개의 음이 아닌 정수들이 있습니다. 이 정수들을 순서를 바꾸지 않고 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다.
- 사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

```python
def solution(numbers, target):
    global answer
    answer = 0
    def search(s,n,i):
        s+=n
        if i==len(numbers)-1:
            if s==target:
                global answer
                answer+=1
            return
        search(s,numbers[i+1],i+1)
        search(s,-numbers[i+1],i+1)
    search(0,numbers[0],0)
    search(0,-numbers[0],0)
    return answer
```

# 요격 시스템
- A 나라가 B 나라를 침공하였습니다. B 나라의 대부분의 전략 자원은 아이기스 군사 기지에 집중되어 있기 때문에 A 나라는 B 나라의 아이기스 군사 기지에 융단폭격을 가했습니다.
- A 나라의 공격에 대항하여 아이기스 군사 기지에서는 무수히 쏟아지는 폭격 미사일들을 요격하려고 합니다. 이곳에는 백발백중을 자랑하는 요격 시스템이 있지만 운용 비용이 상당하기 때문에 미사일을 최소로 사용해서 모든 폭격 미사일을 요격하려 합니다.
- A 나라와 B 나라가 싸우고 있는 이 세계는 2 차원 공간으로 이루어져 있습니다. A 나라가 발사한 폭격 미사일은 x 축에 평행한 직선 형태의 모양이며 개구간을 나타내는 정수 쌍 (s, e) 형태로 표현됩니다. B 나라는 특정 x 좌표에서 y 축에 수평이 되도록 미사일을 발사하며, 발사된 미사일은 해당 x 좌표에 걸쳐있는 모든 폭격 미사일을 관통하여 한 번에 요격할 수 있습니다. 단, 개구간 (s, e)로 표현되는 폭격 미사일은 s와 e에서 발사하는 요격 미사일로는 요격할 수 없습니다. 요격 미사일은 실수인 x 좌표에서도 발사할 수 있습니다.
- 각 폭격 미사일의 x 좌표 범위 목록 targets이 매개변수로 주어질 때, 모든 폭격 미사일을 요격하기 위해 필요한 요격 미사일 수의 최솟값을 return 하도록 solution 함수를 완성해 주세요.

```python
def solution(targets):
    answer = 1
    targets.sort(key=lambda x:x[0])
    e=targets[0][1]
    for i,j in targets:
        if i>=e:
            answer+=1
            e=j
        e=min(e,j)
    return answer
```

# 부대복귀
- 강철부대의 각 부대원이 여러 지역에 뿔뿔이 흩어져 특수 임무를 수행 중입니다. 지도에서 강철부대가 위치한 지역을 포함한 각 지역은 유일한 번호로 구분되며, 두 지역 간의 길을 통과하는 데 걸리는 시간은 모두 1로 동일합니다. 임무를 수행한 각 부대원은 지도 정보를 이용하여 최단시간에 부대로 복귀하고자 합니다. 다만 적군의 방해로 인해, 임무의 시작 때와 다르게 되돌아오는 경로가 없어져 복귀가 불가능한 부대원도 있을 수 있습니다.
- 강철부대가 위치한 지역을 포함한 총지역의 수 n, 두 지역을 왕복할 수 있는 길 정보를 담은 2차원 정수 배열 roads, 각 부대원이 위치한 서로 다른 지역들을 나타내는 정수 배열 sources, 강철부대의 지역 destination이 주어졌을 때, 주어진 sources의 원소 순서대로 강철부대로 복귀할 수 있는 최단시간을 담은 배열을 return하는 solution 함수를 완성해주세요. 복귀가 불가능한 경우 해당 부대원의 최단시간은 -1입니다.

```python
from collections import deque

def solution(n, roads, sources, destination):
    answer = []
    dic={}
    visited=[[0,-1] for i in range(n+1)]
    visited[destination]=[1,0]
    dis=0
    q=deque([int(destination)])
    for i in range(1,n+1):
        dic[i]=set()
    for i,j in roads:
        dic[i].add(j)
        dic[j].add(i)
    while q:
        dis+=1
        ad=[]
        while q:
            ad.append(q.popleft())
        for i in ad:
            for j in dic[i]:
                if not visited[j][0]:
                    visited[j][0]=1
                    visited[j][1]=dis
                    q.append(j)
    for i in sources:
        answer.append(visited[i][1])
    return answer
```

# 합승 택시 요금
- 밤늦게 귀가할 때 안전을 위해 항상 택시를 이용하던 무지는 최근 야근이 잦아져 택시를 더 많이 이용하게 되어 택시비를 아낄 수 있는 방법을 고민하고 있습니다. "무지"는 자신이 택시를 이용할 때 동료인 어피치 역시 자신과 비슷한 방향으로 가는 택시를 종종 이용하는 것을 알게 되었습니다. "무지"는 "어피치"와 귀가 방향이 비슷하여 택시 합승을 적절히 이용하면 택시요금을 얼마나 아낄 수 있을 지 계산해 보고 "어피치"에게 합승을 제안해 보려고 합니다.
- 지점의 개수 n, 출발지점을 나타내는 s, A의 도착지점을 나타내는 a, B의 도착지점을 나타내는 b, 지점 사이의 예상 택시요금을 나타내는 fares가 매개변수로 주어집니다. 이때, A, B 두 사람이 s에서 출발해서 각각의 도착 지점까지 택시를 타고 간다고 가정할 때, 최저 예상 택시요금을 계산해서 return 하도록 solution 함수를 완성해 주세요.

```python
from heapq import heappush,heappop

def solution(n, s, a, b, fares):
    INF = 100001 * n
    answer = INF
    graph = [[INF] * (n+1) for _ in range(n+1)]
    for start,end,f in fares:
        graph[start][end] = f
        graph[end][start] = f
    for k in range(n+1):
        for i in range(n+1):
            for j in range(n+1):
                graph[i][j] = min(graph[i][j], graph[i][k]+graph[k][j])
    for x in range(1,n+1):
        graph[x][x] = 0
    for x in range(1,n+1):
        answer = min(graph[s][x]+graph[x][a]+graph[x][b],answer)
    return answer
```

# 스킬트리
- 선행 스킬이란 어떤 스킬을 배우기 전에 먼저 배워야 하는 스킬을 뜻합니다. 예를 들어 선행 스킬 순서가 스파크 → 라이트닝 볼트 → 썬더일때, 썬더를 배우려면 먼저 라이트닝 볼트를 배워야 하고, 라이트닝 볼트를 배우려면 먼저 스파크를 배워야 합니다.
- 위 순서에 없는 다른 스킬(힐링 등)은 순서에 상관없이 배울 수 있습니다. 따라서 스파크 → 힐링 → 라이트닝 볼트 → 썬더와 같은 스킬트리는 가능하지만, 썬더 → 스파크나 라이트닝 볼트 → 스파크 → 힐링 → 썬더와 같은 스킬트리는 불가능합니다.
- 선행 스킬 순서 skill과 유저들이 만든 스킬트리1를 담은 배열 skill_trees가 매개변수로 주어질 때, 가능한 스킬트리 개수를 return 하는 solution 함수를 작성해주세요.

```python
def solution(skill, skill_trees):
    answer = 0
    skill_arr=list(skill)
    for i in skill_trees:
        skills=list(i)
        pre=0
        for j in skills:
            if j in skill:
                if j==skill_arr[pre]:
                    pre+=1
                else:
                    answer-=1
                    break
        answer+=1
    return answer
```

# 다음 큰 숫자
- 자연수 n이 주어졌을 때, n의 다음 큰 숫자는 다음과 같이 정의 합니다.
```
조건 1. n의 다음 큰 숫자는 n보다 큰 자연수 입니다.
조건 2. n의 다음 큰 숫자와 n은 2진수로 변환했을 때 1의 갯수가 같습니다.
조건 3. n의 다음 큰 숫자는 조건 1, 2를 만족하는 수 중 가장 작은 수 입니다.
예를 들어서 78(1001110)의 다음 큰 숫자는 83(1010011)입니다.
```
- 자연수 n이 매개변수로 주어질 때, n의 다음 큰 숫자를 return 하는 solution 함수를 완성해주세요.

```python
def solution(n):
    answer = 0
    num=list(bin(n))[2:]
    one=0
    v=0
    for i in range(-1,-len(num),-1):
        if v==1 and num[i]=='0':
            num[i]='1'
            for j in range(-1,i,-1):
                if one>1:
                    num[j]='1'
                    one-=1
                else:
                    num[j]='0'
            return int(''.join(num),2)
        elif num[i]=='1':
            v=1
            one+=1
    if num[1]=='0':
        num.append('0')
        return int(''.join(num),2)
    else:
        num2=['1']
        for i in range(len(num)-one):
            num2.append('0')
        for i in range(one):
            num2.append('1')
        return int(''.join(num2),2)
```

# 배달
- N개의 마을로 이루어진 나라가 있습니다. 이 나라의 각 마을에는 1부터 N까지의 번호가 각각 하나씩 부여되어 있습니다. 각 마을은 양방향으로 통행할 수 있는 도로로 연결되어 있는데, 서로 다른 마을 간에 이동할 때는 이 도로를 지나야 합니다. 도로를 지날 때 걸리는 시간은 도로별로 다릅니다. 현재 1번 마을에 있는 음식점에서 각 마을로 음식 배달을 하려고 합니다. 각 마을로부터 음식 주문을 받으려고 하는데, N개의 마을 중에서 K 시간 이하로 배달이 가능한 마을에서만 주문을 받으려고 합니다. 다음은 N = 5, K = 3인 경우의 예시입니다.
-  위 그림에서 1번 마을에 있는 음식점은 [1, 2, 4, 5] 번 마을까지는 3 이하의 시간에 배달할 수 있습니다. 그러나 3번 마을까지는 3시간 이내로 배달할 수 있는 경로가 없으므로 3번 마을에서는 주문을 받지 않습니다. 따라서 1번 마을에 있는 음식점이 배달 주문을 받을 수 있는 마을은 4개가 됩니다.
- 마을의 개수 N, 각 마을을 연결하는 도로의 정보 road, 음식 배달이 가능한 시간 K가 매개변수로 주어질 때, 음식 주문을 받을 수 있는 마을의 개수를 return 하도록 solution 함수를 완성해주세요.

```python
from heapq import heappush, heappop

def solution(N, road, K):
    answer = 0
    INF=1000001
    graph=[[] for i in range(N+1)]
    for i in road:
        graph[i[0]].append((i[2],i[1]))
        graph[i[1]].append((i[2],i[0]))
    distance=[INF]*(N+1)
    q=[]
    heappush(q,(0,1))
    distance[1]=0
    while q:
        d,n=heappop(q)
        if distance[n]<d:
            continue
        for i in graph[n]:
            cost=d+i[0]
            if cost<distance[i[1]]:
                distance[i[1]]=cost
                heappush(q,(cost,i[1]))
    for i in range(N+1):
        if distance[i]<=K:
            answer+=1
    return answer
``` 

# 멀리 뛰기
- 효진이는 멀리 뛰기를 연습하고 있습니다. 효진이는 한번에 1칸, 또는 2칸을 뛸 수 있습니다. 칸이 총 4개 있을 때, 효진이는
```
(1칸, 1칸, 1칸, 1칸)
(1칸, 2칸, 1칸)
(1칸, 1칸, 2칸)
(2칸, 1칸, 1칸)
(2칸, 2칸)
```
- 의 5가지 방법으로 맨 끝 칸에 도달할 수 있습니다. 멀리뛰기에 사용될 칸의 수 n이 주어질 때, 효진이가 끝에 도달하는 방법이 몇 가지인지 알아내, 여기에 1234567를 나눈 나머지를 리턴하는 함수, solution을 완성하세요. 예를 들어 4가 입력된다면, 5를 return하면 됩니다.

```python
def solution(n):
    if n<=2:
        return n
    arr=[1,2]
    while len(arr)<n:
        arr.append(arr[len(arr)-2]+arr[len(arr)-1])
    return arr[-1]%1234567
```

# 등굣길
- 계속되는 폭우로 일부 지역이 물에 잠겼습니다. 물에 잠기지 않은 지역을 통해 학교를 가려고 합니다. 집에서 학교까지 가는 길은 m x n 크기의 격자모양으로 나타낼 수 있습니다.
- 가장 왼쪽 위, 즉 집이 있는 곳의 좌표는 (1, 1)로 나타내고 가장 오른쪽 아래, 즉 학교가 있는 곳의 좌표는 (m, n)으로 나타냅니다.
- 격자의 크기 m, n과 물이 잠긴 지역의 좌표를 담은 2차원 배열 puddles이 매개변수로 주어집니다. 오른쪽과 아래쪽으로만 움직여 집에서 학교까지 갈 수 있는 최단경로의 개수를 1,000,000,007로 나눈 나머지를 return 하도록 solution 함수를 작성해주세요.

```python
def solution(m, n, puddles):
    case=[[0 for i in range(m)] for i in range(n)]
    case[0][0]=1
    for i in range(n):
        for j in range(m):
            if i==0 and j==0:
                continue
            if [j+1,i+1] not in puddles:
                if i==0:
                    case[i][j]=case[i][j-1]
                elif j==0:
                    case[i][j]=case[i-1][j]
                else:
                    case[i][j]=case[i][j-1]+case[i-1][j]
    return case[n-1][m-1]%1000000007
```

# 마법의 엘리베이터
- 마법의 세계에 사는 민수는 아주 높은 탑에 살고 있습니다. 탑이 너무 높아서 걸어 다니기 힘든 민수는 마법의 엘리베이터를 만들었습니다. 마법의 엘리베이터의 버튼은 특별합니다. 마법의 엘리베이터에는 -1, +1, -10, +10, -100, +100 등과 같이 절댓값이 10c (c ≥ 0 인 정수) 형태인 정수들이 적힌 버튼이 있습니다. 마법의 엘리베이터의 버튼을 누르면 현재 층 수에 버튼에 적혀 있는 값을 더한 층으로 이동하게 됩니다. 단, 엘리베이터가 위치해 있는 층과 버튼의 값을 더한 결과가 0보다 작으면 엘리베이터는 움직이지 않습니다. 민수의 세계에서는 0층이 가장 아래층이며 엘리베이터는 현재 민수가 있는 층에 있습니다.
- 마법의 엘리베이터를 움직이기 위해서 버튼 한 번당 마법의 돌 한 개를 사용하게 됩니다.예를 들어, 16층에 있는 민수가 0층으로 가려면 -1이 적힌 버튼을 6번, -10이 적힌 버튼을 1번 눌러 마법의 돌 7개를 소모하여 0층으로 갈 수 있습니다. 하지만, +1이 적힌 버튼을 4번, -10이 적힌 버튼 2번을 누르면 마법의 돌 6개를 소모하여 0층으로 갈 수 있습니다.
- 마법의 돌을 아끼기 위해 민수는 항상 최소한의 버튼을 눌러서 이동하려고 합니다. 민수가 어떤 층에서 엘리베이터를 타고 0층으로 내려가는데 필요한 마법의 돌의 최소 개수를 알고 싶습니다. 민수와 마법의 엘리베이터가 있는 층을 나타내는 정수 storey 가 주어졌을 때, 0층으로 가기 위해 필요한 마법의 돌의 최소값을 return 하도록 solution 함수를 완성하세요.

```python
from math import log10, ceil

def solution(storey):
    answer = 0
    for i in range(1, ceil(log10(storey))+2):
        if (storey%10**i)//10**(i-1)>=6:
            answer+=10-(storey%10**i)//10**(i-1)
            storey+=(10-(storey%10**i)//10**(i-1))*10**(i-1)
        elif (storey%10**i)//10**(i-1)<5:
            answer+=(storey%10**i)//10**(i-1)
            storey-=(storey%10**i//10**(i-1))*10**(i-1)
        else:
            if (storey%10**(i+1))//10**i>=5:
                answer+=10-(storey%10**i)//10**(i-1)
                storey+=(10-(storey%10**i)//10**(i-1))*10**(i-1)
            else:
                answer+=(storey%10**i)//10**(i-1)
                storey-=(storey%10**i//10**(i-1))*10**(i-1)
    return answer
```

# 단속카메라
- 고속도로를 이동하는 모든 차량이 고속도로를 이용하면서 단속용 카메라를 한 번은 만나도록 카메라를 설치하려고 합니다.
- 고속도로를 이동하는 차량의 경로 routes가 매개변수로 주어질 때, 모든 차량이 한 번은 단속용 카메라를 만나도록 하려면 최소 몇 대의 카메라를 설치해야 하는지를 return 하도록 solution 함수를 완성하세요.

```python
def solution(routes):
    answer = 0
    routes.sort(key=lambda x:x[0])
    m=-30000
    for i, j in routes:
        if i>m:
            answer+=1
            m=j
        m=min(m,j)
    return answer
```

# 베스트앨범
- 스트리밍 사이트에서 장르 별로 가장 많이 재생된 노래를 두 개씩 모아 베스트 앨범을 출시하려 합니다. 노래는 고유 번호로 구분하며, 노래를 수록하는 기준은 다음과 같습니다.
```
속한 노래가 많이 재생된 장르를 먼저 수록합니다.
장르 내에서 많이 재생된 노래를 먼저 수록합니다.
장르 내에서 재생 횟수가 같은 노래 중에서는 고유 번호가 낮은 노래를 먼저 수록합니다.
```
- 노래의 장르를 나타내는 문자열 배열 genres와 노래별 재생 횟수를 나타내는 정수 배열 plays가 주어질 때, 베스트 앨범에 들어갈 노래의 고유 번호를 순서대로 return 하도록 solution 함수를 완성하세요.

```python
def solution(genres, plays):
    answer = []
    dic={}
    for i in genres:
        if i not in dic:
            dic[i]=[[],0]
    for i in range(len(plays)):
        dic[genres[i]][0].append([plays[i],i])
        dic[genres[i]][1]+=plays[i]
    for i in dic.keys():
        dic[i][0].sort(key=lambda x:(x[0],-x[1]), reverse=True)
    genres_sorted=sorted(dic.items(), key=lambda x:x[1][1], reverse=True)
    for i in genres_sorted:
        if len(i[1][0])==1:
            answer.append(i[1][0][0][1])
        else:
            for j in range(2):
                answer.append(i[1][0][j][1])
    return answer
```

# 이중우선순위큐
- 이중 우선순위 큐는 다음 연산을 할 수 있는 자료구조를 말합니다.
```
명령어	수신 탑(높이)
I 숫자	큐에 주어진 숫자를 삽입합니다.
D 1	큐에서 최댓값을 삭제합니다.
D -1	큐에서 최솟값을 삭제합니다.
```
- 이중 우선순위 큐가 할 연산 operations가 매개변수로 주어질 때, 모든 연산을 처리한 후 큐가 비어있으면 [0,0] 비어있지 않으면 [최댓값, 최솟값]을 return 하도록 solution 함수를 구현해주세요.

```python
from heapq import heappush, heappop

def solution(operations):
    answer = []
    pos_heap=[]
    neg_heap=[]
    for i in operations:
        if i[0]=="I":
            num=int(i[2:])
            heappush(pos_heap,num)
            heappush(neg_heap,-num)
        elif i[0]=="D":
            if not pos_heap:
                continue
            elif i[2]=="1":
                m=heappop(neg_heap)
                pos_heap.remove(-m)
            else:
                n=heappop(pos_heap)
                neg_heap.remove(-n)
    if not neg_heap:
        answer.append(0)
    else:
        answer.append(-heappop(neg_heap))
    if not pos_heap:
        answer.append(0)
    else:
        answer.append(heappop(pos_heap))
    return answer
```

# 방문 길이
- 게임 캐릭터를 4가지 명령어를 통해 움직이려 합니다. 명령어는 다음과 같습니다.

U: 위쪽으로 한 칸 가기

D: 아래쪽으로 한 칸 가기
 
R: 오른쪽으로 한 칸 가기

L: 왼쪽으로 한 칸 가기

- 캐릭터는 좌표평면의 (0, 0) 위치에서 시작합니다. 좌표평면의 경계는 왼쪽 위(-5, 5), 왼쪽 아래(-5, -5), 오른쪽 위(5, 5), 오른쪽 아래(5, -5)로 이루어져 있습니다.
- 예를 들어, "ULURRDLLU"로 명령했다면 1번 명령어부터 7번 명령어까지 다음과 같이 움직입니다. 8번 명령어부터 9번 명령어까지 다음과 같이 움직입니다.
- 이때, 우리는 게임 캐릭터가 지나간 길 중 캐릭터가 처음 걸어본 길의 길이를 구하려고 합니다. 예를 들어 위의 예시에서 게임 캐릭터가 움직인 길이는 9이지만, 캐릭터가 처음 걸어본 길의 길이는 7이 됩니다. (8, 9번 명령어에서 움직인 길은 2, 3번 명령어에서 이미 거쳐 간 길입니다)
- 단, 좌표평면의 경계를 넘어가는 명령어는 무시합니다.
- 명령어가 매개변수 dirs로 주어질 때, 게임 캐릭터가 처음 걸어본 길의 길이를 구하여 return 하는 solution 함수를 완성해 주세요.

```python
def solution(dirs):
    answer = 0
    dic_ver=[[0 for i in range(11)] for i in range(10)]
    dic_hor=[[0 for i in range(10)] for i in range(11)]
    index=[5,5]
    for i in dirs:
        if i=='U':
            if index[1]!=10:
                if dic_hor[index[0]][index[1]]==0:
                    answer+=1
                    dic_hor[index[0]][index[1]]=1
                index[1]+=1
        elif i=='D':
            if index[1]!=0:
                if dic_hor[index[0]][index[1]-1]==0:
                    answer+=1
                    dic_hor[index[0]][index[1]-1]=1
                index[1]-=1
        elif i=='R':
            if index[0]!=10:
                if dic_ver[index[0]][index[1]]==0:
                    answer+=1
                    dic_ver[index[0]][index[1]]=1
                index[0]+=1
        elif i=='L':
            if index[0]!=0:
                if dic_ver[index[0]-1][index[1]]==0:
                    answer+=1
                    dic_ver[index[0]-1][index[1]]=1
                index[0]-=1
    return answer
```

# 유사 칸토어 비트열
- 수학에서 칸토어 집합은 0과 1 사이의 실수로 이루어진 집합으로, [0, 1]부터 시작하여 각 구간을 3등분하여 가운데 구간을 반복적으로 제외하는 방식으로 만들어집니다.
- 남아는 칸토어 집합을 조금 변형하여 유사 칸토어 비트열을 만들었습니다. 유사 칸토어 비트열은 다음과 같이 정의됩니다.
- 0 번째 유사 칸토어 비트열은 "1" 입니다.
- n(1 ≤ n) 번째 유사 칸토어 비트열은 n - 1 번째 유사 칸토어 비트열에서의 1을 11011로 치환하고 0을 00000로 치환하여 만듭니다.
- 남아는 n 번째 유사 칸토어 비트열에서 특정 구간 내의 1의 개수가 몇 개인지 궁금해졌습니다.
- n과 1의 개수가 몇 개인지 알고 싶은 구간을 나타내는 l, r이 주어졌을 때 그 구간 내의 1의 개수를 return 하도록 solution 함수를 완성해주세요.

```python
def solution(n, l, r):
    answer = 0
    for i in range(l-1,r):
        while i>=5:
            if i%5==2:
                break
            i=i//5
        if i<5 and i!=2:
            answer+=1
    return answer
```

# 완주하지 못한 선수
- 수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.
- 마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.
- 제한사항
```
마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
completion의 길이는 participant의 길이보다 1 작습니다.
참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
참가자 중에는 동명이인이 있을 수 있습니다.
```

```python
def solution(participant, completion):
    answer = ''
    dic={}
    for i in participant:
        if i not in dic:
            dic[i]=[1]
        else :
            dic[i].append(1)
    for i in completion:
        dic[i].pop()
    for i in dic:
        if dic[i]:
            answer=i
    return answer
```

# 덧칠하기
- 어느 학교에 페인트가 칠해진 길이가 n미터인 벽이 있습니다. 벽에 동아리 · 학회 홍보나 회사 채용 공고 포스터 등을 게시하기 위해 테이프로 붙였다가 철거할 때 떼는 일이 많고 그 과정에서 페인트가 벗겨지곤 합니다. 페인트가 벗겨진 벽이 보기 흉해져 학교는 벽에 페인트를 덧칠하기로 했습니다.
- 넓은 벽 전체에 페인트를 새로 칠하는 대신, 구역을 나누어 일부만 페인트를 새로 칠 함으로써 예산을 아끼려 합니다. 이를 위해 벽을 1미터 길이의 구역 n개로 나누고, 각 구역에 왼쪽부터 순서대로 1번부터 n번까지 번호를 붙였습니다. 그리고 페인트를 다시 칠해야 할 구역들을 정했습니다.
- 벽에 페인트를 칠하는 롤러의 길이는 m미터이고, 롤러로 벽에 페인트를 한 번 칠하는 규칙은 다음과 같습니다.
- 롤러가 벽에서 벗어나면 안 됩니다.
- 구역의 일부분만 포함되도록 칠하면 안 됩니다.
- 즉, 롤러의 좌우측 끝을 구역의 경계선 혹은 벽의 좌우측 끝부분에 맞춘 후 롤러를 위아래로 움직이면서 벽을 칠합니다. 현재 페인트를 칠하는 구역들을 완전히 칠한 후 벽에서 롤러를 떼며, 이를 벽을 한 번 칠했다고 정의합니다.
- 한 구역에 페인트를 여러 번 칠해도 되고 다시 칠해야 할 구역이 아닌 곳에 페인트를 칠해도 되지만 다시 칠하기로 정한 구역은 적어도 한 번 페인트칠을 해야 합니다. 예산을 아끼기 위해 다시 칠할 구역을 정했듯 마찬가지로 롤러로 페인트칠을 하는 횟수를 최소화하려고 합니다.
- 정수 n, m과 다시 페인트를 칠하기로 정한 구역들의 번호가 담긴 정수 배열 section이 매개변수로 주어질 때 롤러로 페인트칠해야 하는 최소 횟수를 return 하는 solution 함수를 작성해 주세요.

```python
def solution(n, m, section):
    answer = 0
    com=0
    for i in section:
        if i>=com:
            com=i+m
            answer+=1
    return answer
```

# 시소 짝꿍
- 어느 공원 놀이터에는 시소가 하나 설치되어 있습니다. 이 시소는 중심으로부터 2(m), 3(m), 4(m) 거리의 지점에 좌석이 하나씩 있습니다.
- 이 시소를 두 명이 마주 보고 탄다고 할 때, 시소가 평형인 상태에서 각각에 의해 시소에 걸리는 토크의 크기가 서로 상쇄되어 완전한 균형을 이룰 수 있다면 그 두 사람을 시소 짝꿍이라고 합니다.
-  즉, 탑승한 사람의 무게와 시소 축과 좌석 간의 거리의 곱이 양쪽 다 같다면 시소 짝꿍이라고 할 수 있습니다.
- 사람들의 몸무게 목록 weights이 주어질 때, 시소 짝꿍이 몇 쌍 존재하는지 구하여 return 하도록 solution 함수를 완성해주세요.

```python
def solution(weights):
    answer = 0
    dic={}
    arr=[]
    for i in weights:
        if i in dic:
            dic[i]+=1
        else:
            dic[i]=1
    for i in dic:
        if dic[i]>=2:
            answer+=dic[i]*(dic[i]-1)//2
        arr.append(i)
    for i in range(len(arr)):
        temp=[arr[i]*2,arr[i]*3,arr[i]*4]
        for j in range(i+1,len(arr)):
            if arr[j]*2 in temp:
                answer+=dic[arr[i]]*dic[arr[j]]
            elif arr[j]*3 in temp:
                answer+=dic[arr[i]]*dic[arr[j]]
            elif arr[j]*4 in temp:
                answer+=dic[arr[i]]*dic[arr[j]]
    return answer
```

# 카펫
- Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 노란색으로 칠해져 있고 테두리 1줄은 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다.
- Leo는 집으로 돌아와서 아까 본 카펫의 노란색과 갈색으로 색칠된 격자의 개수는 기억했지만, 전체 카펫의 크기는 기억하지 못했습니다.
- Leo가 본 카펫에서 갈색 격자의 수 brown, 노란색 격자의 수 yellow가 매개변수로 주어질 때 카펫의 가로, 세로 크기를 순서대로 배열에 담아 return 하도록 solution 함수를 작성해주세요.

```python
def solution(brown, yellow):
    answer = []
    for i in range(3,brown//2):
        if (i-2)*(brown//2-i)==yellow:
            answer.append(brown//2+2-i)
            answer.append(i)
            break
    return answer
```

# 대장균들의 자식의 수 구하기 (2024-09-11)
- 대장균들은 일정 주기로 분화하며, 분화를 시작한 개체를 부모 개체, 분화가 되어 나온 개체를 자식 개체라고 합니다.
- 다음은 실험실에서 배양한 대장균들의 정보를 담은 ECOLI_DATA 테이블입니다. ECOLI_DATA 테이블의 구조는 다음과 같으며, ID, PARENT_ID, SIZE_OF_COLONY, DIFFERENTIATION_DATE, GENOTYPE 은 각각 대장균 개체의 ID, 부모 개체의 ID, 개체의 크기, 분화되어 나온 날짜, 개체의 형질을 나타냅니다.
- 대장균 개체의 ID(ID)와 자식의 수(CHILD_COUNT)를 출력하는 SQL 문을 작성해주세요. 자식이 없다면 자식의 수는 0으로 출력해주세요. 이때 결과는 개체의 ID 에 대해 오름차순 정렬해주세요.

```MySQL
SELECT E1.ID, COUNT(E2.ID) CHILD_COUNT
FROM ECOLI_DATA E1 LEFT OUTER JOIN ECOLI_DATA E2
ON E1.ID=E2.PARENT_ID
GROUP BY ID
```

# 주문량이 많은 아이스크림들 조회하기 (2024-09-13)
- 다음은 아이스크림 가게의 상반기 주문 정보를 담은 FIRST_HALF 테이블과 7월의 아이스크림 주문 정보를 담은 JULY 테이블입니다.
- 7월 아이스크림 총 주문량과 상반기의 아이스크림 총 주문량을 더한 값이 큰 순서대로 상위 3개의 맛을 조회하는 SQL 문을 작성해주세요.

```MySQL
SELECT FLAVOR
FROM (SELECT FLAVOR, SUM(TOTAL_ORDER) S
FROM JULY
GROUP BY FLAVOR
UNION
SELECT FLAVOR, SUM(TOTAL_ORDER) S
FROM FIRST_HALF
GROUP BY FLAVOR) T
GROUP BY FLAVOR
ORDER BY SUM(S) DESC
LIMIT 3
```

# 헤비 유저가 소유한 장소 (2024-09-15)
- PLACES 테이블은 공간 임대 서비스에 등록된 공간의 정보를 담은 테이블입니다. PLACES 테이블의 구조는 다음과 같으며 ID, NAME, HOST_ID는 각각 공간의 아이디, 이름, 공간을 소유한 유저의 아이디를 나타냅니다. ID는 기본키입니다.
- 이 서비스에서는 공간을 둘 이상 등록한 사람을 "헤비 유저"라고 부릅니다. 헤비 유저가 등록한 공간의 정보를 아이디 순으로 조회하는 SQL문을 작성해주세요.

```MySQL
SELECT *
FROM PLACES
WHERE HOST_ID IN(
SELECT HOST_ID
FROM PLACES
GROUP BY HOST_ID
HAVING COUNT(*)>=2)
ORDER BY ID
```

# 그룹별 조건에 맞는 식당 목록 출력하기 (2024-09-19)
- MEMBER_PROFILE와 REST_REVIEW 테이블에서 리뷰를 가장 많이 작성한 회원의 리뷰들을 조회하는 SQL문을 작성해주세요. 회원 이름, 리뷰 텍스트, 리뷰 작성일이 출력되도록 작성해주시고, 결과는 리뷰 작성일을 기준으로 오름차순, 리뷰 작성일이 같다면 리뷰 텍스트를 기준으로 오름차순 정렬해주세요.

```MySQL
SELECT M.MEMBER_NAME, R.REVIEW_TEXT, DATE_FORMAT(R.REVIEW_DATE,"%Y-%m-%d")
FROM MEMBER_PROFILE M, REST_REVIEW R
WHERE M.MEMBER_ID=R.MEMBER_ID
AND R.MEMBER_ID=(SELECT MEMBER_ID
FROM REST_REVIEW
GROUP BY MEMBER_ID
ORDER BY COUNT(*) DESC
LIMIT 1)
ORDER BY R.REVIEW_DATE, R.REVIEW_TEXT
```

# 연간 평가점수에 해당하는 평가 등급 및 성과금 조회하기 (2024-09-21)
- HR_DEPARTMENT, HR_EMPLOYEES, HR_GRADE 테이블을 이용해 사원별 성과금 정보를 조회하려합니다. 평가 점수별 등급과 등급에 따른 성과금 정보가 아래와 같을 때, 사번, 성명, 평가 등급, 성과금을 조회하는 SQL문을 작성해주세요.
- 평가등급의 컬럼명은 GRADE로, 성과금의 컬럼명은 BONUS로 해주세요.
- 결과는 사번 기준으로 오름차순 정렬해주세요.

```MySQL
SELECT E.EMP_NO, E.EMP_NAME, 
CASE
WHEN AVG(G.SCORE)>=96 THEN 'S'
WHEN AVG(G.SCORE)>=90 THEN 'A'
WHEN AVG(G.SCORE)>=80 THEN 'B'
ELSE 'C'
END GRADE,
CASE
WHEN AVG(G.SCORE)>=96 THEN E.SAL*0.2
WHEN AVG(G.SCORE)>=90 THEN E.SAL*0.15
WHEN AVG(G.SCORE)>=80 THEN E.SAL*0.1
ELSE 0
END BONUS
FROM HR_EMPLOYEES E, HR_GRADE G
WHERE E.EMP_NO=G.EMP_NO
GROUP BY E.EMP_NO
ORDER BY E.EMP_NO
```

# 서울에 위치한 식당 목록 출력하기 (2024-09-23)
- REST_INFO와 REST_REVIEW 테이블에서 서울에 위치한 식당들의 식당 ID, 식당 이름, 음식 종류, 즐겨찾기수, 주소, 리뷰 평균 점수를 조회하는 SQL문을 작성해주세요. 이때 리뷰 평균점수는 소수점 세 번째 자리에서 반올림 해주시고 결과는 평균점수를 기준으로 내림차순 정렬해주시고, 평균점수가 같다면 즐겨찾기수를 기준으로 내림차순 정렬해주세요.

```MySQL
SELECT I.REST_ID, I.REST_NAME, I.FOOD_TYPE, I.FAVORITES, I.ADDRESS, R.SCORE
FROM REST_INFO I,(
SELECT REST_ID, ROUND(AVG(REVIEW_SCORE),2) SCORE
FROM REST_REVIEW
GROUP BY REST_ID) R
WHERE I.REST_ID=R.REST_ID
AND (I.ADDRESS LIKE '%서울시%' OR I.ADDRESS LIKE'%서울특별시%')
ORDER BY R.SCORE DESC, I.FAVORITES DESC
```

# 대장균의 크기에 따라 분류하기 1 (2024-09-27)
- 대장균 개체의 크기가 100 이하라면 'LOW', 100 초과 1000 이하라면 'MEDIUM', 1000 초과라면 'HIGH' 라고 분류합니다. 대장균 개체의 ID(ID) 와 분류(SIZE)를 출력하는 SQL 문을 작성해주세요.이때 결과는 개체의 ID 에 대해 오름차순 정렬해주세요.

```MySQL
SELECT ID, CASE
WHEN SIZE_OF_COLONY<=100 THEN 'LOW'
WHEN SIZE_OF_COLONY<=1000 THEN 'MEDIUM'
ELSE 'HIGH'
END SIZE
FROM ECOLI_DATA
ORDER BY ID ASC
```

# 우유와 요거트가 담긴 장바구니 (2024-10-03)
- 데이터 분석 팀에서는 우유(Milk)와 요거트(Yogurt)를 동시에 구입한 장바구니가 있는지 알아보려 합니다. 우유와 요거트를 동시에 구입한 장바구니의 아이디를 조회하는 SQL 문을 작성해주세요. 이때 결과는 장바구니의 아이디 순으로 나와야 합니다.

```MySQL
SELECT CART_ID
FROM CART_PRODUCTS
GROUP BY CART_ID
HAVING (GROUP_CONCAT(NAME)) LIKE '%Yogurt%' AND (GROUP_CONCAT(NAME)) LIKE '%Milk%'
ORDER BY CART_ID
```

# 상품을 구매한 회원 비율 구하기 (2024-10-05)
- USER_INFO 테이블과 ONLINE_SALE 테이블에서 2021년에 가입한 전체 회원들 중 상품을 구매한 회원수와 상품을 구매한 회원의 비율(=2021년에 가입한 회원 중 상품을 구매한 회원수 / 2021년에 가입한 전체 회원 수)을 년, 월 별로 출력하는 SQL문을 작성해주세요. 상품을 구매한 회원의 비율은 소수점 두번째자리에서 반올림하고, 전체 결과는 년을 기준으로 오름차순 정렬해주시고 년이 같다면 월을 기준으로 오름차순 정렬해주세요.

```MySQL
SELECT YEAR(SALES_DATE) YEAR, MONTH(SALES_DATE) MONTH, COUNT(DISTINCT USER_ID) PURCHASED_USERS, ROUND(COUNT(DISTINCT USER_ID)/(SELECT COUNT(*)
                                                                                          FROM USER_INFO
                                                                                          WHERE YEAR(JOINED)='2021'),1) PURCHASED_RATIO
FROM ONLINE_SALE
WHERE USER_ID IN (SELECT USER_ID
      FROM USER_INFO
      WHERE YEAR(JOINED)='2021'
)
GROUP BY YEAR(SALES_DATE), MONTH(SALES_DATE)
ORDER BY YEAR, MONTH
```

# [PCCP 기출문제] 3번 / 충돌위험 찾기 (2024-10-07)
- 어떤 물류 센터는 로봇을 이용한 자동 운송 시스템을 운영합니다. 운송 시스템이 작동하는 규칙은 다음과 같습니다.
```
물류 센터에는 (r, c)와 같이 2차원 좌표로 나타낼 수 있는 n개의 포인트가 존재합니다. 각 포인트는 1~n까지의 서로 다른 번호를 가집니다.
로봇마다 정해진 운송 경로가 존재합니다. 운송 경로는 m개의 포인트로 구성되고 로봇은 첫 포인트에서 시작해 할당된 포인트를 순서대로 방문합니다.
운송 시스템에 사용되는 로봇은 x대이고, 모든 로봇은 0초에 동시에 출발합니다. 로봇은 1초마다 r 좌표와 c 좌표 중 하나가 1만큼 감소하거나 증가한 좌표로 이동할 수 있습니다.
다음 포인트로 이동할 때는 항상 최단 경로로 이동하며 최단 경로가 여러 가지일 경우, r 좌표가 변하는 이동을 c 좌표가 변하는 이동보다 먼저 합니다.
마지막 포인트에 도착한 로봇은 운송을 마치고 물류 센터를 벗어납니다. 로봇이 물류 센터를 벗어나는 경로는 고려하지 않습니다.
```
- 이동 중 같은 좌표에 로봇이 2대 이상 모인다면 충돌할 가능성이 있는 위험 상황으로 판단합니다. 관리자인 당신은 현재 설정대로 로봇이 움직일 때 위험한 상황이 총 몇 번 일어나는지 알고 싶습니다. 만약 어떤 시간에 여러 좌표에서 위험 상황이 발생한다면 그 횟수를 모두 더합니다.
- 운송 포인트 n개의 좌표를 담은 2차원 정수 배열 points와 로봇 x대의 운송 경로를 담은 2차원 정수 배열 routes가 매개변수로 주어집니다. 이때 모든 로봇이 운송을 마칠 때까지 발생하는 위험한 상황의 횟수를 return 하도록 solution 함수를 완성해 주세요.

```python
def solution(points, routes):
    answer = 0
    dic_robot={}    # 각 로봇의 경로를 담은 딕셔너리
    for i in range(len(routes)):    # 딕셔너리를 채우는 작업
        dic_robot[i]=[points[routes[i][0]-1]]   # 각 로봇의 시작 좌표를 각 딕셔너리 값의 첫 번째 원소로 저장
        for j in range(1,len(routes[i])):
            while(dic_robot[i][-1]!=points[routes[i][j]-1]):  # 시작 좌표가 목표 좌표와 다른 경우 반복
                if dic_robot[i][-1][0]<points[routes[i][j]-1][0]: # r 값부터 한 칸씩 이동
                    dic_robot[i].append([dic_robot[i][-1][0]+1,dic_robot[i][-1][1]])
                elif dic_robot[i][-1][0]>points[routes[i][j]-1][0]:
                    dic_robot[i].append([dic_robot[i][-1][0]-1,dic_robot[i][-1][1]]) # 현재 좌표의 r 값이 목표 좌표의 r 값보다 작으면 1 더하고 크면 1 빼기
                elif dic_robot[i][-1][1]<points[routes[i][j]-1][1]: # r 값이 같으면 c 값 한 칸씩 이동
                    dic_robot[i].append([dic_robot[i][-1][0],dic_robot[i][-1][1]+1])
                elif dic_robot[i][-1][1]>points[routes[i][j]-1][1]:
                    dic_robot[i].append([dic_robot[i][-1][0],dic_robot[i][-1][1]-1]) # 현재 좌표의 c 값이 목표 좌표의 c 값보다 작으면 1 더하고 크면 1 빼기
    cur_time=0  # 현재 시간
    while(dic_robot):    # 모든 로봇이 운송을 마칠 때까지 반복
        dic_co={}   # 현재 좌표 딕셔너리 생성
        del_robot=[]    # 운송을 마친 로봇을 저장할 리스트 생성
        for i in dic_robot: # 좌표별 로봇의 수를 좌표 딕셔너리에 기록
            cur_co=tuple(dic_robot[i][cur_time])
            if cur_co in dic_co:
                dic_co[cur_co]+=1
            else:
                dic_co[cur_co]=1
            if len(dic_robot[i])==cur_time+1:   # 로봇이 모든 경로를 이동하면 경로 딕셔너리에서 삭제
                del_robot.append(i)
        for i in del_robot:
            del dic_robot[i]
        for i in dic_co:    # 좌표별로 존재하는 로봇 수가 2 이상이면 answer 1 증가
            if dic_co[i]>=2:
                answer+=1
        cur_time+=1 # 현재 시간 1 증가
    return answer
```

# 가장 큰 수 (2024-10-09)
- 0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.
- 예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.
- 0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.

```python
from functools import cmp_to_key

def solution(numbers):
    answer = ''
    def compare(x,y):   # 사용자 정의 함수 생성
        if int(x+y)>=int(y+x):
            return -1
        else:
            return 1
    for i in range(len(numbers)):
        numbers[i]=str(numbers[i])  # 숫자들을 문자열로 변환
    numbers.sort(key=cmp_to_key(compare))  # 사용자 정의 함수를 기준으로 리스트 정렬
    for i in numbers:   # 문자열로 변환
        answer+=i
    return str(int(answer))
```

# 단어 변환 (2024-10-11)
- 두 개의 단어 begin, target과 단어의 집합 words가 있습니다. 아래와 같은 규칙을 이용하여 begin에서 target으로 변환하는 가장 짧은 변환 과정을 찾으려고 합니다.
```
1. 한 번에 한 개의 알파벳만 바꿀 수 있습니다.
2. words에 있는 단어로만 변환할 수 있습니다.
```
- 예를 들어 begin이 "hit", target가 "cog", words가 ["hot","dot","dog","lot","log","cog"]라면 "hit" -> "hot" -> "dot" -> "dog" -> "cog"와 같이 4단계를 거쳐 변환할 수 있습니다.
- 두 개의 단어 begin, target과 단어의 집합 words가 매개변수로 주어질 때, 최소 몇 단계의 과정을 거쳐 begin을 target으로 변환할 수 있는지 return 하도록 solution 함수를 작성해주세요.

```python
def solution(begin, target, words):
    answer = 1
    if target not in words: # target 값이 words에 없을 경우 0 반환
        return 0
    def compare(x,y):   # 두 단어가 하나의 알파벳만 다르다면 1을 반환하는 함수
        diff=0
        for i in range(len(x)):
            if x[i]!=y[i]:
                diff+=1
            if diff>=2:
                return 0
        if diff==1:
            return 1
    temp=[]     # 중간다리 단어로 사용될 단어들을 저장하는 임시 리스트 생성
    t_remove=[]   # 단계마다 삭제할 단어를 저장하는 임시 리스트 생성
    t_append=[]     # 단계마다 추가할 단어를 저장하는 임시 리스트 생성
    temp.append(target)
    words.remove(target)
    while words:
        for i in temp:  # 매 단계를 실행하기 전 temp에 있는 단어를 t_remove에 기록
            if compare(i,begin):    # 만약 temp에 있는 단어가 begin과 하나 차이 난다면 answer 반환
                return answer
            t_remove.append(i)
        for i in words: # temp에 있는 단어들과 하나 차이나는 단어들을 temp에 저장
            for j in temp:
                if compare(i,j):
                    if i not in t_append:
                        t_append.append(i)
        for i in t_append:
            temp.append(i)
        t_append.clear()
        for i in t_remove:    # t_remove에 있는 단어들을 temp에서 삭제
            temp.remove(i)
        t_remove.clear()
        for i in temp:      # temp에 있는 단어들을 words에서 삭제
            words.remove(i)
        if not temp:    # 매 단계마다 중간다리 단어를 체크하여 없으면 0 반환
            return 0
        answer+=1
    for i in temp:      # words가 비었을 경우 마지막으로 temp에 있는 단어들을 비교
        if compare(i,begin):
            return answer
        else:
            return 0
```
- comment
```
알파벳을 하나씩 바꾸어 목표 단어까지 가장 짧은 변환 과정을 찾는 문제이다.
탐색 과정에서 최적의 해인지 알 방법이 없고, 정답과 멀어지는 방향인지 알 방법이 없다.
그렇기 때문에 알파벳이 하나만 다른 단어를 모두 찾아 리스트에 저장하고 리스트에 저장된 단어들에서 탐색을 반복하는 너비 우선 탐색을 사용하였다.
```

# 인사고과 (2024-10-13)
- 완호네 회사는 연말마다 1년 간의 인사고과에 따라 인센티브를 지급합니다. 각 사원마다 근무 태도 점수와 동료 평가 점수가 기록되어 있는데 만약 어떤 사원이 다른 임의의 사원보다 두 점수가 모두 낮은 경우가 한 번이라도 있다면 그 사원은 인센티브를 받지 못합니다. 그렇지 않은 사원들에 대해서는 두 점수의 합이 높은 순으로 석차를 내어 석차에 따라 인센티브가 차등 지급됩니다. 이때, 두 점수의 합이 동일한 사원들은 동석차이며, 동석차의 수만큼 다음 석차는 건너 뜁니다. 예를 들어 점수의 합이 가장 큰 사원이 2명이라면 1등이 2명이고 2등 없이 다음 석차는 3등부터입니다.
- 각 사원의 근무 태도 점수와 동료 평가 점수 목록 scores이 주어졌을 때, 완호의 석차를 return 하도록 solution 함수를 완성해주세요.

```python
def solution(scores):
    answer = 1
    wan_score=scores[0]   # 완호의 점수 기록
    wan_sum=scores[0][0]+scores[0][1]
    scores.sort(key=lambda x:(-x[0],x[1]))   # 점수별로 내림차순, 오름차순 정렬
    max_score=0
    for i in scores:
        if i[1]>=max_score:     # 기준 점수 이상이면 인센티브 합격, 기준 점수 갱신
            max_score=i[1]
            if i[0]+i[1]>wan_sum:   # 완호의 점수 합산보다 점수 합산이 높다면 등수 증가
                answer+=1
        elif i==wan_score:  # 완호가 탈락일 경우 -1 반환
            return -1
    return answer
```
- comment
```
완호가 인센티브를 받을 수 있는지, 그리고 받을 수 있다면 석차는 몇 등인지 구하는 문제이다.
사원끼리 비교하여 두 점수 모두 자신보다 높은 점수를 기록한 사원이 있다면 탈락이므로 모든 사원끼리 비교를 해야 한다.
하지만 그렇게 할 경우 시간 복잡도가 지나치게 증가하여 효과적으로 문제를 해결할 수 없다.
모든 사원의 점수를 내림차순, 오름차순으로 정렬한다면 기준 점수를 이용하여 낮은 시간 복잡도로 문제를 해결할 수 있다.
근무 태도 점수가 가장 큰 사원들은 인센티브를 받게 되고 그보다 낮은 사원들은 동료 평가 점수에서 높은 점수를 얻어야 한다.
동료 평가 점수는 오름차순으로 정렬이 되어 있어 리스트를 탐색하면서 최대 동료 평가 점수를 기준 점수로 갱신한다면 인센티브 수령 여부를 쉽게 판별할 수 있다.
```

# H-Index (2024-10-15)
- H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. 위키백과1에 따르면, H-Index는 다음과 같이 구합니다.
- 어떤 과학자가 발표한 논문 n편 중, h번 이상 인용된 논문이 h편 이상이고 나머지 논문이 h번 이하 인용되었다면 h의 최댓값이 이 과학자의 H-Index입니다.
- 어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

```python
def solution(citations):
    answer = 0
    citations.sort(reverse=True)    # 내림차순 정렬
    for i in range(1,len(citations)+1):
        for j in range(i):          # 인덱스를 1씩 늘리면서 citations의 값이 인덱스보다 작은 경우 인덱스 반환
            if citations[j]<i:
                return answer
        answer+=1
    return len(citations)           # 모든 값이 인덱스보다 큰 경우 h-index의 최대값인 논문 수 반환
```
- comment
```
h번 이상 인용된 논문의 개수가 h 이상인 h값의 최대값을 구하는 문제이다.
내림차순 정렬을 한다면 해당 인덱스의 값보다 더 인용된 논문이 존재하지 않기 때문에 그 인덱스의 값을 이용해 문제를 해결하였다.
```

# 큰 수 만들기 (2024-10-17)
- 어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다.
- 예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다. 이 중 가장 큰 숫자는 94 입니다.
- 문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다. number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.

```python
from collections import deque

def solution(number, k):
    answer = ''
    number=deque(number)
    temp=deque()                    # 스택 역할을 하는 덱 생성
    while k>0:
        if not number:              # 모든 숫자를 체크했을 때 k가 1 이상이면 가장 마지막 숫자를 k만큼 제거
            for i in range(k):
                temp.pop()
            break
        n=number.popleft()
        while temp and temp[-1]<n:  # 스택의 마지막 값이 들어오는 숫자보다 작으면 스택에 있는 숫자 제거 반복
            temp.pop()
            k-=1
            if k==0:
                break
        temp.append(n)
    for n in temp:
        answer+=n
    for n in number:
        answer+=n
    return answer
```
- comment
```
어떤 숫자에서 k개의 수를 제거하여 가장 큰 숫자를 만드는 문제이다.
앞에서부터 다음 자리보다 작은 수인 수를 제거하면 쉽게 문제를 해결할 수 있다.
하지만 이미 존재하는 문자열 혹은 리스트에서 원소를 제거하는 것은 높은 시간 복잡도를 요구해 효율이 좋지 않다.
그리고 하나의 수를 제거하면 다시 비교를 해야 하기 때문에 더욱 높은 시간 복잡도를 요구한다.
스택 자료구조를 이용한다면 비교가 이루어질 때마다 O(1)의 시간 복잡도를 소요하기 때문에 효율적으로 문제를 해결할 수 있다.
원소 제거를 효율적으로 할 수 있는 자료구조인 덱을 사용하여 시간 복잡도를 최소로 줄일 수 있다.
```

# 게임 맵 최단거리 (2024-10-19)
- ROR 게임은 두 팀으로 나누어서 진행하며, 상대 팀 진영을 먼저 파괴하면 이기는 게임입니다. 따라서, 각 팀은 상대 팀 진영에 최대한 빨리 도착하는 것이 유리합니다.
- 지금부터 당신은 한 팀의 팀원이 되어 게임을 진행하려고 합니다. 다음은 5 x 5 크기의 맵에, 당신의 캐릭터가 (행: 1, 열: 1) 위치에 있고, 상대 팀 진영은 (행: 5, 열: 5) 위치에 있는 경우의 예시입니다.
- 위 그림에서 검은색 부분은 벽으로 막혀있어 갈 수 없는 길이며, 흰색 부분은 갈 수 있는 길입니다. 캐릭터가 움직일 때는 동, 서, 남, 북 방향으로 한 칸씩 이동하며, 게임 맵을 벗어난 길은 갈 수 없습니다.
- 게임 맵의 상태 maps가 매개변수로 주어질 때, 캐릭터가 상대 팀 진영에 도착하기 위해서 지나가야 하는 칸의 개수의 최솟값을 return 하도록 solution 함수를 완성해주세요. 단, 상대 팀 진영에 도착할 수 없을 때는 -1을 return 해주세요.

```python
from collections import deque

def solution(maps):
    q=deque()               # 큐 생성
    q.append((1,1,1))       # 시작 위치 삽입
    while q:
        r,c,m=q.popleft()
        if r==len(maps[0]) and c==len(maps):    # 현재 위치가 도착 지점일 경우 움직임 수 반환
            return m
        if c-1>0 and maps[c-2][r-1]:            # 상, 하, 좌, 우 움직일 수 있는 칸이 있으면 움직이고 기존 칸을 0으로 만듬
            if (r,c-1,m+1) not in q:
                q.append((r,c-1,m+1))
                maps[c-1][r-1]=0
        if c+1<=len(maps) and maps[c][r-1]:
            if (r,c+1,m+1) not in q:
                q.append((r,c+1,m+1))
                maps[c-1][r-1]=0
        if r-1>0 and maps[c-1][r-2]:
            if (r-1,c,m+1) not in q:
                q.append((r-1,c,m+1))
                maps[c-1][r-1]=0
        if r+1<=len(maps[0]) and maps[c-1][r]:
            if (r+1,c,m+1) not in q:
                q.append((r+1,c,m+1))
                maps[c-1][r-1]=0
    return -1                                 # 도착 위치까지 도달하지 못했을 경우 -1 반환
```
- comment
```
최단 거리의 움직임 수를 찾는 문제이다.
벽으로 막혀있어 여러 가능성이 존재하고, 깊이 우선 탐색으로 풀 경우 무한 루프에 빠질 수 있기 때문에 너비 우선 탐색을 이용하였다.
큐를 사용하여 현재 위치를 큐에 삽입하고 큐에서 하나씩 뽑아와 움직일 수 있는 곳을 큐에 삽입하였고, 큐가 비었다면 움직일 수 있는 곳이 없다는 뜻이므로 -1을 반환하였다.
```

# 기지국 설치 (2024-10-21)
- N개의 아파트가 일렬로 쭉 늘어서 있습니다. 이 중에서 일부 아파트 옥상에는 4g 기지국이 설치되어 있습니다. 기술이 발전해 5g 수요가 높아져 4g 기지국을 5g 기지국으로 바꾸려 합니다. 그런데 5g 기지국은 4g 기지국보다 전달 범위가 좁아, 4g 기지국을 5g 기지국으로 바꾸면 어떤 아파트에는 전파가 도달하지 않습니다.
- 아파트의 개수 N, 현재 기지국이 설치된 아파트의 번호가 담긴 1차원 배열 stations, 전파의 도달 거리 W가 매개변수로 주어질 때, 모든 아파트에 전파를 전달하기 위해 증설해야 할 기지국 개수의 최솟값을 리턴하는 solution 함수를 완성해주세요

```python
from math import ceil

def solution(n, stations, w):
    answer = 0
    cur=0       # 현재 위치
    for i in stations:
        answer+=ceil((i-w-1-cur)/(w*2+1))   # 이미 설치된 기지국을 만나기 전까지 필요한 기지국의 수
        cur=i+w                             # 현재 위치 갱신
    if cur<n:
        answer+=ceil((n-cur)/(w*2+1))       # 이미 설치된 기지국을 모두 만났으면 남은 필요한 기지국의 수 더하기
    return answer
```
- comment
```
새로 설치해야 할 기지국의 수를 찾는 문제이다.
이미 설치되어있는 기지국을 기준으로 현재 위치를 갱신하며 필요한 기지국의 수를 계산하였다.
```

# 멀리 뛰기 (2024-10-23)
- 효진이는 멀리 뛰기를 연습하고 있습니다. 효진이는 한번에 1칸, 또는 2칸을 뛸 수 있습니다. 칸이 총 4개 있을 때, 효진이는
```
(1칸, 1칸, 1칸, 1칸)
(1칸, 2칸, 1칸)
(1칸, 1칸, 2칸)
(2칸, 1칸, 1칸)
(2칸, 2칸)
```
- 의 5가지 방법으로 맨 끝 칸에 도달할 수 있습니다. 멀리뛰기에 사용될 칸의 수 n이 주어질 때, 효진이가 끝에 도달하는 방법이 몇 가지인지 알아내, 여기에 1234567를 나눈 나머지를 리턴하는 함수, solution을 완성하세요. 예를 들어 4가 입력된다면, 5를 return하면 됩니다.

```python
def solution(n):
    if n<=2:
        return n
    answer=[1,2]
    for i in range(2,n):
        answer.append(answer[i-2]+answer[i-1])
    return answer[-1]%1234567
```
- comment
```
1칸 혹은 2칸씩 뛰어 목적지까지 다다르는 경우의 수를 계산하는 문제이다.
n을 읽고 직접 경우의 수를 계산하기엔 경우의 수가 너무 많다.
마지막에 1칸을 뛰어 도착하는 경우의 수와 2칸을 뛰어 도착하는 경우의 수를 더한 값이 결과가 되는데, 이는 각각 n-1와 n-2의 결과와 같다.
따라서 1부터 n까지 결과를 저장하면서 더하면 쉽게 문제를 해결할 수 있다.
```

# 베스트앨범 (2024-10-25)
- 스트리밍 사이트에서 장르 별로 가장 많이 재생된 노래를 두 개씩 모아 베스트 앨범을 출시하려 합니다. 노래는 고유 번호로 구분하며, 노래를 수록하는 기준은 다음과 같습니다.
```
1. 속한 노래가 많이 재생된 장르를 먼저 수록합니다.
2. 장르 내에서 많이 재생된 노래를 먼저 수록합니다.
3. 장르 내에서 재생 횟수가 같은 노래 중에서는 고유 번호가 낮은 노래를 먼저 수록합니다.
```
- 노래의 장르를 나타내는 문자열 배열 genres와 노래별 재생 횟수를 나타내는 정수 배열 plays가 주어질 때, 베스트 앨범에 들어갈 노래의 고유 번호를 순서대로 return 하도록 solution 함수를 완성하세요.

```python
def solution(genres, plays):
    answer = []
    dic={}
    for i in range(len(genres)):                    # 장르와 재생 횟수를 딕셔너리에 기록
        if genres[i] not in dic:
            dic[genres[i]]=[0,[[i,plays[i]]]]
        else:
            dic[genres[i]][1].append([i,plays[i]])
        dic[genres[i]][0]+=plays[i]                 # 장르 별 총 재생 횟수 기록
    genre_order=sorted(dic.items(), reverse=True, key=lambda x:x[1][0])     # 장르 별 총 재생 횟수에 따른 우선순위 기록
    for i in genre_order:
        play_order=sorted(dic[i[0]][1], reverse=True, key=lambda x:x[1])    # 장르 우선순위에 따라 장르 내 최다 재생 곡 두 개까지 수록
        answer.append(play_order[0][0])
        if len(play_order)>1:
            answer.append(play_order[1][0])
    return answer
```
- comment
```
장르 별로 가장 많이 재생된 노래를 조건에 따라 수록하는 문제이다.
장르 별로 나누어 재생 횟수를 계산하기 위해 딕셔너리를 사용했다.
재생 횟수를 계산하고 조건에 맞게 노래를 분류한 뒤 다시 정렬하여 상위 2개의 곡을 추출하여 수록하였다.
```

# 조이스틱 (2024-10-27)
- 조이스틱으로 알파벳 이름을 완성하세요. 맨 처음엔 A로만 이루어져 있습니다.
- ex) 완성해야 하는 이름이 세 글자면 AAA, 네 글자면 AAAA
- 조이스틱을 각 방향으로 움직이면 아래와 같습니다.
```
▲ - 다음 알파벳
▼ - 이전 알파벳 (A에서 아래쪽으로 이동하면 Z로)
◀ - 커서를 왼쪽으로 이동 (첫 번째 위치에서 왼쪽으로 이동하면 마지막 문자에 커서)
▶ - 커서를 오른쪽으로 이동 (마지막 위치에서 오른쪽으로 이동하면 첫 번째 문자에 커서)
```
- 만들고자 하는 이름 name이 매개변수로 주어질 때, 이름에 대해 조이스틱 조작 횟수의 최솟값을 return 하도록 solution 함수를 만드세요.

```python
def solution(name):
    answer = 0
    min_move=len(name)-1                # 커서 이동 횟수 계산을 위한 최소 이동 횟수 변수
    for i in range(len(name)):
        if ord(name[i])<79:             # 알파벳 수정에 필요한 조작 횟수 계산
            answer+=ord(name[i])-65
        else:
            answer+=91-ord(name[i])
        j=i+1                                   # 최소 이동 횟수 계산을 위한 변수
        while j<len(name) and name[j]=='A':     # 현재 위치에서 가장 가까운 오른쪽에 있는 A가 아닌 알파벳의 위치
            j+=1
        min_move=min(min_move,min(2*i+len(name)-j,2*(len(name)-j)+i))   # 현재 위치와 j의 위치를 탐색하기 위한 가장 짧은 경로를 선택
    answer+=min_move
    return answer
```
- comment
```
모든 알파벳이 A로 설정된 상태에서 이름을 완성할 수 있는 조이스틱 조작 횟수의 최소값을 구하는 문제이다.
A에서 원하는 알파벳으로 설정하는 최소값은 구하기 어렵지 않다. 정답에 따른 최소값이 정해져 있기 때문이다.
하지만 수정해야 하는 알파벳, 즉 A가 아닌 알파벳의 위치에 따라 조이스틱의 최소 조작 경로가 달라지기 때문에 경로를 선택하는 일은 쉽지 않다.
가장 앞에서 뒤로 한 칸 이동하여 이름의 끝으로 이동할 수 있기 때문에 앞으로만 이동할 경우 최소 경로가 보장되지 않는다.
또한 현재 위치에서 가장 가까운 A가 아닌 알파벳의 위치를 탐색한다면 마지막에 먼 길을 돌아서 가야 할 가능성이 생긴다.
그렇기 때문에 이름 중간에 위치한 A의 위치를 기준으로 처음부터 끝까지 직진하는 방법, 먼저 직진했다 돌아가는 방법, 먼저 돌아갔다가 다시 처음으로 되돌아와 직진하는 방법 총 3가지를 비교하여 가장 짧은 경로를 선택하는 방법을 사용하였다.
주어진 이름을 처음부터 탐색하면서 알파벳 수정에 필요한 조작 횟수를 더하고 현재 위치에서 만나는 다음 A가 아닌 알파벳의 위치를 기록하여 커서 조작 최단 경로를 갱신하였다.
```

# 야근 지수 (2024-10-29)
- 회사원 Demi는 가끔은 야근을 하는데요, 야근을 하면 야근 피로도가 쌓입니다. 야근 피로도는 야근을 시작한 시점에서 남은 일의 작업량을 제곱하여 더한 값입니다. Demi는 N시간 동안 야근 피로도를 최소화하도록 일할 겁니다.Demi가 1시간 동안 작업량 1만큼을 처리할 수 있다고 할 때, 퇴근까지 남은 N 시간과 각 일에 대한 작업량 works에 대해 야근 피로도를 최소화한 값을 리턴하는 함수 solution을 완성해주세요.

```python
from heapq import heappush,heappop

def solution(n, works):
    answer = 0
    heap=[]
    for i in works:             # 최대 힙 생성
        heappush(heap,(-i,i))
    while n and heap:
        work=heappop(heap)[1]   # 최대값을 1만큼 줄이기를 n번 반복
        if work>1:
            heappush(heap,(-work+1,work-1))
        n-=1
    for i in heap:              # 남은 작업량 계산
        answer+=i[1]*i[1]
    return answer
```
- comment
```
남은 작업량의 제곱의 합이 최소가 되도록 작업량을 줄이는 문제이다.
제곱의 합이 최소가 되려면 작업량의 최대값이 최소가 되어야 하므로 최대 힙을 통해 문제를 해결하였다.
힙에서 추출하여 1만큼 줄이고 다시 힙에 삽입하기를 n번 반복하였다.
```
