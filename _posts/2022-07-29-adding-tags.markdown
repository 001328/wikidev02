---
layout: post
title:  "Adding tags for Navigation"
date:   2022-07-29 01:10:00 -0400
categories: boom wtf
tags: boom whatever mega wtf
---

Sooo - let's add some tags for navigation.
I have no idea how this works, but I will try..













------------------------

# NOTHING BELOW WORKS

------------------------

<!-- the following is already installed, just add it to _config -->

# Add gem 'jekyll-archives' to your site’s Gemfile

https://learn.cloudcannon.com/jekyll/jekyll-archives/
https://github.com/jekyll/jekyll-archives

How???
go to the Gemfile and do this

```
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.12"
  gem "jekyll-archives"
end
```

run bundle install (!!!)

1. Add the following to your site’s _config.yml:

```
jekyll-archives:
  enabled: all
  layout: 'archive'
  permalinks:
    tag: '/tag/:name/'
    category: '/category/:name/'
```

```
plugins:
  - jekyll-archives
```


NOW IT WORKS!!!!!


# Make the archives pretty and working

---

ok, let's get started with this stuff

I can add tags and navigation throught the jekyll archives

https://jekyll.github.io/jekyll-archives/

https://jekyll.github.io/jekyll-archives/getting-started/

---

you also need to change the permalinks
https://jekyllrb.com/docs/permalinks/#placeholders


---



---

adding navigation

https://jekyllrb.com/tutorials/navigation/
