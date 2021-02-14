---
title: Hexo gitblog 만들기
date: 2021-02-14 00:36:29
tags: "hexo"
categories: "BLOG"
---


## 개요

- `Hexo` 블로그를 만들어 본다. 

### 1. 파일 설치

- 1단계 : [nodejs.org](https://nodejs.org/en/) 다운로드
    - 설치가 되었는지 확인해본다.


```python
$ node -v
```

- 2단계 : [git-scm.com](https://git-scm.com/) 다운로드
    - 설치가 되었는지 확인해본다.


```python
$ git --version
```

- 3단계 : hexo 설치
    - npm을 통해 hexo를 설치한다.


```python
$ npm install -g hexo-cli
```

### 2. 깃허브 설정

- 두개의 깃허브 `Repo`를 생성한다.
    - 포스트 버전관리 (name : myblog)
    - 포스트 배포용 관리 (name : USERNAME.github.io)
    - `USERNAME` 대신에 본인의 `username`을 입력하면 된다.
- 생성 후, `myblog repo`를 `git clone`을 통해 적당한 경로에 내려 받는다.


```python
$ git clone your_git_repo_address.git
```

### 3. 블로그 만들기

- 내려받은 `myblog`의 경로를 찾아 들어간다.
- `myblog`폴더 안에 임의의 블로그 파일명을 만든다.


```python
$ hexo init gitblog # 임의의 파일명
$ cd gitblog
$ npm install
$ npm install hexo-server --save
$ npm install hexo-deployer-git --save
```

- `_config.yml` 파일 수정
    - 싸이트 정보 수정


```python
title: 제목을 지어주세요
subtitle: 부제목을 지어주세요
description: description을 지어주세요
author: YourName
```

- 블로그 URL 정보 설정


```python
url: https://USERNAME.github.io
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:
```

- 깃허브 연동


```python
# Deployment
deploy:
  type: git
  repo: https://github.com/USERNAME/USERNAME.github.io.git
  branch: main
```

### 4. 깃허브에 배포하기

- 배포 전, 로컬환경에서 블로그가 뜨는지 확인해본다.


```python
$ hexo generate
$ hexo server
INFO  Start processing
INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
```

- 확인이 되면 깃허브에 배포한다.

- 사전에, `gitignore` 파일에서 아래와 같이 설정을 진행한다.


```python
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
```

- 최종적으로 배포을 진행한다.


```python
$ hexo deploy
```

- 배포가 완료가 되면 브라우저에서 USERNAME.github.io로 접속해 정상적으로 배포가 되었는지 확인한다.

### 5. 테마 설정하기

- `ICARUS` 테마로 변경


```python
$ git submodule add https://github.com/ppoffice/hexo-theme-icarus.git themes/icarus
```

- `ICARUS` 테마 파일을 `themes` 폴더 안에 이식하는 코드다.

- 그 다음, `_config.yml`에서 `theme: icarus`로 변경한다.

- 그 다음, `hexo server` 실행 시, 에러가 날 것이다.
        - 에러 예제


```python
ERROR Package bulma-stylus is not installed.
ERROR Package hexo-component-inferno is not installed.
ERROR Package hexo-renderer-inferno is not installed.
ERROR Package inferno is not installed.
ERROR Package inferno-create-element is not installed.
ERROR Please install the missing dependencies your Hexo site root directory:
ERROR npm install --save bulma-stylus@0.8.0 hexo-component-inferno@^0.2.4 hexo-renderer-inferno@^0.1.3 inferno@^7.3.3 inferno-create-element@^7.3.3
```

- 위와 같은 에러가 발생하면, 출력되는 에러 문구에 따라 패키지들을 설치한다.


```python
$ npm install bulma-stylus
$ npm install hexo-component-inferno
$ npm install hexo-renderer-inferno
$ npm install inferno
$ npm install inferno-create-element
$ npm install --save bulma-stylus@0.8.0 hexo-component-inferno@^0.4.0 hexo-renderer-inferno@^0.1.3 inferno@^7.3.3 inferno-create-element@^7.3.3
$ hexo server # 로컬에서 확인
```

- 로컬 테스트가 완료되면, 깃허브로 배포를 진행한다.


```python
$ hexo deploy --generate
```

- 마지막으로, 포스트 버전관리를 위해 수정된 내용을 깃허브에 업데이트를 진행한다.


```python
$ git add .
$ git commit -m "add: new post updated"
$ git push origin master
```

### 6. 다른환경에 작업하기

- 새로운 위치에 `myblog`를 `clone`해 준다.

- `myblog`폴더 안에 `gitblog`폴더 로 이동 후, `hexo server`로 확인을 하면 에러가 날 것이다.
        - 에러 예제


```python
ERROR Cannot find module 'hexo' from 'C:\myblog\gitblog'
ERROR Local hexo loading failed in C:\myblog\gitblog
ERROR Try running: 'rm -rf node_modules && npm install --force'
```

- 출력된 문구에 따라 실행해 준다.


```python
rm -rf node_modules && npm install --force
hexo server
```

- 로컬에서 확인이 완료되면 블로그 작업을 한다.

- 블로그 작업이 끝나면, 위와 같이 `deploy`로 배포하고, 깃허브에 `push`해 업데이트 까지 완료해준다.
