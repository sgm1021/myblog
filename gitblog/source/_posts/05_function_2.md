---
title: Jupyter notebook
date: 2021-02-22 17:32:13
tags: python
categories: programming
---


### `%reset` error
- ipython 버전을 downgrade
     - conda uninstall ipython
     - conda instapp ipython=7.2.0
     - conda install jupyter

## 함수 2
- docstring
- scope
- inner function
- lambda function
- map, filter, reduce
- decorlator

### 1. Docstring
- 함수의 설명을 작성


```python
def echo(msg):
    """
    echo return its input agument
    The operation is:
        1. print msg
        2. return msg parameter
    param : msg : str
    return str
    """
    return msg
```


```python
echo?
```


```python
echo??
```


```python
help(echo)
```

    Help on function echo in module __main__:
    
    echo(msg)
        echo return its input agument
        The operation is:
            1. print msg
            2. return msg parameter
        param : msg : str
        return str
    
    


```python
print(echo.__doc__)
```

    
        echo return its input agument
        The operation is:
            1. print msg
            2. return msg parameter
        param : msg : str
        return str
        
    

### 2. Scope 범위
- 함수 안에서 선언되는 변수와 한수 밖에서 선언되는 변수의 범위가 다릅니다.
- global(전역), local(지역)


```python
# global
gv = 10
def echo():
    print(gv)
echo()
```

    10
    


```python
# global
gv = 10
def echo():
    gv = 100
    print(gv)
echo()
```

    100
    


```python
gv
```




    10




```python
# global
gv = 10
def echo():
    global gv
    gv = 100
    print(gv)
echo()
gv # 100
```

    100
    




    100



### 3. Inner Function
- 함수가 지역영역에 선언, 함수 안에 함수가 선언


```python
def outer(a, b):
    
    def inner(c, d):
        return c + d
    
    return inner(a, b)
```


```python
outer(1,2)
```




    3




```python
inner(2, 3)
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-14-468e0d571ba5> in <module>
    ----> 1 inner(2, 3)
    

    NameError: name 'inner' is not defined



```python
def outer(a, b):
    
    def inner(c, d):
        return c + d
    
    return inner
```


```python
outer(1,2)(3, 4)
```




    7




```python
# callback function : 함수를 아규먼트 파라미터로 설정해서 사용
```


```python
def calc(func, a, b):
    # code
    a **= 2
    b **= 2
    return func(a, b)
```


```python
def plus(a, b):
    return a + b
```


```python
def minus(a, b):
    return a - b
```


```python
calc(plus, 1, 2) # 덧셈
```




    5




```python
calc(minus, 1, 2) # 뺄셈
```




    -3



### 4. 람다함수
- 파라미터를 간단한 계산으로 리턴되는 함수 : 삼항연산


```python
def plus(a, b):
    return a + b
```


```python
plus(1, 2)
```




    3




```python
plus2 = lambda a, b: a + b
plus(1, 3)
```




    4




```python
# calc(func, a, b)
calc(lambda a, b: a + b, 3, 4)
```




    25




```python
calc(plus, 3, 4)
```




    25



### 5. map, filter, reduce
- map : 순서가 있는 데이터 집합에서 모든 값에 함수를 적용시킨 결과를 출력


```python
ls = [1, 2, 3, 4]
def odd_even(num):
    return "odd" if num%2 else "even"
    
odd_even(3), odd_even(4)
```




    ('odd', 'even')




```python
list(map(odd_even, ls))
```




    ['odd', 'even', 'odd', 'even']




```python
# input 함수로 구분자로  " "으로 여러개의 숫자를 입력 받습니다.
# str.split(" ") 리스트로 만들고
# 만들어진 리스트의 값들을 int 형변환
```


```python
datas = input("insert numbers : ")
```

    insert numbers : 10 20 30 40 50 60
    


```python
result = datas.split(" ")
result
```




    ['10', '20', '30', '40', '50', '60']




```python
result = list(map(int, result))
result
```




    [10, 20, 30, 40, 50, 60]




```python
# ctrl + alt + 드래그 : 여러줄 수정
```

#### Filter
- 리스트 데이터에서 특정 조건에 맞는 value만 남기는 함수


```python
ls = range(10)
```


```python
# 홀수만 출력
list(filter(lambda data: True if data % 2 else False, ls))
```




    [1, 3, 5, 7, 9]



#### Reduce
- 리스트 데이터를 처음부터 순서대로 특정 함수를 실행하여 결과를 누적시켜 주는 함수


```python
from functools import reduce
```


```python
ls = [3, 1, 2, 4, 5]
reduce(lambda x, y : x + y, ls)
```




    15



### 6. Decorlator
- 함수에서 코드를 바꾸지 않고 기능을 추가하거나 수정하고 싶을때 사용하는 문법

```
def a():
    code_1
    code_2
    code_3
    
def b():
    code_1
    code_2
    code_3
 
```


- 데코레이터의 사용

```
def c(func):
    def wrapper(*args, **kwargs):
        code_1
        result = func(*args, **kwargs)
        code_3
        return result
      
    return wrapper
    
@c
def a():
    code_2

@c
def b():
    code_4
    
```



```python
# a
def plus(a, b):
    print("start") # code_1
    result = a+b # code_2
    print(f'result : {result}') # code_3
    return result
```


```python
# b
def minus(a, b):
    print("start") # code_1
    result = a-b # code_4
    print(f'result : {result}') # code_3
    return result
```


```python
# c
def disp(func):
    def wrapper(*args, **kwargs):
        print("start") # code_1
        result = func(*args, **kwargs) # code_2, code_4
        print(f'result : {result}') # code_3
        return result
    return wrapper        
```


```python
plus(1, 2)
```

    start
    result : 3
    




    3




```python
@disp
def plus(a, b):
    result = a + b
    return result
```


```python
plus(1, 2)
```

    start
    result : 3
    




    3




```python
# 데코레이터를 이용해서 함수의 실행 시간을 출력
```


```python
import time
```


```python
def timer(func):
    def wrapper(*args, **kwargs):
        start_time = time.time() # code_1
        result = func(*args, **kwargs) # code_2, code_4
        end_time = time.time() # code_3
        print("running time : {}".format(end_time - start_time)) # code 3
        return result
    return wrapper
```


```python
@timer
def test1(num1, num2):
    data = range(num1, num2)
    return sum(data)
```


```python
@timer
def test2(num1, num2):
    result = 0
    for num in range(num1, num2+1):
        result += num
    return result
```


```python
test1(1, 100000)
```

    running time : 0.003003358840942383
    




    4999950000




```python
test2(1, 100000)
```

    running time : 0.005014657974243164
    




    5000050000




```python
# 패스워드를 입력 받아야 함수가 실행되도록하는 데코레이터 작성
```


```python
import random
```


```python
def check_password(func):
    def wrapper(*args, **kwargs):
        pw = "dss11"
        # check password
        input_pw = input("insert pw: ")
        if input_pw == pw:
            result = func(*args, **kwargs)
        else:
            result = "not allow!"
        return result
    return wrapper
```


```python
@check_password
def plus(a, b):
    return a+b
```


```python
plus(1, 2)
```

    insert pw: dss11
    




    3




```python
@check_password
def lotto_func():
    lotto = list(range(1, 46))
    lotto = random.sample(lotto, 6)
    lotto.sort()
    return lotto
```


```python
lotto_func()
```

    insert pw: dss11
    




    [4, 11, 12, 23, 26, 45]




```python
lotto_func()
```

    insert pw: asdf
    




    'not allow!'




```python

```
