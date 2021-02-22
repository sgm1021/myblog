---
title: AWS server setting
date: 2021-02-22 17:32:13
tags: AWS
categories: Database
---

### Server Setting
1. OTP 설정
2. EC2 생성
3. FTP 서비스 : cyberduck 설치
4. pyenv 설정
5. jupyter notebook 설치
6. mysql 설치 및 설정

#### 1. OTP 설정
- AWS Console에서 내 보안 자격 증명 메뉴로 이동
- 멀티팩터인증(MFA) 선택
- MFA 활성화 버튼 선택
- 가상 MFA 디바이스 선택
- Authy 다운로드 및 회원가입
    - https://authy.com/download/ 
    - 이메일과 핸드폰 인증이 필요
    - 모바일, 데스크탑, 크롬브라우져앱 설치 가능
    - Authy 앱 실행
- Authy앱에서 Tokens에서 + 버튼을 클릭
- AWS 페이지에서 비밀키 표시 버튼을 클릭하고 나온 문자열을 Authy 앱의 Enter Code given by the website에 입력
- Account Name을 설정 후 Save
- 연속해서 나오는 Key값을 AWS 페이지의 MFA Key1, MFA Key2에 입력

#### 2. EC2 생성
- AWS Console에서 EC2 입력해서 서비스 페이지에 들어감
- 인스턴스 메뉴의 인스턴스 시작 클릭
- Ubuntu Server 18.04 LTS 선택
- t2.micro 선택
- 검토 및 시작 클릭
- 키페어 생성 및 다운로드
- 시작하기 버튼 클릭

#### 접속
- dss.pem 키파일 ~/.ssh 디렉토리로 이동
- dss.pem 파일 권한 변경
    - `$ chmod 400 ~/.ssh/dss.pem`
- 서버 접속
    - `ssh -i ~/.ssh/dss.pem ubuntu@<public ip 주소>`

#### 3. FTP 서비스
- cyberduck
    - https://cyberduck.io/download/
- filezilla
    - https://filezilla-project.org/download.php
- 서버 접속 설정
    - SFTP 선택
    - 서버 : public ip 설정
    - 사용자 이름 : ubuntu
    - SSH Private Key : dss.pem 파일 선택

#### 4. pyenv 설정
- pyenv.sh 파일을 구글 드라이브에서 다운
- cyberduck을 이용하여 서버로 파일 이동
- pyenv.sh 파일 실행
```
$ source pyenv.sh
```

#### 5. jupyter notebook 설치 및 설정
- ipython jupyter 패키지 설치
```
$ pip install ipython jupyter
```
- 설정 파일 생성
```
$ jupyter notebook --generate-conﬁg
```
- 패스워드 생성
```
$ ipython
In [1]: from notebook.auth import passwd
In [2]: passwd()
Enter password: dss
Verify password: dss
sha1:6600c5733ef3:b683d6afba16b3403fdf9a75ac38b7d8e7f733bb
```
- 설정파일 접속
```
$ sudo vi /home/ubuntu/.jupyter/jupyter_notebook_conﬁg.py 
```
- 설정 파일 수정
```
c.NotebookApp.ip = '172.31.26.225' # 내부 IP 주소
c.NotebookApp.open_browser = False
c.NotebookApp.password = 'sha1:6600c5733ef3:b683d6afba16b3403fdf9a75ac38b7d8e7f733bb' 
```
- 서버의 8888 포트 활성화
- 서버에서 jupyter notebook 실행
- 브라우져로 접속
    - `http://<public ip>:8888`

#### 6. Mysql 설치 및 설정

- mysql-server, mysql-client 설치
    - `$ sudo apt install mysql-server`
- mysql 보안 설정 ( n-y-n-y-y 순으로 입력해줍니다. ) 
    - `$ sudo mysql_secure_installation`
    
```

- Would you like to setup VALIDATE PASSWORD plugin? Press y|Y for Yes, any other key for No: n
- 패스워드 설정 : dss
- Remove anonymous users? (Press y|Y for Yes, any other key for No) : y
- Disallow root login remotely? (Press y|Y for Yes, any other key for No) : n
- Remove test database and access to it? (Press y|Y for Yes, any other key for No) : y
- Reload privilege tables now? (Press y|Y for Yes, any other key for No) : y
```

- 최초 패스워드 설정

```
$ sudo mysql
mysql> SELECT user,authentication_string,plugin,host FROM mysql.user;
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'dss';
mysql> FLUSH PRIVILEGES;
mysql> SELECT user,authentication_string,plugin,host FROM mysql.user;
mysql> exit
```

- 접속

```
$ mysql -u root -p
Enter password: dss
```

- 외부 접속 허용
    - mysql 설정파일 bind-address = 0.0.0.0 으로 수정 
        - `$ sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf`        
        ```
        bind-address = 0.0.0.0
        ```
        - 외부접속이 허용되도록 mysql 설정
        ```
        mysql> grant all privileges on *.* to 'root'@'%' identified by 'dss';
        ```
        - 재시작으로 설정 적용
        ```
        $ sudo systemctl restart mysql.service
        ```
        - 서버의 3306 포트 활성화

#### database management application
- windows
    - heidiSQL
    - https://www.sequelpro.com/
- mac
    - Sequel Pro
    - https://www.heidisql.com

#### Save Sample Data
- https://dev.mysql.com/doc/index-other.html
- world database zip 파일 다운로드
- 압축 해제 후 world.sql 파일을 서버로 이동
- database management app을 이용하여 world 데이터 베이스 생성
- 데이터 저장 방법 1
```
$ mysql -u root -p world < world.sql
```
- 데이터 저장 방법 2
```
sql> create database world;
sql> use world;
sql> source world.sql
```
