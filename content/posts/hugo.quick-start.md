---
title: "Hugo :: Quick Start"
date: 2021-07-13T23:25:02+09:00
draft: false
# weight: 1
# aliases: ["/first"]
tags: ["hugo", "quickstart"]
categories: ["Hugo"]
author: "bynaki"
showToc: true
TocOpen: false
hidemeta: false
comments: false
# description: "Desc Text."
canonicalURL: "https://gohugo.io/getting-started/quick-start/"
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

Create a Hugo site using the beautiful Ananke theme.

> This quick start uses macOS in the examples. For instructions about how to install Hugo on other operating systems, see install.
>
> It is recommended to have Git installed to run this tutorial.
>
> For other approaches learning Hugo like book or a video tutorial refer to the external learning resources page.

## Step 1: Install Hugo

> Homebrew and MacPorts, package managers for macOS, can be installed from brew.sh or macports.org respectively. See install if you are running Windows etc.

```bash
brew install hugo
# or
port install hugo
```

To verify your new install:

```bash
hugo version
```

## Step 2: Create a New Site

```bash
hugo new site quickstart
```

The above will create a new Hugo site in a folder named `quickstart`.

## Step 3: Add a Theme

See [themes.gohugo.io](https://themes.gohugo.io) for a list of themes to consider. This quickstart uses the beautiful Ananke theme.

First, download the theme from GitHub and add it to your site’s `themes` directory:

```bash
cd quickstart
git init
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
```

Then, add the theme to the site configuration:

```bash
echo theme = \"ananke\" >> config.toml
```

## Step 4: Add Some Content

You can manually create content files (for example as `content/<CATEGORY>/<FILE>.<FORMAT>`) and provide metadata in them, however you can use the new command to do a few things for you (like add title and date):

```bash
hugo new posts/my-first-post.md
```

Edit the newly created content file if you want, it will start with something like this:

```
---
title: "My First Post"
date: 2019-03-26T08:47:11+01:00
draft: true
---
```

> Drafts do not get deployed; once you finish a post, update the header of the post to say draft: false. More info here.

위 설정은 `/archetypes/default.md`와 연계된다. 만약, 자기만의 것을 설정하고 싶다면 `default.md`를 고치거나 아니면 새로운 파일로 하고 싶다면 (예: `post.md`라고 한다면) 파일을 생성하고 아래와 같이 하자.

```bash
hugo new --kind post posts/my-first-post.md
```

## Step 5: Start the Hugo server

Now, start the Hugo server with drafts enabled:

```bash
▶ hugo server -D

                   | EN
+------------------+----+
  Pages            | 10
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  3
  Processed images |  0
  Aliases          |  1
  Sitemaps         |  1
  Cleaned          |  0

Total in 11 ms
Watching for changes in /Users/bep/quickstart/{content,data,layouts,static,themes}
Watching for config changes in /Users/bep/quickstart/config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

**Navigate to your new site at** http://localhost:1313/.

Feel free to edit or add new content and simply refresh in browser to see changes quickly (You might need to force refresh in webbrowser, something like Ctrl-R usually works).

## Step 6: Customize the Theme

Your new site already looks great, but you will want to tweak it a little before you release it to the public.

### Site Configuration

Open up config.toml in a text editor:

```toml
baseURL = "https://example.org/"
languageCode = "en-us"
title = "My New Hugo Site"
theme = "ananke"
```

Replace the `title` above with something more personal. Also, if you already have a domain ready, set the `baseURL`. Note that this value is not needed when running the local development server.

> **Tip:** Make the changes to the site configuration or any other file in your site while the Hugo server is running, and you will see the changes in the browser right away, though you may need to clear your cache.

For theme specific configuration options, see the theme site.

**For further theme customization, see [Customize a Theme](https://gohugo.io/hugo-modules/theme-components/).**

## Step 7: Build static pages

It is simple. Just call:

```bash
hugo -D
```

Output will be in `./public/` directory by default (`-d/--destination` flag to change it, or set `publishdir` in the config file).

## See Also

- https://gohugo.io/getting-started/quick-start/