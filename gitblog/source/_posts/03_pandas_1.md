### Pandas
- 데이터 분석을 위한 사용이 쉽고 성능이 좋은 오픈소스 python 라이브러리
- R과 Pandas의 특징
    - R보다 Pandas가 학습이 쉽습니다.
    - R보다 Pandas가 성능이 좋습니다.
    - R보다 Python은 활용할 수 있는 분야가 많습니다.
- 크게 두가지 데이터 타입을 사용합니다.
    - Serise : index와 value로 이루어진 데이터 타입
    - DataFrame : index, column, value로 이루어진 데이터 타입


```python
import numpy as np
import pandas as pd
```

### 1. Series
- 동일한 데이터 타입의 값을 갖습니다.


```python
# Series : value 만 설정하면 index는 0부처 자동으로 설정됩니다.
data = pd.Series(np.random.randint(10, size=5))
data
```




    0    3
    1    4
    2    5
    3    0
    4    3
    dtype: int32




```python
# index 설정
data = pd.Series(np.random.randint(10, size=5), index=list('ABCDE'))
data
```




    A    0
    B    7
    C    1
    D    8
    E    2
    dtype: int32




```python
data.index, data.values
```




    (Index(['A', 'B', 'C', 'D', 'E'], dtype='object'), array([0, 7, 1, 8, 2]))




```python
data["B"], data.B
```




    (7, 7)




```python
data["C"] = 10
data
```




    A     0
    B     7
    C    10
    D     8
    E     2
    dtype: int32




```python
# 브로드 캐스팅
data * 10
```




    A      0
    B     70
    C    100
    D     80
    E     20
    dtype: int32




```python
data[["B","C"]]
```




    B     7
    C    10
    dtype: int32




```python
# offset index
data[2::2]
```




    C    10
    E     2
    dtype: int32




```python
data[::-1]
```




    E     2
    D     8
    C    10
    B     7
    A     0
    dtype: int32




```python
# Series 연산
```


```python
data
```




    A     0
    B     7
    C    10
    D     8
    E     2
    dtype: int32




```python
data2 = pd.Series({"D":3, "E":5, "F":7})
data2
```




    D    3
    E    5
    F    7
    dtype: int64




```python
result = data + data2
result # None
```




    A     NaN
    B     NaN
    C     NaN
    D    11.0
    E     7.0
    F     NaN
    dtype: float64




```python
result.isnull()
```




    A     True
    B     True
    C     True
    D    False
    E    False
    F     True
    dtype: bool




```python
result[result.isnull()] = data
result
```




    A     0.0
    B     7.0
    C    10.0
    D    11.0
    E     7.0
    F     NaN
    dtype: float64




```python
result[result.isnull()] = data2
result
```




    A     0.0
    B     7.0
    C    10.0
    D    11.0
    E     7.0
    F     7.0
    dtype: float64



### 2. DataFrame
- 데이터 프레임은 여러개의 Series로 구성
- 같은 컬럼에 있는 value값은 같은 데이터 타입을 갖습니다.


```python
# 데이터 프레임 생성 1 : 딕셔너리의 리스트
```


```python
datas = {
    "name":["dss", "fcamp"],
    "Email":["dss@gmail.com","fcamp@daum.net"]
}
datas
```




    {'name': ['dss', 'fcamp'], 'Email': ['dss@gmail.com', 'fcamp@daum.net']}




```python
df = pd.DataFrame(datas)
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
      <th>Email</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>dss</td>
      <td>dss@gmail.com</td>
    </tr>
    <tr>
      <th>1</th>
      <td>fcamp</td>
      <td>fcamp@daum.net</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 데이터 프레임 생성 2 : 리스트의 딕셔너리
```


```python
datas = [
    {"name":"dss", "email":"dss@gmail.com"},
    {"name":"fcamp", "email":"fcamp@daum.net"},
]
datas
```




    [{'name': 'dss', 'email': 'dss@gmail.com'},
     {'name': 'fcamp', 'email': 'fcamp@daum.net'}]




