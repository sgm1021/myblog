---
title: Try Except
date: 2021-02-22 17:32:13
tags: python
categories: programming
---


### 예외처리
- 코드를 실행중에 에러가 발생한 경우 에러를 처리하는 방법
- try, except, finally, raise


```python
# try, except : 에러가 발생해도 코드의 실행을 계속하고 싶을때
ls = [1, 2, 3]
```


```python
print(ls[3])
print("Done!")
```


    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    <ipython-input-4-f88f334466aa> in <module>
    ----> 1 print(ls[3])
          2 print("Done!")
    

    IndexError: list index out of range



```python
try:
    print(ls[3])
except Exception as e:
    print("error")
    print(e)
print("Done")
```

    error
    list index out of range
    Done
    


```python
# finally : try, except 구문 실행된 후 finally 구문이 실행
try:
    1/0
except:
    print("error")
finally:
    print("Done!")
```

    error
    Done!
    


```python
# raise : 강제로 에러를 발생시키는 명령
```


```python
try:
    1/0
except Exception as e:
    print("error")
    raise(e)

print("Done!")
```

    error
    


    ---------------------------------------------------------------------------

    ZeroDivisionError                         Traceback (most recent call last)

    <ipython-input-9-bcde7d6d4636> in <module>
          3 except Exception as e:
          4     print("error")
    ----> 5     raise(e)
          6 
          7 print("Done!")
    

    <ipython-input-9-bcde7d6d4636> in <module>
          1 try:
    ----> 2     1/0
          3 except Exception as e:
          4     print("error")
          5     raise(e)
    

    ZeroDivisionError: division by zero



```python
# 에러 생성 : 10이상의 숫자가 입력되도록 하는 에러
# LowNumber
```


```python
class LowNumber(Exception):
    
    def __str__(self):
        return "Number grater than 10"
```


```python
def input_number(num):
    if num <= 10:
        raise LowNumber()
    print(num)
```


```python
input_number(8)
```


    ---------------------------------------------------------------------------

    LowNumber                                 Traceback (most recent call last)

    <ipython-input-15-8684a0e33c0b> in <module>
    ----> 1 input_number(8)
    

    <ipython-input-13-2dcc4faaa999> in input_number(num)
          1 def input_number(num):
          2     if num <= 10:
    ----> 3         raise LowNumber()
          4     print(num)
    

    LowNumber: Number grater than 10



```python

```
