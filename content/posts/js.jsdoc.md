---
title: "Js :: JsDoc"
date: 2021-08-23T20:28:29+09:00
draft: false
# weight: 1
# aliases: ["/first"]
tags: ["jsdoc", "js"]
categories: ["Javascript"]
author: "bynaki"
showToc: true
TocOpen: false
hidemeta: false
comments: false
# description: "Desc Text."
canonicalURL: "https://velog.io/@yijaee/JSDoc을-사용해-JavaScript-파일-문서화하기"
disableHLJS: false # to disable highlightjs
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: false
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/bynaki/paran.blue/blob/main/content"
    Text: "Edit" # edit text
    appendFilePath: true # to append file path to Edit link
---



## JSDoc이란?

JSDoc은 Javadoc과 유사한 JavaScript용 API 문서 생성기이다. 문서 주석을 코드와 함께 소스 코드에 직접 추가할 수 있다. JSDoc은 소스 코드를 스캔하고 HTML 문서를 생성한다.

JSDoc의 주목적은 JavaScript 앱 또는 라이브러리 API를 문서화하는 것이다. 모듈, 네임스페이스, 클래스, 메서드, 파라미터 등과 같은 항목을 문서화할 것으로 가정한다.

일반적으로 JSDoc 주석은 코드가 문서화되기 직전에 배치되어야 한다. 각 주석은 `/**` 시퀀스로 시작해야 JSDoc 파서가 인식할 수 있다. `/*`, `/***` 으로 시작되는 설명은 무시된다.



## JSDoc을 사용해서 무엇을 할 수 있을까?

1. API 문서 생성

   가장 쉽게 생성하는 문서는 바로 API 문서이다. 프론트엔드 개발자가 서버에 어떤 데이터를 요청할 수 있고, 어떤 데이터를 응답받는지를 확인할 때 필수적으로 사용되는 것이 API 문서인데, 여기에는 기본적인 응답 요청 방식과 요청시 첨부되어야 하는 값 등이 기술된다.

1. 타입 추론

   또한 함수의 반환값, 파라미터의 타입, 적절한 파라미터가 전달되지 않았을 때의 에러 메시지 등 다양한 내용을 주석으로 작성할 수 있기 때문에 TypeScript를 사용하는 것처럼 타입을 추론하고 디버깅을 쉽게 할 수 있다는 장점이 있다.

