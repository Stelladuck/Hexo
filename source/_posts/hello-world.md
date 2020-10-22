---
title: Hello World + Hexo 설치
mathjax: true
---
Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

다양한 깃블로그를 구경하다가 NexT라는 테마가 마음에 들어 설치해보고자 마음을 먹었다. 우여곡절 끝에 Ubuntu 20.04(혹은 18.04)에 설치하는 것은 성공적이었지만 깃 사용법에 익숙하지 않고 웹서버와 관련된 지식이 전혀 없다보니 여러 시행착오가 있었다. 이 글은 필자가 겪었던 비슷한 어려움에 직면한 이들을 위해 작게나마 도움이 되는 전반적인 방법을 제공한다. 부디 도움이 되길 바란다.

$$\begin{equation*}
\sum_{\delta \in \omega}\kappa(\delta, A) \approx \lim_{x \to q}\left[\frac{\Omega^{\hbar}(x;q)}{3n}\prod_{\delta\in\omega}f(y;\delta)\right]
\end{equation*}$$

## 헥소(Hexo)를 다루기 이전에

### 헥소란 무엇인가?

핵소(Hexo)논 지킬(Jekyll)처럼 강력한 블로그 프레임워크다. 다만 큰 차이점으로 지킬은 Ruby기반이며 헥소는 node.js를 기반으로 하였다. 또한 node.js를 사용하는 헥소는 지킬보다 빠른 속도를 자랑하는 것이 큰 장접이다. 이 글은 node.js와 npm을 설치하는 방법과 헥소를 설정하는 방법을 제공한다.

### Git 설치하기

엄청 간단하다. 다음 명령어를 터미널에 입력하자.
``` bash
$ sudo apt install git
```
깃을 아직 사용할 줄 모른다 하여도 괜찮다. 이미 깃 사용법과 관련된 글들은 구글을 포함하여 많은 포털사이트에서 쉽게 찾을 수 있기 때문이다.

### NVM을 이용해 node.js와 npm 설치하기

헥소를 설정하기 이전에 PC에 먼저 node.js와 npm이 설치되어야 한다. 보통 node.js를 설치하면 npm도 같이 설치가 되기 때문에 이 둘을 분리하여 다룰 필요는 없을 듯 하다. [여기](https://linuxize.com/post/how-to-install-node-js-on-ubuntu-18.04/)를 보면 여러 설치방법이 있지만 헥소를 다루기 위해서는 NVM을 이용해 설치하는 두 번째 방법을 사용해야 할 것 같다. 그 이유로, 첫 번째 방법으로 설치하니 `EACCES`허가에러가 발생하였고 [이 웹페이지](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally)가 서술하길 해당 에러가 발생할 경우 NVM을 이용해 다시 설치하라고 권장한다.

## 헥소(Hexo) 설정하기

### 헥소 설정방법

초기에는 npm을 사용하여 헥소를 전역으로 설치한다.
``` bash
$ npm install hexo-cli -g
```
그 후에는 원하는 공간에 블로그를 위한 디렉토리를 하나 만든다. 필자는 간단히 Home에 Blog라는 디렉토리를 하나 생성했다.
``` bash
$ mkdir Blog
```
그 다음 해당 디렉토리로 이동하여 노드 모듈을 설치한다.
``` bash
$ hexo init hexo
```
기본적인 것은 완료하였다. 로컬에서 웹페이지를 확인하려면 아래 명령어를 치면 된다.
``` bash
$ hexo server -o
```

### Deployer 설치하기

다음으로 해야할 것은 깃에 업로드 하는 것이다. 이를 시행하기 위해서는 Deployer플러그인을 설치해야 한다. 
``` bash
$ npm install hexo-deployer-git --save
```
그리고 나서 루트(즉 Blog 디렉토리)에 있는 `_config.yml`파일을 수정해줘야 한다. 헥소를 잘 다룰 줄 아는 사람은 알아서 잘 하겠지만 본인은 헥소를 처음 접하기 때문에 아주 기본적인 정보만 수정해주었다. 먼저 사이트 정보를 변경한다.
```
title: STELLADUCK + MATH/PHYS
subtitle: ''
description: 별덕의 수리물리학 블로그
keywords:
author: Sanghoon Lee (Stelladuck)
language: ko
timezone: Asia/Seoul
```

그 다음 url 정보도 변경해준다.
```
url: http://stelladuck.github.io
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:
pretty_urls:
  trailing_index: true # Set to false to remove trailing 'index.html' from permalinks
  trailing_html: true # Set to false to remove trailing '.html' from permalinks
```

마지막으로 Deployment 정보도 변경해준다.
```
deploy:
  type: git
  repo: https://github.com/Stelladuck/stelladuck.github.io.git
  branch: master
```

### 테마 설정하기

마지막으로 테마를 설정해야 한다. 필자는 [NexT](https://github.com/theme-next/hexo-theme-next)라는 테마가 마음에 들었다. 설치를 위해 `git clone`명령을 사용하자.
``` bash
$ git clone https://github.com/theme-next/hexo-theme-next.git themes/next
```
그러면 themes 하위에 있는 next라는 디렉토리에 필요한 것들이 추가되어 있을 것이다. 테마를 제공하기 위해 다시 루트에 있는 `_config.yml`에 가서 테마를 `landscape`에서 `next`로 바꿔준다.
``` bash
theme: next
```

## 빠른 시작을 위한 메뉴얼

### 헥소 초기화
우선 초기화를 통해 정적 데이터를 삭제하자. 참고로 아직까지 Blog 디렉토리에 있다는 것을 잊지 말자.
``` bash
$ hexo clean
```

### 새로운 글 만들기

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### 서버 실행하기

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### 동적파일 생성하기

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### 배포하기

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/one-command-deployment.html)

생성과 배포는 한번에 할 수 있다.
``` bash
$ hexo generate -deploy
```
배포 명령을 시행하면 깃 유저이름과 비밀번호를 입력하라고 한다. 입력 후 해당 `<username>.github.io`에 해당하는 레포지토리에 가면 업로드 되어있는 것을 확인할 수 있다. 그리고 블로그도 제대로 만들어져 있는지 확인해보자.
