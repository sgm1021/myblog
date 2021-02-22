---
title: Jupyter notebook
date: 2021-02-22 17:32:13
tags: python
categories: programming
---

### Jupyter notebook
- mode
    - 명령모드(esc) : 셀을 수정할때 사용
    - 편집모드(enter) : 셀안의 내용을 수정할때 사용
- style
    - markdown(명령모드 + m) : 셀안에 설명을 작성할때 사용
    - code(명령모드 + y) : 파이썬 코드를 작성할때 사용
- 단축키
    - 셀 실행 : shift + enter
    - 셀 삭제 : (명령모드) x
    - 되돌리기 : (명령모드) z
    - 셀 생성 : (명령모드) a(위에), b(아래)



```python
1+2
```




    3



### Magic Command
- 셀 내부에서 특별하게 동작하는 커멘드
- % : 한 줄의 magic command를 동작
- %% : 셀단의의 magic command를 동작
- 주요 magic command
    - pwd : 현재 주피터 노트북 파일의 경로
    - ls : 현재 디렉토리의 파일 리스트
    - whos : 현재 선언된 변수를 출력
    - reset : 현재 선언된 변수를 삭제


```python
%pwd
```




    'C:\\Code\\01_python'




```python
%ls
```

     Volume in drive C is Windows10
     Volume Serial Number is E625-BBFB
    
     Directory of C:\Code\01_python
    
    2021-01-21  �삤�썑 10:03    <DIR>          .
    2021-01-21  �삤�썑 10:03    <DIR>          ..
    2021-01-21  �삤�썑 09:53    <DIR>          .ipynb_checkpoints
    2021-01-21  �삤�썑 10:03             1,905 01_jupyter_notebook.ipynb
                   1 File(s)          1,905 bytes
                   3 Dir(s)  67,438,399,488 bytes free
    


```python
%whos
```

    Interactive namespace is empty.
    


```python
%reset
```

    Once deleted, variables cannot be recovered. Proceed (y/[n])? y
    


```python
%whos
```

    Interactive namespace is empty.
    

### Shell Command
- 주피터 노트북을 실행 쉘 환경의 명령을 사용
- 명령어 앞에 !를 붙여서 실행
- 주요 명령어
    - ls, cat, echo ...


```python
!echo python
```

    python
    


```python
!ls
```

    01_jupyter_notebook.ipynb
    
