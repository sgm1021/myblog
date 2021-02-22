---
title: Jupyter notebook
date: 2021-02-22 17:32:13
tags: python
categories: programming
---


### 1. 조건문
- 특정 조건에 따라서 코드를 실행하고자 할때 사용
- if, else, elif


```python
# 조건부분에 bool 데이터 타입 이외의 테이터 타입이 오면 bool으로 형변환 되어 판단
if False:
    print("python")
    
print("done")
```

    done
    


```python
# int : 0을 제외한 나머지 값은 True
bool(0), bool(1), bool(-1), bool(100)
```




    (False, True, True, True)




```python
num = 0

if num :
    print("python_1")

num = 1
if num :
    print("python_2")
```

    python_2
    


```python
number = 7

if number % 2:
    print("홀수")
```

    홀수
    


```python
# float : 0.0을 제외한 나머지 실수는 True
# str : ""를 제외한 나머지 문자열은 True
# list, tuple, dict : [], (), {}를 제외한 나머지는 True
```


```python
# 지갑에 돈이 10000원 이상 있으면 택시를 타고 그렇지 않으면 걸어서 집에 갑니다.
# 2000원 이상이면 버스
money = 5000

if money >= 10000:
    print("택시")
    
if money < 10000:
    print("걸어서")
```

    택시
    


```python
if money >= 10000:
    print("택시")
else:
    print("걸어서")
```

    택시
    


```python
if money >= 10000:
    print("택시")
elif money > 2000:
    print("버스")
else:
    print("걸어서")
```

    택시
    


```python
# 계좌에 10000원이 들어 있다.
# 인출 금액을 입력 받습니다.
# 인출 금액이 계좌에 있는 금액보다 크면 "잔액 부족" 출력
# 아니면 "인출" 출력
# 마지막에 현재 잔액 출력
```


```python
data = int(input("draw money: "))
type(data), data
```

    draw money: 5000
    




    (int, 5000)




```python
10000 - data
```




    5000




```python
account = 10000
draw_money = int(input("insert draw money: "))

if account >= draw_money:
    account -= draw_money
    print(str(draw_money) + "원 출금")
else:
    print("잔액 부족, "+ str(draw_money - account) + "원 부족")

print("현재 잔액 : " + str(account) + "원")
```

    insert draw money: 5000
    5000원 출금
    현재 잔액 : 5000원
    


```python
# string 데이터 타입의 format 함수
print("현재 잔액은 {}원, 인출금액은 {}원 입니다.".format(account, draw_money))
print("현재 잔액은 {data1}원, 인출금액은 {data2}원 입니다.".format(data2 = draw_money, data1 = account))
```

    현재 잔액은 5000원, 인출금액은 5000원 입니다.
    현재 잔액은 5000원, 인출금액은 5000원 입니다.
    


```python
f'현재 {account}'
```




    '현재 5000'



### 삼항연산자
 - 간단한 if, else 구문을 한줄의 코드로 표현할 수 있는 방법
 - (True) if (condition) else (False)



```python
# data  변수에 0이면 "zero" 출력, 아니면 "not zero" 출력
data = 0
if data:
    print("not zero")
else:
    print("zero")
```

    zero
    


```python
data = 1
result = "not zero" if data else "zero"
result
```




    'not zero'



### 2. 반복문
- 반복되는 코드를 실행할 때 사용
- while, for, break, continue
- list comprehention


```python
# while
data = 3
while data:# 조건이 False가 될때까지 구문의 코드를 실행
    # 반복되는 코드
    print(data)
    data -= 1
```

    3
    2
    1
    


```python
# 무한루프
# break : 반복문을 중단 시킬때 사용되는 예약어
result = 1
while result:
    if result >= 10:
        break
    result += 1
print(result)
```

    10
    

### for
- iterable한 값을 하나씩 꺼내서 value에 대입시킨 후 코드를 iterable 변수의 값 갯수 만큼 실행
```
for <variable> in <iterables>:
    <code>
```


