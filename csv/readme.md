# TIL


### 여러 파일 불러오기
### 출처 : https://eclipse360.tistory.com/12


import pandas as pd
import glob
import os
from IPython.core.display import display, HTML

display(HTML("<style>, container{width:90% !important;}</style>"))

input_file = r"C:\Users\psps4\coin_project\prophet_coin" # csv 파일들이 있는 위치
output_file = r"C:\Users\psps4\coin_project\prophet_coin\result_line.csv" # 병합하고 저장하려는 파일명
allFile_list = glob.glob(os.path.join(input_file, 'coin_*')) # glob함수로 coin_으로 시작하는 파일들을 모은다. 
print(allFile_list)

allData = [] # 읽어 들인 csv 파일 내용을 저장할 빈 리스트를 하나 만든다. 
for file in allFile_list:
    df = pd.read_csv(file, engine='python') # for 구문으로 csv파일들을 읽어 들인다. 
    allData.append(df)
allData[1]
