---
title: "Vscode :: Complete uninstall / remove vscode (Mac)"
date: 2021-08-10T20:54:06+09:00
draft: false
# weight: 1
# aliases: ["/first"]
tags: ["vscode"]
categories: ["Vscode"]
author: "bynaki"
showToc: true
TocOpen: false
hidemeta: false
comments: false
# description: "Desc Text."
canonicalURL: "https://jimkang.medium.com/complete-uninstall-remove-vscode-mac-5e48bef3bdec"
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



while writing go this morning, I found that the wrong code are not under lined by `red line` This is really difficult for me and time consuming to keep writing. After 1 hour of wasting time trying to figure out what happened, I decide to kill it all and start again. Hope this will be helpful for those who wants to complete remove `vscode` on their mac

## ATTENTION

please write down your extension lists, and settings (JSON) because you won’t be seeing this anymore (screen shot?)

> remember to quit vscode first

## Step1

remove settings and configs

```sh
rm -rf $HOME/Library/Application\ Support/Code
// add sudo if you needed to// if you're using insider*
sudo rm -rf $HOME/Library/Application\ Support/Code\ -\ Insiders/
```

## Step2

remove all the extensions

```sh
rm -rf $HOME/.vscode
// add sudo if you needed to// if you're using insider*
sudo rm -rf $HOME/.vscode-insiders/
```

## Step3

remove vscode from application

## Step4

[download vscode](https://code.visualstudio.com/download) and install again ;)
