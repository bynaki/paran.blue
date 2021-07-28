---
title: "Js :: Generator"
date: 2021-07-26T01:18:06+09:00
draft: false
# weight: 1
# aliases: ["/first"]
tags: ["js"]
categories: ["Javascript"]
author: "bynaki"
showToc: true
TocOpen: false
hidemeta: false
comments: false
# description: "Desc Text."
canonicalURL: "https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Generator"
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



# Generator

`**Generator**` 객체는 [generator function](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/function*) 으로부터 반환된 값이며 [반복자와 반복자 프로토콜](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols)을 준수합니다.



## [문법](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Generator#문법)

```js
function* gen() {
  yield 1;
  yield 2;
  yield 3;
}

var g = gen(); // "Generator { }"
```



## [메서드](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Generator#메서드)

- [`Generator.prototype.next()`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Generator/next)

  [`yield`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/yield) 표현을 통해 yield된 값을 반환합니다.

- [`Generator.prototype.return()`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Generator/return)

  주어진 값을 반환하고 생성기를 종료합니다.

- [`Generator.prototype.throw()`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Generator/throw)

  생성기로 에러를 throw합니다.



## [예시](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Generator#예시)

### [무한 반복자](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Generator#무한_반복자)

```js
function* idMaker(){
    var index = 0;
    while(true)
        yield index++;
}

var gen = idMaker(); // "Generator { }"

console.log(gen.next().value); // 0
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
// ...
```



## See Also

- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Generator