```python
# for : continue : 조건부분으로 올라가서 코드가 실행
ls = [0, 1, 2, 3, 4]
for data in ls: # data가 홀수면 continue 실행
    if data % 2:
        continue
    # data가 짝수면 print 실행
    print(data, end=" ")
```

    0 2 4 


```python
# for문을 이용하여 코드를 100번 실행
# range 함수
list(range(100))
result = 0
for data in range(100):
    result += data
result
```




    4950




```python
# offset index 개념과 비슷하게 사용
list(range(5)), list(range(5, 10)), list(range(0, 10, 2)), list(range(10, 0, -2))
```




    ([0, 1, 2, 3, 4], [5, 6, 7, 8, 9], [0, 2, 4, 6, 8], [10, 8, 6, 4, 2])




```python
# 0~10 까지 짝수 합
result = 0
for number in range(0, 11, 2):
    result += number
result
```




    30




```python
dict = {"one": 1, "two":2, "three":3}
```


```python
# 키값만 출력
for data in dict:
    print(data)
```

    one
    two
    three
    


```python
list(dict.items())
```




    [('one', 1), ('two', 2), ('three', 3)]




```python
for subject, point in dict.items():
    print(subject, point)
```

    one 1
    two 2
    three 3
    


```python
# 구구단
for num2 in range(1, 10):
    for num1 in range(2, 10):
        print("{}*{}={}".format(num1, num2, num1*num2), end='\t')
    print()
```

    2*1=2	3*1=3	4*1=4	5*1=5	6*1=6	7*1=7	8*1=8	9*1=9	
    2*2=4	3*2=6	4*2=8	5*2=10	6*2=12	7*2=14	8*2=16	9*2=18	
    2*3=6	3*3=9	4*3=12	5*3=15	6*3=18	7*3=21	8*3=24	9*3=27	
    2*4=8	3*4=12	4*4=16	5*4=20	6*4=24	7*4=28	8*4=32	9*4=36	
    2*5=10	3*5=15	4*5=20	5*5=25	6*5=30	7*5=35	8*5=40	9*5=45	
    2*6=12	3*6=18	4*6=24	5*6=30	6*6=36	7*6=42	8*6=48	9*6=54	
    2*7=14	3*7=21	4*7=28	5*7=35	6*7=42	7*7=49	8*7=56	9*7=63	
    2*8=16	3*8=24	4*8=32	5*8=40	6*8=48	7*8=56	8*8=64	9*8=72	
    2*9=18	3*9=27	4*9=36	5*9=45	6*9=54	7*9=63	8*9=72	9*9=81	
    

### 3. list comprehention
- 리스트 데이터를 만들어 주는 방법
- for문 보다 빠르게 동작


```python
# 각각 값에 제곡한 결과 출력
ls = [0, 1, 2, 3]
result = []
for data in ls:
    result.append(data**2)
result
```




    [0, 1, 4, 9]




```python
result = [data**2 for data in ls]
result
```




    [0, 1, 4, 9]




```python
# 리스트 컴프리헨션을 써서 홀수와 짝수를 리스트로 출력해주는 코드
# 삼항연산 사용
ls = [0, 1, 2, 3]
result = ["짝수", "홀수", "짝수", "홀수"]

result = [
    "홀수" if data % 2 else "짝수" for data in ls
]
result
```




    ['짝수', '홀수', '짝수', '홀수']




```python
# 리스트 컴프리헨션 조건문
ls = range(10)
[data for data in ls if data % 2]
```




    [1, 3, 5, 7, 9]




```python
ls = [1, 2, 3]
[func for func in dir(ls) if func[:2] != "__" and func[0] == 'c']
```




    ['clear', 'copy', 'count']




```python
# for문과 list comprehention 성능 비교
```


```python
%%timeit
ls = []
for num in range(1, 10001):
    ls.append(num)
len(ls)
```

    785 µs ± 23.4 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
    


```python
%%timeit
ls = [num for num in range(1, 10001) if num % 3 == 0]
len(ls)
```

    735 µs ± 3.17 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
    


```python

```
