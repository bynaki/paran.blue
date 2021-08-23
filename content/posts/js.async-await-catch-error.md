---
title: "Js :: async/await Catch Error"
date: 2021-08-16T19:58:31+09:00
draft: false
# weight: 1
# aliases: ["/first"]
tags: ["js", "async", "await"]
categories: ["Javascript"]
author: "bynaki"
showToc: true
TocOpen: false
hidemeta: false
comments: false
# description: "Desc Text."
# canonicalURL: ""
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



async function을 바로 return하면 error를 catch 하지 못한다.

```js
let count = 0
function asyncFunc() {
  return new Promise((resolve, reject) => {
    if(count % 10 === 0) {
      count++
      reject(new Error('error!!'))
      return
    }
    resolve(++count)
  })
}

async function bad() {
  try {
    // await 하지 않고 바로 리턴하면 에러를 캣치하지 못한다.
    return asyncFunc()
  } catch(e) {
    console.log(e.message)
    return asyncFunc()
  }
}

async function right() {
  try {
    const res = await asyncFunc()
    return res
  } catch(e) {
    console.log(e.message)
    return asyncFunc()
  }
}

test('test async reject', async t => {
  for(let i = 0; i < 100; i++) {
    const res = await right()
    console.log(res)
  }
  t.pass()
})
```

```sh
error!!
2
3
4
5
6
7
8
9
10
error!!
12
.
.
.
110
error!!
112
```

