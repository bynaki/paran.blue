---
title: "CSS :: Web Font (@font-face)"
date: 2021-07-15T23:38:46+09:00
draft: false
# weight: 1
# aliases: ["/first"]
tags: ["css", "font-face", "webfont"]
categories: ["CSS"]
author: "bynaki"
showToc: true
TocOpen: false
hidemeta: false
comments: false
# description: "Desc Text."
canonicalURL: "https://webclub.tistory.com/261"
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



웹 폰트 또한 `font-family` 속성을 사용하지만, `@font-face` 지시어(directive)라는 CSS 명령어를 사용해서 웹 브라우저에게 해당 서체를 다운로드할 것을 알리면서 사용할 수 있습니다.

웹 폰트를 위해 사용하는 CSS 코드는 매우 간단하며, 두 개의 CSS 명령어만이 필요합니다.

- `@font-face` 지시어는 웹 브라우저에게 서체 이름과 다운받을 위치를 알려줍니다.  이 명령어의 동작 방식은 뒤에서 살펴봅니다.
- `font-family` 속성의 사용법은 위에서 언급한 일반 폰트의 사용법과 같습니다. 일단 `@font-face` 를 사용해 브라우저에게 서체를 다운받으라 알린 다음에는, 어느 CSS에서도 일반 폰트와 동일하게 `font-family`를 통해 사용할 수 있게 됩니다.


## Web Font Sysntax

웹 폰트의 마법은 @font-face 지시어라는 CSS 명령어부터 시작됩니다.
이 명령어는 사용할 폰트의 이름 및 해당 폰트를 다운받을 수 있는 위치를 브라우저에게 알리는 명령어입니다.
아래 코드에서 간단히 사용 방법을 살펴봅니다.

```css
@font-face {
    font-family: <a-remote-font-name>
    src: <source> [, <source>]*;
    [font-weight: <weight>];
    [font-style: <style>];
}
```

속성값들의 내용은 아래와 같습니다.

- **\<a-remote-font-name\>** : font 속성에서 폰트명(font face)으로 지정될 이름을 설정한다.
- **\<source\>** : 원격 폰트(remote font) 파일의 위치를 나타내는 URL 값을 지정하거나, 사용자 컴퓨터에 설치된 폰트명을 local("Font Name")형식으로 지정하는 속성이다.
- **\<weight\>** : 폰트의 굵기(font weight) 값.
- **\<style\>** : 폰트 스타일(font style) 값.


## Usage

```css
@font-face {
    font-family: 'MaruBuri-Regular';
    src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_20-10-21@1.0/MaruBuri-Regular.woff') format('woff');
    font-weight: normal;
    font-style: normal;
}

body {
    font-family:'나눔고딕', 'NanumGothic', 'MaruBuri-Regular';
}
```


## See Also

- https://webclub.tistory.com/261
- [Google Fonts](https://fonts.google.com)
- [Adobe Fonts](https://fonts.adobe.com)
- [cufon](http://cufon.shoqolate.com/generate/)
- [눈누](https://noonnu.cc)
- [Font Squirrel (웹폰트 생성기)](https://www.fontsquirrel.com/tools/webfont-generator)
- [이롭게 바탕체](http://font.iropke.com/batang/#structure)
