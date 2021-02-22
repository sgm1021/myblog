---
title: Jupyter notebook
date: 2021-02-22 17:32:13
tags: python
categories: programming
---


### 파이썬의 기본 문법
- 변수 선언, 식별자, 자료형, 형변환, 연산자 학습

#### 1. 주석(comment)과 축력(print)


```python
# 주석 : 앞에 #을 붙이면 코드로 실행이 안됩니다.
# 코드에 대한 설명이나 중간에 코드를 샐행시키고 시퓨지 않을때 사용
# 단축키 : ctrl(cmd) + /
# 블럭설정 : shift + 방향키

# 1,2,3을 출력하는 코드
print(1)
#print(2)
print(3)
```

    1
    3
    


```python
# 출력 : print 함수
# 코드 중간에 변수안에 들어있는 값을 확인하고 싶을때 사용
```


```python
a = 1
b = 2
print(b)
c = 3
b = 4
print(b)
```

    2
    4
    


```python
# print 함수의 옵션
# docstring : 함수에 대한 설명 : 단축키(shift + tab)
# 자동완성 : tab
print(1,2, sep="-", end="\t")
print(3)
```

    1-2	3
    


```python
python_data_science = 1
```


```python
python_data_science
```




    1



#### 2. 변수 선언
- RAM 저장공간에 값을 할당하는 행위


```python
a = 1
b = 2
c = a + b
```


```python
d, e = 3, 4
f = g = 5
```

#### 3. 식별자
- 변수, 함수, 클래스, 모듈등의 이름을 식별자 라고 합니다.
- 식별자 규칙 
    - 소문자, 대문자, 숫자, 언더스코어(_)를 사용합니다.
    - 가장 압에 숫자 사용 불가
    - 예약어의 사용 불가 : def, class, try, except ...
    - 컨벤션
        - snake case : fast_campus : 변수, 함수
        _ camel case : FastCampus, fastCampus : 클래스

#### 4. 데이터 다입
- RAM 저장공간을 효율적으로 사용하기 위해 저장공간의 타입을 설정
- 동적타이핑
    - 변수 선언시 저장되는 값에 따라서 자동으로 데이터 타입이 설정
- 기본 데이터 타입 : int, float, bool, str
- 컬렉션 데이터 타입 : list, tuple, dict


```python
a = 1
# int a = 1 
b = "python"
type(a), type(b)
```




    (int, str)




```python
# 기본 데이터 타입 : int, float, bool, str
a = 1
b = 1.2
c = True
d = "data"
type(a),type(b),type(c),type(d)
```




    (int, float, bool, str)




```python
a + b
```




    2.2




