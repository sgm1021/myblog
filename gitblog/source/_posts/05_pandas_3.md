### Pandas Pivot
- 데이터 프레임의 컬럼 데이터에서 index, column, value를 선택해서 데이터 프레임을 만드는 방법
- `df.pivot(index, columns, values)`
    - groupby 하고 pivot을 실행
- `df.pivot_table(values, index, columns, aggfunc)`

#### pandas io
- 데이터 프레임을 저장, 로드


```python
# lod
titanic = pd.read_csv("datas/train.csv")
titanic.tail(2)
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>889</th>
      <td>890</td>
      <td>1</td>
      <td>1</td>
      <td>Behr, Mr. Karl Howell</td>
      <td>male</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>111369</td>
      <td>30.00</td>
      <td>C148</td>
      <td>C</td>
    </tr>
    <tr>
      <th>890</th>
      <td>891</td>
      <td>0</td>
      <td>3</td>
      <td>Dooley, Mr. Patrick</td>
      <td>male</td>
      <td>32.0</td>
      <td>0</td>
      <td>0</td>
      <td>370376</td>
      <td>7.75</td>
      <td>NaN</td>
      <td>Q</td>
    </tr>
  </tbody>
</table>
</div>




```python
# save
titanic.to_csv("datas/titanic.tsv", sep="\t", index=False)
```


```python
# load : encoding
df = pd.read_csv("datas/2014_p.csv", encoding="euc_kr")
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
      <th>ID</th>
      <th>RCTRCK</th>
      <th>RACE_DE</th>
      <th>RACE_NO</th>
      <th>PARTCPT_NO</th>
      <th>RANK</th>
      <th>RCHOSE_NM</th>
      <th>HRSMN</th>
      <th>RCORD</th>
      <th>ARVL_DFFRNC</th>
      <th>EACH_SCTN_PASAGE_RANK</th>
      <th>A_WIN_SYTM_EXPECT_ALOT</th>
      <th>WIN_STA_EXPECT_ALOT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>27216</th>
      <td>27217</td>
      <td>제주</td>
      <td>2014-11-29</td>
      <td>9</td>
      <td>7</td>
      <td>6.0</td>
      <td>미주여행</td>
      <td>김경휴</td>
      <td>0:01:31.1</td>
      <td>13</td>
      <td>2 -  -  - 2 - 3 - 6</td>
      <td>6.2</td>
      <td>9.4</td>
    </tr>
    <tr>
      <th>27217</th>
      <td>27218</td>
      <td>제주</td>
      <td>2014-11-29</td>
      <td>9</td>
      <td>6</td>
      <td>1.0</td>
      <td>철옹성</td>
      <td>장우성</td>
      <td>0:01:26.6</td>
      <td>NaN</td>
      <td>1 -  -  - 1 - 1 - 1</td>
      <td>3.9</td>
      <td>2.9</td>
    </tr>
  </tbody>
</table>
</div>



#### kaggle
- 데이터 분석, 모델을 경쟁할 수 있도록 만든 서비스
- https://www.kaggle.com/

#### 1. 성별, 좌석등급에 따른 데이터의 수


```python
df1 = titanic.groupby(["Sex", "Pclass"]).size().reset_index(name="counts")
df1
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
      <th>Sex</th>
      <th>Pclass</th>
      <th>counts</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>female</td>
      <td>1</td>
      <td>94</td>
    </tr>
    <tr>
      <th>1</th>
      <td>female</td>
      <td>2</td>
      <td>76</td>
    </tr>
    <tr>
      <th>2</th>
      <td>female</td>
      <td>3</td>
      <td>144</td>
    </tr>
    <tr>
      <th>3</th>
      <td>male</td>
      <td>1</td>
      <td>122</td>
    </tr>
    <tr>
      <th>4</th>
      <td>male</td>
      <td>2</td>
      <td>108</td>
    </tr>
    <tr>
      <th>5</th>
      <td>male</td>
      <td>3</td>
      <td>347</td>
    </tr>
  </tbody>
</table>
</div>




```python
# pivot
result = df1.pivot("Sex", "Pclass", "counts")
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
      <th>Pclass</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
    <tr>
      <th>Sex</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>94</td>
      <td>76</td>
      <td>144</td>
    </tr>
    <tr>
      <th>male</th>
      <td>122</td>
      <td>108</td>
      <td>347</td>
    </tr>
  </tbody>
</table>
</div>




