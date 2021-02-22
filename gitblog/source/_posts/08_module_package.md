---
title: Jupyter notebook
date: 2021-02-22 17:32:13
tags: python
categories: programming
---


## Module Package
- 모듈 : 변수와 함수, 클래스를 모아놓은 (.py) 확장자를 가진 파일
- 패키지 : 모듈의 기능을 디렉토리별로 정리해 놓은 개념

### 1. 모듈
- 모듈 생성
- 모듈 호출


```python
%%writefile dss.py

num = 1234

def disp1(msg):
    print("disp1", msg)
    
def disp2(msg):
    print("disp2", msg)

class Calc:
    def plus(self, *args):
        return sum(args)
```

    Writing dss.py
    


```python
!ls
```

    01_jupyter_notebook.ipynb
    02_basic_syntax.ipynb
    03_condition_loop.ipynb
    04_function.ipynb
    05_function_2.ipynb
    06_class_1.ipynb
    07_class_2.ipynb
    08_module_package.ipynb
    dss.py
    


```python
%reset
```

    Once deleted, variables cannot be recovered. Proceed (y/[n])? y
    


```python
%whos
```

    Interactive namespace is empty.
    


```python
# 모듈 호출 : import
import dss
```


```python
%whos
```

    Variable   Type      Data/Info
    ------------------------------
    dss        module    <module 'dss' from 'C:\\Code\\01_python\\dss.py'>
    


```python
dss.num
```




    1234




```python
dss.disp1("python")
```

    disp1 python
    


```python
calc = dss.Calc()
```


```python
calc.plus(1,2,3,4)
```




    10




```python
import random
```


```python
random.randint(1, 5)
```




    1




```python
# 모듈 안에 특정 함수, 변수, 클래스 호출
```


```python
from dss import num, disp2
```


```python
%whos
```

    Variable   Type        Data/Info
    --------------------------------
    calc       Calc        <dss.Calc object at 0x0000026C12554340>
    disp2      function    <function disp2 at 0x0000026C12626670>
    dss        module      <module 'dss' from 'C:\\Code\\01_python\\dss.py'>
    num        int         1234
    random     module      <module 'random' from 'C:<...>aconda3\\lib\\random.py'>
    


```python
dss.num
```




    1234




```python
num
```




    1234




```python
%reset
```

    Once deleted, variables cannot be recovered. Proceed (y/[n])? y
    


```python
from dss import *
```


```python
%whos
```

    Variable   Type        Data/Info
    --------------------------------
    Calc       type        <class 'dss.Calc'>
    disp1      function    <function disp1 at 0x0000026C12626940>
    disp2      function    <function disp2 at 0x0000026C12626670>
    num        int         1234
    

### 2. Package
- 패키지 생성
- 패키지 호출
- setup.py 패키지 설치 파일 만들기


```python
# 디렉토리 생성
```


```python
!mkdir -p school/dss
```

    The syntax of the command is incorrect.
    


```python
!mkdir -p school/web
```

    The syntax of the command is incorrect.
    

- tree 설치 mac
    - homebrew : https://brew.sh/
    - homebrew : osx 패키지 설치 관리툴
    - '/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"'
    - brew install tree


```python
!tree school
```

    Folder PATH listing for volume Windows10
    Volume serial number is E625-BBFB
    C:\CODE\01_PYTHON\SCHOOL
    ├───dss
    └───web
    


```python
# 패키지 사용시 디렉토리에 __init__.py 파일을 추가
# python 3.3 버전 이상에서는 필요없음
```


```python
!touch school/dss/__init__.py
!touch school/web/__init__.py
```


```python
!tree school
```

    Folder PATH listing for volume Windows10
    Volume serial number is E625-BBFB
    C:\CODE\01_PYTHON\SCHOOL
    ├───dss
    └───web
    


```python
%%writefile school/dss/data1.py

def plus(*args):
    print("data1")
    return sum(args)
```

    Writing school/dss/data1.py
    


```python
%%writefile school/dss/data2.py

def plus2(*args):
    print("data2")
    return sum(args)
```

    Writing school/dss/data2.py
    


```python
%%writefile school/web/url.py

def make(url):
    return url if url[:7] == "http://" else "http://" + url
```

    Writing school/web/url.py
    


```python
!tree school/
```

    Folder PATH listing for volume Windows10
    Volume serial number is E625-BBFB
    C:\CODE\01_PYTHON\SCHOOL
    ├───dss
    └───web
    


```python
%reset
```

    Once deleted, variables cannot be recovered. Proceed (y/[n])? y
    


```python
import school.dss.data1
```