```python
df = pd.DataFrame(datas)
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
      <th>email</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>dss</td>
      <td>dss@gmail.com</td>
    </tr>
    <tr>
      <th>1</th>
      <td>fcamp</td>
      <td>fcamp@daum.net</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 인덱스를 추가하는 방법
df = pd.DataFrame(datas, index = ["one", "two"])
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
      <th>email</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>one</th>
      <td>dss</td>
      <td>dss@gmail.com</td>
    </tr>
    <tr>
      <th>two</th>
      <td>fcamp</td>
      <td>fcamp@daum.net</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.index
```




    Index(['one', 'two'], dtype='object')




```python
df.columns
```




    Index(['name', 'email'], dtype='object')




```python
df.values
```




    array([['dss', 'dss@gmail.com'],
           ['fcamp', 'fcamp@daum.net']], dtype=object)




```python
# 데이터 프레임에서 데이터의 선택 : row, column, (row, column)
```


```python
# row 선택 : loc
df = pd.DataFrame(datas)
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
      <th>email</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>dss</td>
      <td>dss@gmail.com</td>
    </tr>
    <tr>
      <th>1</th>
      <td>fcamp</td>
      <td>fcamp@daum.net</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.loc[1]["email"]
```




    'fcamp@daum.net'




```python
# index가 있으면 수정, 없으면 추가
df.loc[2] = {"name":"andy", "email":"andy@naver.com"}
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
      <th>email</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>dss</td>
      <td>dss@gmail.com</td>
    </tr>
    <tr>
      <th>1</th>
      <td>fcamp</td>
      <td>fcamp@daum.net</td>
    </tr>
    <tr>
      <th>2</th>
      <td>andy</td>
      <td>andy@naver.com</td>
    </tr>
  </tbody>
</table>
</div>




```python
# column 선택
```


```python
df["name"]
```




    0      dss
    1    fcamp
    2     andy
    Name: name, dtype: object




```python
df["id"] = ""
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
      <th>email</th>
      <th>id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>dss</td>
      <td>dss@gmail.com</td>
      <td></td>
    </tr>
    <tr>
      <th>1</th>
      <td>fcamp</td>
      <td>fcamp@daum.net</td>
      <td></td>
    </tr>
    <tr>
      <th>2</th>
      <td>andy</td>
      <td>andy@naver.com</td>
      <td></td>
    </tr>
  </tbody>
</table>
</div>




```python
df["id"] = range(1, 4) # np.arange(1, 4)
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
      <th>email</th>
      <th>id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>dss</td>
      <td>dss@gmail.com</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>fcamp</td>
      <td>fcamp@daum.net</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>andy</td>
      <td>andy@naver.com</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.dtypes
```




    name     object
    email    object
    id        int32
    dtype: object




```python
# row, column 선택
```


```python
df.loc[[0,2], ["email", "id"]]
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
      <th>email</th>
      <th>id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>dss@gmail.com</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>andy@naver.com</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 컬럼 데이터 순서 설정
```


```python
df[["id", "name", "email"]]
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
      <th>id</th>
      <th>name</th>
      <th>email</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>dss</td>
      <td>dss@gmail.com</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>fcamp</td>
      <td>fcamp@daum.net</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>andy</td>
      <td>andy@naver.com</td>
    </tr>
  </tbody>
</table>
</div>




```python
# head, tail
```


```python
df.head(2)
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
      <th>email</th>
      <th>id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>dss</td>
      <td>dss@gmail.com</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>fcamp</td>
      <td>fcamp@daum.net</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.tail(2)
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
      <th>email</th>
      <th>id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>fcamp</td>
      <td>fcamp@daum.net</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>andy</td>
      <td>andy@naver.com</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



### 3. apply 함수
- map 함수와 비슷


```python
# email 컬럽에서 메일의 도메인만 가져와서 새로운 domain컬럼을 생성
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
      <th>email</th>
      <th>id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>dss</td>
      <td>dss@gmail.com</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>fcamp</td>
      <td>fcamp@daum.net</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>andy</td>
      <td>andy@naver.com</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
def domain(email):
    return email.split("@")[1].split(".")[0]

domain(df.loc[0]["email"])
```




    'gmail'




```python
df["domain"] = df["email"].apply(domain)
```


