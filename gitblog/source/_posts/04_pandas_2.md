### summary
- pandas
    - 데이터 분석 : 데이터 전처리 파트
    - 테이블 형태의 데이터를 처리할때 사용하는 python 라이브러리
    - Series, DataFrame
    - Series
        - 생성, 선택, 수정 방법
    - DataFrame
        - 생성 방법 1 : 딕셔너리의 리스트 : 리스트 -> 컬럼 데이터
        - 생성 방법 2 : 리스트의 딕셔너리 : 딕셔너리 -> 로우 데이터
        - row 선택 : `df.loc[idx]`
        - column 선택 : `df[column name]`
        - row, column 선택 : `df.loc[idx, column]`
        - 함수
            - apply, append, concat
            - groupby, merge


```python
import makedata
```


```python
makedata.get_age(), makedata.get_name()
```




    (21, 'Billy')




```python
makedata.make_data()
```




    [{'Age': 32, 'Name': 'Alvin'},
     {'Age': 26, 'Name': 'Alan'},
     {'Age': 25, 'Name': 'Anthony'},
     {'Age': 40, 'Name': 'Anthony'},
     {'Age': 35, 'Name': 'Billy'},
     {'Age': 39, 'Name': 'Anthony'},
     {'Age': 30, 'Name': 'Andrew'},
     {'Age': 24, 'Name': 'Andrew'},
     {'Age': 31, 'Name': 'Anthony'},
     {'Age': 40, 'Name': 'Andrew'}]



#### quiz
- makedata 모듈을 이용해서 데이터 프레임 만들기
- user_df
    - 8명의 데이터가 있는 데이터 프레임을 만드세요.
    - UserID : 1 ~ 8
    - Name : makedata.get_name()
    - Age  : makedata.get_age()
    - 중복되는 Name 값이 없도록


```python
# 딕셔너리의 리스트 : UserID, Name, Age
datas = {}
datas["UserID"] = list(range(1, 9))
datas["Age"] = [makedata.get_age() for _ in range(8)]
names = []
while True:
    name = makedata.get_name()
    if name not in names:
        names.append(name)
    if len(names) >= 8:
        break
datas["Name"] = names

user_df = pd.DataFrame(datas)
user_df
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
      <th>UserID</th>
      <th>Age</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>22</td>
      <td>Anchal</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>35</td>
      <td>Andrew</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>29</td>
      <td>Anthony</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>21</td>
      <td>Billy</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>35</td>
      <td>Arnold</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>32</td>
      <td>Alan</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>34</td>
      <td>Alvin</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>22</td>
      <td>Adam</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 딕셔너리 데이터를 데이터 프레임에 하나씩 추가하기 : UserID, Name, Age
user_df = pd.DataFrame(columns=["UserID", "Name", "Age"])

for idx in range(1, 9):

    name = makedata.get_name()
    while name in list(user_df["Name"]):
        name = makedata.get_name()

    data = {"Name": name, "UserID": idx, "Age": makedata.get_age()}

    user_df.loc[len(user_df)] = data

user_df
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
      <th>UserID</th>
      <th>Name</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Billy</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Adam</td>
      <td>26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Anchal</td>
      <td>23</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Alan</td>
      <td>39</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Alvin</td>
      <td>20</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Andrew</td>
      <td>32</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Arnold</td>
      <td>22</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>Alex</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
</div>



#### quiz
- money_df 만들기
    - 15개의 데이터
    - ID : 1 ~ 8 랜덤한 숫자 데이터
    - Money : 1000원 단위로 1000원 ~ 20000원까지의 숫자가 저장


```python
# 딕셔너리 데이터를 데이터 프레임에 하나씩 추가하기
money_df = pd.DataFrame(columns=["ID", "Money"])
# np.random.randint(1, 9)
for _ in range(15):
    money_df.loc[len(money_df)] = {
        "ID": np.random.randint(1, 9),
        "Money": np.random.randint(1, 21) * 1000,
    }
    
