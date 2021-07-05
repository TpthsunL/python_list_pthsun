# 기타 외부적인 요소에 관한 코드

1. 디렉토리
import os 
현재 디렉토리 : os.getcwd()
디렉토리 변경: os.chdir("디렉토리 경로")
디렉토리 파일 확인: os.listdir()

csv파일 호출: pd.read_csv("파일 이름")


2. 경고

 - (1) 경고 메시지를 무시하고 숨기거나 (Ignore warning message)
      import warnings
    : warnings.filterwarnings(action='ignore')

 - (2) 숨기기했던 경고 메시지를 다시 보이게 (Reset to default)
      import warnings
    : warnings.filterwarnings(action='default')