```python
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
      <th>email</th>
      <th>id</th>
      <th>domain</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>dss</td>
      <td>dss@gmail.com</td>
      <td>1</td>
      <td>gmail</td>
    </tr>
    <tr>
      <th>1</th>
      <td>fcamp</td>
      <td>fcamp@daum.net</td>
      <td>2</td>
      <td>daum</td>
    </tr>
    <tr>
      <th>2</th>
      <td>andy</td>
      <td>andy@naver.com</td>
      <td>3</td>
      <td>naver</td>
    </tr>
  </tbody>
</table>
</div>




```python
df["domain"] = df["email"].apply(lambda email:email.split("@")[1].split(".")[0])
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
      <th>email</th>
      <th>id</th>
      <th>domain</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>dss</td>
      <td>dss@gmail.com</td>
      <td>1</td>
      <td>gmail</td>
    </tr>
    <tr>
      <th>1</th>
      <td>fcamp</td>
      <td>fcamp@daum.net</td>
      <td>2</td>
      <td>daum</td>
    </tr>
    <tr>
      <th>2</th>
      <td>andy</td>
      <td>andy@naver.com</td>
      <td>3</td>
      <td>naver</td>
    </tr>
  </tbody>
</table>
</div>




```python
from makedata import *
```


```python
get_name()
```




    'Alvin'




```python
get_age()
```




    30




```python
df1= pd.DataFrame(make_data(5))
df2= pd.DataFrame(make_data(5))
df2
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
      <th>Age</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>40</td>
      <td>Billy</td>
    </tr>
    <tr>
      <th>1</th>
      <td>32</td>
      <td>Anchal</td>
    </tr>
    <tr>
      <th>2</th>
      <td>35</td>
      <td>Alvin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>22</td>
      <td>Andrew</td>
    </tr>
    <tr>
      <th>4</th>
      <td>27</td>
      <td>Andrew</td>
    </tr>
  </tbody>
</table>
</div>



### 4. append


```python
# append 데이터 프레임 합치기
df3 = df1.append(df2)
df3[2:7]
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
      <th>Age</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Alvin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>29</td>
      <td>Billy</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25</td>
      <td>Anchal</td>
    </tr>
    <tr>
      <th>0</th>
      <td>40</td>
      <td>Billy</td>
    </tr>
    <tr>
      <th>1</th>
      <td>32</td>
      <td>Anchal</td>
    </tr>
  </tbody>
</table>
</div>




```python
# reset_index 인덱스 재정렬
df3.reset_index(drop=True, inplace=True)
df3
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
      <th>Age</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>21</td>
      <td>Alan</td>
    </tr>
    <tr>
      <th>1</th>
      <td>27</td>
      <td>Alan</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Alvin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>29</td>
      <td>Billy</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25</td>
      <td>Anchal</td>
    </tr>
    <tr>
      <th>5</th>
      <td>40</td>
      <td>Billy</td>
    </tr>
    <tr>
      <th>6</th>
      <td>32</td>
      <td>Anchal</td>
    </tr>
    <tr>
      <th>7</th>
      <td>35</td>
      <td>Alvin</td>
    </tr>
    <tr>
      <th>8</th>
      <td>22</td>
      <td>Andrew</td>
    </tr>
    <tr>
      <th>9</th>
      <td>27</td>
      <td>Andrew</td>
    </tr>
  </tbody>
</table>
</div>




```python
df3 = df1.append(df2, ignore_index=True)
df3
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
      <th>Age</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>21</td>
      <td>Alan</td>
    </tr>
    <tr>
      <th>1</th>
      <td>27</td>
      <td>Alan</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Alvin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>29</td>
      <td>Billy</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25</td>
      <td>Anchal</td>
    </tr>
    <tr>
      <th>5</th>
      <td>40</td>
      <td>Billy</td>
    </tr>
    <tr>
      <th>6</th>
      <td>32</td>
      <td>Anchal</td>
    </tr>
    <tr>
      <th>7</th>
      <td>35</td>
      <td>Alvin</td>
    </tr>
    <tr>
      <th>8</th>
      <td>22</td>
      <td>Andrew</td>
    </tr>
    <tr>
      <th>9</th>
      <td>27</td>
      <td>Andrew</td>
    </tr>
  </tbody>
