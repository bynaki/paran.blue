---
title: "Node :: Usage nvm"
date: 2021-07-29T00:51:46+09:00
draft: false
# weight: 1
# aliases: ["/first"]
tags: ["node", "nvm"]
categories: ["Node"]
author: "bynaki"
showToc: true
TocOpen: false
hidemeta: false
comments: false
# description: "Desc Text."
canonicalURL: "https://github.com/nvm-sh/nvm"
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



## Usage NVM

To download, compile, and install the latest release of node, do this:

```shell
nvm install node # "node" is an alias for the latest version
```

To install a specific version of node:

```shell
nvm install 6.14.4 # or 10.10.0, 8.9.1, etc
```

The first version installed becomes the default. New shells will start with the default version of node (e.g., `nvm alias default`).

You can list available versions using `ls-remote`:

```shell
nvm ls-remote
```

And then in any new shell just use the installed version:

```shell
nvm use node
```

Or you can just run it:

```shell
nvm run node --version
```

Or, you can run any arbitrary command in a subshell with the desired version of node:

```shell
nvm exec 4.2 node --version
```

You can also get the path to the executable to where it was installed:

```shell
nvm which 5.0
```
