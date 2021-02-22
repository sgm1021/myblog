### Numpy
- 데이터는 행렬 표현
- 행렬 데이터 빠르게 계산을 해야 합니다.
- 행렬 데이터 생성, 수정, 계산 등을 빠르게 처리해 주는 패키지
- 특징
    - C, C++, 포트란으로 작성
    - 선형대수학을 빠르게 연산
        - 스칼라, 벡터, 매트릭스


```python
import numpy as np
```


```python
# 행렬 데이터 생성
# ndarray : 한가지 데이터 타입만 값으로 사용이 가능
```


```python
arrary = np.array([1, 2, 3])
type(arrary), arrary
```




    (numpy.ndarray, array([1, 2, 3]))




```python
arrary2 = np.array(
    [[1, 2, 3],
    [4, 5, 6]],
)
arrary2, arrary2.ndim, arrary2.shape
```




    (array([[1, 2, 3],
            [4, 5, 6]]),
     2,
     (2, 3))




```python
# 행렬의 모양(shape) 변경하기
arrary2.reshape(3,2)
```




    array([[1, 2],
           [3, 4],
           [5, 6]])




```python
# 행렬 데이터의 선택 : offset index : masking
```


```python
arrary2[1][::-1]
```




    array([6, 5, 4])




```python
arrary2[1,2] # arrary2[1][2]
```




    6




```python
# 데이터 수정
```


```python
ls = [1,2,3]
ls[1] = 5
ls
```




    [1, 5, 3]




```python
arrary2[1][2] = 10
arrary2
```




    array([[ 1,  2,  3],
           [ 4,  5, 10]])




```python
# 브로드 캐스팅
arrary2[0] = 0
arrary2
```




    array([[ 0,  0,  0],
           [ 4,  5, 10]])




```python
arrary2[0] = [7, 8, 9]
arrary2
```




    array([[ 7,  8,  9],
           [ 4,  5, 10]])




```python
# 조건으로 선택
idx = arrary2 >7
idx
```




    array([[False,  True,  True],
           [False, False,  True]])




```python
arrary2[idx]
```




    array([ 8,  9, 10])




```python
arrary2[idx] = 100
arrary2
```




    array([[  7, 100, 100],
           [  4,   5, 100]])




```python
# 행렬 데이터의 생성 2
data = np.zeros((2,3))
data
```




    array([[0., 0., 0.],
           [0., 0., 0.]])




```python
data.dtype
```




    dtype('float64')




```python
data2 = data.astype("int")
data2.dtype
```




    dtype('int32')




```python
data = np.ones((2, 3, 2))
data
```




    array([[[1., 1.],
            [1., 1.],
            [1., 1.]],
    
           [[1., 1.],
            [1., 1.],
            [1., 1.]]])




```python
# arange
np.arange(5)
```




    array([0, 1, 2, 3, 4])




```python
np.arange(5,10)
```




    array([5, 6, 7, 8, 9])




```python
np.arange(5, 10, 2)
```




    array([5, 7, 9])




```python

```
