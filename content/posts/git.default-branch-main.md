---
title: "Git :: Default Branch를 'master'에서 'main'으로 변경"
date: 2021-07-17T01:47:32+09:00
draft: false
# weight: 1
# aliases: ["/first"]
tags: ["git", "main"]
categories: ["Git"]
author: "bynaki"
showToc: true
TocOpen: false
hidemeta: false
comments: false
# description: "Desc Text."
canonicalURL: "https://dunchi.tistory.com/92"
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



오래된 프로젝트의 기본 branch 이름이  `master`라면 `main`으로 변경하자.

`github` 에서 `Settings` > `Branches` > `Default branch` 에서 `master` 를 `main` 으로 변경한 후 로컬에서 다음을 실행한다.

```shell
git branch -m master main
git fetch origin
git branch -u origin/main main
git remote set-head origin -a
```

`git int` 할때 기본 branch를 `main`으로 하기 위한 config 설정.

```shell
$ git config --global init.defaultBranch main
```

