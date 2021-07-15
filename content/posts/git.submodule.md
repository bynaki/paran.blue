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

## Submodule Push

서브모듈의 변경사항을 Push 하지 않은 채로 메인 프로젝트에서 커밋을 Push 하면 안 된다. 변경 사항을 Checkout 한 다른 사람은 서브모듈이 의존하는 코드를 어디서도 가져올 수 없는 상황이 돼 곤란해진다. 서브모듈의 변경사항은 우리의 로컬에만 있다.

이런 불상사가 발생하지 않도록 하려면 메인 프로젝트를 Push 하기 전에 서브모듈을 모두 Push 했는지 검사하도록 Git에게 물어보면 된다. `git push` 명령에 `--recurse-submodules` 옵션을 주고 이 옵션의 값으로 `check` 나 `on-demand` 를 설정한다. `check` 는 간단히 서브모듈의 로컬 커밋이 Push 되지 않은 상태라면 현재의 `Push 명령도 실패하도록 하는 옵션이다.

```bash
$ git push --recurse-submodules=check
The following submodule paths contain changes that can
not be found on any remote:
  DbConnector

Please try

    git push --recurse-submodules=on-demand

or cd to the path and use

    git push

to push them to a remote.
```

예제에서 볼 수 있는 대로 이러한 상황에서 다음으로 무엇을 해야 하는지 Git은 도움을 준다. 가장 단순한 방법은 각 서브모듈 디렉토리로 가서 직접 일일이 Push를 해서 외부로 공유하고 나서 메인 프로젝트를 Push 하는 것이다. 이 옵션이 항상 적용되도록 하고 싶으면 `git config push.recurseSubmodules check` 명령으로 설정한다.

옵션으로 설정할 수 있는 다른 값으로 `on-demand` 값이 있는데, 이 값으로 설정하면 Git이 Push를 대신 시도한다.

```bash
$ git push --recurse-submodules=on-demand
Pushing submodule 'DbConnector'
Counting objects: 9, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (8/8), done.
Writing objects: 100% (9/9), 917 bytes | 0 bytes/s, done.
Total 9 (delta 3), reused 0 (delta 0)
To https://github.com/chaconinc/DbConnector
   c75e92a..82d2ad3  stable -> stable
Counting objects: 2, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 266 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
To https://github.com/chaconinc/MainProject
   3d6d338..9a377d1  master -> master
```

위에서 보듯이 Git이 메인 프로젝트를 Push 하기 전에 DbConnector 모듈로 들어가서 Push를 한다. 모종의 이유로 서브모듈 Push에 실패한다면 메인 프로젝트의 Push 또한 실패하게 된다. `git config push.recurseSubmodules on-demand` 명령으로 설정할 수 있다.


## See Also

- [7.11 Git 도구 - 서브모듈](https://git-scm.com/book/ko/v2/Git-도구-서브모듈)