# 시계열 데이터

-----

판다스에서 시계열 자료형은 Timestamp와 Period 두가지 타입이 있습니다.

- Timestamp 자료형은 `to_datetime()`함수로 생성가능하며 날짜형태의 자료형을 시계열 타입으로 변환합니다.

- period 자료형은 Timestamp(datetime)객체를 다시 기간에 따른 자료형으로 이용하고자 할때 사용합니다.

# 2. 자료형의 시계열 객체 변환 : to_datetime(), to_period()

먼저 시계열 데이터의 대표주자인 주식 데이터를 로드합니다.


```python
import pandas as pd

df = pd.read_csv('../data/stock.csv')
df.head()
```

info 메소드를 통해 데이터 요약정보를 확인해봅시다.


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 105 entries, 0 to 104
    Data columns (total 7 columns):
     #   Column     Non-Null Count  Dtype 
    ---  ------     --------------  ----- 
     0   Date       105 non-null    object
     1   High       105 non-null    int64 
     2   Low        105 non-null    int64 
     3   Open       105 non-null    int64 
     4   Close      105 non-null    int64 
     5   Volume     105 non-null    int64 
     6   Adj Close  105 non-null    int64 
    dtypes: int64(6), object(1)
    memory usage: 5.9+ KB
    

현재 날짜를 나타내는 Date 컬럼의 Dtype은 object로 문자형임을 알 수 있습니다.

`to_datetime()` 함수를 이용해서 Date컬럼을 시계열 객체(Timestamp)로 변환해봅시다.


```python
df['new_date'] = pd.to_datetime(df['Date'])
df.head()
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
      <th>Date</th>
      <th>High</th>
      <th>Low</th>
      <th>Open</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Adj Close</th>
      <th>new_date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-03-02</td>
      <td>55500</td>
      <td>53600</td>
      <td>54300</td>
      <td>55000</td>
      <td>30403412</td>
      <td>55000</td>
      <td>2020-03-02</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-03-03</td>
      <td>56900</td>
      <td>55100</td>
      <td>56700</td>
      <td>55400</td>
      <td>30330295</td>
      <td>55400</td>
      <td>2020-03-03</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-03-04</td>
      <td>57600</td>
      <td>54600</td>
      <td>54800</td>
      <td>57400</td>
      <td>24765728</td>
      <td>57400</td>
      <td>2020-03-04</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-03-05</td>
      <td>58000</td>
      <td>56700</td>
      <td>57600</td>
      <td>57800</td>
      <td>21698990</td>
      <td>57800</td>
      <td>2020-03-05</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-03-06</td>
      <td>57200</td>
      <td>56200</td>
      <td>56500</td>
      <td>56500</td>
      <td>18716656</td>
      <td>56500</td>
      <td>2020-03-06</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 105 entries, 0 to 104
    Data columns (total 8 columns):
     #   Column     Non-Null Count  Dtype         
    ---  ------     --------------  -----         
     0   Date       105 non-null    object        
     1   High       105 non-null    int64         
     2   Low        105 non-null    int64         
     3   Open       105 non-null    int64         
     4   Close      105 non-null    int64         
     5   Volume     105 non-null    int64         
     6   Adj Close  105 non-null    int64         
     7   new_date   105 non-null    datetime64[ns]
    dtypes: datetime64[ns](1), int64(6), object(1)
    memory usage: 6.7+ KB
    


```python
type(df.new_date[0])
```




    pandas._libs.tslibs.timestamps.Timestamp



to_datetime 함수를 이용해 object(문자)형 데이터였던 Date 컬럼을 시계열객체로 변경했습니다.

info 메소드의 결과로 new_date 컬럼의 Dtype은 datetime으로 시계열객체가 된 것을 확인할 수 있습니다.

마찬가지로 new_date의 첫번째 row의 type을 확인한 결과 timestamp로 나타나는 것을 알 수 있습니다.

이제 기존 Date열은 삭제하고 new_date를 인덱스로 지정하겠습니다.


```python
df.drop('Date', axis=1, inplace=True)
df.set_index('new_date', inplace=True)
```


```python
df.head()
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
      <th>High</th>
      <th>Low</th>
      <th>Open</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Adj Close</th>
    </tr>
    <tr>
      <th>new_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-03-02</th>
      <td>55500</td>
      <td>53600</td>
      <td>54300</td>
      <td>55000</td>
      <td>30403412</td>
      <td>55000</td>
    </tr>
    <tr>
      <th>2020-03-03</th>
      <td>56900</td>
      <td>55100</td>
      <td>56700</td>
      <td>55400</td>
      <td>30330295</td>
      <td>55400</td>
    </tr>
    <tr>
      <th>2020-03-04</th>
      <td>57600</td>
      <td>54600</td>
      <td>54800</td>
      <td>57400</td>
      <td>24765728</td>
      <td>57400</td>
    </tr>
    <tr>
      <th>2020-03-05</th>
      <td>58000</td>
      <td>56700</td>
      <td>57600</td>
      <td>57800</td>
      <td>21698990</td>
      <td>57800</td>
    </tr>
    <tr>
      <th>2020-03-06</th>
      <td>57200</td>
      <td>56200</td>
      <td>56500</td>
      <td>56500</td>
      <td>18716656</td>
      <td>56500</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 105 entries, 2020-03-02 to 2020-07-30
    Data columns (total 6 columns):
     #   Column     Non-Null Count  Dtype
    ---  ------     --------------  -----
     0   High       105 non-null    int64
     1   Low        105 non-null    int64
     2   Open       105 non-null    int64
     3   Close      105 non-null    int64
     4   Volume     105 non-null    int64
     5   Adj Close  105 non-null    int64
    dtypes: int64(6)
    memory usage: 5.7 KB
    

