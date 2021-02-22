### summary
- numpy : 선형대수를 빠르게 현산해주는 패키지
- 행렬의 생성 1 : ndarray, np.array(iterable)
- 행렬의 생성 2 : ones, zeros
- 행렬 데이터 선택 : array[x, y, z]
- 행렬 데이터 수정
    - 행렬 데이터를 선택
    - =, > (값(scala, vactor, matrix))
    - 브로드 캐스팅 개녕
- arange : list에서 사용하는 range : 결과가 ndarray


```python
### quiz
- 1000 ~ 130 까지 랜덤한 숫자를 가지는 8*8행렬을 만들고,
- 3의 배수는 fiz, 5의 배수는 buz, 3과 5의 배수는 fbz 문자로 변환
- 랜덤한 행렬 데이터
```
datas = np.random.randint(100, 130, size=(8, 8))
```
- 데이터 타입이 정수 -> 문자열 : ndarray.astype()
```


```python
import numpy as np
datas = np.random.randint(100, 130, size=(8, 8))
datas
```




    array([[102, 102, 108, 128, 102, 114, 121, 111],
           [125, 118, 112, 105, 110, 119, 111, 114],
           [127, 109, 127, 101, 117, 113, 123, 109],
           [110, 123, 128, 102, 124, 127, 103, 109],
           [104, 106, 123, 115, 118, 117, 106, 110],
           [104, 120, 109, 108, 120, 126, 109, 101],
           [111, 107, 100, 118, 118, 118, 108, 104],
           [118, 111, 102, 126, 126, 120, 108, 115]])




```python
data1 = np.array([1,2,3])
data2 = [True, False, True]
data1[data2]
```




    array([1, 3])




```python
# 3의 배수 , 5의 배수, 15의 배수 위치값에 대한 T, F matrix 생성
idx_3 = datas % 3 == 0
idx_5 = datas % 5 == 0
idx_15 = datas % 15 == 0
```


```python
# 데이터 타입을 str으로 변환
datas.dtype
```




    dtype('int32')




```python
result = datas.astype("str")
result
```




    array([['113', '123', '107', '126', '102', '116', '109', '102'],
           ['103', '106', '103', '129', '109', '109', '115', '104'],
           ['125', '120', '103', '114', '102', '103', '129', '102'],
           ['114', '107', '120', '107', '118', '103', '110', '121'],
           ['101', '113', '114', '124', '101', '126', '115', '109'],
           ['125', '121', '101', '116', '124', '121', '108', '108'],
           ['129', '119', '119', '129', '108', '122', '114', '108'],
           ['101', '103', '126', '120', '127', '109', '127', '105']],
          dtype='<U11')




```python
# T, F matrix를 이용하여 특정 조건의 데이터를 선택 후 브로트캐스팅하게 값을 대입
```


```python
result[idx_3] = "fiz"
result[idx_5] = "buz"
result[idx_15] = "fbz"
```


```python
result
```




    array([['113', 'fiz', '107', 'fiz', 'fiz', '116', '109', 'fiz'],
           ['103', '106', '103', 'fiz', '109', '109', 'buz', '104'],
           ['buz', 'fbz', '103', 'fiz', 'fiz', '103', 'fiz', 'fiz'],
           ['fiz', '107', 'fbz', '107', '118', '103', 'buz', '121'],
           ['101', '113', 'fiz', '124', '101', 'fiz', 'buz', '109'],
           ['buz', '121', '101', '116', '124', '121', 'fiz', 'fiz'],
           ['fiz', '119', '119', 'fiz', 'fiz', '122', 'fiz', 'fiz'],
           ['101', '103', 'fiz', 'fbz', '127', '109', '127', 'fbz']],
          dtype='<U11')



### Quiz
- 1~20까지 랜덤한 숫자를 가지는 5*5 행렬 생성
- 최대값에는 MAX, 최소값에는 MIN 문자열이 들어가도록 치환하는 코드
```
np.min(ndarray), np.max(ndarray)
```


```python
datas = np.random.randint(1, 20, (5, 5))
datas
```




    array([[ 9,  6, 10, 19,  4],
           [14,  8,  6,  6,  6],
           [15, 14,  6, 17, 12],
           [ 5,  9,  6, 13,  8],
           [16,  3,  9, 10, 13]])




```python
min_num, max_num = np.min(datas), np.max(datas)
min_num, max_num
```




    (3, 19)




```python
idx_min = datas == min_num
idx_max = datas == max_num
```


```python
idx_min
```




    array([[False, False, False, False, False],
           [False, False, False, False, False],
           [False, False, False, False, False],
           [False, False, False, False, False],
           [False,  True, False, False, False]])




```python
idx_max
```




    array([[False, False, False,  True, False],
           [False, False, False, False, False],
           [False, False, False, False, False],
           [False, False, False, False, False],
           [False, False, False, False, False]])