```python
# pivot table 이용
titanic["counts"] = 1
titanic.tail(2)
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
      <th>counts</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>889</th>
      <td>890</td>
      <td>1</td>
      <td>1</td>
      <td>Behr, Mr. Karl Howell</td>
      <td>male</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>111369</td>
      <td>30.00</td>
      <td>C148</td>
      <td>C</td>
      <td>1</td>
    </tr>
    <tr>
      <th>890</th>
      <td>891</td>
      <td>0</td>
      <td>3</td>
      <td>Dooley, Mr. Patrick</td>
      <td>male</td>
      <td>32.0</td>
      <td>0</td>
      <td>0</td>
      <td>370376</td>
      <td>7.75</td>
      <td>NaN</td>
      <td>Q</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
result = titanic.pivot_table("counts", ["Pclass"], ["Survived"], aggfunc=np.sum)
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
      <th>Survived</th>
      <th>0</th>
      <th>1</th>
    </tr>
    <tr>
      <th>Pclass</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>80</td>
      <td>136</td>
    </tr>
    <tr>
      <th>2</th>
      <td>97</td>
      <td>87</td>
    </tr>
    <tr>
      <th>3</th>
      <td>372</td>
      <td>119</td>
    </tr>
  </tbody>
</table>
</div>




```python
result["total"] = result[0]+result[1]
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
      <th>Survived</th>
      <th>0</th>
      <th>1</th>
      <th>total</th>
    </tr>
    <tr>
      <th>Pclass</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>80</td>
      <td>136</td>
      <td>216</td>
    </tr>
    <tr>
      <th>2</th>
      <td>97</td>
      <td>87</td>
      <td>184</td>
    </tr>
    <tr>
      <th>3</th>
      <td>372</td>
      <td>119</td>
      <td>491</td>
    </tr>
  </tbody>
</table>
</div>




```python
result.loc["total"] = result.loc[1] + result.loc[2] + result.loc[3]
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
      <th>Survived</th>
      <th>0</th>
      <th>1</th>
      <th>total</th>
    </tr>
    <tr>
      <th>Pclass</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>80</td>
      <td>136</td>
      <td>216</td>
    </tr>
    <tr>
      <th>2</th>
      <td>97</td>
      <td>87</td>
      <td>184</td>
    </tr>
    <tr>
      <th>3</th>
      <td>372</td>
      <td>119</td>
      <td>491</td>
    </tr>
    <tr>
      <th>total</th>
      <td>549</td>
      <td>342</td>
      <td>891</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1 = pd.read_csv("datas/2014_p.csv", encoding="euc-kr")
df1.tail(2)
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
      <th>RCTRCK</th>
      <th>RACE_DE</th>
      <th>RACE_NO</th>
      <th>PARTCPT_NO</th>
      <th>RANK</th>
      <th>RCHOSE_NM</th>
      <th>HRSMN</th>
      <th>RCORD</th>
      <th>ARVL_DFFRNC</th>
      <th>EACH_SCTN_PASAGE_RANK</th>
      <th>A_WIN_SYTM_EXPECT_ALOT</th>
      <th>WIN_STA_EXPECT_ALOT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>27216</th>
      <td>27217</td>
      <td>제주</td>
      <td>2014-11-29</td>
      <td>9</td>
      <td>7</td>
      <td>6.0</td>
      <td>미주여행</td>
      <td>김경휴</td>
      <td>0:01:31.1</td>
      <td>13</td>
      <td>2 -  -  - 2 - 3 - 6</td>
      <td>6.2</td>
      <td>9.4</td>
    </tr>
    <tr>
      <th>27217</th>
      <td>27218</td>
      <td>제주</td>
      <td>2014-11-29</td>
      <td>9</td>
      <td>6</td>
      <td>1.0</td>
      <td>철옹성</td>
      <td>장우성</td>
      <td>0:01:26.6</td>
      <td>NaN</td>
      <td>1 -  -  - 1 - 1 - 1</td>
      <td>3.9</td>
      <td>2.9</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2 = pd.read_csv("datas/2014_s.csv", encoding="euc-kr")
df2.tail(2)
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
      <th>RCTRCK</th>
      <th>RACE_DE</th>
      <th>PRDCTN_NATION_NM</th>
      <th>SEX</th>
      <th>AGE</th>
      <th>BND_WT</th>
      <th>TRNER</th>
      <th>RCHOSE_OWNR_NM</th>
      <th>RCHOSE_BDWGH</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>27216</th>
      <td>27217</td>
      <td>제주</td>
      <td>2014-11-29</td>
      <td>한</td>
      <td>거</td>
      <td>NaN</td>
      <td>53.0</td>
      <td>강대은</td>
      <td>김기준</td>
      <td>281</td>
    </tr>
    <tr>
      <th>27217</th>
      <td>27218</td>
      <td>제주</td>
      <td>2014-11-29</td>
      <td>한</td>
      <td>거</td>
      <td>NaN</td>
      <td>57.5</td>
      <td>박병진</td>
      <td>강상우</td>
      <td>314</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