데이터요약정보에서 인덱스가 `DatetimeIndex`로 나타나는 것을 알 수 있고 2020-03-02부터 2020-07-30으로 나타나는 것을 알 수있습니다.

이번에는 Timestamp와 Period의 차이를 알아보겠습니다.


```python
# Timestamp를 Period로 변환

dates = ['2021-01-01', '2021-02-01', '2021-03-01']

ts_dates = pd.to_datetime(dates)

print(ts_dates)
```

    DatetimeIndex(['2021-01-01', '2021-02-01', '2021-03-01'], dtype='datetime64[ns]', freq=None)
    


```python
# Timestamp를 Period변환
pr_day = ts_dates.to_period(freq='D') # 1일의 기간
print(pr_day)
```

    PeriodIndex(['2021-01-01', '2021-02-01', '2021-03-01'], dtype='period[D]', freq='D')
    


```python
pr_month = ts_dates.to_period(freq='M') # 1개월의 기간
print(pr_month)
```

    PeriodIndex(['2021-01', '2021-02', '2021-03'], dtype='period[M]', freq='M')
    


```python
pr_year = ts_dates.to_period(freq='A') # 1년의 기간
print(pr_year)
```

    PeriodIndex(['2021', '2021', '2021'], dtype='period[A-DEC]', freq='A-DEC')
    

이처럼 Period 객체는 `to_period(freq='기간인수')`를 통해 datetime 변수에 대해 어떤 기간에 따른 자료형을 생성하고자 할 때 사용됩니다.

이는 바로 아무 자료형에나 사용할 수 없고 datetime 타입에 대해 적용 가능합니다.

아래는 freq에 사용할 수 있는 다양한 기간인수입니다.

![image.png](attachment:image.png)

# 시계열 데이터 만들기 : date_range(), period_range()

---

## Timestamp 배열

Timestamp를 배열하는 `date_range`함수는 내장함수 range() 함수와 동일한 개념입니다.

다음과 같이 옵션을 지정하면 원하는 일정 기간의 Timestamp(datetime)배열을 얻을 수 있습니다.


```python
ts_ms = pd.date_range(start = '2020-01-01', # 날짜 범위 시작
                      end = None,          # 날짜 범위 끝
                      periods = 20,        # 생성할 Timestamp 수
                      freq ='B',           # 시간 간격 (B: 평일)
                      tz = 'Asia/Seoul')   # 시간대(timezone)

print(ts_ms)
```

    DatetimeIndex(['2020-01-01 00:00:00+09:00', '2020-01-02 00:00:00+09:00',
                   '2020-01-03 00:00:00+09:00', '2020-01-06 00:00:00+09:00',
                   '2020-01-07 00:00:00+09:00', '2020-01-08 00:00:00+09:00',
                   '2020-01-09 00:00:00+09:00', '2020-01-10 00:00:00+09:00',
                   '2020-01-13 00:00:00+09:00', '2020-01-14 00:00:00+09:00',
                   '2020-01-15 00:00:00+09:00', '2020-01-16 00:00:00+09:00',
                   '2020-01-17 00:00:00+09:00', '2020-01-20 00:00:00+09:00',
                   '2020-01-21 00:00:00+09:00', '2020-01-22 00:00:00+09:00',
                   '2020-01-23 00:00:00+09:00', '2020-01-24 00:00:00+09:00',
                   '2020-01-27 00:00:00+09:00', '2020-01-28 00:00:00+09:00'],
                  dtype='datetime64[ns, Asia/Seoul]', freq='B')
    

