---
title: Jupyter notebook
date: 2021-02-22 17:32:13
tags: python
categories: programming
---


### class : 클래스
- 변수와 함수를 묶어 놓은 개념
- 사용 방법
    - 변수와 함수가 들어있는 클래스를 선언
    - 클래스를 객체로 만들어서 클래스 안에 선언된 변수와 함수를 사용

#### 1. 기본 클래스의 사용


```python
# 클래스의 선언
class Calculator:
    num1 = 1
    num2 = 2
    
    def plus(self):
        return self.num1 + self.num2
    
    def minus(self):
        return self.num1 - self.num2
```


```python
# 클래스의 사용
calc = Calculator()
calc
```




    <__main__.Calculator at 0x1d17368fca0>




```python
calc.num1, calc.num2, calc.plus(), calc.minus()
```




    (1, 2, 3, -1)




```python
# self의 의미 : 객체 자신
calc2 = Calculator()
```


```python
calc2.num1 = 10
```


```python
calc2.plus()
```




    12



### 2. 객체지향
- 실체 세계를 코드에 반영해서 개발하는 방법
- 여러명의 개발자가 코드를 효율적으로 작성해서 프로젝트를 완성시키기 위한 방법
- 설계도 작성(class) -> 실제 물건(object)
- 사용자 정의 데이터 타입


```python
calc2.plus()
```




    12




```python
obj = "python"
obj.upper()
```




    'PYTHON'




```python
ls = [1, 3, 2]
ls.sort()
```


```python
ls
```




    [1, 2, 3]




```python
[data for data in dir(calc) if data[:2] != '__']
```




    ['minus', 'num1', 'num2', 'plus']



### 3. 생성자
- 클래스가 객체로 생성될때 실행되는 함수
- 변수(재료)를 추가할때 사용됩니다.


```python
class Calculator:
    # 생정자 함수 : __init__
    def __init__(self, num1, num2=10):
        self.num1 = num1
        self.num2 = num2
    
    def plus(self):
        return self.num1 + self.num2
    
    def minus(self):
        return self.num1 - self.num2
```


```python
calc1 = Calculator(3)
```


```python
calc1.plus()
```




    13




```python
calc2 = Calculator(3, 5)
```


```python
calc2.plus()
```




    8




```python
# join
ls = ["python", "is", "good"]
sep = " "
sep.join(ls)
```




    'python is good'




```python
# pandas dataframe
import pandas as pd
```


```python
df = pd.DataFrame([
    {"name":"jin", "age":20}, 
    {"name":"andy", "age":21},
])
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>jin</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1</th>
      <td>andy</td>
      <td>21</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
