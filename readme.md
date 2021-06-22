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
map : 값 바꿔주기 // apply도 동일하지만 map은 series, apply는 dataframe
columns와 다른 것.

dayofweek="월화수목금토일"
dayofweek[1]

def find_dayofweek(day_no):
    dayofweek = "월화수목금토일"
    return dayofweek[day_no]

df["요일명"]=df["요일"].map(find_dayofweek)

### 5. 결측치

isna(), fillna() 
dropna(how='all', axis=1) #결측치가 하나라도 있는 곳을 제거 
dropna(how='all', axis=0)

### 6. 인덱스
set_index : 인덱스 넣기
reset_index : 인덱스 빼기 

### 7. 누적수 구하는 방법
cumsum()

### 8. pd.concat 함수
concat은 단순히 합치는 것이다. 
axis=0 행이니까 밑으로
axis=1 열이니까 옆으로

### 9. pivot_table : 빠르게 계산해주는 함수 
pdf1 = pd.pivot_table(df,                # 피벗할 데이터프레임
                     index = 'class',    # 행 위치에 들어갈 열
                     columns = 'sex',    # 열 위치에 들어갈 열
                     values = 'age',     # 데이터로 사용할 열
                     aggfunc = 'mean') 
 
 * pivot_table과 crosstab의 차이점 
  pivot_table는 입력 데이터가 이미 DataFrame 일 것으로 예상한다는 것.
 
### 10. melt

  (1) pd.melt(data, id_vars=['id1', 'id2', ...]) 를 사용한 데이터 재구조화를 하는데, 
      여기서 id_vars의 역항은 이자식은 건들지 않고 나머지를 열에서 행으로 내린다. 이때 열의 이름은 variable과 values이다. 
  (2) # (b) melt()

In [9]: data_melt = pd.melt(data, id_vars=['cust_ID', 'prd_CD'],

   ...: var_name='pch_CD', value_name='pch_value')
In [10]: data_melt

Out[10]:

  cust_ID prd_CD   pch_CD  pch_value
0   C_001  P_001  pch_amt        100
1   C_001  P_002  pch_amt        200
2   C_002  P_001  pch_amt        300
3   C_002  P_002  pch_amt        400
4   C_001  P_001  pch_cnt          1
5   C_001  P_002  pch_cnt          2
6   C_002  P_001  pch_cnt          3
7   C_002  P_002  pch_cnt          4
출처: https://rfriend.tistory.com/278 [R, Python 분석과 프로그래밍의 친구 (by R Friend)]

(3) # (c) pd.pivot_table()

In [13]: data_melt_pivot = pd.pivot_table(data_melt, index=['cust_ID', 'prd_CD'],

    ...: columns='pch_CD', values='pch_value',

    ...: aggfunc=np.mean)



In [14]: data_melt_pivot

Out[14]:

pch_CD             pch_amt   pch_cnt
cust_ID prd_CD                 
C_001   P_001       100        1
           P_002       200        2
C_002   P_001       300        3
           P_002       400        4



출처: https://rfriend.tistory.com/278 [R, Python 분석과 프로그래밍의 친구 (by R Friend)]



### 11. plot 

(1) 일반 그래프 그릴때, 겹쳐서 나온다??? 
이때,g= df_last.groupby(["지역명","전용면적"])["평당분양가격"].mean().unstack() 이처럼 unstack()을 사용하여 쉽게 나타낸다. 

(2) 플랏에서 선을 그리고 싶다??
plt.axhline(15000) 기준선이 그어지는데, 중요하긴 하다. 

(3) plot에서는 subplot도 지원한다. 
great[["경기","서울", "제주"]].plot(figsize=(14,8), rot=30, title="연도와 지역별 평당분양가격", subplots=True)

*여러개가 많이 나올때, 특정 칼럼만 지정하여, subplots=True를 사용하여 쉽게 나타낸다.

(4) 


### 12. sns
(1) 스타일 변경방법
sns.set(style='darkgrid')
(2) hue : 분류
예를들어, gender라는 hue가 "male"과 "female"이 있다면, 그래프에서 다른색으로 표시된다. 















출처: https://rfriend.tistory.com/278 [R, Python 분석과 프로그래밍의 친구 (by R Friend)]