## Period 배열

마찬가지로 Period 배열을 생성해주는 `period_range()` 함수를 알아봅시다.

Timestamp와의 차이점은 Period는 기간을 나타내는 자료형으로 배열을 적용할 때 `freq=` 옵션은 기간의 단위를 의미한다는 점입니다.


```python
# 1개월 길이

pr_m = pd.period_range(start='2020-01-01', end=None, periods=3, freq='D')
pr_m
```




    PeriodIndex(['2020-01-01', '2020-01-02', '2020-01-03'], dtype='period[D]', freq='D')




```python
# 1시간 길이

pr_h = pd.period_range(start='2020-01-01', end=None, periods=3, freq='H')
pr_h
```




    PeriodIndex(['2020-01-01 00:00', '2020-01-01 01:00', '2020-01-01 02:00'], dtype='period[H]', freq='H')




```python
# 2시간 길이

pr_2h = pd.period_range(start='2020-01-01', end=None, periods=3, freq='2H')
pr_2h
```




    PeriodIndex(['2020-01-01 00:00', '2020-01-01 02:00', '2020-01-01 04:00'], dtype='period[2H]', freq='2H')



# 시계열데이터 활용

-----

## 날짜 데이터 분리: dt.year,  dt.month, dt.day


```python
df = pd.read_csv("../data/stock.csv")
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
      <th>Date</th>
      <th>High</th>
      <th>Low</th>
      <th>Open</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Adj Close</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-03-02</td>
      <td>55500</td>
      <td>53600</td>
      <td>54300</td>
      <td>55000</td>
      <td>30403412</td>
      <td>55000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-03-03</td>
      <td>56900</td>
      <td>55100</td>
      <td>56700</td>
      <td>55400</td>
      <td>30330295</td>
      <td>55400</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-03-04</td>
      <td>57600</td>
      <td>54600</td>
      <td>54800</td>
      <td>57400</td>
      <td>24765728</td>
      <td>57400</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-03-05</td>
      <td>58000</td>
      <td>56700</td>
      <td>57600</td>
      <td>57800</td>
      <td>21698990</td>
      <td>57800</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-03-06</td>
      <td>57200</td>
      <td>56200</td>
      <td>56500</td>
      <td>56500</td>
      <td>18716656</td>
      <td>56500</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>100</th>
      <td>2020-07-24</td>
      <td>54400</td>
      <td>53700</td>
      <td>54000</td>
      <td>54200</td>
      <td>10994535</td>
      <td>54200</td>
    </tr>
    <tr>
      <th>101</th>
      <td>2020-07-27</td>
      <td>55700</td>
      <td>54300</td>
      <td>54300</td>
      <td>55600</td>
      <td>21054421</td>
      <td>55600</td>
    </tr>
    <tr>
      <th>102</th>
      <td>2020-07-28</td>
      <td>58800</td>
      <td>56400</td>
      <td>57000</td>
      <td>58600</td>
      <td>48431566</td>
      <td>58600</td>
    </tr>
    <tr>
      <th>103</th>
      <td>2020-07-29</td>
      <td>60400</td>
      <td>58600</td>
      <td>60300</td>
      <td>59000</td>
      <td>36476611</td>
      <td>59000</td>
    </tr>
    <tr>
      <th>104</th>
      <td>2020-07-30</td>
      <td>60100</td>
      <td>59000</td>
      <td>59700</td>
      <td>59000</td>
      <td>19285354</td>
      <td>59000</td>
    </tr>
  </tbody>
</table>
<p>105 rows × 7 columns</p>
</div>



datetime 타입에 적용하는 `dt`접근자를 활용해 연(year), 월(month), 일(day)을 추출해봅시다.


```python
df['Date'] = pd.to_datetime(df['Date'])
```


```python
df['year'] = df['Date'].dt.year
df['month'] = df['Date'].dt.month
df['day'] = df['Date'].dt.day

