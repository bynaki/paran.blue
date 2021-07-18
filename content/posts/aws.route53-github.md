---
title: "AWS :: How to deploy GitHub pages with AWS Route 53 registered custom domain and force HTTPS"
date: 2021-07-18T23:35:55+09:00
draft: false
# weight: 1
# aliases: ["/first"]
tags: ["aws", "githubpages"]
categories: ["AWS"]
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


In this guide I will explain how to deploy a website to GitHub pages forcing HTTPS over a custom domain that is registered with AWS Route 53. We will set up our domain so that the www subdomain will redirect to the apex domain.

## Summary

- Set up the GitHub repo
- Commit and push an index.html or use Jekyll
- Configure AWS Route 53

## Step 1: Create GitHub repo and turn on GitHub Pages

1. If it does not exist yet, create a repository using the naming pattern `your-github-username.github.io`. Since my username is *benwiz* my repository is called `benwiz.github.io` .
2. Click the *Settings* tab and scroll down the *GitHub Pages* section
3. From the *Source* dropdown select *master branch*
4. Click *Save*

## Step 2: Push source code to GitHub

- Clone the repo to your local machine

```
git clone git@github.com:your-github-username/your-github-username.github.io.git && cd your-github-username.github.io 
```

- Create an *index.html* file with some content

```
echo "Hello GitHub Pages!" > index.html
```

- Looking forward, we will need to have a file named *CNAME* that contains a single row: your custom domain. My *CNAME* file has the following contents.

```
benwiz.com
```

- Push the files to GitHub

```
git add . && git commit -m 'Create content and CNAME record' && git push
```

## Step 3: Confirm that GitHub pages has been deployed

Visit [http://your-github-username.github.io](http://your-github-username.github.io/) and [https://your-github-username.github.io.](https://your-github-username.github.io./) You should see the contents of your *index.html* file at both the unsecured and secured addresses.

## Step 4: Configure AWS Route 53 to use your custom vanity domain

1. Log into the AWS console and go to the [Route 53 dashboard](https://console.aws.amazon.com/route53/home).
2. Click *Hosted zones*
3. Click the domain you would like to use
4. Click *Create Record Set*
5. Do not enter anything into the *Name* field
6. Under the *Type* dropdown, select *A — IPv4 addresses*
7. The *Alias* toggle should be set to *No*
8. Enter the following four IP addresses into the *value* text area. Then click *Save Record Set*.

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

![picture 1](/images/cad09110d2784bd05bacb8cb5aef5c86aa9770987c6f70434c6b8bb6c6358aee.png)  

1. Click *Create Record Set*, again
2. Into the *Name* field, enter `www`
3. Under the *Type* dropdown, select *A — IPv4 addresses*, again
4. The *Alias* toggle should be set to *Yes*, unlike before
5. In the *Alias Target* field, select the apex domain we previously set up. For me this is *benwiz.*com.
6. Click *Save Record Set*, again

![picture 2](/images/bdac45dc1525ab97b85c57a414646a0f163ef76694f04662c17c5ed2dd24d620.png)  

## Step 5: Configure GitHub to serve over your custom domain

1. Return to your GitHub repository’s settings tab
2. Scroll down to the GitHub Pages section
3. In the *Custom domain* field enter your custom domain: `your-custom-domain.com`
4. Click *Save*
5. Check *Enforce HTTPS*

## Step 6: Confirm that your page is accessible at your custom domain

Visit `https://your-custom-domain.com`. You should see the contents of your *index.html*.

1. Visit [https://www.your-custom-domain.com](https://your-custom-domain.com/). You should be redirected to [https://your-custom-domain.com](https://your-custom-domain.com/).
2. Visit [http://your-custom-domain.com](http://your-custom-domain.com./). You should be redirected to [https://your-custom-domain.com](https://your-custom-domain.com/).
3. Visit [http://www.your-custom-domain.com](http://www.your-custom-domain.com/). You should be redirected to [https://your-custom-domain.com](https://your-custom-domain.com/).
