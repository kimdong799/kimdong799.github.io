{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# 시계열 데이터"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "-----"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "판다스에서 시계열 자료형은 Timestamp와 Period 두가지 타입이 있습니다."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "- Timestamp 자료형은 `to_datetime()`함수로 생성가능하며 날짜형태의 자료형을 시계열 타입으로 변환합니다."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "- period 자료형은 Timestamp(datetime)객체를 다시 기간에 따른 자료형으로 이용하고자 할때 사용합니다."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# 2. 자료형의 시계열 객체 변환 : to_datetime(), to_period()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "먼저 시계열 데이터의 대표주자인 주식 데이터를 로드합니다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T14:52:56.036174Z",
     "start_time": "2021-03-31T14:52:55.984314Z"
    }
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Open</th>\n",
       "      <th>Close</th>\n",
       "      <th>Volume</th>\n",
       "      <th>Adj Close</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2020-03-02</td>\n",
       "      <td>55500</td>\n",
       "      <td>53600</td>\n",
       "      <td>54300</td>\n",
       "      <td>55000</td>\n",
       "      <td>30403412</td>\n",
       "      <td>55000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2020-03-03</td>\n",
       "      <td>56900</td>\n",
       "      <td>55100</td>\n",
       "      <td>56700</td>\n",
       "      <td>55400</td>\n",
       "      <td>30330295</td>\n",
       "      <td>55400</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2020-03-04</td>\n",
       "      <td>57600</td>\n",
       "      <td>54600</td>\n",
       "      <td>54800</td>\n",
       "      <td>57400</td>\n",
       "      <td>24765728</td>\n",
       "      <td>57400</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2020-03-05</td>\n",
       "      <td>58000</td>\n",
       "      <td>56700</td>\n",
       "      <td>57600</td>\n",
       "      <td>57800</td>\n",
       "      <td>21698990</td>\n",
       "      <td>57800</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2020-03-06</td>\n",
       "      <td>57200</td>\n",
       "      <td>56200</td>\n",
       "      <td>56500</td>\n",
       "      <td>56500</td>\n",
       "      <td>18716656</td>\n",
       "      <td>56500</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "         Date   High    Low   Open  Close    Volume  Adj Close\n",
       "0  2020-03-02  55500  53600  54300  55000  30403412      55000\n",
       "1  2020-03-03  56900  55100  56700  55400  30330295      55400\n",
       "2  2020-03-04  57600  54600  54800  57400  24765728      57400\n",
       "3  2020-03-05  58000  56700  57600  57800  21698990      57800\n",
       "4  2020-03-06  57200  56200  56500  56500  18716656      56500"
      ]
     },
     "execution_count": 2,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "import pandas as pd\n",
    "\n",
    "df = pd.read_csv('../data/stock.csv')\n",
    "df.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "info 메소드를 통해 데이터 요약정보를 확인해봅시다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T14:53:31.250250Z",
     "start_time": "2021-03-31T14:53:31.224273Z"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 105 entries, 0 to 104\n",
      "Data columns (total 7 columns):\n",
      " #   Column     Non-Null Count  Dtype \n",
      "---  ------     --------------  ----- \n",
      " 0   Date       105 non-null    object\n",
      " 1   High       105 non-null    int64 \n",
      " 2   Low        105 non-null    int64 \n",
      " 3   Open       105 non-null    int64 \n",
      " 4   Close      105 non-null    int64 \n",
      " 5   Volume     105 non-null    int64 \n",
      " 6   Adj Close  105 non-null    int64 \n",
      "dtypes: int64(6), object(1)\n",
      "memory usage: 5.9+ KB\n"
     ]
    }
   ],
   "source": [
    "df.info()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "현재 날짜를 나타내는 Date 컬럼의 Dtype은 object로 문자형임을 알 수 있습니다."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "`to_datetime()` 함수를 이용해서 Date컬럼을 시계열 객체(Timestamp)로 변환해봅시다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T14:55:03.335432Z",
     "start_time": "2021-03-31T14:55:03.306344Z"
    }
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Open</th>\n",
       "      <th>Close</th>\n",
       "      <th>Volume</th>\n",
       "      <th>Adj Close</th>\n",
       "      <th>new_date</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2020-03-02</td>\n",
       "      <td>55500</td>\n",
       "      <td>53600</td>\n",
       "      <td>54300</td>\n",
       "      <td>55000</td>\n",
       "      <td>30403412</td>\n",
       "      <td>55000</td>\n",
       "      <td>2020-03-02</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2020-03-03</td>\n",
       "      <td>56900</td>\n",
       "      <td>55100</td>\n",
       "      <td>56700</td>\n",
       "      <td>55400</td>\n",
       "      <td>30330295</td>\n",
       "      <td>55400</td>\n",
       "      <td>2020-03-03</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2020-03-04</td>\n",
       "      <td>57600</td>\n",
       "      <td>54600</td>\n",
       "      <td>54800</td>\n",
       "      <td>57400</td>\n",
       "      <td>24765728</td>\n",
       "      <td>57400</td>\n",
       "      <td>2020-03-04</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2020-03-05</td>\n",
       "      <td>58000</td>\n",
       "      <td>56700</td>\n",
       "      <td>57600</td>\n",
       "      <td>57800</td>\n",
       "      <td>21698990</td>\n",
       "      <td>57800</td>\n",
       "      <td>2020-03-05</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2020-03-06</td>\n",
       "      <td>57200</td>\n",
       "      <td>56200</td>\n",
       "      <td>56500</td>\n",
       "      <td>56500</td>\n",
       "      <td>18716656</td>\n",
       "      <td>56500</td>\n",
       "      <td>2020-03-06</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "         Date   High    Low   Open  Close    Volume  Adj Close   new_date\n",
       "0  2020-03-02  55500  53600  54300  55000  30403412      55000 2020-03-02\n",
       "1  2020-03-03  56900  55100  56700  55400  30330295      55400 2020-03-03\n",
       "2  2020-03-04  57600  54600  54800  57400  24765728      57400 2020-03-04\n",
       "3  2020-03-05  58000  56700  57600  57800  21698990      57800 2020-03-05\n",
       "4  2020-03-06  57200  56200  56500  56500  18716656      56500 2020-03-06"
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df['new_date'] = pd.to_datetime(df['Date'])\n",
    "df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T14:56:09.271749Z",
     "start_time": "2021-03-31T14:56:09.244822Z"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 105 entries, 0 to 104\n",
      "Data columns (total 8 columns):\n",
      " #   Column     Non-Null Count  Dtype         \n",
      "---  ------     --------------  -----         \n",
      " 0   Date       105 non-null    object        \n",
      " 1   High       105 non-null    int64         \n",
      " 2   Low        105 non-null    int64         \n",
      " 3   Open       105 non-null    int64         \n",
      " 4   Close      105 non-null    int64         \n",
      " 5   Volume     105 non-null    int64         \n",
      " 6   Adj Close  105 non-null    int64         \n",
      " 7   new_date   105 non-null    datetime64[ns]\n",
      "dtypes: datetime64[ns](1), int64(6), object(1)\n",
      "memory usage: 6.7+ KB\n"
     ]
    }
   ],
   "source": [
    "df.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T14:55:59.971876Z",
     "start_time": "2021-03-31T14:55:59.956754Z"
    }
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "pandas._libs.tslibs.timestamps.Timestamp"
      ]
     },
     "execution_count": 11,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "type(df.new_date[0])"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "to_datetime 함수를 이용해 object(문자)형 데이터였던 Date 컬럼을 시계열객체로 변경했습니다.\n",
    "\n",
    "info 메소드의 결과로 new_date 컬럼의 Dtype은 datetime으로 시계열객체가 된 것을 확인할 수 있습니다.\n",
    "\n",
    "마찬가지로 new_date의 첫번째 row의 type을 확인한 결과 timestamp로 나타나는 것을 알 수 있습니다."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T14:58:19.690385Z",
     "start_time": "2021-03-31T14:58:19.682442Z"
    }
   },
   "source": [
    "이제 기존 Date열은 삭제하고 new_date를 인덱스로 지정하겠습니다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T14:59:29.159783Z",
     "start_time": "2021-03-31T14:59:29.149179Z"
    }
   },
   "outputs": [],
   "source": [
    "df.drop('Date', axis=1, inplace=True)\n",
    "df.set_index('new_date', inplace=True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T14:59:33.155510Z",
     "start_time": "2021-03-31T14:59:33.126585Z"
    }
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Open</th>\n",
       "      <th>Close</th>\n",
       "      <th>Volume</th>\n",
       "      <th>Adj Close</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>new_date</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2020-03-02</th>\n",
       "      <td>55500</td>\n",
       "      <td>53600</td>\n",
       "      <td>54300</td>\n",
       "      <td>55000</td>\n",
       "      <td>30403412</td>\n",
       "      <td>55000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-03</th>\n",
       "      <td>56900</td>\n",
       "      <td>55100</td>\n",
       "      <td>56700</td>\n",
       "      <td>55400</td>\n",
       "      <td>30330295</td>\n",
       "      <td>55400</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-04</th>\n",
       "      <td>57600</td>\n",
       "      <td>54600</td>\n",
       "      <td>54800</td>\n",
       "      <td>57400</td>\n",
       "      <td>24765728</td>\n",
       "      <td>57400</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-05</th>\n",
       "      <td>58000</td>\n",
       "      <td>56700</td>\n",
       "      <td>57600</td>\n",
       "      <td>57800</td>\n",
       "      <td>21698990</td>\n",
       "      <td>57800</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-06</th>\n",
       "      <td>57200</td>\n",
       "      <td>56200</td>\n",
       "      <td>56500</td>\n",
       "      <td>56500</td>\n",
       "      <td>18716656</td>\n",
       "      <td>56500</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "             High    Low   Open  Close    Volume  Adj Close\n",
       "new_date                                                   \n",
       "2020-03-02  55500  53600  54300  55000  30403412      55000\n",
       "2020-03-03  56900  55100  56700  55400  30330295      55400\n",
       "2020-03-04  57600  54600  54800  57400  24765728      57400\n",
       "2020-03-05  58000  56700  57600  57800  21698990      57800\n",
       "2020-03-06  57200  56200  56500  56500  18716656      56500"
      ]
     },
     "execution_count": 21,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T14:59:35.875922Z",
     "start_time": "2021-03-31T14:59:35.850718Z"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "DatetimeIndex: 105 entries, 2020-03-02 to 2020-07-30\n",
      "Data columns (total 6 columns):\n",
      " #   Column     Non-Null Count  Dtype\n",
      "---  ------     --------------  -----\n",
      " 0   High       105 non-null    int64\n",
      " 1   Low        105 non-null    int64\n",
      " 2   Open       105 non-null    int64\n",
      " 3   Close      105 non-null    int64\n",
      " 4   Volume     105 non-null    int64\n",
      " 5   Adj Close  105 non-null    int64\n",
      "dtypes: int64(6)\n",
      "memory usage: 5.7 KB\n"
     ]
    }
   ],
   "source": [
    "df.info()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "데이터요약정보에서 인덱스가 `DatetimeIndex`로 나타나는 것을 알 수 있고 2020-03-02부터 2020-07-30으로 나타나는 것을 알 수있습니다."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "이번에는 Timestamp와 Period의 차이를 알아보겠습니다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:07:29.822423Z",
     "start_time": "2021-03-31T15:07:29.800477Z"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "DatetimeIndex(['2021-01-01', '2021-02-01', '2021-03-01'], dtype='datetime64[ns]', freq=None)\n"
     ]
    }
   ],
   "source": [
    "# Timestamp를 Period로 변환\n",
    "\n",
    "dates = ['2021-01-01', '2021-02-01', '2021-03-01']\n",
    "\n",
    "ts_dates = pd.to_datetime(dates)\n",
    "\n",
    "print(ts_dates)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:07:30.054549Z",
     "start_time": "2021-03-31T15:07:30.037595Z"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "PeriodIndex(['2021-01-01', '2021-02-01', '2021-03-01'], dtype='period[D]', freq='D')\n"
     ]
    }
   ],
   "source": [
    "# Timestamp를 Period변환\n",
    "pr_day = ts_dates.to_period(freq='D') # 1일의 기간\n",
    "print(pr_day)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 35,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:07:30.243102Z",
     "start_time": "2021-03-31T15:07:30.223113Z"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "PeriodIndex(['2021-01', '2021-02', '2021-03'], dtype='period[M]', freq='M')\n"
     ]
    }
   ],
   "source": [
    "pr_month = ts_dates.to_period(freq='M') # 1개월의 기간\n",
    "print(pr_month)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 36,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:07:30.414563Z",
     "start_time": "2021-03-31T15:07:30.406584Z"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "PeriodIndex(['2021', '2021', '2021'], dtype='period[A-DEC]', freq='A-DEC')\n"
     ]
    }
   ],
   "source": [
    "pr_year = ts_dates.to_period(freq='A') # 1년의 기간\n",
    "print(pr_year)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "이처럼 Period 객체는 `to_period(freq='기간인수')`를 통해 datetime 변수에 대해 어떤 기간에 따른 자료형을 생성하고자 할 때 사용됩니다.\n",
    "\n",
    "이는 바로 아무 자료형에나 사용할 수 없고 datetime 타입에 대해 적용 가능합니다.\n",
    "\n",
    "아래는 freq에 사용할 수 있는 다양한 기간인수입니다."
   ]
  },
  {
   "attachments": {
    "image.png": {
     "image/png": "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"
    }
   },
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "![image.png](attachment:image.png)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# 시계열 데이터 만들기 : date_range(), period_range()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "---"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Timestamp 배열"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Timestamp를 배열하는 `date_range`함수는 내장함수 range() 함수와 동일한 개념입니다.\n",
    "\n",
    "다음과 같이 옵션을 지정하면 원하는 일정 기간의 Timestamp(datetime)배열을 얻을 수 있습니다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 42,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:16:10.160262Z",
     "start_time": "2021-03-31T15:16:10.135328Z"
    }
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "DatetimeIndex(['2020-01-01 00:00:00+09:00', '2020-01-02 00:00:00+09:00',\n",
      "               '2020-01-03 00:00:00+09:00', '2020-01-06 00:00:00+09:00',\n",
      "               '2020-01-07 00:00:00+09:00', '2020-01-08 00:00:00+09:00',\n",
      "               '2020-01-09 00:00:00+09:00', '2020-01-10 00:00:00+09:00',\n",
      "               '2020-01-13 00:00:00+09:00', '2020-01-14 00:00:00+09:00',\n",
      "               '2020-01-15 00:00:00+09:00', '2020-01-16 00:00:00+09:00',\n",
      "               '2020-01-17 00:00:00+09:00', '2020-01-20 00:00:00+09:00',\n",
      "               '2020-01-21 00:00:00+09:00', '2020-01-22 00:00:00+09:00',\n",
      "               '2020-01-23 00:00:00+09:00', '2020-01-24 00:00:00+09:00',\n",
      "               '2020-01-27 00:00:00+09:00', '2020-01-28 00:00:00+09:00'],\n",
      "              dtype='datetime64[ns, Asia/Seoul]', freq='B')\n"
     ]
    }
   ],
   "source": [
    "ts_ms = pd.date_range(start = '2020-01-01', # 날짜 범위 시작\n",
    "                      end = None,          # 날짜 범위 끝\n",
    "                      periods = 20,        # 생성할 Timestamp 수\n",
    "                      freq ='B',           # 시간 간격 (B: 평일)\n",
    "                      tz = 'Asia/Seoul')   # 시간대(timezone)\n",
    "\n",
    "print(ts_ms)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:15:58.732084Z",
     "start_time": "2021-03-31T15:15:57.508224Z"
    }
   },
   "source": [
    "## Period 배열"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "마찬가지로 Period 배열을 생성해주는 `period_range()` 함수를 알아봅시다."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Timestamp와의 차이점은 Period는 기간을 나타내는 자료형으로 배열을 적용할 때 `freq=` 옵션은 기간의 단위를 의미한다는 점입니다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 46,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:22:24.941876Z",
     "start_time": "2021-03-31T15:22:24.928859Z"
    }
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "PeriodIndex(['2020-01-01', '2020-01-02', '2020-01-03'], dtype='period[D]', freq='D')"
      ]
     },
     "execution_count": 46,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 1개월 길이\n",
    "\n",
    "pr_m = pd.period_range(start='2020-01-01', end=None, periods=3, freq='D')\n",
    "pr_m"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 48,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:23:47.021887Z",
     "start_time": "2021-03-31T15:23:47.001942Z"
    }
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "PeriodIndex(['2020-01-01 00:00', '2020-01-01 01:00', '2020-01-01 02:00'], dtype='period[H]', freq='H')"
      ]
     },
     "execution_count": 48,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 1시간 길이\n",
    "\n",
    "pr_h = pd.period_range(start='2020-01-01', end=None, periods=3, freq='H')\n",
    "pr_h"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 50,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:24:30.368198Z",
     "start_time": "2021-03-31T15:24:30.350981Z"
    }
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "PeriodIndex(['2020-01-01 00:00', '2020-01-01 02:00', '2020-01-01 04:00'], dtype='period[2H]', freq='2H')"
      ]
     },
     "execution_count": 50,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# 2시간 길이\n",
    "\n",
    "pr_2h = pd.period_range(start='2020-01-01', end=None, periods=3, freq='2H')\n",
    "pr_2h"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# 시계열데이터 활용"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "-----"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 날짜 데이터 분리: dt.year,  dt.month, dt.day"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 54,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:26:05.247910Z",
     "start_time": "2021-03-31T15:26:05.209050Z"
    }
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Open</th>\n",
       "      <th>Close</th>\n",
       "      <th>Volume</th>\n",
       "      <th>Adj Close</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2020-03-02</td>\n",
       "      <td>55500</td>\n",
       "      <td>53600</td>\n",
       "      <td>54300</td>\n",
       "      <td>55000</td>\n",
       "      <td>30403412</td>\n",
       "      <td>55000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2020-03-03</td>\n",
       "      <td>56900</td>\n",
       "      <td>55100</td>\n",
       "      <td>56700</td>\n",
       "      <td>55400</td>\n",
       "      <td>30330295</td>\n",
       "      <td>55400</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2020-03-04</td>\n",
       "      <td>57600</td>\n",
       "      <td>54600</td>\n",
       "      <td>54800</td>\n",
       "      <td>57400</td>\n",
       "      <td>24765728</td>\n",
       "      <td>57400</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2020-03-05</td>\n",
       "      <td>58000</td>\n",
       "      <td>56700</td>\n",
       "      <td>57600</td>\n",
       "      <td>57800</td>\n",
       "      <td>21698990</td>\n",
       "      <td>57800</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2020-03-06</td>\n",
       "      <td>57200</td>\n",
       "      <td>56200</td>\n",
       "      <td>56500</td>\n",
       "      <td>56500</td>\n",
       "      <td>18716656</td>\n",
       "      <td>56500</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>100</th>\n",
       "      <td>2020-07-24</td>\n",
       "      <td>54400</td>\n",
       "      <td>53700</td>\n",
       "      <td>54000</td>\n",
       "      <td>54200</td>\n",
       "      <td>10994535</td>\n",
       "      <td>54200</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>101</th>\n",
       "      <td>2020-07-27</td>\n",
       "      <td>55700</td>\n",
       "      <td>54300</td>\n",
       "      <td>54300</td>\n",
       "      <td>55600</td>\n",
       "      <td>21054421</td>\n",
       "      <td>55600</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>102</th>\n",
       "      <td>2020-07-28</td>\n",
       "      <td>58800</td>\n",
       "      <td>56400</td>\n",
       "      <td>57000</td>\n",
       "      <td>58600</td>\n",
       "      <td>48431566</td>\n",
       "      <td>58600</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>103</th>\n",
       "      <td>2020-07-29</td>\n",
       "      <td>60400</td>\n",
       "      <td>58600</td>\n",
       "      <td>60300</td>\n",
       "      <td>59000</td>\n",
       "      <td>36476611</td>\n",
       "      <td>59000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>104</th>\n",
       "      <td>2020-07-30</td>\n",
       "      <td>60100</td>\n",
       "      <td>59000</td>\n",
       "      <td>59700</td>\n",
       "      <td>59000</td>\n",
       "      <td>19285354</td>\n",
       "      <td>59000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>105 rows × 7 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "           Date   High    Low   Open  Close    Volume  Adj Close\n",
       "0    2020-03-02  55500  53600  54300  55000  30403412      55000\n",
       "1    2020-03-03  56900  55100  56700  55400  30330295      55400\n",
       "2    2020-03-04  57600  54600  54800  57400  24765728      57400\n",
       "3    2020-03-05  58000  56700  57600  57800  21698990      57800\n",
       "4    2020-03-06  57200  56200  56500  56500  18716656      56500\n",
       "..          ...    ...    ...    ...    ...       ...        ...\n",
       "100  2020-07-24  54400  53700  54000  54200  10994535      54200\n",
       "101  2020-07-27  55700  54300  54300  55600  21054421      55600\n",
       "102  2020-07-28  58800  56400  57000  58600  48431566      58600\n",
       "103  2020-07-29  60400  58600  60300  59000  36476611      59000\n",
       "104  2020-07-30  60100  59000  59700  59000  19285354      59000\n",
       "\n",
       "[105 rows x 7 columns]"
      ]
     },
     "execution_count": 54,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df = pd.read_csv(\"../data/stock.csv\")\n",
    "df"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "datetime 타입에 적용하는 `dt`접근자를 활용해 연(year), 월(month), 일(day)을 추출해봅시다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 61,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:28:55.783477Z",
     "start_time": "2021-03-31T15:28:55.772509Z"
    }
   },
   "outputs": [],
   "source": [
    "df['Date'] = pd.to_datetime(df['Date'])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 62,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:28:56.806963Z",
     "start_time": "2021-03-31T15:28:56.769029Z"
    }
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Open</th>\n",
       "      <th>Close</th>\n",
       "      <th>Volume</th>\n",
       "      <th>Adj Close</th>\n",
       "      <th>year</th>\n",
       "      <th>month</th>\n",
       "      <th>day</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2020-03-02</td>\n",
       "      <td>55500</td>\n",
       "      <td>53600</td>\n",
       "      <td>54300</td>\n",
       "      <td>55000</td>\n",
       "      <td>30403412</td>\n",
       "      <td>55000</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>2</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2020-03-03</td>\n",
       "      <td>56900</td>\n",
       "      <td>55100</td>\n",
       "      <td>56700</td>\n",
       "      <td>55400</td>\n",
       "      <td>30330295</td>\n",
       "      <td>55400</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>3</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2020-03-04</td>\n",
       "      <td>57600</td>\n",
       "      <td>54600</td>\n",
       "      <td>54800</td>\n",
       "      <td>57400</td>\n",
       "      <td>24765728</td>\n",
       "      <td>57400</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>4</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2020-03-05</td>\n",
       "      <td>58000</td>\n",
       "      <td>56700</td>\n",
       "      <td>57600</td>\n",
       "      <td>57800</td>\n",
       "      <td>21698990</td>\n",
       "      <td>57800</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>5</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2020-03-06</td>\n",
       "      <td>57200</td>\n",
       "      <td>56200</td>\n",
       "      <td>56500</td>\n",
       "      <td>56500</td>\n",
       "      <td>18716656</td>\n",
       "      <td>56500</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>6</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "        Date   High    Low   Open  Close    Volume  Adj Close  year  month  \\\n",
       "0 2020-03-02  55500  53600  54300  55000  30403412      55000  2020      3   \n",
       "1 2020-03-03  56900  55100  56700  55400  30330295      55400  2020      3   \n",
       "2 2020-03-04  57600  54600  54800  57400  24765728      57400  2020      3   \n",
       "3 2020-03-05  58000  56700  57600  57800  21698990      57800  2020      3   \n",
       "4 2020-03-06  57200  56200  56500  56500  18716656      56500  2020      3   \n",
       "\n",
       "   day  \n",
       "0    2  \n",
       "1    3  \n",
       "2    4  \n",
       "3    5  \n",
       "4    6  "
      ]
     },
     "execution_count": 62,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df['year'] = df['Date'].dt.year\n",
    "df['month'] = df['Date'].dt.month\n",
    "df['day'] = df['Date'].dt.day\n",
    "\n",
    "df.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "여기서 주의할 점은 dt 접근자를 사용하기 위해선 Date 컬럼을 to_datetime 함수를 이용해 시계열 타입으로 변환해야합니다."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 날짜 인덱스 활용"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "----"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "시계열 타입의 컬럼을 인덱스로 활용하는 방법을 알아보겠습니다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 63,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:32:30.054089Z",
     "start_time": "2021-03-31T15:32:30.024173Z"
    }
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Open</th>\n",
       "      <th>Close</th>\n",
       "      <th>Volume</th>\n",
       "      <th>Adj Close</th>\n",
       "      <th>year</th>\n",
       "      <th>month</th>\n",
       "      <th>day</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2020-03-02</td>\n",
       "      <td>55500</td>\n",
       "      <td>53600</td>\n",
       "      <td>54300</td>\n",
       "      <td>55000</td>\n",
       "      <td>30403412</td>\n",
       "      <td>55000</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>2</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2020-03-03</td>\n",
       "      <td>56900</td>\n",
       "      <td>55100</td>\n",
       "      <td>56700</td>\n",
       "      <td>55400</td>\n",
       "      <td>30330295</td>\n",
       "      <td>55400</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>3</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2020-03-04</td>\n",
       "      <td>57600</td>\n",
       "      <td>54600</td>\n",
       "      <td>54800</td>\n",
       "      <td>57400</td>\n",
       "      <td>24765728</td>\n",
       "      <td>57400</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>4</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2020-03-05</td>\n",
       "      <td>58000</td>\n",
       "      <td>56700</td>\n",
       "      <td>57600</td>\n",
       "      <td>57800</td>\n",
       "      <td>21698990</td>\n",
       "      <td>57800</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>5</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2020-03-06</td>\n",
       "      <td>57200</td>\n",
       "      <td>56200</td>\n",
       "      <td>56500</td>\n",
       "      <td>56500</td>\n",
       "      <td>18716656</td>\n",
       "      <td>56500</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>6</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>100</th>\n",
       "      <td>2020-07-24</td>\n",
       "      <td>54400</td>\n",
       "      <td>53700</td>\n",
       "      <td>54000</td>\n",
       "      <td>54200</td>\n",
       "      <td>10994535</td>\n",
       "      <td>54200</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>24</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>101</th>\n",
       "      <td>2020-07-27</td>\n",
       "      <td>55700</td>\n",
       "      <td>54300</td>\n",
       "      <td>54300</td>\n",
       "      <td>55600</td>\n",
       "      <td>21054421</td>\n",
       "      <td>55600</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>27</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>102</th>\n",
       "      <td>2020-07-28</td>\n",
       "      <td>58800</td>\n",
       "      <td>56400</td>\n",
       "      <td>57000</td>\n",
       "      <td>58600</td>\n",
       "      <td>48431566</td>\n",
       "      <td>58600</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>28</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>103</th>\n",
       "      <td>2020-07-29</td>\n",
       "      <td>60400</td>\n",
       "      <td>58600</td>\n",
       "      <td>60300</td>\n",
       "      <td>59000</td>\n",
       "      <td>36476611</td>\n",
       "      <td>59000</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>29</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>104</th>\n",
       "      <td>2020-07-30</td>\n",
       "      <td>60100</td>\n",
       "      <td>59000</td>\n",
       "      <td>59700</td>\n",
       "      <td>59000</td>\n",
       "      <td>19285354</td>\n",
       "      <td>59000</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>30</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>105 rows × 10 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "          Date   High    Low   Open  Close    Volume  Adj Close  year  month  \\\n",
       "0   2020-03-02  55500  53600  54300  55000  30403412      55000  2020      3   \n",
       "1   2020-03-03  56900  55100  56700  55400  30330295      55400  2020      3   \n",
       "2   2020-03-04  57600  54600  54800  57400  24765728      57400  2020      3   \n",
       "3   2020-03-05  58000  56700  57600  57800  21698990      57800  2020      3   \n",
       "4   2020-03-06  57200  56200  56500  56500  18716656      56500  2020      3   \n",
       "..         ...    ...    ...    ...    ...       ...        ...   ...    ...   \n",
       "100 2020-07-24  54400  53700  54000  54200  10994535      54200  2020      7   \n",
       "101 2020-07-27  55700  54300  54300  55600  21054421      55600  2020      7   \n",
       "102 2020-07-28  58800  56400  57000  58600  48431566      58600  2020      7   \n",
       "103 2020-07-29  60400  58600  60300  59000  36476611      59000  2020      7   \n",
       "104 2020-07-30  60100  59000  59700  59000  19285354      59000  2020      7   \n",
       "\n",
       "     day  \n",
       "0      2  \n",
       "1      3  \n",
       "2      4  \n",
       "3      5  \n",
       "4      6  \n",
       "..   ...  \n",
       "100   24  \n",
       "101   27  \n",
       "102   28  \n",
       "103   29  \n",
       "104   30  \n",
       "\n",
       "[105 rows x 10 columns]"
      ]
     },
     "execution_count": 63,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 66,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:32:56.371878Z",
     "start_time": "2021-03-31T15:32:56.332924Z"
    }
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Open</th>\n",
       "      <th>Close</th>\n",
       "      <th>Volume</th>\n",
       "      <th>Adj Close</th>\n",
       "      <th>year</th>\n",
       "      <th>month</th>\n",
       "      <th>day</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Date</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2020-03-02</th>\n",
       "      <td>2020-03-02</td>\n",
       "      <td>55500</td>\n",
       "      <td>53600</td>\n",
       "      <td>54300</td>\n",
       "      <td>55000</td>\n",
       "      <td>30403412</td>\n",
       "      <td>55000</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>2</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-03</th>\n",
       "      <td>2020-03-03</td>\n",
       "      <td>56900</td>\n",
       "      <td>55100</td>\n",
       "      <td>56700</td>\n",
       "      <td>55400</td>\n",
       "      <td>30330295</td>\n",
       "      <td>55400</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>3</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-04</th>\n",
       "      <td>2020-03-04</td>\n",
       "      <td>57600</td>\n",
       "      <td>54600</td>\n",
       "      <td>54800</td>\n",
       "      <td>57400</td>\n",
       "      <td>24765728</td>\n",
       "      <td>57400</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>4</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-05</th>\n",
       "      <td>2020-03-05</td>\n",
       "      <td>58000</td>\n",
       "      <td>56700</td>\n",
       "      <td>57600</td>\n",
       "      <td>57800</td>\n",
       "      <td>21698990</td>\n",
       "      <td>57800</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>5</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-06</th>\n",
       "      <td>2020-03-06</td>\n",
       "      <td>57200</td>\n",
       "      <td>56200</td>\n",
       "      <td>56500</td>\n",
       "      <td>56500</td>\n",
       "      <td>18716656</td>\n",
       "      <td>56500</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>6</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-07-24</th>\n",
       "      <td>2020-07-24</td>\n",
       "      <td>54400</td>\n",
       "      <td>53700</td>\n",
       "      <td>54000</td>\n",
       "      <td>54200</td>\n",
       "      <td>10994535</td>\n",
       "      <td>54200</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>24</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-07-27</th>\n",
       "      <td>2020-07-27</td>\n",
       "      <td>55700</td>\n",
       "      <td>54300</td>\n",
       "      <td>54300</td>\n",
       "      <td>55600</td>\n",
       "      <td>21054421</td>\n",
       "      <td>55600</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>27</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-07-28</th>\n",
       "      <td>2020-07-28</td>\n",
       "      <td>58800</td>\n",
       "      <td>56400</td>\n",
       "      <td>57000</td>\n",
       "      <td>58600</td>\n",
       "      <td>48431566</td>\n",
       "      <td>58600</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>28</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-07-29</th>\n",
       "      <td>2020-07-29</td>\n",
       "      <td>60400</td>\n",
       "      <td>58600</td>\n",
       "      <td>60300</td>\n",
       "      <td>59000</td>\n",
       "      <td>36476611</td>\n",
       "      <td>59000</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>29</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-07-30</th>\n",
       "      <td>2020-07-30</td>\n",
       "      <td>60100</td>\n",
       "      <td>59000</td>\n",
       "      <td>59700</td>\n",
       "      <td>59000</td>\n",
       "      <td>19285354</td>\n",
       "      <td>59000</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>30</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>105 rows × 10 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                 Date   High    Low   Open  Close    Volume  Adj Close  year  \\\n",
       "Date                                                                           \n",
       "2020-03-02 2020-03-02  55500  53600  54300  55000  30403412      55000  2020   \n",
       "2020-03-03 2020-03-03  56900  55100  56700  55400  30330295      55400  2020   \n",
       "2020-03-04 2020-03-04  57600  54600  54800  57400  24765728      57400  2020   \n",
       "2020-03-05 2020-03-05  58000  56700  57600  57800  21698990      57800  2020   \n",
       "2020-03-06 2020-03-06  57200  56200  56500  56500  18716656      56500  2020   \n",
       "...               ...    ...    ...    ...    ...       ...        ...   ...   \n",
       "2020-07-24 2020-07-24  54400  53700  54000  54200  10994535      54200  2020   \n",
       "2020-07-27 2020-07-27  55700  54300  54300  55600  21054421      55600  2020   \n",
       "2020-07-28 2020-07-28  58800  56400  57000  58600  48431566      58600  2020   \n",
       "2020-07-29 2020-07-29  60400  58600  60300  59000  36476611      59000  2020   \n",
       "2020-07-30 2020-07-30  60100  59000  59700  59000  19285354      59000  2020   \n",
       "\n",
       "            month  day  \n",
       "Date                    \n",
       "2020-03-02      3    2  \n",
       "2020-03-03      3    3  \n",
       "2020-03-04      3    4  \n",
       "2020-03-05      3    5  \n",
       "2020-03-06      3    6  \n",
       "...           ...  ...  \n",
       "2020-07-24      7   24  \n",
       "2020-07-27      7   27  \n",
       "2020-07-28      7   28  \n",
       "2020-07-29      7   29  \n",
       "2020-07-30      7   30  \n",
       "\n",
       "[105 rows x 10 columns]"
      ]
     },
     "execution_count": 66,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.set_index(df['Date'], inplace=True)\n",
    "df"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "시계열 타입이 인덱스인 경우에는 꼭 인덱스 이름과 같지 않아도 특정 연도, 연월, 연월일등과 같이 인덱싱이 가능하다는 특징이 있습니다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 68,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:33:53.791905Z",
     "start_time": "2021-03-31T15:33:53.758339Z"
    }
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Open</th>\n",
       "      <th>Close</th>\n",
       "      <th>Volume</th>\n",
       "      <th>Adj Close</th>\n",
       "      <th>year</th>\n",
       "      <th>month</th>\n",
       "      <th>day</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Date</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2020-03-02</th>\n",
       "      <td>2020-03-02</td>\n",
       "      <td>55500</td>\n",
       "      <td>53600</td>\n",
       "      <td>54300</td>\n",
       "      <td>55000</td>\n",
       "      <td>30403412</td>\n",
       "      <td>55000</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>2</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-03</th>\n",
       "      <td>2020-03-03</td>\n",
       "      <td>56900</td>\n",
       "      <td>55100</td>\n",
       "      <td>56700</td>\n",
       "      <td>55400</td>\n",
       "      <td>30330295</td>\n",
       "      <td>55400</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>3</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-04</th>\n",
       "      <td>2020-03-04</td>\n",
       "      <td>57600</td>\n",
       "      <td>54600</td>\n",
       "      <td>54800</td>\n",
       "      <td>57400</td>\n",
       "      <td>24765728</td>\n",
       "      <td>57400</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>4</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-05</th>\n",
       "      <td>2020-03-05</td>\n",
       "      <td>58000</td>\n",
       "      <td>56700</td>\n",
       "      <td>57600</td>\n",
       "      <td>57800</td>\n",
       "      <td>21698990</td>\n",
       "      <td>57800</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>5</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-06</th>\n",
       "      <td>2020-03-06</td>\n",
       "      <td>57200</td>\n",
       "      <td>56200</td>\n",
       "      <td>56500</td>\n",
       "      <td>56500</td>\n",
       "      <td>18716656</td>\n",
       "      <td>56500</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>6</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                 Date   High    Low   Open  Close    Volume  Adj Close  year  \\\n",
       "Date                                                                           \n",
       "2020-03-02 2020-03-02  55500  53600  54300  55000  30403412      55000  2020   \n",
       "2020-03-03 2020-03-03  56900  55100  56700  55400  30330295      55400  2020   \n",
       "2020-03-04 2020-03-04  57600  54600  54800  57400  24765728      57400  2020   \n",
       "2020-03-05 2020-03-05  58000  56700  57600  57800  21698990      57800  2020   \n",
       "2020-03-06 2020-03-06  57200  56200  56500  56500  18716656      56500  2020   \n",
       "\n",
       "            month  day  \n",
       "Date                    \n",
       "2020-03-02      3    2  \n",
       "2020-03-03      3    3  \n",
       "2020-03-04      3    4  \n",
       "2020-03-05      3    5  \n",
       "2020-03-06      3    6  "
      ]
     },
     "execution_count": 68,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.loc['2020-03'].head() # 3월 인덱싱"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 70,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:34:24.181137Z",
     "start_time": "2021-03-31T15:34:24.156206Z"
    }
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Open</th>\n",
       "      <th>Close</th>\n",
       "      <th>Volume</th>\n",
       "      <th>Adj Close</th>\n",
       "      <th>year</th>\n",
       "      <th>month</th>\n",
       "      <th>day</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Date</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2020-05-04</th>\n",
       "      <td>2020-05-04</td>\n",
       "      <td>49100</td>\n",
       "      <td>48500</td>\n",
       "      <td>48900</td>\n",
       "      <td>48500</td>\n",
       "      <td>26083749</td>\n",
       "      <td>48500</td>\n",
       "      <td>2020</td>\n",
       "      <td>5</td>\n",
       "      <td>4</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-05-06</th>\n",
       "      <td>2020-05-06</td>\n",
       "      <td>49200</td>\n",
       "      <td>48500</td>\n",
       "      <td>49000</td>\n",
       "      <td>49200</td>\n",
       "      <td>18070225</td>\n",
       "      <td>49200</td>\n",
       "      <td>2020</td>\n",
       "      <td>5</td>\n",
       "      <td>6</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-05-07</th>\n",
       "      <td>2020-05-07</td>\n",
       "      <td>49300</td>\n",
       "      <td>48700</td>\n",
       "      <td>49200</td>\n",
       "      <td>48800</td>\n",
       "      <td>13884411</td>\n",
       "      <td>48800</td>\n",
       "      <td>2020</td>\n",
       "      <td>5</td>\n",
       "      <td>7</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-05-08</th>\n",
       "      <td>2020-05-08</td>\n",
       "      <td>49350</td>\n",
       "      <td>48800</td>\n",
       "      <td>49100</td>\n",
       "      <td>48800</td>\n",
       "      <td>15319700</td>\n",
       "      <td>48800</td>\n",
       "      <td>2020</td>\n",
       "      <td>5</td>\n",
       "      <td>8</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-05-11</th>\n",
       "      <td>2020-05-11</td>\n",
       "      <td>49250</td>\n",
       "      <td>48300</td>\n",
       "      <td>48900</td>\n",
       "      <td>48400</td>\n",
       "      <td>16357743</td>\n",
       "      <td>48400</td>\n",
       "      <td>2020</td>\n",
       "      <td>5</td>\n",
       "      <td>11</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                 Date   High    Low   Open  Close    Volume  Adj Close  year  \\\n",
       "Date                                                                           \n",
       "2020-05-04 2020-05-04  49100  48500  48900  48500  26083749      48500  2020   \n",
       "2020-05-06 2020-05-06  49200  48500  49000  49200  18070225      49200  2020   \n",
       "2020-05-07 2020-05-07  49300  48700  49200  48800  13884411      48800  2020   \n",
       "2020-05-08 2020-05-08  49350  48800  49100  48800  15319700      48800  2020   \n",
       "2020-05-11 2020-05-11  49250  48300  48900  48400  16357743      48400  2020   \n",
       "\n",
       "            month  day  \n",
       "Date                    \n",
       "2020-05-04      5    4  \n",
       "2020-05-06      5    6  \n",
       "2020-05-07      5    7  \n",
       "2020-05-08      5    8  \n",
       "2020-05-11      5   11  "
      ]
     },
     "execution_count": 70,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df['2020-05'].head() # 5월 인덱싱"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 71,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:34:56.755071Z",
     "start_time": "2021-03-31T15:34:56.729144Z"
    }
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Open</th>\n",
       "      <th>Close</th>\n",
       "      <th>Volume</th>\n",
       "      <th>Adj Close</th>\n",
       "      <th>year</th>\n",
       "      <th>month</th>\n",
       "      <th>day</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Date</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2020-03-02</th>\n",
       "      <td>2020-03-02</td>\n",
       "      <td>55500</td>\n",
       "      <td>53600</td>\n",
       "      <td>54300</td>\n",
       "      <td>55000</td>\n",
       "      <td>30403412</td>\n",
       "      <td>55000</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>2</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-03</th>\n",
       "      <td>2020-03-03</td>\n",
       "      <td>56900</td>\n",
       "      <td>55100</td>\n",
       "      <td>56700</td>\n",
       "      <td>55400</td>\n",
       "      <td>30330295</td>\n",
       "      <td>55400</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>3</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-04</th>\n",
       "      <td>2020-03-04</td>\n",
       "      <td>57600</td>\n",
       "      <td>54600</td>\n",
       "      <td>54800</td>\n",
       "      <td>57400</td>\n",
       "      <td>24765728</td>\n",
       "      <td>57400</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>4</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-05</th>\n",
       "      <td>2020-03-05</td>\n",
       "      <td>58000</td>\n",
       "      <td>56700</td>\n",
       "      <td>57600</td>\n",
       "      <td>57800</td>\n",
       "      <td>21698990</td>\n",
       "      <td>57800</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>5</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-06</th>\n",
       "      <td>2020-03-06</td>\n",
       "      <td>57200</td>\n",
       "      <td>56200</td>\n",
       "      <td>56500</td>\n",
       "      <td>56500</td>\n",
       "      <td>18716656</td>\n",
       "      <td>56500</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>6</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-09</th>\n",
       "      <td>2020-03-09</td>\n",
       "      <td>56500</td>\n",
       "      <td>56500</td>\n",
       "      <td>56500</td>\n",
       "      <td>56500</td>\n",
       "      <td>0</td>\n",
       "      <td>56500</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>9</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-10</th>\n",
       "      <td>2020-03-10</td>\n",
       "      <td>54900</td>\n",
       "      <td>53700</td>\n",
       "      <td>53800</td>\n",
       "      <td>54600</td>\n",
       "      <td>32106554</td>\n",
       "      <td>54600</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>10</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                 Date   High    Low   Open  Close    Volume  Adj Close  year  \\\n",
       "Date                                                                           \n",
       "2020-03-02 2020-03-02  55500  53600  54300  55000  30403412      55000  2020   \n",
       "2020-03-03 2020-03-03  56900  55100  56700  55400  30330295      55400  2020   \n",
       "2020-03-04 2020-03-04  57600  54600  54800  57400  24765728      57400  2020   \n",
       "2020-03-05 2020-03-05  58000  56700  57600  57800  21698990      57800  2020   \n",
       "2020-03-06 2020-03-06  57200  56200  56500  56500  18716656      56500  2020   \n",
       "2020-03-09 2020-03-09  56500  56500  56500  56500         0      56500  2020   \n",
       "2020-03-10 2020-03-10  54900  53700  53800  54600  32106554      54600  2020   \n",
       "\n",
       "            month  day  \n",
       "Date                    \n",
       "2020-03-02      3    2  \n",
       "2020-03-03      3    3  \n",
       "2020-03-04      3    4  \n",
       "2020-03-05      3    5  \n",
       "2020-03-06      3    6  \n",
       "2020-03-09      3    9  \n",
       "2020-03-10      3   10  "
      ]
     },
     "execution_count": 71,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df['2020-03':'2020-03-10'] # 특정기간 슬라이싱"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 현재 날짜와 차이 컬럼 생성"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "----"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "현재날짜를 구해 경과일이라는 컬럼을 만들어봅시다.\n",
    "\n",
    "현재 날짜를 구하는 함수로는 `datetime의 now와 today`가 있습니다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 74,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:35:48.409417Z",
     "start_time": "2021-03-31T15:35:48.397477Z"
    }
   },
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\ProgramData\\Anaconda3\\lib\\site-packages\\ipykernel_launcher.py:1: FutureWarning: The pandas.datetime class is deprecated and will be removed from pandas in a future version. Import from datetime module instead.\n",
      "  \"\"\"Entry point for launching an IPython kernel.\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "datetime.datetime(2021, 4, 1, 0, 35, 48, 403428)"
      ]
     },
     "execution_count": 74,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "pd.datetime.now()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 75,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:35:56.866596Z",
     "start_time": "2021-03-31T15:35:56.846649Z"
    }
   },
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\ProgramData\\Anaconda3\\lib\\site-packages\\ipykernel_launcher.py:1: FutureWarning: The pandas.datetime class is deprecated and will be removed from pandas in a future version. Import from datetime module instead.\n",
      "  \"\"\"Entry point for launching an IPython kernel.\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "datetime.datetime(2021, 4, 1, 0, 35, 56, 847646)"
      ]
     },
     "execution_count": 75,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "pd.datetime.today()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 172,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:58:31.753099Z",
     "start_time": "2021-03-31T15:58:31.731157Z"
    }
   },
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\ProgramData\\Anaconda3\\lib\\site-packages\\ipykernel_launcher.py:1: FutureWarning: The pandas.datetime class is deprecated and will be removed from pandas in a future version. Import from datetime module instead.\n",
      "  \"\"\"Entry point for launching an IPython kernel.\n"
     ]
    }
   ],
   "source": [
    "today = pd.datetime.now()\n",
    "\n",
    "df['Elapsed_days'] = today - df.index"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 173,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:58:32.180509Z",
     "start_time": "2021-03-31T15:58:32.129470Z"
    }
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Open</th>\n",
       "      <th>Close</th>\n",
       "      <th>Volume</th>\n",
       "      <th>Adj Close</th>\n",
       "      <th>year</th>\n",
       "      <th>month</th>\n",
       "      <th>day</th>\n",
       "      <th>Elapsed_days</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Date</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2020-03-02</th>\n",
       "      <td>2020-03-02</td>\n",
       "      <td>55500</td>\n",
       "      <td>53600</td>\n",
       "      <td>54300</td>\n",
       "      <td>55000</td>\n",
       "      <td>30403412</td>\n",
       "      <td>55000</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>2</td>\n",
       "      <td>395 days 00:58:31.733470</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-03</th>\n",
       "      <td>2020-03-03</td>\n",
       "      <td>56900</td>\n",
       "      <td>55100</td>\n",
       "      <td>56700</td>\n",
       "      <td>55400</td>\n",
       "      <td>30330295</td>\n",
       "      <td>55400</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>3</td>\n",
       "      <td>394 days 00:58:31.733470</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-04</th>\n",
       "      <td>2020-03-04</td>\n",
       "      <td>57600</td>\n",
       "      <td>54600</td>\n",
       "      <td>54800</td>\n",
       "      <td>57400</td>\n",
       "      <td>24765728</td>\n",
       "      <td>57400</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>4</td>\n",
       "      <td>393 days 00:58:31.733470</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-05</th>\n",
       "      <td>2020-03-05</td>\n",
       "      <td>58000</td>\n",
       "      <td>56700</td>\n",
       "      <td>57600</td>\n",
       "      <td>57800</td>\n",
       "      <td>21698990</td>\n",
       "      <td>57800</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>5</td>\n",
       "      <td>392 days 00:58:31.733470</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-06</th>\n",
       "      <td>2020-03-06</td>\n",
       "      <td>57200</td>\n",
       "      <td>56200</td>\n",
       "      <td>56500</td>\n",
       "      <td>56500</td>\n",
       "      <td>18716656</td>\n",
       "      <td>56500</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>6</td>\n",
       "      <td>391 days 00:58:31.733470</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-07-24</th>\n",
       "      <td>2020-07-24</td>\n",
       "      <td>54400</td>\n",
       "      <td>53700</td>\n",
       "      <td>54000</td>\n",
       "      <td>54200</td>\n",
       "      <td>10994535</td>\n",
       "      <td>54200</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>24</td>\n",
       "      <td>251 days 00:58:31.733470</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-07-27</th>\n",
       "      <td>2020-07-27</td>\n",
       "      <td>55700</td>\n",
       "      <td>54300</td>\n",
       "      <td>54300</td>\n",
       "      <td>55600</td>\n",
       "      <td>21054421</td>\n",
       "      <td>55600</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>27</td>\n",
       "      <td>248 days 00:58:31.733470</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-07-28</th>\n",
       "      <td>2020-07-28</td>\n",
       "      <td>58800</td>\n",
       "      <td>56400</td>\n",
       "      <td>57000</td>\n",
       "      <td>58600</td>\n",
       "      <td>48431566</td>\n",
       "      <td>58600</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>28</td>\n",
       "      <td>247 days 00:58:31.733470</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-07-29</th>\n",
       "      <td>2020-07-29</td>\n",
       "      <td>60400</td>\n",
       "      <td>58600</td>\n",
       "      <td>60300</td>\n",
       "      <td>59000</td>\n",
       "      <td>36476611</td>\n",
       "      <td>59000</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>29</td>\n",
       "      <td>246 days 00:58:31.733470</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-07-30</th>\n",
       "      <td>2020-07-30</td>\n",
       "      <td>60100</td>\n",
       "      <td>59000</td>\n",
       "      <td>59700</td>\n",
       "      <td>59000</td>\n",
       "      <td>19285354</td>\n",
       "      <td>59000</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>30</td>\n",
       "      <td>245 days 00:58:31.733470</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>105 rows × 11 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                 Date   High    Low   Open  Close    Volume  Adj Close  year  \\\n",
       "Date                                                                           \n",
       "2020-03-02 2020-03-02  55500  53600  54300  55000  30403412      55000  2020   \n",
       "2020-03-03 2020-03-03  56900  55100  56700  55400  30330295      55400  2020   \n",
       "2020-03-04 2020-03-04  57600  54600  54800  57400  24765728      57400  2020   \n",
       "2020-03-05 2020-03-05  58000  56700  57600  57800  21698990      57800  2020   \n",
       "2020-03-06 2020-03-06  57200  56200  56500  56500  18716656      56500  2020   \n",
       "...               ...    ...    ...    ...    ...       ...        ...   ...   \n",
       "2020-07-24 2020-07-24  54400  53700  54000  54200  10994535      54200  2020   \n",
       "2020-07-27 2020-07-27  55700  54300  54300  55600  21054421      55600  2020   \n",
       "2020-07-28 2020-07-28  58800  56400  57000  58600  48431566      58600  2020   \n",
       "2020-07-29 2020-07-29  60400  58600  60300  59000  36476611      59000  2020   \n",
       "2020-07-30 2020-07-30  60100  59000  59700  59000  19285354      59000  2020   \n",
       "\n",
       "            month  day             Elapsed_days  \n",
       "Date                                             \n",
       "2020-03-02      3    2 395 days 00:58:31.733470  \n",
       "2020-03-03      3    3 394 days 00:58:31.733470  \n",
       "2020-03-04      3    4 393 days 00:58:31.733470  \n",
       "2020-03-05      3    5 392 days 00:58:31.733470  \n",
       "2020-03-06      3    6 391 days 00:58:31.733470  \n",
       "...           ...  ...                      ...  \n",
       "2020-07-24      7   24 251 days 00:58:31.733470  \n",
       "2020-07-27      7   27 248 days 00:58:31.733470  \n",
       "2020-07-28      7   28 247 days 00:58:31.733470  \n",
       "2020-07-29      7   29 246 days 00:58:31.733470  \n",
       "2020-07-30      7   30 245 days 00:58:31.733470  \n",
       "\n",
       "[105 rows x 11 columns]"
      ]
     },
     "execution_count": 173,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "차잇값을 보면 자동으로 days까지 붙어서 표기되는 것을 알 수 있다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 174,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:58:32.600482Z",
     "start_time": "2021-03-31T15:58:32.588443Z"
    }
   },
   "outputs": [],
   "source": [
    "df['Elapsed_days'] = df['Elapsed_days'].astype(str)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 176,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:58:37.877666Z",
     "start_time": "2021-03-31T15:58:37.856592Z"
    }
   },
   "outputs": [],
   "source": [
    "df['Elapsed_days'] = df['Elapsed_days'].str.split('00')"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "str.get() 함수는 split된 개별원소를 갖는 시리즈 객체에 인덱싱이 가능하도록 합니다."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 177,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:58:42.946776Z",
     "start_time": "2021-03-31T15:58:42.934075Z"
    }
   },
   "outputs": [],
   "source": [
    "df['Elapsed_days'] = df['Elapsed_days'].str.get(0) "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 178,
   "metadata": {
    "ExecuteTime": {
     "end_time": "2021-03-31T15:58:45.159386Z",
     "start_time": "2021-03-31T15:58:45.114485Z"
    }
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Open</th>\n",
       "      <th>Close</th>\n",
       "      <th>Volume</th>\n",
       "      <th>Adj Close</th>\n",
       "      <th>year</th>\n",
       "      <th>month</th>\n",
       "      <th>day</th>\n",
       "      <th>Elapsed_days</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Date</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2020-03-02</th>\n",
       "      <td>2020-03-02</td>\n",
       "      <td>55500</td>\n",
       "      <td>53600</td>\n",
       "      <td>54300</td>\n",
       "      <td>55000</td>\n",
       "      <td>30403412</td>\n",
       "      <td>55000</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>2</td>\n",
       "      <td>395 days</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-03</th>\n",
       "      <td>2020-03-03</td>\n",
       "      <td>56900</td>\n",
       "      <td>55100</td>\n",
       "      <td>56700</td>\n",
       "      <td>55400</td>\n",
       "      <td>30330295</td>\n",
       "      <td>55400</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>3</td>\n",
       "      <td>394 days</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-04</th>\n",
       "      <td>2020-03-04</td>\n",
       "      <td>57600</td>\n",
       "      <td>54600</td>\n",
       "      <td>54800</td>\n",
       "      <td>57400</td>\n",
       "      <td>24765728</td>\n",
       "      <td>57400</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>4</td>\n",
       "      <td>393 days</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-05</th>\n",
       "      <td>2020-03-05</td>\n",
       "      <td>58000</td>\n",
       "      <td>56700</td>\n",
       "      <td>57600</td>\n",
       "      <td>57800</td>\n",
       "      <td>21698990</td>\n",
       "      <td>57800</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>5</td>\n",
       "      <td>392 days</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-03-06</th>\n",
       "      <td>2020-03-06</td>\n",
       "      <td>57200</td>\n",
       "      <td>56200</td>\n",
       "      <td>56500</td>\n",
       "      <td>56500</td>\n",
       "      <td>18716656</td>\n",
       "      <td>56500</td>\n",
       "      <td>2020</td>\n",
       "      <td>3</td>\n",
       "      <td>6</td>\n",
       "      <td>391 days</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-07-24</th>\n",
       "      <td>2020-07-24</td>\n",
       "      <td>54400</td>\n",
       "      <td>53700</td>\n",
       "      <td>54000</td>\n",
       "      <td>54200</td>\n",
       "      <td>10994535</td>\n",
       "      <td>54200</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>24</td>\n",
       "      <td>251 days</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-07-27</th>\n",
       "      <td>2020-07-27</td>\n",
       "      <td>55700</td>\n",
       "      <td>54300</td>\n",
       "      <td>54300</td>\n",
       "      <td>55600</td>\n",
       "      <td>21054421</td>\n",
       "      <td>55600</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>27</td>\n",
       "      <td>248 days</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-07-28</th>\n",
       "      <td>2020-07-28</td>\n",
       "      <td>58800</td>\n",
       "      <td>56400</td>\n",
       "      <td>57000</td>\n",
       "      <td>58600</td>\n",
       "      <td>48431566</td>\n",
       "      <td>58600</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>28</td>\n",
       "      <td>247 days</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-07-29</th>\n",
       "      <td>2020-07-29</td>\n",
       "      <td>60400</td>\n",
       "      <td>58600</td>\n",
       "      <td>60300</td>\n",
       "      <td>59000</td>\n",
       "      <td>36476611</td>\n",
       "      <td>59000</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>29</td>\n",
       "      <td>246 days</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-07-30</th>\n",
       "      <td>2020-07-30</td>\n",
       "      <td>60100</td>\n",
       "      <td>59000</td>\n",
       "      <td>59700</td>\n",
       "      <td>59000</td>\n",
       "      <td>19285354</td>\n",
       "      <td>59000</td>\n",
       "      <td>2020</td>\n",
       "      <td>7</td>\n",
       "      <td>30</td>\n",
       "      <td>245 days</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>105 rows × 11 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                 Date   High    Low   Open  Close    Volume  Adj Close  year  \\\n",
       "Date                                                                           \n",
       "2020-03-02 2020-03-02  55500  53600  54300  55000  30403412      55000  2020   \n",
       "2020-03-03 2020-03-03  56900  55100  56700  55400  30330295      55400  2020   \n",
       "2020-03-04 2020-03-04  57600  54600  54800  57400  24765728      57400  2020   \n",
       "2020-03-05 2020-03-05  58000  56700  57600  57800  21698990      57800  2020   \n",
       "2020-03-06 2020-03-06  57200  56200  56500  56500  18716656      56500  2020   \n",
       "...               ...    ...    ...    ...    ...       ...        ...   ...   \n",
       "2020-07-24 2020-07-24  54400  53700  54000  54200  10994535      54200  2020   \n",
       "2020-07-27 2020-07-27  55700  54300  54300  55600  21054421      55600  2020   \n",
       "2020-07-28 2020-07-28  58800  56400  57000  58600  48431566      58600  2020   \n",
       "2020-07-29 2020-07-29  60400  58600  60300  59000  36476611      59000  2020   \n",
       "2020-07-30 2020-07-30  60100  59000  59700  59000  19285354      59000  2020   \n",
       "\n",
       "            month  day Elapsed_days  \n",
       "Date                                 \n",
       "2020-03-02      3    2    395 days   \n",
       "2020-03-03      3    3    394 days   \n",
       "2020-03-04      3    4    393 days   \n",
       "2020-03-05      3    5    392 days   \n",
       "2020-03-06      3    6    391 days   \n",
       "...           ...  ...          ...  \n",
       "2020-07-24      7   24    251 days   \n",
       "2020-07-27      7   27    248 days   \n",
       "2020-07-28      7   28    247 days   \n",
       "2020-07-29      7   29    246 days   \n",
       "2020-07-30      7   30    245 days   \n",
       "\n",
       "[105 rows x 11 columns]"
      ]
     },
     "execution_count": 178,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.7.6"
  },
  "toc": {
   "base_numbering": 1,
   "nav_menu": {},
   "number_sections": true,
   "sideBar": true,
   "skip_h1_title": false,
   "title_cell": "Table of Contents",
   "title_sidebar": "Contents",
   "toc_cell": false,
   "toc_position": {},
   "toc_section_display": true,
   "toc_window_display": false
  },
  "varInspector": {
   "cols": {
    "lenName": 16,
    "lenType": 16,
    "lenVar": 40
   },
   "kernels_config": {
    "python": {
     "delete_cmd_postfix": "",
     "delete_cmd_prefix": "del ",
     "library": "var_list.py",
     "varRefreshCmd": "print(var_dic_list())"
    },
    "r": {
     "delete_cmd_postfix": ") ",
     "delete_cmd_prefix": "rm(",
     "library": "var_list.r",
     "varRefreshCmd": "cat(var_dic_list()) "
    }
   },
   "types_to_exclude": [
    "module",
    "function",
    "builtin_function_or_method",
    "instance",
    "_Feature"
   ],
   "window_display": false
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
