### 1. merge

출처 : https://mizykk.tistory.com/82

import pandas as pd


# 기준열 이름이 같을 때
pd.merge(left, right, on = '기준열', how = '조인방식')

# 기준열 이름이 다를 때
pd.merge(left, right, left_on = '왼쪽 열', right_on = '오른쪽 열', how = '조인방식')

left : 왼쪽 데이터프레임

right : 오른쪽 데이터프레임

on : (두 데이터프레임의 기준열 이름이 같을 때) 기준열

how : 조인 방식 {'left', 'right', 'inner', 'outer'} 기본값은 'inner'

left_on : 기준열 이름이 다를 때, 왼쪽 기준열

right_on : 기준열 이름이 다를 때, 오른쪽 기준열
