# LIST GGUL TIP

### 1. 기본 데이터 분석시 필요한 라이브러리
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

plt.rc("font", family="Malgun Gothic") #한글 폰트 
plt.rc("axes", unicode_minus=False) #마이너스 코드 
print(plt.style.available) #스타일 보기 
plt.style.use("fivethirtyeight") # plot() 테마설정하기 

### 2. 빈도수 구하기 3가지 방법 ex) '월', '지역'
month_gu=df_oversea.groupby(["월", "지역"])["연번"].count().unstack()
pd.crosstab(df_oversea["월"],df_oversea["지역"])
pd.pivot_table(df_oversea, index="월", values="지역", aggfunc="count", fill_value=0)

### 3. 확진일로 칼럼 만들기 
df["연도"]=df["확진일"].dt.year
df["월"]=df["확진일"].dt.month
df["일"]=df["확진일"].dt.day
df["요일"]=df["확진일"].dt.dayofweek

### 4. map & 함수
map : 값 바꿔주기
columns와 다른 것.

dayofweek="월화수목금토일"
dayofweek[1]

def find_dayofweek(day_no):
    dayofweek = "월화수목금토일"
    return dayofweek[day_no]

df["요일명"]=df["요일"].map(find_dayofweek)

### 5. 결측치

isna(), fillna() 
dropna(how='all', axis=1)
dropna(how='all', axis=0)

### 6. 인덱스
set_index : 인덱스 넣기
reset_index : 인덱스 빼기 

### 7. 누적수 구하는 방법
cumsum()

### 8. 