df.head()
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
      <th>Date</th>
      <th>High</th>
      <th>Low</th>
      <th>Open</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Adj Close</th>
      <th>year</th>
      <th>month</th>
      <th>day</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-03-02</td>
      <td>55500</td>
      <td>53600</td>
      <td>54300</td>
      <td>55000</td>
      <td>30403412</td>
      <td>55000</td>
      <td>2020</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-03-03</td>
      <td>56900</td>
      <td>55100</td>
      <td>56700</td>
      <td>55400</td>
      <td>30330295</td>
      <td>55400</td>
      <td>2020</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-03-04</td>
      <td>57600</td>
      <td>54600</td>
      <td>54800</td>
      <td>57400</td>
      <td>24765728</td>
      <td>57400</td>
      <td>2020</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-03-05</td>
      <td>58000</td>
      <td>56700</td>
      <td>57600</td>
      <td>57800</td>
      <td>21698990</td>
      <td>57800</td>
      <td>2020</td>
      <td>3</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-03-06</td>
      <td>57200</td>
      <td>56200</td>
      <td>56500</td>
      <td>56500</td>
      <td>18716656</td>
      <td>56500</td>
      <td>2020</td>
      <td>3</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>



여기서 주의할 점은 dt 접근자를 사용하기 위해선 Date 컬럼을 to_datetime 함수를 이용해 시계열 타입으로 변환해야합니다.

## 날짜 인덱스 활용

----

시계열 타입의 컬럼을 인덱스로 활용하는 방법을 알아보겠습니다.


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
      <th>Date</th>
      <th>High</th>
      <th>Low</th>
      <th>Open</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Adj Close</th>
      <th>year</th>
      <th>month</th>
      <th>day</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-03-02</td>
      <td>55500</td>
      <td>53600</td>
      <td>54300</td>
      <td>55000</td>
      <td>30403412</td>
      <td>55000</td>
      <td>2020</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-03-03</td>
      <td>56900</td>
      <td>55100</td>
      <td>56700</td>
      <td>55400</td>
      <td>30330295</td>
      <td>55400</td>
      <td>2020</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-03-04</td>
      <td>57600</td>
      <td>54600</td>
      <td>54800</td>
      <td>57400</td>
      <td>24765728</td>
      <td>57400</td>
      <td>2020</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-03-05</td>
      <td>58000</td>
      <td>56700</td>
      <td>57600</td>
      <td>57800</td>
      <td>21698990</td>
      <td>57800</td>
      <td>2020</td>
      <td>3</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-03-06</td>
      <td>57200</td>
      <td>56200</td>
      <td>56500</td>
      <td>56500</td>
      <td>18716656</td>
      <td>56500</td>
      <td>2020</td>
      <td>3</td>
      <td>6</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>100</th>
      <td>2020-07-24</td>
      <td>54400</td>
      <td>53700</td>
      <td>54000</td>
      <td>54200</td>
      <td>10994535</td>
      <td>54200</td>
      <td>2020</td>
      <td>7</td>
      <td>24</td>
    </tr>
    <tr>
      <th>101</th>
      <td>2020-07-27</td>
      <td>55700</td>
      <td>54300</td>
      <td>54300</td>
      <td>55600</td>
      <td>21054421</td>
      <td>55600</td>
      <td>2020</td>
      <td>7</td>
      <td>27</td>
    </tr>
    <tr>
      <th>102</th>
      <td>2020-07-28</td>
      <td>58800</td>
      <td>56400</td>
      <td>57000</td>
      <td>58600</td>
      <td>48431566</td>
      <td>58600</td>
      <td>2020</td>
      <td>7</td>
      <td>28</td>
    </tr>
    <tr>
      <th>103</th>
      <td>2020-07-29</td>
      <td>60400</td>
      <td>58600</td>
      <td>60300</td>
      <td>59000</td>
      <td>36476611</td>
      <td>59000</td>
      <td>2020</td>
      <td>7</td>
      <td>29</td>
    </tr>
    <tr>
      <th>104</th>
      <td>2020-07-30</td>
      <td>60100</td>
      <td>59000</td>
      <td>59700</td>
      <td>59000</td>
      <td>19285354</td>
      <td>59000</td>
      <td>2020</td>
      <td>7</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
<p>105 rows × 10 columns</p>
</div>




