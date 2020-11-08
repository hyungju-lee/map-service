## Node.js

Node.js는 JavaScript 런타임이다.  
런타임이란 프로그래밍 언어가 구동되는 환경을 뜻한다.  
JavaScript는 원래는 브라우저에서만 돌아가는 언어였음에도 불구하고 현재는 현재는 Node.js를 통해서 다양한 부분, 
서버라던지 다른 부분에서 활용되고 있다.

## npm (Node Package Manager)

npm이란 node package manager를 뜻하는데, 모듈에 대한 개념을 먼저 알고가면 좋을 것 같다.  

## 모듈

모듈이란 어플리케이션을 구성하는 개별적 요소를 뜻한다.  
모듈을 사용함으로써 기능적으로 분리가 되고 개발 효율성과 유지보수성이 향상된다.  
npm은 이러한 모듈들을 패키지화 하여 모아둔 저장소 역할을하고 또 이를 설치하고 관리해주는 툴이다.  

## Node 설치확인 명령어

```bash
node --version
node -v

npm --version
npm -v
```

## express 및 nodemon 설치, 실행하기

```bash
npm i -g nodemon
```

`-g` 플래그는 글로벌로 설치하여 프로젝트 폴더경로 상관없이 모든 곳에서 **nodemon** 패키지를 쓸 수 있도록 해주는 것이다.  
**nodemon** 패키지는 서버를 껐다 켰다하는 그런 불편함을 좀 해소시켜주는 패키지라고 보면 되겠다.  

```bash
npm i -g express-generator
```

동일하게 `global`로 설치를 할 거고 `express`는 웹 서버를 쉽게 만들 수 있는 프레임워크이다.  

## express 를 활용하여 프로젝트 생성하기

```bash
express --ejs (프로젝트명)
express --ejs myfirstmap
```

위와 같은 명령어를 실행하게 되면 myfirstmap 폴더가 생성되고 자연스럽게 프레임워크가 생성되는 것을 알 수 있다.

![](/img/image00.jpg)

```bash
cd myfirstmap
```

myfirstmap 폴더로 이동하고

```bash
npm i
```

해당 `package.json`에 명시되어있는 패키지를 설치한다.

---

이제 기본 준비는 끝났다.  
아까 설치했던 **nodemon** 패키지를 통해서 서버를 한번 켜 보도록 하겠다.  

```bash
nodemon ./bin/www
```

![](/img/image01.jpg)
![](/img/image02.jpg)