```python
result = datas.astype("str")
result
```




    array([['9', '6', '10', '19', '4'],
           ['14', '8', '6', '6', '6'],
           ['15', '14', '6', '17', '12'],
           ['5', '9', '6', '13', '8'],
           ['16', '3', '9', '10', '13']], dtype='<U11')




```python
result[idx_min] = "MIN"
result[idx_max] = "MAX"
result
```




    array([['9', '6', '10', 'MAX', '4'],
           ['14', '8', '6', '6', '6'],
           ['15', '14', '6', '17', '12'],
           ['5', '9', '6', '13', '8'],
           ['16', 'MIN', '9', '10', '13']], dtype='<U11')



### 1. linspace, logspace 함수
- linspace : 설정한 범위에서 선형적으로 분할한 위치의 값을 출력
- logspace : 설정한 범위에서 로그로 분할한 위치의 값을 축력


```python
# linspace
np.linspace(0, 100, 5)
```




    array([  0.,  25.,  50.,  75., 100.])




```python
# logspace
# Log10(X1)=2, log10(X2)=3, log10(X3)=4
np.logspace(2, 4, 3)
```




    array([  100.,  1000., 10000.])




```python
# 30세 연봉이 $100000 이고 60세의 연봉이 $1000000 일때
# 연봉이 선형으로 증가, 지수함수로 증가하는 두 경우에서의 40, 50세 연봉을 출력
```


```python
age_30 = 100000
age_60 = 1000000
```


```python
np.linspace(age_30, age_60, 4)
```




    array([ 100000.,  400000.,  700000., 1000000.])




```python
np.logspace(np.log10(age_30), np.log10(age_60), 4)
```




    array([ 100000.        ,  215443.46900319,  464158.88336128,
           1000000.        ])



### 2. numpy random
- seed : 램덤값을 설정값
- rand : 균등분포로 랜덤한 값 생성
- randn : 정규분포로 난수를 발생
- randint : 균등분포로 정수값을 발생
- suffle : 행렬 데이터를 섞어 줍니다.
- choice : 특정 확률로 데이터를 선택


```python
# seed
np.random.seed(1)
result1 = np.random.randint(10, 100, 10)

np.random.seed(1)
result2 = np.random.randint(10, 100, 10)

np.random.seed(2)
result3 = np.random.randint(10, 100, 10)

result1, result2, result3
```




    (array([47, 22, 82, 19, 85, 15, 89, 74, 26, 11]),
     array([47, 22, 82, 19, 85, 15, 89, 74, 26, 11]),
     array([50, 25, 82, 32, 53, 92, 85, 17, 44, 59]))




```python
np.random.rand(10)
```




    array([0.20464863, 0.61927097, 0.29965467, 0.26682728, 0.62113383,
           0.52914209, 0.13457995, 0.51357812, 0.18443987, 0.78533515])




```python
# shuffle
r = np.random.randint(1, 10, (3, 4))
r
```




    array([[2, 3, 5, 8],
           [4, 5, 1, 2],
           [1, 9, 6, 9]])




```python
np.random.shuffle(r)
r
```




    array([[1, 9, 6, 9],
           [4, 5, 1, 2],
           [2, 3, 5, 8]])




```python
#choice
np.random.choice(5, 10, p=[0.1, 0.4, 0.2, 0.3])
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-10-e648bb30cd70> in <module>
          1 #choice
    ----> 2 np.random.choice(5, 10, p=[0.1, 0.4, 0.2, 0.3])
    

    mtrand.pyx in numpy.random.mtrand.RandomState.choice()
    

    ValueError: 'a' and 'p' must have same size



```python
# unique
number, counts = np.unique(r, return_counts=True)
print(number)
print(counts)
```

    [1 2 3 4 5 6 8 9]
    [2 2 1 1 2 1 1 2]
    

### 3. 행렬 데이터의 결합
- concatenate


```python
na1 = np.random.randint(10, size=(2,3))
na2 = np.random.randint(10, size=(3,2))
na3 = np.random.randint(10, size=(3,3))
```


```python
# 셀로 결합
na1
```




    array([[9, 3, 0],
           [3, 2, 6]])




```python
na2
```




    array([[8, 1],
           [8, 8],
           [2, 9]])




```python
na3
```




    array([[2, 0, 0],
           [2, 7, 7],
           [2, 3, 7]])




```python
np.concatenate((na1, na3))
```




    array([[9, 3, 0],
           [3, 2, 6],
           [2, 0, 0],
           [2, 7, 7],
           [2, 3, 7]])




```python
np.concatenate((na2, na3,), axis=1)
```




    array([[8, 1, 2, 0, 0],
           [8, 8, 2, 7, 7],
           [2, 9, 2, 3, 7]])




```python
# c_, r_
np.c_[np.array([1,2,3]), np.array([4,5,6])]
```




    array([[1, 4],
           [2, 5],
           [3, 6]])




```python
np.r_[np.array([1,2,3]), np.array([4,5,6])]
```




    array([1, 2, 3, 4, 5, 6])




```python
# split, bar, std, mean ...
```


```python

```