```python
df.set_index(df['Date'], inplace=True)
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
      <th>Date</th>
      <th>High</th>
      <th>Low</th>
      <th>Open</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Adj Close</th>
      <th>year</th>
      <th>month</th>
      <th>day</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-03-02</th>
      <td>2020-03-02</td>
      <td>55500</td>
      <td>53600</td>
      <td>54300</td>
      <td>55000</td>
      <td>30403412</td>
      <td>55000</td>
      <td>2020</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2020-03-03</th>
      <td>2020-03-03</td>
      <td>56900</td>
      <td>55100</td>
      <td>56700</td>
      <td>55400</td>
      <td>30330295</td>
      <td>55400</td>
      <td>2020</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2020-03-04</th>
      <td>2020-03-04</td>
      <td>57600</td>
      <td>54600</td>
      <td>54800</td>
      <td>57400</td>
      <td>24765728</td>
      <td>57400</td>
      <td>2020</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2020-03-05</th>
      <td>2020-03-05</td>
      <td>58000</td>
      <td>56700</td>
      <td>57600</td>
      <td>57800</td>
      <td>21698990</td>
      <td>57800</td>
      <td>2020</td>
      <td>3</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2020-03-06</th>
      <td>2020-03-06</td>
      <td>57200</td>
      <td>56200</td>
      <td>56500</td>
      <td>56500</td>
      <td>18716656</td>
      <td>56500</td>
      <td>2020</td>
      <td>3</td>
      <td>6</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2020-07-24</th>
      <td>2020-07-24</td>
      <td>54400</td>
      <td>53700</td>
      <td>54000</td>
      <td>54200</td>
      <td>10994535</td>
      <td>54200</td>
      <td>2020</td>
      <td>7</td>
      <td>24</td>
    </tr>
    <tr>
      <th>2020-07-27</th>
      <td>2020-07-27</td>
      <td>55700</td>
      <td>54300</td>
      <td>54300</td>
      <td>55600</td>
      <td>21054421</td>
      <td>55600</td>
      <td>2020</td>
      <td>7</td>
      <td>27</td>
    </tr>
    <tr>
      <th>2020-07-28</th>
      <td>2020-07-28</td>
      <td>58800</td>
      <td>56400</td>
      <td>57000</td>
      <td>58600</td>
      <td>48431566</td>
      <td>58600</td>
      <td>2020</td>
      <td>7</td>
      <td>28</td>
    </tr>
    <tr>
      <th>2020-07-29</th>
      <td>2020-07-29</td>
      <td>60400</td>
      <td>58600</td>
      <td>60300</td>
      <td>59000</td>
      <td>36476611</td>
      <td>59000</td>
      <td>2020</td>
      <td>7</td>
      <td>29</td>
    </tr>
    <tr>
      <th>2020-07-30</th>
      <td>2020-07-30</td>
      <td>60100</td>
      <td>59000</td>
      <td>59700</td>
      <td>59000</td>
      <td>19285354</td>
      <td>59000</td>
      <td>2020</td>
      <td>7</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
<p>105 rows × 10 columns</p>
</div>



시계열 타입이 인덱스인 경우에는 꼭 인덱스 이름과 같지 않아도 특정 연도, 연월, 연월일등과 같이 인덱싱이 가능하다는 특징이 있습니다.


```python
df.loc['2020-03'].head() # 3월 인덱싱
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
      <th>Date</th>
      <th>High</th>
      <th>Low</th>
      <th>Open</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Adj Close</th>
      <th>year</th>
      <th>month</th>
      <th>day</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-03-02</th>
      <td>2020-03-02</td>
      <td>55500</td>
      <td>53600</td>
      <td>54300</td>
      <td>55000</td>
      <td>30403412</td>
      <td>55000</td>
      <td>2020</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2020-03-03</th>
      <td>2020-03-03</td>
      <td>56900</td>
      <td>55100</td>
      <td>56700</td>
      <td>55400</td>
      <td>30330295</td>
      <td>55400</td>
      <td>2020</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2020-03-04</th>
      <td>2020-03-04</td>
      <td>57600</td>
      <td>54600</td>
      <td>54800</td>
      <td>57400</td>
      <td>24765728</td>
      <td>57400</td>
      <td>2020</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2020-03-05</th>
      <td>2020-03-05</td>
      <td>58000</td>
      <td>56700</td>
      <td>57600</td>
      <td>57800</td>
      <td>21698990</td>
      <td>57800</td>
      <td>2020</td>
      <td>3</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2020-03-06</th>
      <td>2020-03-06</td>
      <td>57200</td>
      <td>56200</td>
      <td>56500</td>
      <td>56500</td>
      <td>18716656</td>
      <td>56500</td>
      <td>2020</td>
      <td>3</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['2020-05'].head() # 5월 인덱싱
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
      <th>Date</th>
      <th>High</th>
      <th>Low</th>
      <th>Open</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Adj Close</th>
      <th>year</th>
      <th>month</th>
      <th>day</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-05-04</th>
      <td>2020-05-04</td>
      <td>49100</td>
      <td>48500</td>
      <td>48900</td>
      <td>48500</td>
      <td>26083749</td>
      <td>48500</td>
      <td>2020</td>
      <td>5</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2020-05-06</th>
      <td>2020-05-06</td>
      <td>49200</td>
      <td>48500</td>
      <td>49000</td>
      <td>49200</td>
      <td>18070225</td>
      <td>49200</td>
      <td>2020</td>
      <td>5</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2020-05-07</th>
      <td>2020-05-07</td>
      <td>49300</td>
      <td>48700</td>
      <td>49200</td>
      <td>48800</td>
      <td>13884411</td>
      <td>48800</td>
      <td>2020</td>
      <td>5</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2020-05-08</th>
      <td>2020-05-08</td>
      <td>49350</td>
      <td>48800</td>
      <td>49100</td>
      <td>48800</td>
      <td>15319700</td>
      <td>48800</td>
      <td>2020</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2020-05-11</th>
      <td>2020-05-11</td>
      <td>49250</td>
      <td>48300</td>
      <td>48900</td>
      <td>48400</td>
      <td>16357743</td>
      <td>48400</td>
      <td>2020</td>
      <td>5</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['2020-03':'2020-03-10'] # 특정기간 슬라이싱
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
      <th>Date</th>
      <th>High</th>
      <th>Low</th>
      <th>Open</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Adj Close</th>
      <th>year</th>
      <th>month</th>
      <th>day</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-03-02</th>
      <td>2020-03-02</td>
      <td>55500</td>
      <td>53600</td>
      <td>54300</td>
      <td>55000</td>
      <td>30403412</td>
      <td>55000</td>
      <td>2020</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2020-03-03</th>
      <td>2020-03-03</td>
      <td>56900</td>
      <td>55100</td>
      <td>56700</td>
      <td>55400</td>
      <td>30330295</td>
      <td>55400</td>
      <td>2020</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2020-03-04</th>
      <td>2020-03-04</td>
      <td>57600</td>
      <td>54600</td>
      <td>54800</td>
      <td>57400</td>
      <td>24765728</td>
      <td>57400</td>
      <td>2020</td>
      <td>3</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2020-03-05</th>
      <td>2020-03-05</td>
      <td>58000</td>
      <td>56700</td>
      <td>57600</td>
      <td>57800</td>
      <td>21698990</td>
      <td>57800</td>
      <td>2020</td>
      <td>3</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2020-03-06</th>
      <td>2020-03-06</td>
      <td>57200</td>
      <td>56200</td>
      <td>56500</td>
      <td>56500</td>
      <td>18716656</td>
      <td>56500</td>
      <td>2020</td>
      <td>3</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2020-03-09</th>
      <td>2020-03-09</td>
      <td>56500</td>
      <td>56500</td>
      <td>56500</td>
      <td>56500</td>
      <td>0</td>
      <td>56500</td>
      <td>2020</td>
      <td>3</td>
      <td>9</td>
    </tr>
    <tr>
      <th>2020-03-10</th>
      <td>2020-03-10</td>
      <td>54900</td>
      <td>53700</td>
      <td>53800</td>
      <td>54600</td>
      <td>32106554</td>
      <td>54600</td>
      <td>2020</td>
      <td>3</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>



