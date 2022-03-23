+++
title = "My first post"
date = "2022-03-23"
author = "Heath"
cover = "img/my_first_post/computer-screen-js.jpg"
description = "You have to start somewhere right?"
+++

# Where to begin??
Well I suppose lets start, how the heck did I get this site, well as you can tell by my generic computer image from a free image source, it involves super complex javascript and understanding of the large frontend enterprise...

No for real though, what a breeze this was and thanks to amazing content and theme creators like [panr](https://twitter.com/panr) who created this simple but fantastic Hugo theme I could stand this up and get started towards achieving my goals in no time at all.

So why don't we start with that, how did I stand up all of this in just a few minutes? To be fair, there is plenty of resources and guides online but if you do not know what you are looking for how do you start.

## The frame

This particular site is a [Hugo](https://gohugo.io/) site, a golang developed static website generator that uses markdown and themes to produce funky looking websites quickly and if you are like me, makes frontend systems and development look so easy (guess what it's not).

So following the Hugo documentation I got started in creating my blog site:

```bash
hugo new site my-blog-site
```
A simple command, this creates a directory called my-blog-site and inside contains a lovely collection of directories and a config.toml file.

But now I want a theme, displaying a white page of text I could of just done that with some html so lets go find a [theme](https://themes.gohugo.io/themes).

There are many themes to choose from Hugo and the authors are kind enough to offer them to you for free! Once you choose one you like in this case I choice [Hello-Friends](https://github.com/panr/hugo-theme-hello-friend).

Following the documentation I added the theme as a git submodule, of course remember to initialise your repo for your site in that case!

Make sure to remember to do this inside your sites root directory.
```bash
git init
```
```bash
git submodule add -f https://github.com/panr/hugo-theme-hello-friend.git themes/hello-friend
```

Now I have a theme!

One more step though, add the default config to my main config.toml as shown in the theme:

config.toml
```toml
baseurl = "/"
languageCode = "en-us"
theme = "hello-friend"
paginate = 5

[params]
  # dir name of your blog content (default is `content/posts`).
  # the list of set content will show up on your index page (baseurl).
  contentTypeName = "posts"

  # "light" or "dark"
  defaultTheme = "dark"

  # if you set this to 0, only submenu trigger will be visible
  showMenuItems = 2

  # Show reading time in minutes for posts
  showReadingTime = false

  # Show table of contents at the top of your posts (defaults to false)
  # Alternatively, add this param to post front matter for specific posts
  # toc = true

  # Show full page content in RSS feed items
  #(default is Description or Summary metadata in the front matter)
  # rssFullText = true

[languages]
  [languages.en]
    title = "Hello Friend"
    subtitle = "A simple theme for Hugo"
    keywords = ""
    copyright = ""
    menuMore = "Show more"
    writtenBy = "Written by"
    readMore = "Read more"
    readOtherPosts = "Read other posts"
    newerPosts = "Newer posts"
    olderPosts = "Older posts"
    minuteReadingTime = "min read"
    dateFormatSingle = "2006-01-02"
    dateFormatList = "2006-01-02"
    # leave empty to disable, enter display text to enable
    # lastModDisplay = ""

    [languages.en.params.logo]
      logoText = "hello friend"
      logoHomeLink = "/"
    # or
    #
    # path = "/img/your-example-logo.svg"
    # alt = "Your example logo alt text"

    [languages.en.menu]
      [[languages.en.menu.main]]
        identifier = "about"
        name = "About"
        url = "/about"
      [[languages.en.menu.main]]
        identifier = "showcase"
        name = "Showcase"
        url = "/showcase"
```

Lets start the server and see what it looks like!
```bash
hugo server run
```

Wow and just like a funky little site but its a bit empty lets make our first post!

### Creating a post

This can be done manually but to make it easier lets use Hugo's tools!

Create your first post using the following:

```bash
hugo new posts/blog_entry_1/index.md
```
This should look something similar to the following: `content/posts/blog_entry_1/index.md`

You should notice that the index.md has some info at the top, this is kind of the config for this page and allows hugo to grab those values and use the variables, it is how this blog will show up on the home page!

Just get to writing, whatever you want!

But how do I host this site? Do I need to build a server in AWS? Well I am glad that the answer for that is NO! well at least unless you want to, but in my case I just needed something simple, so lets use github!

## Github hosting HUGO

Github has an amazing functionality that allows you to host your own repository as a website and not only that, it has full Hugo integration!

To start lets get the necessary Hugo config to tell github that please run this using Hugo.

Following Hugos [docs](https://gohugo.io/hosting-and-deployment/hosting-on-github/) we can see it is quite simple.

First create a directory called `.github/workflows/` and create a file called `gh-pages.yml` and add the following:

```yml
name: github pages

on:
  push:
    branches:
      - main  # Set a branch to deploy
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          # extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: github.ref == 'refs/heads/main'
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

This is what we will have github pages use.

Lets get this to a repository in github, create a new repository in github with the following syntax `<user>.github.io`. Replace user with your username.

Add this github repo as the remote for your local git hub:
```bash
git remote add origin <mygitrepourl>
```
and now push all your commits to the remote repository!
```bash
git push origin master
```

Now we need to tell github to run the site!

Following the github [instructions](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages) we now want to switch what branch the pages settings is looking at. By changing it to gh-pages and now you should be able to go to https://<user>.github.io 

If all things worked you now have an amazing static website.

There is of course so much more that can be done, I recommend to explore and try different things out yourself, I certainly will be and be using this site to show what it is!

Until next time!

Noho ora Mai