```python
a + d
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-22-4fbab87c839c> in <module>
    ----> 1 a + d
    

    TypeError: unsupported operand type(s) for +: 'int' and 'str'



```python
# 데이터 타입에 함수 : 문자열
# upper : 대문자로 변환
e = d.upper()
```


```python
d, e
```




    ('data', 'DATA')




```python
f = "Fast Campus"
```


```python
# lower : 소문자로 변환
f.lower()
```




    'fast campus'




```python
# strip : 공백제거
f.strip()
```




    'Fast Campus'




```python
# replace : 특정 문자열 치환
f.replace("Fast", "Slow")
```




    'Slow Campus'




```python
f.replace(" ", "")
```




    'FastCampus'




```python
dir(f)
```




    ['__add__',
     '__class__',
     '__contains__',
     '__delattr__',
     '__dir__',
     '__doc__',
     '__eq__',
     '__format__',
     '__ge__',
     '__getattribute__',
     '__getitem__',
     '__getnewargs__',
     '__gt__',
     '__hash__',
     '__init__',
     '__init_subclass__',
     '__iter__',
     '__le__',
     '__len__',
     '__lt__',
     '__mod__',
     '__mul__',
     '__ne__',
     '__new__',
     '__reduce__',
     '__reduce_ex__',
     '__repr__',
     '__rmod__',
     '__rmul__',
     '__setattr__',
     '__sizeof__',
     '__str__',
     '__subclasshook__',
     'capitalize',
     'casefold',
     'center',
     'count',
     'encode',
     'endswith',
     'expandtabs',
     'find',
     'format',
     'format_map',
     'index',
     'isalnum',
     'isalpha',
     'isascii',
     'isdecimal',
     'isdigit',
     'isidentifier',
     'islower',
     'isnumeric',
     'isprintable',
     'isspace',
     'istitle',
     'isupper',
     'join',
     'ljust',
     'lower',
     'lstrip',
     'maketrans',
     'partition',
     'replace',
     'rfind',
     'rindex',
     'rjust',
     'rpartition',
     'rsplit',
     'rstrip',
     'split',
     'splitlines',
     'startswith',
     'strip',
     'swapcase',
     'title',
     'translate',
     'upper',
     'zfill']




```python
# 오프셋 인덱스 : 마스크, 마스킹 : []
# 문자열은 순서가 있는 문자들의 집합
g = "abcdefg"
```


```python
g[2], g[-2], g[2:5], g[:2], g[3:], g[-2:], g[::2], g[::-1]
```




    ('c', 'f', 'cde', 'ab', 'defg', 'fg', 'aceg', 'gfedcba')




```python
numbers = "123456789" # 97531 출력
```


```python
result = numbers[::2]
result[::-1]
```




    '97531'




```python
numbers[::2][::-1]
```




    '97531'




```python
numbers[::-2]
```




    '97531'



#### 컬렉션 데이터 타입 : list, tuple, dict
- list [] : 순서가 있는 수정이 가능한 데이터 타입
- tuple () : 순서가 있는 수정이 불가능한 데이터 타입
- dict {}: 순서가 없고 키:값 으로 구성된 데이터 타입


```python
# list
ls = [1,2,3,"four", [5,6], True, 1.2]
type(ls), ls
```




    (list, [1, 2, 3, 'four', [5, 6], True, 1.2])




```python
# offset index 사용 가능
ls[3], ls[1:3], ls[::-1]
```




    ('four', [2, 3], [1.2, True, [5, 6], 'four', 3, 2, 1])




```python
# list 함수
ls = [1, 5, 2, 4]
```


```python
# append : 가장 뒤에 값을 추가
ls.append(3)
ls
```




    [1, 5, 2, 4, 3]




```python
# sort : 오름차순으로 정렬
ls.sort()
ls[::-1]
```




    [5, 4, 3, 2, 1]




```python
# pop : 가장 마지막 데이터를 출력하고 출력한 데이터를 삭제
# ctrl + enter : 현재 셀을 계속 실행
num = ls.pop()
num, ls
```




    (3, [1, 2])




```python
# 리스트의 복사
```


```python
ls1 = [1, 2, 3]
ls2 = ls1 # 얕은 복사 : 주소값 복사
ls1, ls2
```




    ([1, 2, 3], [1, 2, 3])




```python
ls1[2] = 5
ls1, ls2
```




    ([1, 2, 5], [1, 2, 5])




```python
ls3 = ls1.copy()
ls1, ls3
```




    ([1, 2, 5], [1, 2, 5])




```python
ls1[2] = 10
```


```python
ls1, ls3
```




    ([1, 2, 10], [1, 2, 5])



#### Tuple
- 리스트와 같지만 수정이 불가능한 데이터 타입
- 튜플은 리스트보다 같은 데이터를 가졌을때 공간을 적게 사용


```python
tp1 = 1, 2, 3
tp2 = (4, 5, 6)
type(tp1), type(tp2), tp1, tp2
```




    (tuple, tuple, (1, 2, 3), (4, 5, 6))




```python
a, b = 1, 2
a, b
```




    (1, 2)




```python
# offset index 사용 가능
tp1[1], tp1[::-1]
```




    (2, (3, 2, 1))




```python
# 리스트와 튜플의 저장공간 차이 비교
import sys

ls = [1, 2, 3]
tp = (1, 2, 3)

