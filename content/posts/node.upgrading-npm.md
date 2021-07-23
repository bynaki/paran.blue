---
title: "Node :: Upgrading npm"
date: 2021-07-18T00:34:28+09:00
draft: false
# weight: 1
# aliases: ["/first"]
tags: ["node", "npm"]
categories: ["Node"]
author: "bynaki"
showToc: true
TocOpen: false
hidemeta: false
comments: false
# description: "Desc Text."
canonicalURL: "https://www.carlrippon.com/upgrading-npm-dependencies/"
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



Is there a quicker way of just updating all the dependencies, including major version changes? So, like `npm update` but for major version updates as well?

Yes, there is a tool called [npm-check-updates](https://github.com/tjunnone/npm-check-updates) that will do this. Just run the following command:

```shell
npx npm-check-updates -u
```

This will update the dependencies to the latest versions (including major version changes) in the `package.json` file. If we are happy to go ahead with the upgrades we need to run the following command:

```shell
npm install
```

This will then upgrade the packages in the `node_modules` folder, and the `package-lock.json` file will be updated as well.
