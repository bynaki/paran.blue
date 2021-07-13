---
title: "Git :: Submodule"
date: 2021-07-13T22:02:06+09:00
draft: false
# weight: 1
# aliases: ["/first"]
tags: ["git", "submodule"]
categories: ["Git"]
author: "bynaki"
showToc: true
TocOpen: false
hidemeta: false
comments: false
# description: "Desc Text."
canonicalURL: "https://git-scm.com/book/ko/v2/Git-도구-서브모듈"
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

About submodule.

## Add Submodule

서브모듈 추가 하기

```bash
$ git submodule add https://github.com/chaconinc/DbConnector
```

기본적으로 서브모듈은 프로젝트 저장소의 이름으로 디렉토리를 만든다. 예제에서는 `DbConnector`라는 이름으로 만든다. 명령의 마지막에 원하는 이름을 넣어 다른 디렉토리 이름으로 서브모듈을 추가할 수도 있다.
우선 `.gitmodules` 파일이 만들어졌다. 이 파일은 서브디렉토리와 하위 프로젝트 URL의 매핑 정보를 담은 설정파일이다.

```
[submodule "DbConnector"]
    path = DbConnector
    url = https://github.com/chaconinc/DbConnector
```

## Submodule 포함한 프로젝트 Clone

서브모듈을 포함하는 프로젝트를 Clone 하는 예제를 살펴본다. 이런 프로젝트를 Clone 하면 기본적으로 서브모듈 디렉토리는 빈 디렉토리이다.

```bash
$ git clone https://github.com/chaconinc/MainProject
```

분명히 `DbConnector` 디렉토리는 있지만 비어 있다. 서브모듈에 관련된 두 명령을 실행해야 완전히 Clone 과정이 끝난다. 먼저 `git submodule init` 명령을 실행하면 서브모듈 정보를 기반으로 로컬 환경설정 파일이 준비된다. 이후 `git submodule update` 명령으로 서브모듈의 리모트 저장소에서 데이터를 가져오고 서브모듈을 포함한 프로젝트의 현재 스냅샷에서 Checkout 해야 할 커밋 정보를 가져와서 서브모듈 프로젝트에 대한 Checkout을 한다.

```bash
$ git submodule init
$ git submodule update
```

DbConnector 디렉토리는 마지막으로 커밋을 했던 상태로 복원된다.

하지만, 같은 과정을 더 간단하게 실행하는 방법도 있다. 메인 프로젝트를 Clone 할 때 git clone 명령 뒤에 `--recurse-submodules` 옵션을 붙이면 서브모듈을 자동으로 초기화하고 업데이트한다.

```bash
$ git clone --recurse-submodules https://github.com/chaconinc/MainProject
```

## Submodule 포함한 프로젝트 작업

서브모듈 디렉토리에서 `Fetch` 명령과 `Merge` 명령을 실행하지 않아도 `git submodule update --remote` 명령을 실행하면 Git이 알아서 서브모듈 프로젝트를 Fetch 하고 업데이트한다.

```bash
$ git submodule update --remote DbConnector
```

## See Also

- [7.11 Git 도구 - 서브모듈](https://git-scm.com/book/ko/v2/Git-도구-서브모듈)