print(sys.getsizeof(ls), sys.getsizeof(tp))
```

    80 64
    

#### dict {}
- 순서가 없고 {키:값}으로 구성된 데이터 타입


```python
# 선언 : 키는 정수, 문자열 데이터 타입만 사용 가능
# 인덱스 대신 키를 사용
dic = {
    1: "one",
    "two": 2,
    "three" : [1, 2, 3],
}
type(dic), dic
```




    (dict, {1: 'one', 'two': 2, 'three': [1, 2, 3]})




```python
dic[1], dic["three"]
```




    ('one', [1, 2, 3])




```python
dic["two"] = 123
dic
```




    {1: 'one', 'two': 123, 'three': [1, 2, 3]}




```python
# 아래의 데이터를 list와 dict로 선언
# 도시 : seoul, busan, daegu
# 인구 : 9,700,000, 3,400,00, 2,400,000
```


```python
# 리스트
city = ["seoul", "busan", "daegu"]
population = [9700000, 3400000, 2400000]
```


```python
# 딕셔너리
data = {
    "seoul" : 9700000,
    "busan" : 3400000,
    "daegu" : 2400000,
}
```


```python
sum(population)
```




    15500000




```python
sum(data.values())
```




    15500000



### 5. 형변환
- 데이터 타입을 변환하는 방법
- int, float, bool, str, list, tuple, dict


```python
a = 1
b = "2"
a + int(b)
```




    3




```python
str(a) + b
```




    '12'




```python
list(data.values())
```




    [9700000, 3400000, 2400000]




```python
city, population
```




    (['seoul', 'busan', 'daegu'], [9700000, 3400000, 2400000])




```python
# zip : 같은 인덱스 데이터끼리 묶어주는 함수
list(zip(city, population))
```




    [('seoul', 9700000), ('busan', 3400000), ('daegu', 2400000)]




```python
result = dict(zip(city, population))
```


```python
data1 = list(result.keys())
data2 = list(result.values())
data1, data2
```




    (['seoul', 'busan', 'daegu'], [9700000, 3400000, 2400000])




```python
string = "python"
int(string)
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-113-3eb1982ee741> in <module>
          1 string = "python"
    ----> 2 int(string)
    

    ValueError: invalid literal for int() with base 10: 'python'


### 6. 연산자
- 산술연산자 : +, -, *, /, //, %, **
- 할당연산자 : 변수에 누적시켜서 연산 : +=, //=, **=
- 비교연산자 : <, >, ==, !=, <=, >= : 결과로 True, False
- 멤버연산자 : 특정 데이터가 있는지 확인할때 사용 : not in, in
- 논리연산자 : True, False를 연산 : or, and, not


```python
# 산술연산
1 + 4 / 2 ** 2
```




    2.0




```python
# 할당연산
a = 10
a+=10
a+=10
a
```




    30




```python
# 비교연산
b=2
print(a, b)
a < b, a == b, a !=b
```

    30 2
    




    (False, False, True)




```python
# 논리연산
True and False, True or False, not True or False
```




    (False, True, False)




```python
# 멤버연산
ls = ['jin', 'andy', 'john']
```


```python
'andy' in ls, 'anchel' in ls
```




    (True, False)




```python
### 랜덤함수
import random

random.randint(1, 10)
```




    10




```python
# 입력함수
data = input("insert string: ")
data
```

    insert string: 안녕하세요
    




    '안녕하세요'




```python
# 해결의 책 : 질문을 하면 질문에 대한 답변을 해주는 책
```


```python
# 솔루션을 리스트로 작성
# 질문 입력 받음
# 솔루션의 갯수에 맞게 랜덤한 index 정수 값을 생성
# index 해당하는 솔루션 리스트의 데이터를 출력
```


```python
# 솔루션을 리스트로 작성
solutions = [
    "무엇을 하든 잘 안될것이다.",
    "생각지도 않게 좋은 일이 생길것이다.",
    "무엇을 상상하든 그 이상이다."
]

# 질문 입력 받음
input("질문을 입력하세요.: ")

# 솔루션의 갯수에 맞게 랜덤한 index 정수 값을 생성
idx = random.randint(0, len(solutions) - 1)

# index 해당하는 솔루션 리스트의 데이터를 출력
solutions[idx]
```

    질문을 입력하세요.: d
    




    '무엇을 하든 잘 안될것이다.'




```python

```
