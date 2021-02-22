---
title: Jupyter notebook
date: 2021-02-22 17:32:13
tags: python
categories: programming
---


### 함수
- 반복되는 코드를 묶음으로 효율적인 코드를 작성하도록 해주는 기능
- 기본 함수 
- 파라미터와 아규먼트
- 리턴
- '*args', '**kwargs'
- docstring
- scope
- inner function
- lambda function
- Map, Filter, Reduce
- Decorlator

### 1. 기본함수
- 함수의 선언과 호출


```python
point = 88

if point >= 90:
    print("A")
elif point >= 80:
    print("B")
elif point >= 70:
    print("C")
```

    B
    


```python
%reset
```

    Once deleted, variables cannot be recovered. Proceed (y/[n])? y
    


```python
%whos
```

    Interactive namespace is empty.
    


```python
# 함수 선언
def grade(point):
    if point >= 90:
        print("A")
    elif point >= 80:
        print("B")
    elif point >= 70:
        print("C")
```


```python
a = 1
ls = [1, 2, 3]
```


```python
%whos
```

    Variable   Type        Data/Info
    --------------------------------
    a          int         1
    grade      function    <function grade at 0x0000025592D26820>
    ls         list        n=3
    


```python
# 함수 호출
grade(88)
```

    B
    


```python
# code ...
```


```python
grade(78)
```

    C
    

### 2. 파라미터와 아규먼트
- 파라미터 : 함수를 선언할때 호툴하는 부분에서 보내주는 데이터를 받는 변수
- 아규먼트 : 함수를 호출할때 함수에 보내주는 데이터


```python
def plus(num1, num2=10, num3=20): # 파라미터 : 디폴트 파라미터
    print(num1 + num2 - num3)
```


```python
plus(1, 2) # 아규먼트
```

    3
    


```python
plus(3) # 아규먼트
```

    13
    


```python
plus(3, num3=100) # 아규먼트 : 키워드 아큐먼트
```

    -87
    


```python
print(1, 2, end="-")
print(3)
```

    1 2-3
    

### 3. 리턴
- 함수를 실행한 결과를 저장하고 싶을때 사용
- return


```python
def plus(num1, num2):
    print(num1+num2)
    return num1+num2
```


```python
result = plus(1, 2)
print(result)
```

    3
    3
    


```python
data1 = "python"
result = data1.upper()
print(result)
```

    PYTHON
    


```python
data2 = [3, 1, 2]
result = data2.sort()
print(result)
```

    None
    


```python
# 함수에서 return 코드가 샐행되면 무조건 함수의 코드 실행이 종료
def echo(msg):
    if msg == "quit":
        return
    print(msg)
```


```python
echo("python")
```

    python
    


```python
echo("quit")
```

### 4. `*args`, `**kwargs`
- 함수를 호출할때 아규먼트와 키워드 아규먼트의 갯수를 특정지을수 없을때 사용


```python
def plus(*args, **kwargs):
    print(type(args), args)
    print(type(kwargs), kwargs)
    return sum(args) + sum(list(kwargs.values()))
```


```python
plus(1, 2, num1=3, num2=4)
```

    <class 'tuple'> (1, 2)
    <class 'dict'> {'num1': 3, 'num2': 4}
    




    10




```python
def func(num1, num2, num3):
    return num1, num2, num3
data = [1, 2, 3]
func(*data) # func(1, 2, 3)
```




    (1, 2, 3)




```python
data = {
    "num2": 100,
    "num3": 200,
}
func(1, **data) # func(1, num2=100, num3=200)
```




    (1, 100, 200)




```python

```
