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

오래된 프로젝트의 기본 branch가 `master`라면 `main`으로 바꾸어 보자.

```bash
$ git checkout master # master branch로 이동
$ git branch -m master main # 로컬에서 master 이름을 main으로 변경
$ git fetch # 서버(Github)에서 최신 커밋을 가져옴
$ git branch --unset-upstream # origin/master와 연결 제거
$ git branch -u origin/main # origin/main과 연결
$ git symbolic-ref refs/remotes/origin/HEAD refs/remotes/origin/main # Default branch를 origin/main으로 업데이트
```

`git int` 할때 기본 branch를 `main`으로 하기 위한 config 설정.

```bash
$ git config --global init.defaultBranch main
```