# 컬럼데이터에서 Unique 값 확인
ids = money_df["ID"].unique()
ids.sort()
len(ids), ids
```




    (6, array([1, 2, 3, 5, 6, 7], dtype=object))




```python
money_df
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
      <th>ID</th>
      <th>Money</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5</td>
      <td>20000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>9000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7</td>
      <td>4000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3</td>
      <td>13000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>14000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1</td>
      <td>16000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2</td>
      <td>6000</td>
    </tr>
    <tr>
      <th>9</th>
      <td>6</td>
      <td>13000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>7</td>
      <td>9000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1</td>
      <td>16000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2</td>
      <td>15000</td>
    </tr>
    <tr>
      <th>14</th>
      <td>7</td>
      <td>14000</td>
    </tr>
  </tbody>
</table>
</div>




```python
user_df
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
      <th>UserID</th>
      <th>Name</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Billy</td>
      <td>23</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Adam</td>
      <td>26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Anchal</td>
      <td>23</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Alan</td>
      <td>39</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Alvin</td>
      <td>20</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Andrew</td>
      <td>32</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Arnold</td>
      <td>22</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>Alex</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
</div>



### 1. merge


```python
user_df.merge(money_df, left_on="UserID", right_on="ID")
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
      <th>UserID</th>
      <th>Name</th>
      <th>Age</th>
      <th>ID</th>
      <th>Money</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Billy</td>
      <td>23</td>
      <td>1</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Billy</td>
      <td>23</td>
      <td>1</td>
      <td>16000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Billy</td>
      <td>23</td>
      <td>1</td>
      <td>16000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>Billy</td>
      <td>23</td>
      <td>1</td>
      <td>10000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>Adam</td>
      <td>26</td>
      <td>2</td>
      <td>9000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>Adam</td>
      <td>26</td>
      <td>2</td>
      <td>14000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2</td>
      <td>Adam</td>
      <td>26</td>
      <td>2</td>
      <td>6000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2</td>
      <td>Adam</td>
      <td>26</td>
      <td>2</td>
      <td>15000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>3</td>
      <td>Anchal</td>
      <td>23</td>
      <td>3</td>
      <td>13000</td>
    </tr>
    <tr>
      <th>9</th>
      <td>5</td>
      <td>Alvin</td>
      <td>20</td>
      <td>5</td>
      <td>20000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>6</td>
      <td>Andrew</td>
      <td>32</td>
      <td>6</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>6</td>
      <td>Andrew</td>
      <td>32</td>
      <td>6</td>
      <td>13000</td>
    </tr>
    <tr>
      <th>12</th>
      <td>7</td>
      <td>Arnold</td>
      <td>22</td>
      <td>7</td>
      <td>4000</td>
    </tr>
    <tr>
      <th>13</th>
      <td>7</td>
      <td>Arnold</td>
      <td>22</td>
      <td>7</td>
      <td>9000</td>
    </tr>
    <tr>
      <th>14</th>
      <td>7</td>
      <td>Arnold</td>
      <td>22</td>
      <td>7</td>
      <td>14000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 컬럼명 변경
user_df.rename(columns={"UserID":"ID"}, inplace=True)
user_df.tail(1)
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
      <th>ID</th>
      <th>Name</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>Alex</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
</div>




```python
user_df.merge(money_df).tail(2)
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
      <th>ID</th>
      <th>Name</th>
      <th>Age</th>
      <th>Money</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>13</th>
      <td>7</td>
      <td>Arnold</td>
      <td>22</td>
      <td>9000</td>
    </tr>
    <tr>
      <th>14</th>
      <td>7</td>
      <td>Arnold</td>
      <td>22</td>
      <td>14000</td>
    </tr>
  </tbody>
</table>
</div>




```python
result_df = pd.merge(money_df, user_df)
result_df.tail()
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
      <th>ID</th>
      <th>Money</th>
      <th>Name</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>3</td>
      <td>13000</td>
      <td>Anchal</td>
      <td>23</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1</td>
      <td>3000</td>
      <td>Billy</td>
      <td>23</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1</td>
      <td>16000</td>
      <td>Billy</td>
      <td>23</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1</td>
      <td>16000</td>
      <td>Billy</td>
      <td>23</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1</td>
      <td>10000</td>
      <td>Billy</td>
      <td>23</td>
    </tr>
  </tbody>
