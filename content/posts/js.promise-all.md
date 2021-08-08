---
title: "Js :: Promise.all()"
date: 2021-08-08T12:54:59+09:00
draft: false
# weight: 1
# aliases: ["/first"]
tags: ["js", "promise"]
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



## Promise.all()



**source:**

```js
const times = [2000, 500, 3000, 1000]
await Promise.all(times.map(async t => {
  await stop(t)
  console.log(t)
}))
```



**output:**

```shell
500
1000
2000
3000
```