```python
whos
```

    Variable   Type      Data/Info
    ------------------------------
    school     module    <module 'school' (namespace)>
    


```python
school.dss.data1.plus(1,2,3)
```

    data1
    




    6




```python
import school.dss.data1 as dss
```


```python
dss.plus(1,2)
```

    data1
    




    3




```python
# school.web : 디렉토리
# url : 모듈
from school.web import url
```


```python
url.make("google.com")
```




    'http://google.com'




```python
url.make("naver.com")
```




    'http://naver.com'




```python
# 패키지의 위치 : 특정 디렉토리에 있는 패키지는 어디에서나 import 가능
```


```python
import random
```


```python
!ls
```

    01_jupyter_notebook.ipynb
    02_basic_syntax.ipynb
    03_condition_loop.ipynb
    04_function.ipynb
    05_function_2.ipynb
    06_class_1.ipynb
    07_class_2.ipynb
    08_module_package.ipynb
    __pycache__
    dss.py
    school
    


```python
import sys

for path in sys.path:
    print(path)
```

    C:\Code\01_python
    C:\Users\USER\anaconda3\python38.zip
    C:\Users\USER\anaconda3\DLLs
    C:\Users\USER\anaconda3\lib
    C:\Users\USER\anaconda3
    
    C:\Users\USER\anaconda3\lib\site-packages
    C:\Users\USER\anaconda3\lib\site-packages\win32
    C:\Users\USER\anaconda3\lib\site-packages\win32\lib
    C:\Users\USER\anaconda3\lib\site-packages\Pythonwin
    C:\Users\USER\anaconda3\lib\site-packages\IPython\extensions
    C:\Users\USER\.ipython
    


```python
packages = !ls C:\Users\USER\anaconda3\lib
len(packages)
```




    207




```python
packages[-5:]
```




    ['xml', 'xmlrpc', 'zipapp.py', 'zipfile.py', 'zipimport.py']




```python
# setup.py 를 작성해서 패키지를 설치해서 사용
# setuptools를 이용
```


```python
!tree school/
```

    Folder PATH listing for volume Windows10
    Volume serial number is E625-BBFB
    C:\CODE\01_PYTHON\SCHOOL
    ├───dss
    │   └───__pycache__
    └───web
        └───__pycache__
    


```python
%%writefile school/dss/__init__.py

__all__ = ["data1", "data2"]
```

    Overwriting school/dss/__init__.py
    


```python
%%writefile school/setup.py

from setuptools import setup, find_packages

setup(
    nume="dss",
    packages=find_packages(),
    include_package_data=True,
    version="0.0.1",
    author_email="manimahn12@gmail.com"
    zip_safe=False
)
```

    Overwriting school/setup.py
    


```python
!rm dss.py
```


```python
# 패키지 설치 확인
```


```python
!pip list | grep dss # dss가 들어간 패키지 확인
```

    grep: #: No such file or directory
    grep: dss媛�: No such file or directory
    grep: �뱾�뼱媛�: No such file or directory
    grep: �뙣�궎吏�: No such file or directory
    grep: �솗�씤: No such file or directory
    ERROR: Pipe to stdout was broken
    Exception ignored in: <_io.TextIOWrapper name='<stdout>' mode='w' encoding='cp949'>
    OSError: [Errno 22] Invalid argument
    


```python
# 패키지 설치
# school $ python setup.py develop
# 커널 리스타트
# develop : 개발자모드, 코드를 수정하면 설치된 패키지도 같이 수정
# build : 일반모드, 코드를 수정하면 다시 설치해야 수정된 코드가 적용
```


```python
!pip list | grep dss
```


```python
!pip list | grep numpy
```

    numpy                              1.19.2
    numpydoc                           1.1.0
    


```python
from dss import *
```


```python
%whos
```

    Variable   Type      Data/Info
    ------------------------------
    dss        module    <module 'school.dss.data1<...>\\school\\dss\\data1.py'>
    np         module    <module 'numpy' from 'C:\<...>ges\\numpy\\__init__.py'>
    packages   SList     ['__future__.py', '__phel<...>file.py', 'zipimport.py']
    path       str       C:\Users\USER\.ipython
    random     module    <module 'random' from 'C:<...>aconda3\\lib\\random.py'>
    school     module    <module 'school' (namespace)>
    sys        module    <module 'sys' (built-in)>
    url        module    <module 'school.web.url' <...>on\\school\\web\\url.py'>
    


```python
data1.plus(1,2)
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-64-572e254ac59d> in <module>
    ----> 1 data1.plus(1,2)
    

    NameError: name 'data1' is not defined



```python
# uninstall
# pip uninstall dss
```


```python
!pip list | grep dss
```


```python

```
