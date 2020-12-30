---
layout: single
title: Jekyll up and running
author: aNNufriy
tags: [web, jekyll]
cover_url: "/images/jekyll.png"
---

Today I created my first static site with _**Jekyll**_ - good day to create post about my way to do it.

## Hacker theme

I decided to use [Hacker theme](https://github.com/pages-themes/hacker){:target="_blank"}, which looks nice for me and is, for sure, fully functional.

```bash
git clone git@github.com:hexlet-boilerplates/jekyll-bootstrap4-docker.git
```
## Docker environment

Theme authors offer docker environment as an option to build and run Jekyll site, here is my way to create it.

I created two containers: _jekyll-build_ and _jekyll-serve_: first start of every container takes a while

```bash
docker run --name jekyll-build --volume="<path_to_site_root>:/srv/jekyll" -it jekyll/jekyll:3.5 jekyll build
docker run --name jekyll-serve --volume="<path_to_site_root>:/srv/jekyll" -p 4000:4000 -it jekyll/jekyll:3.5 jekyll serve --watch --drafts
```

Build should finish normally and corresponding container stops.
Serving container remains running, at this point you are free to edit your new blog and play with it.
At some point you will have to stop serving container, but it's not a problem: you can start it again any time:

```bash
# build project again (if you need to add gem, plugin, etc.)
docker start -i jekyll-build
# start serving again
docker start -i jekyll-serve
```
