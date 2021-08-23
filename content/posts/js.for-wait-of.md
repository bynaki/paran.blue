---
title: "Js :: for wait...of"
date: 2021-08-09T18:36:53+09:00
draft: false
# weight: 1
# aliases: ["/first"]
tags: ["js", "async", "wait", "promise"]
categories: ["Javascript"]
author: "bynaki"
showToc: true
TocOpen: false
hidemeta: false
comments: false
# description: "Desc Text."
canonicalURL: "https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for-await...of"
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



## for await...of

**`for await...of` 구문**은 보통 비동기에 대응하는 열거자를 나열할 때 쓰이지만, [`String`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String), [`Array`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array), `Array` 같은 객체 (e.g., [`arguments`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/arguments) or [`NodeList`](https://developer.mozilla.org/en-US/docs/Web/API/NodeList)), [`TypedArray`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/TypedArray), `Map`, [`Set`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Set) 같은 동기적으로 열거 가능한 객체 또한 가능하며, 사용자가 직접 정의한 동기 또는 비동기 객체도 나열할 수 있도록 해준다. 일반적인 **`for ...of`** 문과 마찬가지로 열거자 심볼이 정의한 속성을 실행하게 되어 열거한 값을 변수로 받아 처리한다.



## [구문](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for-await...of#구문)

```js
for await (variable of iterable) {
  statement
}
```

- `variable`

  열거할 때마다 `variable`. 문을 통해 변수로 받을 수 있다. `variable` 문 안에서는 `const`, `let` 및 `var`. 문으로 선언된 변수 및 상수를 선언할 수 있다.

- `iterable`

  열거 가능한 속성이 들어가 있는 객체 및 식을 포함한다.



### [비동기 열거 속성을 통한 열거 식](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for-await...of#비동기_열거_속성을_통한_열거_식)

비동기 열거 프로토콜을 담은 객체를 아래와 같이 열거할 수 있다.

```js
const asyncIterable = {
  [Symbol.asyncIterator]() {
    return {
      i: 0,
      next() {
        if (this.i < 3) {
          return Promise.resolve({ value: this.i++, done: false });
        }

        return Promise.resolve({ done: true });
      }
    };
  }
};

(async function() {
   for await (let num of asyncIterable) {
     console.log(num);
   }
})();

// 0
// 1
// 2
```



### [비동기 생성자를 통한 열거 식](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for-await...of#비동기_생성자를_통한_열거_식)

비동기 생성자는 애초부터 비동기 열거 프로토콜을 탑재한 채로 정의한다.이를 `for await...of` 식으로 아래와 같이 사용할 수 있다.

```js
async function* asyncGenerator() {
  let i = 0;
  while (i < 3) {
    yield i++;
  }
}

(async function() {
  for await (let num of asyncGenerator()) {
    console.log(num);
  }
})();
// 0
// 1
// 2
```

좀 더 상세한 비동기 생성자를 통한 `for await...of `식의 사용법을 위해 기본 API를 통해 값을 비동기적으로 열거하는 방법을 알아본다.

아래 예제를 통해 먼저 API를 사용하여 스트림 데이터를 통해 비동기 열거자를 만든 뒤, 스트림에서 응답이 끝나면 최종 응답 데이터 크기를 가져온다.

```js
async function* streamAsyncIterator(stream) {
  const reader = stream.getReader();
  try {
    while (true) {
      const { done, value } = await reader.read();
      if (done) {
        return;
      }
      yield value;
    }
  } finally {
    reader.releaseLock();
  }
}
// 주소로부터 데이터를 받아온 뒤, 응답 크기를 구하는 비동기 생성자 함수.
async function getResponseSize(url) {
  const response = await fetch(url);
  // 여기에 응답 크기를 바이트 단위로 적재한다.
  let responseSize = 0;
  // for-await-of 문을 통해 응답이 들어올 때마다 열거 프로토콜을 통해 반복문이 작동한다.
  for await (const chunk of streamAsyncIterator(response.body)) {
    // 총 응답 크기를 지속적으로 누적한다.
    responseSize += chunk.length;
  }

  console.log(`응답 크기: ${responseSize} 바이트`);
  // 예상 출력: "응답 크기: 1071472 바이트"
  return responseSize;
}
getResponseSize('https://jsonplaceholder.typicode.com/photos');
```



## My Example

```js
export class TradeDb {
  constructor(private readonly filename: string) {
  }
  // *
  // *
  // *

  async * each(code: string): AsyncGenerator<Iu.TradeTickType, void, unknown> {
    const length = 500
    let offset = 0
    let trs = []
    do {
      trs = await this.get(code, offset, length)
      for(let tr of trs) {
        yield tr
      }
      offset += trs.length
    } while(trs.length !== 0)
  }
}
```



```js
export class UPbitTradeMock extends BaseUPbitSocket {
  constructor(private readonly db: TradeDb) {
    super(db.staticCodes())
  }

  async open(): Promise<void> {
    await this.start()
    const codes = await this.db.codes()
    for(let code of codes) {
      const bots = this.getBots(I.ReqType.Trade, code)
      for await (let tr of this.db.each(code)) {
        const converted = this.convertTradeType(tr)
        await Promise.all(bots.map(bot => bot.trigger(converted)))
      }
      await Promise.all(bots.map(bot => bot.finish()))
    }
  }
}
```



## See Also

- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for-await...of