</table>
</div>



### 5. concat
- row나 column으로 데이터 프레임을 합칠때 사용


```python
df3 = pd.concat([df1, df2]).reset_index(drop=True)
df3
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
      <th>Age</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>21</td>
      <td>Alan</td>
    </tr>
    <tr>
      <th>1</th>
      <td>27</td>
      <td>Alan</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Alvin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>29</td>
      <td>Billy</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25</td>
      <td>Anchal</td>
    </tr>
    <tr>
      <th>5</th>
      <td>40</td>
      <td>Billy</td>
    </tr>
    <tr>
      <th>6</th>
      <td>32</td>
      <td>Anchal</td>
    </tr>
    <tr>
      <th>7</th>
      <td>35</td>
      <td>Alvin</td>
    </tr>
    <tr>
      <th>8</th>
      <td>22</td>
      <td>Andrew</td>
    </tr>
    <tr>
      <th>9</th>
      <td>27</td>
      <td>Andrew</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.concat([df3, df1], axis=1, join="inner")
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
      <th>Age</th>
      <th>Name</th>
      <th>Age</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>21</td>
      <td>Alan</td>
      <td>21</td>
      <td>Alan</td>
    </tr>
    <tr>
      <th>1</th>
      <td>27</td>
      <td>Alan</td>
      <td>27</td>
      <td>Alan</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Alvin</td>
      <td>34</td>
      <td>Alvin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>29</td>
      <td>Billy</td>
      <td>29</td>
      <td>Billy</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25</td>
      <td>Anchal</td>
      <td>25</td>
      <td>Anchal</td>
    </tr>
  </tbody>
</table>
</div>



### group by
- 특정 컬럽의 중복되는 데이터를 합쳐서 새로운 데이터 프레임을 만드는 방법


```python
df = pd.DataFrame(make_data())
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
      <th>Age</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>35</td>
      <td>Alvin</td>
    </tr>
    <tr>
      <th>1</th>
      <td>26</td>
      <td>Arnold</td>
    </tr>
    <tr>
      <th>2</th>
      <td>26</td>
      <td>Jin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>23</td>
      <td>Anchal</td>
    </tr>
    <tr>
      <th>4</th>
      <td>30</td>
      <td>Adam</td>
    </tr>
    <tr>
      <th>5</th>
      <td>21</td>
      <td>Arnold</td>
    </tr>
    <tr>
      <th>6</th>
      <td>33</td>
      <td>Adam</td>
    </tr>
    <tr>
      <th>7</th>
      <td>21</td>
      <td>Adam</td>
    </tr>
    <tr>
      <th>8</th>
      <td>24</td>
      <td>Alvin</td>
    </tr>
    <tr>
      <th>9</th>
      <td>32</td>
      <td>Andrew</td>
    </tr>
  </tbody>
</table>
</div>




```python
# size
result_df = df.groupby("Name").size().reset_index(name="count")
result_df
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
      <th>Name</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Adam</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alvin</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anchal</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Andrew</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Arnold</td>
      <td>2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Jin</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# sort_values : 설정한 컬럼으로 데이터 프레임을 정렬
```


```python
result_df.sort_values(["count"], ascending = False, inplace = True)
result_df.reset_index(drop=True, inplace=True)
result_df
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
      <th>Name</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Adam</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alvin</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Arnold</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Anchal</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Andrew</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Jin</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# agg
# size(), min(), max(), mean()
```


```python
df.groupby("Name").agg("min").reset_index()
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
      <th>Name</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Adam</td>
      <td>21</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alvin</td>
      <td>24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anchal</td>
      <td>23</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Andrew</td>
      <td>32</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Arnold</td>
      <td>21</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Jin</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 데이터를 요약해서 보여주는 함수
df.describe()
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
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>10.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>27.100000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>5.087021</td>
    </tr>
    <tr>
      <th>min</th>
      <td>21.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>23.250000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>26.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>31.500000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>35.000000</td>
    </tr>
  </tbody>
</table>
</div>



### 7. Merge = sql(join)
- 두개 이상의 데이터 프레임을 합쳐서 결과를 출력하는 방법


```python

```