## 현재 날짜와 차이 컬럼 생성

----

현재날짜를 구해 경과일이라는 컬럼을 만들어봅시다.

현재 날짜를 구하는 함수로는 `datetime의 now와 today`가 있습니다.


```python
pd.datetime.now()
```

    C:\ProgramData\Anaconda3\lib\site-packages\ipykernel_launcher.py:1: FutureWarning: The pandas.datetime class is deprecated and will be removed from pandas in a future version. Import from datetime module instead.
      """Entry point for launching an IPython kernel.
    




    datetime.datetime(2021, 4, 1, 0, 35, 48, 403428)




```python
pd.datetime.today()
```

    C:\ProgramData\Anaconda3\lib\site-packages\ipykernel_launcher.py:1: FutureWarning: The pandas.datetime class is deprecated and will be removed from pandas in a future version. Import from datetime module instead.
      """Entry point for launching an IPython kernel.
    




    datetime.datetime(2021, 4, 1, 0, 35, 56, 847646)




```python
today = pd.datetime.now()

df['Elapsed_days'] = today - df.index
```

    C:\ProgramData\Anaconda3\lib\site-packages\ipykernel_launcher.py:1: FutureWarning: The pandas.datetime class is deprecated and will be removed from pandas in a future version. Import from datetime module instead.
      """Entry point for launching an IPython kernel.
    


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
      <th>Date</th>
      <th>High</th>
      <th>Low</th>
      <th>Open</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Adj Close</th>
      <th>year</th>
      <th>month</th>
      <th>day</th>
      <th>Elapsed_days</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-03-02</th>
      <td>2020-03-02</td>
      <td>55500</td>
      <td>53600</td>
      <td>54300</td>
      <td>55000</td>
      <td>30403412</td>
      <td>55000</td>
      <td>2020</td>
      <td>3</td>
      <td>2</td>
      <td>395 days 00:58:31.733470</td>
    </tr>
    <tr>
      <th>2020-03-03</th>
      <td>2020-03-03</td>
      <td>56900</td>
      <td>55100</td>
      <td>56700</td>
      <td>55400</td>
      <td>30330295</td>
      <td>55400</td>
      <td>2020</td>
      <td>3</td>
      <td>3</td>
      <td>394 days 00:58:31.733470</td>
    </tr>
    <tr>
      <th>2020-03-04</th>
      <td>2020-03-04</td>
      <td>57600</td>
      <td>54600</td>
      <td>54800</td>
      <td>57400</td>
      <td>24765728</td>
      <td>57400</td>
      <td>2020</td>
      <td>3</td>
      <td>4</td>
      <td>393 days 00:58:31.733470</td>
    </tr>
    <tr>
      <th>2020-03-05</th>
      <td>2020-03-05</td>
      <td>58000</td>
      <td>56700</td>
      <td>57600</td>
      <td>57800</td>
      <td>21698990</td>
      <td>57800</td>
      <td>2020</td>
      <td>3</td>
      <td>5</td>
      <td>392 days 00:58:31.733470</td>
    </tr>
    <tr>
      <th>2020-03-06</th>
      <td>2020-03-06</td>
      <td>57200</td>
      <td>56200</td>
      <td>56500</td>
      <td>56500</td>
      <td>18716656</td>
      <td>56500</td>
      <td>2020</td>
      <td>3</td>
      <td>6</td>
      <td>391 days 00:58:31.733470</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2020-07-24</th>
      <td>2020-07-24</td>
      <td>54400</td>
      <td>53700</td>
      <td>54000</td>
      <td>54200</td>
      <td>10994535</td>
      <td>54200</td>
      <td>2020</td>
      <td>7</td>
      <td>24</td>
      <td>251 days 00:58:31.733470</td>
    </tr>
    <tr>
      <th>2020-07-27</th>
      <td>2020-07-27</td>
      <td>55700</td>
      <td>54300</td>
      <td>54300</td>
      <td>55600</td>
      <td>21054421</td>
      <td>55600</td>
      <td>2020</td>
      <td>7</td>
      <td>27</td>
      <td>248 days 00:58:31.733470</td>
    </tr>
    <tr>
      <th>2020-07-28</th>
      <td>2020-07-28</td>
      <td>58800</td>
      <td>56400</td>
      <td>57000</td>
      <td>58600</td>
      <td>48431566</td>
      <td>58600</td>
      <td>2020</td>
      <td>7</td>
      <td>28</td>
      <td>247 days 00:58:31.733470</td>
    </tr>
    <tr>
      <th>2020-07-29</th>
      <td>2020-07-29</td>
      <td>60400</td>
      <td>58600</td>
      <td>60300</td>
      <td>59000</td>
      <td>36476611</td>
      <td>59000</td>
      <td>2020</td>
      <td>7</td>
      <td>29</td>
      <td>246 days 00:58:31.733470</td>
    </tr>
    <tr>
      <th>2020-07-30</th>
      <td>2020-07-30</td>
      <td>60100</td>
      <td>59000</td>
      <td>59700</td>
      <td>59000</td>
      <td>19285354</td>
      <td>59000</td>
      <td>2020</td>
      <td>7</td>
      <td>30</td>
      <td>245 days 00:58:31.733470</td>
    </tr>
  </tbody>
</table>
<p>105 rows × 11 columns</p>
</div>



차잇값을 보면 자동으로 days까지 붙어서 표기되는 것을 알 수 있다.


```python
df['Elapsed_days'] = df['Elapsed_days'].astype(str)
```


```python
df['Elapsed_days'] = df['Elapsed_days'].str.split('00')
```

str.get() 함수는 split된 개별원소를 갖는 시리즈 객체에 인덱싱이 가능하도록 합니다.


```python
df['Elapsed_days'] = df['Elapsed_days'].str.get(0) 
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
      <th>Date</th>
      <th>High</th>
      <th>Low</th>
      <th>Open</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Adj Close</th>
      <th>year</th>
      <th>month</th>
      <th>day</th>
      <th>Elapsed_days</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-03-02</th>
      <td>2020-03-02</td>
      <td>55500</td>
      <td>53600</td>
      <td>54300</td>
      <td>55000</td>
      <td>30403412</td>
      <td>55000</td>
      <td>2020</td>
      <td>3</td>
      <td>2</td>
      <td>395 days</td>
    </tr>
    <tr>
      <th>2020-03-03</th>
      <td>2020-03-03</td>
      <td>56900</td>
      <td>55100</td>
      <td>56700</td>
      <td>55400</td>
      <td>30330295</td>
      <td>55400</td>
      <td>2020</td>
      <td>3</td>
      <td>3</td>
      <td>394 days</td>
    </tr>
    <tr>
      <th>2020-03-04</th>
      <td>2020-03-04</td>
      <td>57600</td>
      <td>54600</td>
      <td>54800</td>
      <td>57400</td>
      <td>24765728</td>
      <td>57400</td>
      <td>2020</td>
      <td>3</td>
      <td>4</td>
      <td>393 days</td>
    </tr>
    <tr>
      <th>2020-03-05</th>
      <td>2020-03-05</td>
      <td>58000</td>
      <td>56700</td>
      <td>57600</td>
      <td>57800</td>
      <td>21698990</td>
      <td>57800</td>
      <td>2020</td>
      <td>3</td>
      <td>5</td>
      <td>392 days</td>
    </tr>
    <tr>
      <th>2020-03-06</th>
      <td>2020-03-06</td>
      <td>57200</td>
      <td>56200</td>
      <td>56500</td>
      <td>56500</td>
      <td>18716656</td>
      <td>56500</td>
      <td>2020</td>
      <td>3</td>
      <td>6</td>
      <td>391 days</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2020-07-24</th>
      <td>2020-07-24</td>
      <td>54400</td>
      <td>53700</td>
      <td>54000</td>
      <td>54200</td>
      <td>10994535</td>
      <td>54200</td>
      <td>2020</td>
      <td>7</td>
      <td>24</td>
      <td>251 days</td>
    </tr>
    <tr>
      <th>2020-07-27</th>
      <td>2020-07-27</td>
      <td>55700</td>
      <td>54300</td>
      <td>54300</td>
      <td>55600</td>
      <td>21054421</td>
      <td>55600</td>
      <td>2020</td>
      <td>7</td>
      <td>27</td>
      <td>248 days</td>
    </tr>
    <tr>
      <th>2020-07-28</th>
      <td>2020-07-28</td>
      <td>58800</td>
      <td>56400</td>
      <td>57000</td>
      <td>58600</td>
      <td>48431566</td>
      <td>58600</td>
      <td>2020</td>
      <td>7</td>
      <td>28</td>
      <td>247 days</td>
    </tr>
    <tr>
      <th>2020-07-29</th>
      <td>2020-07-29</td>
      <td>60400</td>
      <td>58600</td>
      <td>60300</td>
      <td>59000</td>
      <td>36476611</td>
      <td>59000</td>
      <td>2020</td>
      <td>7</td>
      <td>29</td>
      <td>246 days</td>
    </tr>
    <tr>
      <th>2020-07-30</th>
      <td>2020-07-30</td>
      <td>60100</td>
      <td>59000</td>
      <td>59700</td>
      <td>59000</td>
      <td>19285354</td>
      <td>59000</td>
      <td>2020</td>
      <td>7</td>
      <td>30</td>
      <td>245 days</td>
    </tr>
  </tbody>
</table>
<p>105 rows × 11 columns</p>
</div>




```python

```
