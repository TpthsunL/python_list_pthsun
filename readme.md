# LIST GGUL TIP

### 1. 기본 데이터 분석시 필요한 라이브러리
import pandas as pd 
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

plt.rc("font", family="Malgun Gothic") #한글 폰트 
plt.rc("axes", unicode_minus=False) #마이너스 코드 
from IPython.display import set_matplotlib_formats #폰트 선명하게 설정.
set_matplotlib_formats('retina') 
pd.Series([-1,0,1,3,5]).plot(title="한글폰트") # 한글폰트와 마이너스 폰트 설정 확인

print(plt.style.available) #스타일 보기 
plt.style.use("fivethirtyeight") # plot() 테마설정하기 

+ 파이썬 라이브러리
1. 
* 날짜를 만들어 저장하기 위해 오늘 날짜를 구합니다. 
import datetime
today = datetime.datetime.today().strftime('%Y-%m-%d')

order_df['order_purchase_timestamp'][0].strftime("%A") #요일 만드는 간다한 

2. 그래픽 라이브러리
from mpl_toolkits.mplot3d import Axes3D # matplotlib의 2D 그래프에 3D 오브젝트를 그리도록 해주는 라이브러리
from mpl_toolkits.mplot3d import proj3d

3. 점수
from sklearn.metrics import silhouette_score
silhouette score의 경우는 개별 개체에 대해서 값을 도출할 수 있습니다. sklearn은 각 sample에 대해서 계산할 수 있게도 하고, 평균 값을 내는 것도 지원함.

4. counter
from collections import Counter
1. Counter([1,2,1,2,13,34,2,134,1]) -> Counter({1: 3, 2: 3, 13: 1, 34: 1, 134: 1}) -> 각각의 개수를 세서 딕셔너리 형태로 나온다. 다음과 같이.
2. Counter([1,2,1,2,13,34,2,134,1]).most_common(1) -> [(3,3)] 가장 많은거 한개를 뽑은것이다. 



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

df["요일명"]=df["요일"].apply(find_dayofweek)

### 5. 결측치

isna(), fillna() 
axis=
0: 행 1: 열
how ='any' : 결측치가 있는 곳이라면 전부다. 삭제 
    ='all' : 전체가 결측있는 곳만 삭제 
    
결측치 값이 0인 행 제거 : df.loc[:, (df != 0).any(axis=0)]

전체적으로 결측치 존재하는가? : data.isnull().any().any()
열 별로 결측치 존재하는가? data.isnull().any()


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
(3) x축 라벨 바꾸기
g = sns.lineplot(data=df_month,x='Month', y='PercentOfBaseline')
g.set_xticks(range(3,13)) 
g.set_xticklabels(['3','4','5','6','7','8','9','10','11','12'])





### 13. 파이썬 저장방법에 대하여 
(1) 저장할때,
df.to_csv(파일이름,....)
* 옵션
현재 인덱스는 빼고 넣는다. : index = False

(2) 불러올때
pd.read_csv(파일이름,....)
* 옵션
- itemcode 숫자 앞의 0 이 지워진다면 dtype={"itemcode": np.object} 로 타입을 지정해 주면 문자형태로
- sep='|' : 토큰나이징 얘기 나오면

### 14. 삭제
열 삭제 : .drop(axis=1)
행 삭제 : .drop(axis=0)
행 전체가 0인 것을 삭제시킬때 : df.loc[:, (df != 0).any(axis=0)]

### 15. 정렬
(1) 기본정렬 
- df.sort_values(by='total', ascending=False).groupby('name', sort=False).head(3)
- df.groupby('name').apply(lambda x: x.nlargest(3, 'total'))

(2) 혼합정렬
df.sort_values(by=['carat', 'depth'], ascending=[False, True]).head(5)

### 16. groupby 
(1) 기본정렬 
grouped_ww.mean() # Series
(2) 리스트로 사용하는 .agg 함수방법
function_list = ['size', 'mean', 'std', 'min', 'max']

grouped_ww.agg(function_list)
출처: https://rfriend.tistory.com/392 [R, Python 분석과 프로그래밍의 친구 (by R Friend)]

### 17. loc와 iloc
loc는 위에서 인덱스번호대로 
iloc는 위에서 순서대로 

* loc 쓸때 주의할 점 : df.loc[df['xx']=='xx','xx'], 혹은 df.loc[(df['xx']=='xx') & (df['xx']=='xx')]

### 18. 이것을 포함하는 여부  (isin)
isin(values)
 * 구성된 애들이 있는 놈들만 데이터프레임화 시키기 : df[df['clarity'].isin(top_index)]

### 19. plotly 

### 20. range와 enumerate 함수 
enumerate 함수
리스트가 있는 경우 순서와 리스트의 값을 전달하는 기능을 가집니다.
### 30. sns 
- markers 크기 조절
plt.figure(figsize=(15,6))

sns.lineplot(data=df, x="Month", y="PercentOfBaseline", hue="Country", marker='o', ci=None)
plt.legend(bbox_to_anchor=(1.02, 1), loc='upper left', borderaxespad=0)
paper_rc = {'lines.linewidth': 1, 'lines.markersize': 5}                  
sns.set_context("paper", rc = paper_rc)


### 31. map과 apply
map : 자료형 변환시 사용한다.
apply 는 다르다.  
### 32. 행추출
- 홀수만 뽑기
ch5 = ch3.iloc[1::2]
- 짝수만 뽑기
ch5 = ch3.iloc[::2]

### 33. 사진 업로드
1. ctrl+v로 그냥 마크다운 상태에서 붙여넣을수도 있음. (크기조절은 불가능)
2. 따라서 <img src='cnn.PNG' style='width:500px;'> 이 방법을 사용한다면 크기조절 가능한 것이 가능하게 된다. 
  + style 안에 'height:(원하는숫자)px; => <img src='cnn.PNG' style='width:500px, height:200px;'> 


* 알아두면 좋은 팁
- 도움말을 보고자 할때는 ? 를 사용하고 소스코드를 볼 때는 ??를 사용합니다.
- 주피터 노트북에서는 함수나 메소드의 괄호 안에서 shift + tab 키를 누르면 도움말을 볼 수 있습니다.
- 이미지 넣는 방법 : <img src="url" width="넓이의 값">
 ex) <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c9/JSON_vector_logo.svg/300px-JSON_vector_logo.svg.png" width="100">

### 34. 소수점 고쳐주기 
pd.set_option('display.float_format', lambda x: '%.3f' % x)

### 35. 더블 칼럼명 합치기
city_df.columns = city_df.columns.to_flat_index()

### 36. 결측치 제거 안될때 사용해보기
idx= []
lt = clean_data['Power'].tolist()
for i in range(len(lt)):
    if( lt[i] == 'null'):
        idx.append(i)
clean_data = clean_data.drop(idx)
clean_data = clean_data.reset_index(drop=True)

### 37. lineregression에 담겨있다. 

### 38. df_2008['출루율'] = df_2008['출루율'].apply(round, args=(3, ))


### 39. 열 만들기
* 여러개 만들때 짱 좋음.
1. assign 이용할 것. 
 
2.  transform을 사용해야 한다. 
-> 왜냐하면 max는 행이 5개인데 이것을 고르게 배분하기 위해서는 현재 방법이 필요하다고 볼 수 있다. 
ex) df['new_max'] = df.groupby('MSZoning')['LotArea'].transform(lamda x : x.max())

3. agg 이용하는 방법

### 
출처: https://rfriend.tistory.com/278 [R, Python 분석과 프로그래밍의 친구 (by R Friend)]