</table>
</div>




```python
# groupby : sum, size, min .. 함수 : Series
money_list = result_df.groupby("Name").sum()["Money"].reset_index()
money_list
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
      <th>Money</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Adam</td>
      <td>44000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alvin</td>
      <td>20000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anchal</td>
      <td>13000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Andrew</td>
      <td>18000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Arnold</td>
      <td>27000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Billy</td>
      <td>45000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# groupby : agg("sum"), agg("mean") .. : DataFrame
money_list = result_df.groupby("Name").agg("sum").reset_index()[["Name", "Money"]]
money_list
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
      <th>Money</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Adam</td>
      <td>44000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alvin</td>
      <td>20000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anchal</td>
      <td>13000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Andrew</td>
      <td>18000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Arnold</td>
      <td>27000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Billy</td>
      <td>45000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# merge : money_list, user_df : outer
```


```python
result = pd.merge(user_df, money_list, how="outer")
result
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
      <th>ID</th>
      <th>Name</th>
      <th>Age</th>
      <th>Money</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Billy</td>
      <td>23</td>
      <td>45000.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Adam</td>
      <td>26</td>
      <td>44000.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Anchal</td>
      <td>23</td>
      <td>13000.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Alan</td>
      <td>39</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Alvin</td>
      <td>20</td>
      <td>20000.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Andrew</td>
      <td>32</td>
      <td>18000.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Arnold</td>
      <td>22</td>
      <td>27000.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>Alex</td>
      <td>30</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# fillna : NaN 을 특정 데이터로 채워줌
```


```python
result.fillna(value=0, inplace=True)
result
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
      <th>ID</th>
      <th>Name</th>
      <th>Age</th>
      <th>Money</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Billy</td>
      <td>23</td>
      <td>45000.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Adam</td>
      <td>26</td>
      <td>44000.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Anchal</td>
      <td>23</td>
      <td>13000.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Alan</td>
      <td>39</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Alvin</td>
      <td>20</td>
      <td>20000.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Andrew</td>
      <td>32</td>
      <td>18000.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Arnold</td>
      <td>22</td>
      <td>27000.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>Alex</td>
      <td>30</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# money 컬럼을 정수로 데이터 타입을 변경
result.dtypes
```




    ID         int64
    Name      object
    Age        int64
    Money    float64
    dtype: object




```python
result["Money"] = result["Money"].astype("int")
result
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
      <th>ID</th>
      <th>Name</th>
      <th>Age</th>
      <th>Money</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Billy</td>
      <td>23</td>
      <td>45000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Adam</td>
      <td>26</td>
      <td>44000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Anchal</td>
      <td>23</td>
      <td>13000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Alan</td>
      <td>39</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Alvin</td>
      <td>20</td>
      <td>20000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Andrew</td>
      <td>32</td>
      <td>18000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Arnold</td>
      <td>22</td>
      <td>27000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>Alex</td>
      <td>30</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
result.sort_values("Money", ascending=False)
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
      <th>ID</th>
      <th>Name</th>
      <th>Age</th>
      <th>Money</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Billy</td>
      <td>23</td>
      <td>45000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Adam</td>
      <td>26</td>
      <td>44000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Arnold</td>
      <td>22</td>
      <td>27000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Alvin</td>
      <td>20</td>
      <td>20000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Andrew</td>
      <td>32</td>
      <td>18000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Anchal</td>
      <td>23</td>
      <td>13000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Alan</td>
      <td>39</td>
      <td>0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>Alex</td>
      <td>30</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
np.average(result.sort_values("Money", ascending=False)[:3]["Age"])
```




    23.666666666666668