1. 버그 픽스 리포트

   [주석 분석기를 이용한 간단한 API 문서화 방법](https://engineering.linecorp.com/ko/blog/comments-parsing-api-documentation/)에서 소개한 방법처럼 버그 픽스 리포트로 사용할 수도 있겠다. 버전 별로 개선점 등을 작성하면 어떤 목적과 방향으로 개발이 진행되어 왔는지 한눈에 알 수 있을 것이다.



## 기본 사용법

```javascript
/** foo 함수에 대한 주석을 여기에 작성한다 */
function foo() {
}
```

특수 JSDoc 태그를 사용하면 더 많은 정보를 제공할 수 있고, 실제로 JSDoc을 사용하는 목적이 여기에 있다. 예를 들어 함수가 클래스의 생성자일 경우 @constructor 태그를 사용해 다음과 같이 작성할 수 있다.

```javascript
/**
 * Book 함수
 * @constructor
 */
function Book(title, author) {
}
```

이외에도 다양한 JSDoc 태그를 사용할 수 있다.

```javascript
/**
 * Book 함수
 * @constructor
 * @param {string} title - The title of the book.
 * @param {string} author - The author of the book.
 */
function Book(title, author) {
}
```

Javadoc 가이트 템플릿을 참고해 다음과 같이 꼼꼼하게 주석을 작성할 수 있다.

```javascript
/**
* 기본 작성 기준
* boolean 값이라면 언제 true이고 언제 false인지 작성
* 숫자라면 범위나 값의 의미를 작성
* enum이면 어떤 값을 쓸 수 있는지 나열
* 이 메서드를 호출하기 전후에 해야하는 작업이 있다면 해당 내용을 작성
* 특정 상황에서 이 메서드를 사용하지 않아야 한다면 해당 내용을 작성

* @global 전역에 해당하는 내용을 작성

* @function 어떤 파라미터를 받아서 어떤 값을 반환하는 함수인지 작성

* @param 어떤 타입의 파라미터를 전달해야 하는지 작성
* 허락되지 않은 파라미터를 전달했을 때 어떤 일이 발생하는지 작성

* @return 무엇을 반환해야 하는지 작성
* 문제가 발생했을 때 일반 상황과 다른 의미의 값을 반환한다면 해당 내용을 작성

* @callback 전역인지 지역인지 구분 및 어떤 함수인지 작성

* @event 어떤 이벤트인지 작성
*/
```

각 소스 코드에 맞는 JSDoc 태그의 사용법은 https://jsdoc.app/ 에서 확인하자.



## JSDoc 사용해보기

이제 JSDoc을 직접 사용해보자. 간단하게 사칙연산에 대한 문서를 작성하려고 한다.

JSDoc을 테스트 해 볼 새로운 폴더를 생성해 기본 환경 세팅한다.

```shell
$ mkdir test-jsdoc && cd test-jsdoc
$ npm init -y
$ touch index.js
$ npm i -d jsdoc
```

여기까지 하면 JSDoc을 사용하기 위한 준비를 마쳤다.

이제 루트 위치에 있는 `index.js` 파일에 덧셈을 하는 함수에 대한 주석을 작성해보자.

```javascript
/** @function addition
 * @param {number} a 연산하고자 하는 0 이상의 정수
 * @param {number} b 연산하고자 하는 0 이상의 정수
 * @returns {number} a + b
 */

const addition = (a, b) => a + b;
```



### 문서화 하기

이제 작성한 주석을 확인해야 한다. 터미널에서 다음 명령어를 입력한다.

```shell
$ ./node_modules/.bin/jsdoc index.js
```

명령어가 굉장히 긴데, webpack을 사용해 npm 명령어를 사용하는 방법이 하단에 소개되어 있다. 다만 로컬로 JSDoc을 설치하지 않고 다음과 같이 전역으로 설치했다면

```shell
$ npm install -g jsdoc
```

컴파일할 때 좀 더 간편한 명령어를 사용할 수 있다.

```shell
$ jsdoc ./index.js
```

다만 여기서는 로컬에 설치했다고 가정하고 엄청나게 긴 명령어 `./node_modules/.bin/jsdoc index.js`를 입력해보자.

그러면 다음과 같이 `out` 폴더가 생성된다.

![img](https://user-images.githubusercontent.com/47887717/112429877-a9db8b80-8d80-11eb-9f1f-9bc9854bc4e9.png)

생성된 `out` 폴더 내부에 있는 `index.html`을 열면 문서화 된 주석 내용을 확인할 수 있다.

![img](https://user-images.githubusercontent.com/47887717/112429908-b6f87a80-8d80-11eb-819b-457770a49633.png)

`index.js`에 작성했던 `addition` 함수에 관한 주석이 생성된 것이 보인다.

![img](https://user-images.githubusercontent.com/47887717/112429938-c7105a00-8d80-11eb-8dc9-a14a32b3ae17.png)

이번에는 뺄셈에 관한 함수를 추가해보자.

```javascript
/** 
 * a는 b보다 크거나 같다
 * a가 b보다 적은 수라면 -1을 반환한다
 * @function subtraction
 * @param {number} a 연산하고자 하는 0 이상의 정수
 * @param {number} b 연산하고자 하는 0 이상의 정수
 * @returns {number} a - b
 */

const subtraction = (a, b) => a >= b ? a - b : -1;
```

그러면 문서는 다음과 같이 작성된다. `Global` 아래 `addition` 함수와 `subtraction` 함수가 나열된다.

![img](https://user-images.githubusercontent.com/47887717/112429963-d2638580-8d80-11eb-9694-ed0a0ec85875.png)

우측의 메뉴를 누르면 해당 함수 위치로 이동한다.



### 구분된 폴더 내부의 .js 모두 문서화하기

만약 모든 함수를 루트 위치에 있는 `index.js`에 작성하지 않고 src 폴더를 만들어 폴더 내부의 .js 파일에 작성하면 어떻게 문서가 만들어질까? 그래서 이번에는 src 폴더를 만들고 폴더 내부에 `test.js` 라는 파일을 만들어 곱셈에 대한 함수를 작성해보았다.

```javascript
/** @function multiplication
 * @param {number} a 연산하고자 하는 0 이상의 정수
 * @param {number} b 연산하고자 하는 0 이상의 정수
 * @returns {number} a * b
 */

const multiplication = (a, b) => a * b;
```

작성한 주석을 확인해보자.

```shell
./node_modules/.bin/jsdoc src/test.js
```

이미 문서로 만들어진 `index.js`는 그대로 존재하고 거기에 곱셈에 관한 함수가 추가될 거라고 생각했는데 실제로는 기존에 작성했던 주석이 사라지고 방금 작성한 주석만 남아있다.

![img](https://user-images.githubusercontent.com/47887717/112429993-df807480-8d80-11eb-8fcb-da0e2b51817d.png)

경로를 직접 입력하며 문서를 만드는 경우에는 다음과 같이 모든 경로를 다 써줘야 처음에 생각했던 대로 모든 문서가 합쳐진 하나의 문서가 만들어진다.

```shell
./node_modules/.bin/jsdoc index.js src/test.js
```

이 방법은 너무 번거롭고 효율적이지도 못하기 때문에 폴더 내부의 모든 js, jsx, jsdoc 확장자를 가진 파일이 한꺼번에 동작할 수 있도록 설정 파일을 수정해보자.



## 설정 파일을 수정해 JSDoc 편리하게 사용하기

루트 위치에 `jsdoc.config.json` 이라는 이름을 가진 파일을 하나 생성한다. 그리고 위에서 언급한 확장자를 가진 파일을 모두 문서로 만들어줄 수 있도록 객체를 만들어주자.



### 기본 설정

기본 공식 문서에 나와있는 기본 설정값은 다음과 같다.

```json
{
    "plugins": [],
    "recurseDepth": 10,
    "source": {
        "includePattern": ".+\\.js(doc|x)?$",
        "excludePattern": "(^|\\/|\\\\)_"
    },
    "sourceType": "module",
    "tags": {
        "allowUnknownTags": true,
        "dictionaries": ["jsdoc","closure"]
    },
    "templates": {
        "cleverLinks": false,
        "monospaceLinks": false
    }
}
```

1. plugins: 플러그인 사용시 추가하는 부분. 기본값은 빈 상태이다.
2. recurseDepth: `-r` 명령 행 플래그로 재귀를 사용하면 JSDoc은 10 레벨 깊이의 파일을 검색한다.
3. source.includePattern: js, jsx, jsdoc으로 끝나는 파일만 처리한다.
4. source.excludePattern: 밑줄로 시작하거나 밑줄로 시작하는 디렉토리의 모든 파일은 무시한다.
5. sourceType: ES2015 모듈을 사용하는 코드를 지원한다.
6. tags.allowUnknownTags: JSDoc에서 인식할 수 없는 태그를 사용할 수 있다.
7. tags.dictionaries: 표준 JSDoc 태그와 Closure Compiler 태그가 모두 활성화 된다.
8. templates.cleverLinks, templates.monospaceLinks: 인라인 {@link} 태그는 일반 텍스트로 렌더링 된다.

기본 설정을 입력하고, 이 설정대로 문서를 만드는 명령어는 다음과 같다.

```shell
./node_modules/.bin/jsdoc -c jsdoc.config.json .
```

이렇게 문서를 만들면 아래와 같은 문서가 만들어진다.

![img](https://user-images.githubusercontent.com/47887717/112430022-eb6c3680-8d80-11eb-8bfc-72faa7daee9a.png)

src 폴더에 만들었던 `multiplication` 함수에 대한 문서가 사라졌다. 폴더가 구분이 되어있어서 발생하는 문제인데, 루트 위치가 아닌 폴더에 있는 js 파일에 대한 문서화도 함께 진행하려면 설정값을 조금 수정해야 한다.



### 폴더 내부 파일 문서화 지원 설정

`source` 객체 내부에 `"include": ["폴더명"],` 를 추가해준다. 배열이기 때문에 루트 위치와 특정 폴더 위치를 모두 삽입해준다. `source` 객체는 다음과 같은 형태로 구성된다.

```json
"source": {
        "include": [".", "src"],
        "includePattern": ".+\\.js(doc|x)?$",
        "excludePattern": "(^|\\/|\\\\)_"
    },
```

설정 값을 수정하고 다시 문서를 만들면 의도했던 대로 모든 .js 파일을 문서로 확인할 수 있다!

![img](https://user-images.githubusercontent.com/47887717/112430056-f6bf6200-8d80-11eb-9f12-4b957047f674.png)

### README.md 추가하기

문서화는 완료됐는데 문서로 진입하기 전 메인 화면이 텅 비어있으니 너무 썰렁하다. 여기에 README.md를 추가해서 문서에 관한 간단한 설명을 작성해보자. 루트 위치에 `README.md`를 생성하고 다음과 같이 작성한다.

```markdown
# 사칙연산 문서

## [addition](global.html#addition)

## [subtraction](global.html#subtraction)

## [multiplication](global.html#multiplication)
```

이제 JSDoc이 md 파일을 인식할 수 있도록 해야 한다. 설정으로 돌아가 `plugins`와 `opts`를 아래와 같이 변경한다.

```json
"plugins": [
  "plugins/markdown"
],

"opts": {
  "readme": "README.md"
}
```

설정값을 변경한 후 문서를 만들면 아래와 같이 메인 화면이 변경된다.

![img](https://user-images.githubusercontent.com/47887717/112430100-03dc5100-8d81-11eb-9476-c70bcc03a923.png)

링크를 클릭하면 해당 함수의 설명 위치로 가는 README.md 파일이 생성되었다!

추가로 Docs에서 한글을 사용하는데 무리가 없도록 인코딩 설정을 수정하면 기본적인 설정은 완료된다.

```json
"opts": {
        "encoding": "utf8",
        "readme": "README.md"
    }
```



## webpack으로 문서화 명령어 변경하기

지금까지는 매번 `./node_modules/.bin/jsdoc -c jsdoc.config.json .` 명령어를 사용해서 문서화를 했다. 이것도 설정 파일을 만들기 전에는 `index.js`, `src/test.js` 하는 식으로 직접 경로까지 지정해줬어야 했는데 설정 파일을 만들면서 .js 파일을 몇 개를 더 만들든 같은 명령어로 동작할 수 있게 되었다.

하지만 조금 개선됐다고 하더라도 컴파일 명령어 자체가 너무 길고 파일에 변화가 있을 때마다 매번 이렇게 긴 명령어를 입력해야 한다는 단점이 있다. 이걸 좀 더 간단한 명령어를 사용할 수는 없을까? webpack을 사용하면 이런 문제를 해결할 수 있다.

먼저 `webpack`과 `jsdoc-webpack-plugin`을 설치하자.

```shell
$ npm i -d webpack webpack-cli jsdoc-webpack-plugin
```

설치가 완료됐으면 루트 위치에 `webpack.config.js` 파일을 생성해 webpack에 대한 설정을 한다.

```javascript
const path = require("path");
const JsDocPlugin = require("jsdoc-webpack-plugin");

module.exports = {
  entry: "./index.js",
  output: {
    path: path.join(__dirname, "dist"),
    filename: "main.js"
  },
  plugins: [
    new JsDocPlugin({
      conf: "jsdoc.config.json",
      cwd: ".",
      preserveTmpFile: false
    })
  ]
};
```

그리고 `package.json` 파일에서 `start` 명령어를 추가해준다.

```json
"scripts": {
    "start": "webpack"
  },
```

이제 `npm start` 라고 명령어를 입력하면 문서화 작업을 진행할 수 있다.

------

**참고**

- [JSDoc 3.5 (한국어)](https://runebook.dev/ko/docs/jsdoc/-index-)
- [Javascript Documentation 라이브러리 JSDoc를 사용해 봅시다](https://noogoonaa.tistory.com/36)
- [주석 분석기를 이용한 간단한 API 문서화 방법](https://engineering.linecorp.com/ko/blog/comments-parsing-api-documentation/)
